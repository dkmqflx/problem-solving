해당 문제는 Dynamic Programming 으로 해결할 수 있는 문제로 목적지 까지 합을 통해서 해결할 수 있습니다

문제에서 오른쪽과 아래쪽으로만 움직일 수 있다는 조건이 있기 때문에 [i,j]로 도착하는 방법은 [i-1,j], [i, j-1] 두가지 입니다.

그리고 물에잠긴 지역은 이동할 수 없으므로, 이 경우에는 continue를 통해서 지나치도록 합니다

문제에서 주어진 m과 n이 행열의 반대인 m은 열, n은 행이기 때문에 이러한 [row, col]이 아닌 [col, row]로 물에 잠긴 지역을 확인해줍니다

```python
def solution(m, n, puddles):
    mat = [[0] * (m+1) for _ in range(n+1)]
    mat[1][1] = 1

    for r in range(1, n+1):
        for c in range(1, m+1):
            if [c, r] in puddles:
                continue
            if r==1 and c ==1:
                continue
            mat[r][c] = mat[r-1][c] + mat[r][c-1]

    return mat[n][m] % 1000000007

```
