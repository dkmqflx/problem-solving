- 문자열이 주어졌을 때 여는 괄호 (와 닫는 괄호 )가 올바르게 짝지어졌는지 확인하는 문제입니다

- 문제를 해결하기 위해서 여는 괄호를 만나게 되면 우선 배열에 넣어줍니다

- 그리고 닫는 괄호를 만나면 배열에서 여는 괄호를 하나 씩 꺼내줍니다

- 이 때 닫는 괄호를 만났지만 배열에 여는 괄호가 하나도 없는 경우가 바로 올바르게 괄호가 짝지어 지지 않는 경우이기 때문에 false를 리턴해 줍니다

- 모든 괄호에 대해서 반복이 다 끝난 이후에 배열에 하나도 괄호가 남아있지 않는 경우는 닫는 괄호에 맞게 여는 괄호가 있었다는 뜻이므로 true를 반환해주고, 만약 여는 괄호가 배열에 남아 있는 경우는 닫는 괄호가 여는 괄호의 수에 맞게 존재하지 않았다는 뜻이므로 false를 리턴해 줍니다

```javascript
function solution(s) {
  let openArr = [];
  for (let i = 0; i < s.length; i++) {
    if (s[i] === '(') openArr.push(s[i]);
    else {
      if (openArr.pop()) continue;
      else return false;
    }
  }
  if (openArr.length === 0) return true;
  else return false;
}
```
