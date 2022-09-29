- 입력 문자열 중에 첫번째 문자가 아닌 다른 문자에 대문자가 있는 경우가 있으므로 모두 소문자로 바꾸어준다

- 그리고 첫번 째 문자가 숫자가 아닌 경우, 대문자로 바꾸어준다

```javascript
s = s.toLowerCase().split('');
if (isNaN(s[0])) s[0] = s[0].toUpperCase();
```

- 해당 문제를 풀 때 for the last week, for the last week 와 같이 문자열 사이 또는 뒤에 연속으로 공백이 존재하는 경우가 있다

- 따라서 아래 반복문처럼 공백 다음 문자열이 공백이 아닌 경우에만 대문자로 바꾸도록해서 연속적인 공백이 존재하는 경우를 처리한다

```javascript
for (let i = 1; i < s.length - 1; i++) {
  if (s[i] === ' ' && s[i + 1] !== ' ') s[i + 1] = s[i + 1].toUpperCase();
}
```

- 전체 코드

```javascript
function solution(s) {
  s = s.toLowerCase().split('');
  if (isNaN(s[0])) s[0] = s[0].toUpperCase();

  for (let i = 1; i < s.length - 1; i++) {
    if (s[i] === ' ' && s[i + 1] !== ' ') s[i + 1] = s[i + 1].toUpperCase();
  }

  return s.join('');
}
```
