- 문제를 풀기 위해서는 현재 기지국이 설치된 곳에서 도달하지 않는 곳을 구해주어야 합니다

- 그리고 주어진 예시를 통해 도달하지 않는 곳의 길이에 따라 필요한 기지국의 개수를 구할 수 있습니다

- w가 1일 때

  - 도달하지 않는 길이가 2인 경우에는 1개
  - 도달하지 않는 길이가 3인 경우에는 2개

- w가 2일 때

  - 도달하지 않는 길이가 6인 경우에는 2개
  - 도달하지 않는 길이가 5인 경우에는 1개
  - 따라서 도달하지 않는 거리의 길이에 따라 필요한 기지국 개수는 도달하지 않는 길이 / 2 \* w + 기지국 설치 위치 의 값을 올림한 것을 알 수 있습니다

```python
import math

def solution(n, stations, w):
    dist = []

    # stations의 가장 왼쪽을 기준으로 도달하지 않는 곳을 구해준다
    if(stations[0]-w-1 >=1):
        dist.append(stations[0]-w - 1)

    # stations의 가장 오른쪽을 기준으로 도달하지 않는 곳을 구해준다
    if(stations[-1]+w < n):
        dist.append(n - (stations[-1]+w ))

    # 각 기지국 사이에서 도달하지 않는 곳을 구해준다
    for i in range(len(stations)-1):
        dist.append((stations[i+1]-w ) - (stations[i]+w)-1)

    count_4g = 0
    for d in dist:
        count_4g += math.ceil(d/(2*w+1))

    return count_4g

```
