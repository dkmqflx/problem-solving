- 반복문을 돌면서 앞의 단어의 맨 마지막 문자와 다음에 올 단어의 맨 앞글자를 비교해 줍니다

- 그리고 모든 사람이 한번씩 단어를 말하고 나면 몇번이나 반복되었는지 확인하기 위한 변수 turn을 +1 해줍니다

```javascript
if ((i + 1) % n === 0) turn += 1;
```

- 만약 앞 단어의 맨 마지막 문자와 다음에 올 단어가 다른 경우나 다음 단어가 이미 앞에서 언급된 단어인 경우 [번호, 차례] 값을 반환합니다

```javascript
if (
  words[i][words[i].length - 1] !== words[i + 1][0] ||
  check.includes(words[i + 1])
) {
  return [((i + 1) % n) + 1, turn];
}
```

- 전체 코드

```javascript
function solution(n, words) {
  let turn = 1;
  let check = []; // 단어 반복되었는지 체크하기 위한 배열
  for (let i = 0; i < words.length - 1; i++) {
    if ((i + 1) % n === 0) turn += 1;
    if (
      words[i][words[i].length - 1] !== words[i + 1][0] ||
      check.includes(words[i + 1])
    ) {
      return [((i + 1) % n) + 1, turn];
    }

    check.push(words[i]);
  }
  return [0, 0];
}
```
