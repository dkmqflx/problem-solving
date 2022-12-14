해당 문제는 Dynamic Programming 으로 해결할 수 있는 문제로 삼각형의 꼭지점에서 출발해서 가장 아래줄 까지 내려가는 방법 주에서 숫자의 합이 가장 큰 방법을 찾는 문제입니다

문제를 해결하기 위해서 한줄 씩 내려갈 때 마다 각 요소가 최대가 되도록 더해줍니다

이 때 가장 왼쪽과 가장 오른쪽은 선택할 수 없으므로 이전 줄의 같은 위치의 값을 더해주면 됩니다

그리고 가장 왼쪽과 가장 오른쪽을 제외한 가운데 수는 다음줄과 더했을 때 더 큰 수가 되도록 만들어줍니다

예를들어 세번째 줄의 1의 경우, 3에서 오면 합이 4가 되고 8에서 오면 합이 9가 되므로 합이 9가 되어야 합니다

```python
def solution(triangle):

    for i in range(1, len(triangle)):
        # 가장 왼쪽과 오른쪽은 이전 줄의 가장 왼쪽과 오른쪽 값을 각각 더해준다
        triangle[i][0] += triangle[i-1][0]
        triangle[i][i] += triangle[i-1][i-1]

        # 가운데 요소는 대소비교를 한 후, 더 큰 수가 되도록 합해준다
        for j in range(1, i):
            sum_left = triangle[i][j] + triangle[i-1][j-1]
            sum_right = triangle[i][j] + triangle[i-1][j]

            if(sum_left > sum_right):
                triangle[i][j] = sum_left
            else:
                triangle[i][j] = sum_right


    return max(triangle[len(triangle)-1])

```
