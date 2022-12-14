- 주어진 문자열에 대해서 문자열이 표현하는 튜플을 배열에 담아 반환하는 문제입니다

- 이 문제를 해결하기 위한 키 포인트는 주어진 원소에서 각각의 원소의 개수를 파악한 다음 가장 많은 원소 개수를 가지는 원소를 기준으로 내림차순 정렬을 하는 것입니다.

- 원소의 개수를 파악하는 이유는 가장 많이 등장하는 원소가 집합을 만드는데 가장 많이 포함되기 때문입니다

- 주어진 문자열에서 집합의 원소는 순서가 바뀌어도 상관 없기 때문에 이 점을 고려해서 각 원소의 개수를 구해줍니다

- 우선 입력받은 문자열을 정규식을 사용해서 필요없는 부분을 없애고 배열로 만들어줍니다

```javascript
s = s.replace(/{|}/g, '');
s = s.split(',');
```

- 그 다음 해당 s_set이라는 모든 원소를 하나만 가진 set을 만든다음, 각 원소 별로 개수를 세고 [원소 이름, 원소 개수]를 원소로 갖는 배열을 만듭니다

```javascript
let s_set = [...new Set(s)];

let arr = [];
for (let i = 0; i < s_set.length; i++) {
  let count = 0;
  for (let j = 0; j < s.length; j++) {
    if (s_set[i] === s[j]) {
      count += 1;
    }
  }
  arr.push([s_set[i], count]);
}
```

- 마지막으로 원소 개수를 기준으로 정렬한 다음 결과를 반환합니다

```javascript
arr.sort((a, b) => b[1] - a[1]);
```

- 전체 코드

```javascript
function solution(s) {
  s = s.replace(/{|}/g, '');
  s = s.split(',');
  let s_set = [...new Set(s)];

  let arr = [];
  for (let i = 0; i < s_set.length; i++) {
    let count = 0;
    for (let j = 0; j < s.length; j++) {
      if (s_set[i] === s[j]) {
        count += 1;
      }
    }
    arr.push([s_set[i], count]);
  }
  arr.sort((a, b) => b[1] - a[1]);

  let answer = arr.map((i) => parseInt(i[0]));

  return answer;
}
```
