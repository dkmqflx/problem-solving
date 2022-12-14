- 해당 문제는 처음에는 다음과 같은 방법으로 풀었습니다

```javascript
function solution(s) {
  while (1) {
    let arrLen = s.length;
    s = s.split(''); // 문자열을 배열로 변환

    for (let i = 0; i < s.length - 1; i++) {
      // 앞뒤 문자열이 같은 경우 없애준다
      if (s[i] === s[i + 1]) {
        s[i] = '';
        s[i + 1] = '';
      }
    }
    // 다시 배열을 문자열로 합쳐준다
    s = s.join('');

    // 반복문 이후에도 합친 문자열이 처음 문자열과 같은 경우 0을 리턴
    if (arrLen === s.length) return 0;
    else if (s.length === 0) return 1;
  }
}
```

- 하지만 시간 초과 문제가 발생하였고 다음처럼 stack을 사용하여 문제를 해결하였습니다

- 반복문을 통해 스택에 있는 맨 마지막 문자와 추가할 문자를 비교해줍니다

- 그리고 해당 문자가 같은 경우 마지막 문자를 스택에서 꺼내고, 새로운 문자를 추가하지 않습니다

- 만약 스택의 마지막 문자와 새로 추가할 문자가 다른 경우 새로운 문자를 추가해줍니다

- 예를 들어 ‘baabaa’가 주어진 경우

- 처음 반복문이 두번 반복될 동안 스택에는 ['b', 'a']가 존재합니다

- 하지만 세번째 반복문에서 추가할 문자 a는 스택의 마지막 문자 a와 같기 때문에 새로운 문자를 추가하지 않고 스택에서도 마지막 문자 a를 빼줍니다

- 이러한 식으로 반복을 해서 최종적으로 스택에 문자가 하나도 없다면 모든 문자열이 짝지어 제거가 되었기 때문에 1을 리턴해줍니다

```javascript
function solution(s) {
  s = s.split('');
  let stack = [];

  for (let i = 0; i < s.length; i++) {
    if (stack.length === 0 || stack[stack.length - 1] !== s[i])
      stack.push(s[i]);
    else stack.pop();
  }

  return stack.length === 0 ? 1 : 0;
}
```
