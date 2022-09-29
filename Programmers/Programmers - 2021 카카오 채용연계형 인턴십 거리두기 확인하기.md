```javascript
function solution(places) {
  let result = [];

  for (let i = 0; i < places.length; i++) {
    const matrix = places[i].map((item) => item.split(''));
    // console.log('matrix: ', matrix)

    // 거리 1 - 위, 위오른쪽, 오른쪽, 오른쪽아래, 아래, /아래왼쪽, 왼쪽, 왼쪽위
    const dr = [-1, -1, 0, 1, 1, 1, 0, -1];
    const dc = [0, 1, 1, 1, 0, -1, -1, -1];

    // 거리 2 - 위, 오른쪽, 아래, 왼쪽
    const dr2 = [-2, 0, 2, 0];
    const dc2 = [0, 2, 0, -2];

    let check = 1;

    for (r = 0; r < 5; r++) {
      for (c = 0; c < 5; c++) {
        // 사람이 있는 위치에서
        if (matrix[r][c] === 'P') {
          // 한칸 거리를 모두  탐색
          for (let i = 0; i < 8; i++) {
            const nr = r + dr[i];
            const nc = c + dc[i];

            if (-1 < nr && nr < 5 && -1 < nc && nc < 5) {
              // 탐색한 위치가 P이고
              // 대각선에 위치한 경우에는 대각선 가는 곳에 X가 하나 밖에 없는 경우 거리두기 지켜지지 않는 경우
              if (
                matrix[nr][nc] === 'P' &&
                (matrix[r][nc] !== 'X' || matrix[nr][c] !== 'X')
              ) {
                check = 0;
                break;
              }
            }
          }
          // 두칸 거리를 모두 탐색
          for (let i = 0; i < 4; i++) {
            const nr2 = r + dr2[i];
            const nc2 = c + dc2[i];

            if (-1 < nr2 && nr2 < 5 && -1 < nc2 && nc2 < 5) {
              // 한칸 거리위치가 X로 막혀 있는지 확인
              if (
                matrix[nr2][nc2] === 'P' &&
                matrix[r + dr2[i] / 2][c + dc2[i] / 2] !== 'X'
              ) {
                check = 0;
                break;
              }
            }
          }
        }
      }
    }
    result.push(check);
  }
  return result;
}
```
