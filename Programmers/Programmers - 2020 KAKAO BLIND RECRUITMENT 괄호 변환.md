- 균형잡힌 괄호 문자열을 올바른 괄호 문자열로 바꾸는 문제입니다

- 문제의 3단계와 4단계 조건을 통해서 재귀적으로 문제를 해결해야한다는 것을 알 수 있습니다

- 주어진 문자열 p 가 올바른 괄호 문자열 또는 빈 문자열인 경우 그대로 반환해줍니다

```javascript
if (rightCheck(p)) return p;
```

- 주어진 문자열 p 가 균형잡힌 괄호 주어진 조건 2단계에 따라 두 균형잡힌 괄호 문자열로 분리해줍니다

- 이 때 p는 짝수로만 이루어져 있기 때문에 균형잡힌 문자열 u 를 찾으면 v도 균형잡힌 괄호 문자열이 됩니다

```javascript
// u, v를 나누는 함수
function divide(p) {
  let check = [];
  let openCheck = 0;
  let closeCheck = 0;

  for (let i = 0; i < p.length; i++) {
    if (p[i] === '(') openCheck += 1;
    else closeCheck += 1;
    // 여는 괄호와 닫는 괄호 개수 같아지는 index i가 균형잡힌 괄호 문자열이 완성되는 위치
    if (openCheck === closeCheck) break;
  }
  // u와 v 반환
  return [
    p.slice(0, openCheck + closeCheck),
    p.slice(openCheck + closeCheck, p.length + 1),
  ];
}
```

- u와 v를 나누었을 때 u가 올바른 괄호 문자열이라면 3단계 조건에 따라 다시 v를 1단계 부터 수행합니다

```javascript
if (rightCheck(u)) {
  // u가 올바른 문자열이라면
  return (answer = u + solution(v));
}
```

- v를 다시 solution 함수에 인자로 전달해주는데 재귀적으로 v는 또 다시 u 또는 v로 나뉘고 나눈 결과에 따라 3단계 또는 4단계 조건에 따라 처리됩니다

- u와 v를 나누었을 때 u가 올바른 괄호 문자열이 아니라면 4단계 조건을 실행합니다

```javascript
else{
    // u가 올바른 괄호 문자열이 아니라면
    answer = "("
    answer += solution(v) + ")" + change(u.slice(1, u.length-1));
    return answer
  }

```

- 전체 코드

```javascript
function solution(p) {
  let answer = '';

  // 올바른 문자열인지 확인
  if (rightCheck(p)) return p;

  // 균형잡힌 문자열로 바꾸니까, u는 개수가 같도록 한다
  let value = divide(p);
  let u = value[0];
  let v = value[1];

  if (rightCheck(u)) {
    // u가 올바른 문자열이라면
    return (answer = u + solution(v));
  } else {
    // u가 올바른 문자열이 아니라면
    answer = '(';
    answer += solution(v) + ')' + change(u.slice(1, u.length - 1));
    return answer;
  }
}

// '('와 ')'를 바꾸는 함수
function change(p) {
  let value = [];
  for (let i = 0; i < p.length; i++) {
    if (p[i] === '(') {
      value.push(')');
    } else value.push('(');
  }
  return value.join('');
}

// u, v를 나누는 함수
function divide(p) {
  let check = [];
  let openCheck = 0;
  let closeCheck = 0;

  for (let i = 0; i < p.length; i++) {
    if (p[i] === '(') openCheck += 1;
    else closeCheck += 1;
    if (openCheck === closeCheck) break;
  }

  return [
    p.slice(0, openCheck + closeCheck),
    p.slice(openCheck + closeCheck, p.length + 1),
  ];
}

// 올바른 문자열인지 확인하는 함수
function rightCheck(s) {
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
