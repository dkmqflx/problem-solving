- 주어진 입력 n을 2진수로 변환하고 변환한 결과와 1의 개수를 리턴하는 함수를 정의합니다

```javascript
// 2진수로 바꾸어주는 함수
function toBinary(n) {
  let value = [];
  let oneCount = 0;
  while (n !== 0) {
    if (parseInt(n % 2) === 1) {
      value.push(1);
      oneCount += 1;
    } else value.push(0);
    n = parseInt(n / 2);
  }
  // 2진수로 바꾼 결과와 1의 개수를 반환한다
  return [value.reverse().join(''), oneCount];
}
```

- 그리고 반복문을 통해 n을 1씩 증가시키고 1의 개수가 같은 n을 찾으면 이를 반환해줍니다
  전체 코드

```javascript
function solution(n) {
  const binary = toBinary(n);
  const binaryStr = binary[0];
  const binaryNum = binary[1];

  n += 1;
  while (1) {
    const binaryComp = toBinary(n);
    const binaryCompStr = binaryComp[0];
    const binaryCompNum = binaryComp[1];
    if (binaryNum === binaryCompNum) return n;
    n += 1;
  }
}

// 2진수로 바꾸어주는 함수
function toBinary(n) {
  let value = [];
  let oneCount = 0;
  while (n !== 0) {
    if (parseInt(n % 2) === 1) {
      value.push(1);
      oneCount += 1;
    } else value.push(0);
    n = parseInt(n / 2);
  }
  // 2진수로 바꾼 결과와 1의 개수를 반환한다
  return [value.reverse().join(''), oneCount];
}
```
