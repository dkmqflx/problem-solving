- 두 다중집합의 교집합과 합집합을 구한 후 교집합/합집합 \* 65536을 곱해준 값을 구하는 문제입니다

- 입력이 문자열로 주어지기 때문에 주어진 문자열을 다중 집합으로 변환시켜주는데 이 때 대소문자의 구분이 없기 때문에 모두 소문자로 바꾼다음에 다중집합으로 변환시켜줍니다

- 이 때 aa1+aa2같은 문자열에 대해 정규식으로 미리 영문자가 아닌 값을 제거하지 않고, 문자열에 대해 모든 다중 집합을 구해준 다음에 영문자가 이외에 다른 값을 포함하는 원소를 제거해주는 방식으로 처리해야 합니다

- 예를 들어 aa1+aa2의 경우 다중집합을 구하면 {aa, a1, 1+, +a, aa, a2}가 되고 영문자가 포함되지 않은 원소를 제거하면 결과는 {aa, aa}가 됩니다

- 하지만 미리 정규식으로 영문자가 아닌 문자를 처리해주면 aaaa가 되고, 가능한 다중 집합은 {aa, aa, aa}가 되어 다른 결과가 나오므로 미리 정규식으로 처리하지 않는 것이 중요합니다

```javascript
// 다중집합으로 변환하는 함수
function toSet(arr) {
  let setArr = [];
  for (let i = 0; i < arr.length - 1; i++) {
    setArr.push(arr[i] + arr[i + 1]);
  }
  // 다중집합은 영문자로된 글자쌍만 우효하기 때문에
  // 정규식을 통해 특수문자, 공백, 숫자가 포함된 문자쌍은 제거한다
  setArr = setArr.filter((x) => !/[^a-zA-Z]/g.test(x));
  return setArr;
}
그리고 다중집합에 대해 각 원소가 몇개씩 있는지 객체를 사용해서 key-value 형태로 구해줍니다
// 집합 원소당 몇개 있는지 개수를 구해준다
function setCount(arr) {
  let setObj = {};
  for (let i = 0; i < arr.length; i++) {
    setObj[arr[i]] = 1 + (setObj[arr[i]] || 0);
  }
  return setObj;
}

```

- 다중집합의 교집합은 두 집합의 공통 원소의 최소 개수와 같습니다

- 3번 예시처럼 A={1,1,2,2,3}, B={1,2,2,4,5} 인 경우, A와 B의 공통 원소는 {1, 2}가 되고 A의 1의 개수는 2개, B의 1의 개수는 1개이므로 공통원소 1의 최소 개수인 1이 되고 2의 경우에는 A와 B 모두 원소의 개수가 2로 같기 때문에 A∩B는 {1,2,2}이 됩니다

- 앞서 구한 원소 개수에 대한 객체를 입력받는 함수를 아래처럼 정의해줍니다

- 이 때 set1의 key값을 구해주고 set2에 해당하는 key가 있는 경우에만 두 set을 비교하는데 교집합을 구하는 과정이기 때문에 set2의 key를 구하고 set1에 key가 있는 경우를 확인해도 결과는 같습니다

```javascript
// 교집합 개수 구해준다
function intersection(set1, set2) {
  let minCount = 0;
  // set1의 key를 구해준다
  let keys = Object.keys(set1);

  // 공통적인 key가 있는 경우에만 비교해서 작은 것 추가
  for (let i = 0; i < keys.length; i++) {
    if (set2[keys[i]]) {
      const count = Math.min(set1[keys[i]], set2[keys[i]]);
      minCount += count;
    }
  }
  return minCount;
}
```

- 합집합의 경우, 공통되지 않은 원소인 경우 해당 원소의 개수 만큼 포함시키고 공통 원소인 경우 최대 개수를 포함시킵니다.

- 앞의 A와 B의 에시에서 A와 B 공통 원소는 {1, 2}이고 1의 경우에는 A가 2개로 더 많고, 2의 경우에는 개수가 같기 때문에 A∪B는 {1,1,2,2,3,4,5}가 됩니다

- set1와 set2의 모든 key를 구해주고 공통적으로 key가 존재하는 경우에는 최대 value를, 공통적인 key가 존재하지 않는 경우에는 해당하는 set의 value를 더해주고 이를 반환해줍니다

```javascript
function union(set1, set2) {
  // set1과 set2의 모든 key를 구해준다
  let keys = new Set([...Object.keys(set1), ...Object.keys(set2)]);
  keys = Array.from(keys);

  let maxCount = 0;
  for (let i = 0; i < keys.length; i++) {
    // 공통 key가 있는 경우
    if (set1[keys[i]] && set2[keys[i]])
      maxCount += Math.max(set1[keys[i]], set2[keys[i]]);
    // 공통 key가 없는 경우
    else if (set1[keys[i]]) maxCount += set1[keys[i]];
    else maxCount += set2[keys[i]];
  }
  return maxCount;
}
```

- 전체코드

```javascript
function solution(str1, str2) {
  let set1 = toSet(str1.toLowerCase());
  let set2 = toSet(str2.toLowerCase());

  let setCount1 = setCount(set1);
  let setCount2 = setCount(set2);

  const interCount = intersection(setCount1, setCount2);
  const uniconCount = union(setCount1, setCount2);
  if (interCount === 0 && uniconCount === 0) return 65536;
  else return Math.floor((interCount / uniconCount) * 65536);
}

// 다중집합으로 변환하는 함수
function toSet(arr) {
  let setArr = [];
  for (let i = 0; i < arr.length - 1; i++) {
    setArr.push(arr[i] + arr[i + 1]);
  }
  setArr = setArr.filter((x) => !/[^a-zA-Z]/g.test(x));
  return setArr;
}

// 집합 원소당 몇개 있는지 개수를 구해준다
function setCount(arr) {
  let setObj = {};
  for (let i = 0; i < arr.length; i++) {
    setObj[arr[i]] = 1 + (setObj[arr[i]] || 0);
  }
  return setObj;
}

// 교집합 개수 구해준다
function intersection(set1, set2) {
  let minCount = 0;
  let keys = Object.keys(set1);
  // 공통적인 key가 있는 경우에만 비교해서 작은 것 추가
  for (let i = 0; i < keys.length; i++) {
    if (set2[keys[i]]) {
      const count = Math.min(set1[keys[i]], set2[keys[i]]);
      minCount += count;
    }
  }
  return minCount;
}

// 합집합 개수 구해준다
function union(set1, set2) {
  let keys = new Set([...Object.keys(set1), ...Object.keys(set2)]);
  keys = Array.from(keys);

  let maxCount = 0;
  for (let i = 0; i < keys.length; i++) {
    if (set1[keys[i]] && set2[keys[i]])
      maxCount += Math.max(set1[keys[i]], set2[keys[i]]);
    else if (set1[keys[i]]) maxCount += set1[keys[i]];
    else maxCount += set2[keys[i]];
  }
  return maxCount;
}
```
