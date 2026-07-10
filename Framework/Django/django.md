# Django 란?

Django는 Python으로 웹 서비스를 빠르고 안전하게 개발할 수 있는 오픈소스 웹 프레임워크이다.   
ORM, 인증, 관리자 페이지 등 웹 개발에 필요한 기능을 기본으로 제공한다.

### 1. **프로젝트와 앱**

- **Project**: 웹사이트 전체의 설정과 구조
- **App**: 회원, 게시판, 결제처럼 특정 기능을 담당하는 모듈

```bash
django-admin startproject <프로젝트 이름>
python manage.py startapp <앱 이름> # like 도메인
```

⇒ 하나의 프로젝트에 여러 앱을 조합하는 구조

#### django-admin startproject 이후 생성되는 파일:

```bash
project_name/
    manage.py
    mysite/
        __init__.py
        settings.py # 프로젝트의 환경 및 구성 저장 (보안이 중요한 설정변수는 별도의 파일)
        urls.py
        asgi.py
        wsgi.py
```

### 2. MVT 패턴

Django 는 일반적으로 MVT(Model-View-Template) 구조 사용

- **Model**: 데이터 구조와 DB 작업 (MVC 와 의미 동일)
- **View**: 요청을 처리하는 로직
- **Template**: 사용자에게 보여줄 HTML
- **URLconf**: URL 을 적절한 View 에 연결

```
브라우저 요청 → URLconf → View → Model → Template → HTTP 응답
```

### 3. URL 라우팅 (요청 URL 과 View 를 연결)

```python
# posts/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path("", views.post_list, name="post_list"),
]
```

```python
# 프로젝트의 urls.py 에서 앱 URL 을 포함
path("posts/", include("posts.urls"))
```

### 4. View (HTTP 요청을 받아 응답을 반환)

```python
from django.shortcuts import render

def post_list(request):
    return render(request, "posts/post_list.html")
```

View 는 함수 기반과 클래스 기반으로 작성 가능하다.

### 5. Model 과 ORM

Model 은 데이터베이스 테이블을 Python 클래스로 표현한다.

```python
from django.db import models

class Post(models.Model):
    title = models.CharField(max_length=200)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
```

```python
# ORM을 통해 SQL 없이 데이터를 다룸

Post.objects.create(title="첫 글", content="내용")
Post.objects.all()
Post.objects.filter(title__contains="Django")
```

```bash
# 모델을 변경하면 마이그레이션 해야 함

python manage.py makemigrations
python manage.py migrate
```

### 6. Template

Django Template Language로 데이터를 HTML에 표현한다.

```html
{% for post in posts %}
  <h2>{{ post.title }}</h2>
  <p>{{ post.content }}</p>
{% empty %}
  <p>게시물이 없습니다.</p>
{% endfor %}
```

- `{{ value }}`: 값 출력
- `{% ... %}`: 반복문, 조건문 등의 로직
- `{% extends %}` / `{% block %}`: 템플릿 상속

### 7. Form

입력 검증과 HTML 폼 처리를 담당합니다. Model과 연결된 `ModelForm`이 자주 사용된다.

```python
from django.forms import ModelForm
from .models import Post

class PostForm(ModelForm):
    class Meta:
        model = Post
        fields = ["title", "content"]
```

```python
<form method="post">
  {% csrf_token %} # POST 요청에서는 CSRF 토큰이 필요
  {{ form.as_p }}
  <button type="submit">저장</button>
</form>
```

### 8. 요청과 응답

(View에서 자주 사용하는 객체와 함수)

- `request.GET`: URL 쿼리 데이터
- `request.POST`: 폼 데이터
- `request.user`: 로그인 사용자
- `render()`: HTML 응답
- `redirect()`: 다른 URL로 이동
- `JsonResponse`: JSON 응답

### 9. 인증과 권한

Django에는 기본 인증 시스템이 포함되어 있다.

- 사용자 생성과 로그인·로그아웃
- 세션 및 비밀번호 해싱
- 그룹과 권한
- `@login_required` 접근 제한

초기부터 커스텀 사용자 모델을 정의하는 것을 추천

```python
from django.contrib.auth.models import AbstractUser

class User(AbstractUser):
    pass
```

```python
AUTH_USER_MODEL = "users.User"
```

### 10. Admin

Model을 등록하면 관리자 페이지에서 데이터를 관리 가능

```python
from django.contrib import admin
from .models import Post

admin.site.register(Post)
```

```bash
python manage.py createsuperuser
```

### 11. Middleware

요청이 View에 도달하기 전과 응답이 브라우저로 돌아가기 전에 공통 처리 수행  
ex. 인증과 세션 / 보안 / CSRF 방어 / 로깅 / CORS 처리
