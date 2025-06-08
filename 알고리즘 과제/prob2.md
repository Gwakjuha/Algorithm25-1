# 문제 2. 루트 트리에서 깊이 계산

## 선택 알고리즘: BFS (너비 우선 탐색)

## 선택 이유 및 장단점 비교

1. **깊이를 구하기 위해서는 루트 노드(1번)로부터 몇 단계 떨어져 있는지를 알아야 함**
2. **BFS는 가까운 노드부터 차례로 탐색하고, 그 탐색 레벨이 곧 깊이가 됨**
3. DFS는 깊이를 `depth` 변수로 **직접 넘겨서 관리해야 하므로 비효율적**
4. 따라서 BFS가 구조적으로 **더 자연스럽고 간결하게 깊이를 계산할 수 있음**

> 예시:  
> `queue.append((neighbor, depth[current] + 1))`

---

## 구현 코드 및 실행 결과 캡처

```python
from collections import deque, defaultdict

def calculate_depth(n, edges):
    # 그래프 생성 (양방향)
    graph = defaultdict(list)
    for u, v in edges:
        graph[u].append(v)
        graph[v].append(u)

    # 깊이 저장 배열 (-1은 아직 미방문)
    depth = [-1] * (n + 1)
    depth[1] = 0  # 루트 노드의 깊이는 0

    # BFS 시작
    queue = deque([1])
    while queue:
        current = queue.popleft()
        for neighbor in graph[current]:
            if depth[neighbor] == -1:  # 방문하지 않은 경우
                depth[neighbor] = depth[current] + 1
                queue.append(neighbor)

    # 출력
    for i in range(1, n + 1):
        print(f"node {i}: {depth[i]}")

# 예제 입력
n = 5
edges = [(1,2), (1,3), (2,4), (3,5)]
calculate_depth(n, edges)
#결과과
node 1: 0
node 2: 1
node 3: 1
node 4: 2
node 5: 2
