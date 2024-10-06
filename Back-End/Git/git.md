# Git 명령어 정리

### 기초 명령어
> pull : 원격 저장소(remote repository)에 있는 모든 변경 내역을 받아옴  
> push : 로컬 저장소(local repository)에 있는 커밋을 원격 저장소로 전송함  
> patch : 원격 저장소에 저장되어 있는 내용을 다운로드 받기위해 먼저 변경된 내용이 있는지 새로고침  
> branch :브랜치 관리(생성,삭제 기능)  
> merge : 각 브랜치간 파일 합치는 기능  
> stash : tracked 상태 파일의 임시 저장  

### 계정 정보 등록 및 확인
> git config --global user.name <사용자명>  
> git config --global user.email <사용자 이메일>  
> git config user.name : 저장된 사용자 이름 출력  
> git config user.email : 저장된 사용자 이메일 출력  

### 경로 세팅 준비
> cd /c/code/studying : 경로 세팅  
> git init : git이 관리하는 폴더로 지정 (지정하게 되면 비밀폴더로 .git이 생성됨)  

### 기본으로 생성되는 master 브랜치를 main 브랜치로 변경
> git checkout -b main : main 브랜치를 생성하고 해당 브랜치로 이동  
> git branch -M main : 기본 브랜치를 main 브랜치로 지정  
> git status : 상태 확인  
> git config --h : 전체 명령어 확인  

### 파일을 생성하고 add, commit
> git add <파일명> : 파일을 staging area에 추가  
> git add . : 모든 파일을 staging area에 추가  
> git commit : commit에 대한 메시지를 남기기 위해 vi 에디터가 실행  
> i -> 입력 모드로 변경  
> esc -> 입력 모드에서 나오기  
> :wq -> 저장 및 종료  
> git commit -m 'message' : commit을 하고, commit에 대한 간단한 메시지 작성  
> git log : commit 내역 확인  
> git log --oneline : commit 내역 간단하게 확인  

### 특정 coomit 지점으로 되돌리기

1) git log 또는 git reflog를 통해 commit id 확인  

> git reset --soft<commit> : commit 내역을 되돌리고, commit만 취소  
> git reset --mixed<commit> : commit 내역을 되돌리고, staging 까지만 취소  
> git reset --hard<commit> : commit 내역을 되돌리고 파일을 rollback  
> git revert <commit> : 지정한 commit으로 인해 발생한 변경을 되돌리고 새로운 commit을 생성해 commit에 추가  

### 원격 리포지토리 추가 및 push / pull
> git remote add origin <remote repository 주소>  
> git pull --allow--unrelated-histories  
> git push -u origin main  
> u : push할 기본 원격저장소와 브랜치를 기억. 이후에는 git push만 해도 됨  

### git 브랜치
> git checkout -b <브랜치명> : 새로운 브랜치를 생성하고 이동  
> git checkout <브랜치명> : 기존의 브랜치로 이동  
> git merge <브랜치명> : 브랜치 병합. (병합할 브랜치의 commit 내역도 함께 병합)  
> git merge --squash <브랜치명> : 브랜치 병합. 병합할 브랜치의 commit 내역을 합친 새로운 commit 생성

- merge 이후 반드시 새롭게 commit하기  
  - git rm -cached * : staging area에 올라간 파일들이 전부 working directory에 내려오게 됨  
