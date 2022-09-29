```javascript
function solution(board, moves) {
  let count = 0; // 인형 개수 count하는 변수
  let stack = []; //뽑은 인형 저장하는 배열

  for (let i = 0; i < moves.length; i++) {
    let c = moves[i] - 1; // moves의 element는 board의 column에 해당한다
    let item = 0;

    // row를 증가시키면서 인형이 존재하는지 찾는다
    for (let r = 0; r < board[0].length; r++) {
      // 인형이 있는 경우
      if (board[r][c] !== 0) {
        item = board[r][c];
        board[r][c] = 0;
        break;
      }
    }

    // 인형을 찾은 경우
    if (item !== 0) {
      if (stack[stack.length - 1] === item) {
        stack.splice(stack.length - 1, 1);
        count += 2;
      } else {
        stack.push(item);
      }
    }
  }
  return count;
}
```
