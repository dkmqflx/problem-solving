```javascript
function solution(numbers, hand) {
  // keypad 위치 저장
  let keypad = {
    1: [1, 1],
    2: [1, 2],
    3: [1, 3],
    4: [2, 1],
    5: [2, 2],
    6: [2, 3],
    7: [3, 1],
    8: [3, 2],
    9: [3, 3],
    '*': [4, 1],
    0: [4, 2],
    '#': [4, 3],
  };

  let leftPos = '*';
  let rightPos = '#';
  let result = [];

  for (let i = 0; i < numbers.length; i++) {
    // 왼손 엄지손가락 사용하는 경우
    if ([1, 4, 7].includes(numbers[i])) {
      result.push('L');
      leftPos = numbers[i];
    }

    // 오른손 엄지손가락 사용하는 경우
    else if ([3, 6, 9].includes(numbers[i])) {
      result.push('R');
      rightPos = numbers[i];
    }

    // 나머지 경우
    else {
      // 왼손 엄지손가락까지의 거리와 오른손 엄지손가락까지의 거리를 비교한다
      let leftDiff =
        Math.abs(keypad[leftPos][0] - keypad[numbers[i]][0]) +
        Math.abs(keypad[leftPos][1] - keypad[numbers[i]][1]);

      let rightDiff =
        Math.abs(keypad[rightPos][0] - keypad[numbers[i]][0]) +
        Math.abs(keypad[rightPos][1] - keypad[numbers[i]][1]);

      // 오른손이 더 가까운 경우
      if (leftDiff > rightDiff) {
        rightPos = numbers[i];
        result.push('R');
      }
      // 왼손이 더 가까운 경우
      else if (leftDiff < rightDiff) {
        leftPos = numbers[i];
        result.push('L');
      }
      // 거리 같은 경우
      else {
        // 오른 손 잡이인 경우
        if (hand === 'right') {
          rightPos = numbers[i];
          result.push('R');
        } else {
          // 왼손잡이인 경우
          result.push('L');
          leftPos = numbers[i];
        }
      }
    }
  }

  return result.join('');
}
```
