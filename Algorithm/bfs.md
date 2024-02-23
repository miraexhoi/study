# BFS(Breadth First Search)란?
![image](https://github.com/miraexhoi/study/assets/109408165/7334cd23-445f-43f8-ba31-a76d5c3f59af)

> BFS는 너비 우선 탐색이라는 의미로, 가까운 노드부터 탐색하는 알고리즘
### 동작 방식
1) 탐색 시작 노드를 큐에 삽입하고 방문 처리 한다.

2) 큐에서 노드를 꺼내 해당 노드의 인접 노드 중에서 방문하지 않은 노드를 모두 큐에 삽입하고 방문 처리 한다.

3) 2번의 과정을 더 이상 수행할 수 없을 때까지 반복한다.

```python
from collections import deque

def bfs(graph, start, visited):
queue = dequeue([start])
visited[start] = True # 현재 노드 방문 처리

# 큐가 빌 때까지 반복
while queue:
  v = queue.popleft() 
  print(v, end=' ')
  # 해당 원소와 연결되어 있으며, 아직 방문하지 않은 원소들 삽입
  for i in graph[v]:
    if not visited[i]:
      queue.append(i)
      visited[i] = True
      
graph = [
  [],
  [2, 3, 8],
  [1,7],
  [1, 4, 5],
  [3, 5],
  [3, 4],
  [7],
  [2, 6, 8],
  [1,7]
]

visited = [False] * 9
bfs(graph, 1, visited) # 1 2 3 8 7 4 5 6
```

bfs를 코드로 구현하면 데이터를 담기 위한 queue를 구현하고, 큐가 빌 때까지 계속 반복하면서 연결된 원소들을 차례대로 큐에 삽입하는 형태이다.  
DFS/BFS는 1차원 배열이나 2차원 배열 문제에서 많이 사용된다. 각 배열의 값들이 좌표라고 생각하고, 좌표를 상하좌우로만 이동하면서 탐색을 하는 문제들이 많이 출제된다.
