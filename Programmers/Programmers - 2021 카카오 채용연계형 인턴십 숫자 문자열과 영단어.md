```javascript
function solution(s) {
  const numbers = {
    0: 'zero',
    1: 'one',
    2: 'two',
    3: 'three',
    4: 'four',
    5: 'five',
    6: 'six',
    7: 'seven',
    8: 'eight',
    9: 'nine',
  };

  let result = '';
  let next;

  for (let i = 0; i < s.length; i = i + next) {
    next = 0;

    // 숫자인 경우
    for (let j = 0; j < Object.keys(numbers).length; j++) {
      if (Number.isInteger(parseInt(s[i]))) {
        result = result.concat(s[i]);
        next += 1;
        break;
      }

      //  문자열의 알파벳이 특정 문자로 시작하는 경우
      if (numbers[j].startsWith(s[i])) {
        const len = numbers[j].length;

        // 해당 문자열의 길이와 객체의 값이 일치하는 경우
        if (s.substr(i, len) === numbers[j]) {
          result = result.concat(j);
          next += numbers[j].length;
          break;
        }
      }
    }
  }
  return Number(result);
}
```
