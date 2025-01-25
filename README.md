# day19
from collections import deque

def bfs(N, K):
    # BFS에 필요한 큐
    queue = deque([N])
    
    # visited 배열과 경로 수 배열
    visited = [-1] * 100001  # 방문 배열 (-1로 초기화)
    count = [0] * 100001     # 경로 수 배열
    visited[N] = 0           # 수빈이의 시작 위치는 0초
    count[N] = 1             # 시작 위치에서 경로 수는 1

    while queue:
        current = queue.popleft()
        
        # 3가지 가능한 이동 (X-1, X+1, 2*X)
        for next_pos in [current - 1, current + 1, current * 2]:
            # 이동한 위치가 범위 내이고, 아직 방문하지 않은 곳이라면
            if 0 <= next_pos <= 100000:
                # 처음 방문한 곳이라면, 시간 기록하고 큐에 추가
                if visited[next_pos] == -1:
                    visited[next_pos] = visited[current] + 1
                    count[next_pos] = count[current]
                    queue.append(next_pos)
                # 이미 방문한 곳인데, 더 빠른 시간에 도달한 경우
                elif visited[next_pos] == visited[current] + 1:
                    count[next_pos] += count[current]
    
    return visited[K], count[K]

# 입력
N, K = map(int, input().split())

# 결과 출력
min_time, min_ways = bfs(N, K)
print(min_time)
print(min_ways)
