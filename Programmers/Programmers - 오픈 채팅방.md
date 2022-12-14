- 마지막에 설정한 이름름으로 기존의 채팅방을 들어오고 나간 기록을 바꾸는 문제입니다

- 우선 입력을 배열로 바꾸어줍니다

```javascript
const recordArr = record.map((x) => x.split(' '));
```

- 유저아이디- 닉네임으로 저장되는 해쉬맵을 위한 객체를 만들고, Enter 또는 Change 기록이 있을 때 마다 유저아이디의 닉네임을 변경합니다

```javascript
let recordSet = {};
for (let i = 0; i < recordArr.length; i++) {
  if (recordArr[i][0] !== 'Leave') recordSet[recordArr[i][1]] = recordArr[i][2];
}
```

- 마지막으로 모든 기록이 저장되어 있는 배열에 모든 요소에 대해서 Enter 또는 Leave에 맞는 메시지를 정해줍니다
- 그리고 이 때 해쉬맵에 저장되어 유저아이디에 맞는 닉네임을 선택합니다

```javascript
let answer = [];
for (let i = 0; i < recordArr.length; i++) {
  if (recordArr[i][0] === 'Enter')
    answer.push(recordSet[recordArr[i][1]] + '님이 들어왔습니다.');
  else if (recordArr[i][0] === 'Leave')
    answer.push(recordSet[recordArr[i][1]] + '님이 나갔습니다.');
}
```

- 전체 코드

```javascript
function solution(record) {
  const recordArr = record.map((x) => x.split(' '));

  let recordSet = {};
  for (let i = 0; i < recordArr.length; i++) {
    if (recordArr[i][0] !== 'Leave')
      recordSet[recordArr[i][1]] = recordArr[i][2];
  }

  let answer = [];
  for (let i = 0; i < recordArr.length; i++) {
    if (recordArr[i][0] === 'Enter')
      answer.push(recordSet[recordArr[i][1]] + '님이 들어왔습니다.');
    else if (recordArr[i][0] === 'Leave')
      answer.push(recordSet[recordArr[i][1]] + '님이 나갔습니다.');
  }

  return answer;
}
```
