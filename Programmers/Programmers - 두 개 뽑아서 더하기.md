```javascript
function solution(numbers) {
  let result = []; // 결과를 저장하는 배열

  for (let i = 0; i < numbers.length; i++) {
    let arr = numbers.slice(); // 하나씩 숫자 선택
    let num = arr.splice(i, 1)[0]; // 선택한 숫자 제외한 나머지

    for (let j = 0; j < arr.length; j++) {
      // 더한 값이 아직 결과를 리턴하는 배열에 포함되어 있지 않은 경우 배열에 추가한다
      if (!result.includes(num + arr[j])) {
        result.push(num + arr[j]);
      }
    }
  }

  return result.sort((a, b) => a - b);
}
```
