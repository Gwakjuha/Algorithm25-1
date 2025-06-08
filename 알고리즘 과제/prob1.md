# 문제 1. 친구 네트워크 탐색 (연결 요소 개수 구하기)

## 선택 알고리즘 : 깊이 우선 탐색 (DFS)

## 선택 이유 및 장단점 비교

1. **재귀적으로 구현이 직관적**이고 간결함  
2. **연결 요소 완전 탐색**에 매우 적합함  
3. 단점으로는 **깊은 그래프 구조에서는 재귀 깊이 제한** 문제가 있을 수 있으나,  
   **이 문제는 노드 수가 작기 때문에 큰 장애물로 작용하지 않음**

---

## 구현 코드 및 실행 결과

```python
from collections import defaultdict

def count_connected_components(n, edges):
    # 그래프 생성 (인접 리스트)
    graph = defaultdict(list)
    for u, v in edges:
        graph[u].append(v)
        graph[v].append(u)  # 무방향이므로 양쪽 다 추가

    visited = [False] * (n + 1)  # 노드 번호는 1부터 시작

    def dfs(node):
        visited[node] = True
        for neighbor in graph[node]:
            if not visited[neighbor]:
                dfs(neighbor)

    count = 0
    for i in range(1, n + 1):
        if not visited[i]:
            dfs(i)
            count += 1

    return count

# 예제 입력
n = 6
edges = [(1, 2), (2, 3), (4, 5)]
print(count_connected_components(n, edges))  # 출력: 3
