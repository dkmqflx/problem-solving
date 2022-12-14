- 처음에 문제를 해결할 때는 첫번째 행에 가장 큰 수를 선택하고 다음 행 부터는 이전 행과 다른 열에서 가장 큰 수를 선택하면 결과가 최대값을 반환할 것이라고 생각해서 아래와 같이 코드를 작성했습니다

```javascript
function findMax(arr1, arr2){
  let maxArr = []
  for(let i=0; i< arr2.length;i++){
    let arr = []
    for(let j=0;j<arr1.length;j++){
      if(i!==j)
        arr.push(arr2[i] + arr1[j])
      else
        arr.push(arr2[j])
    }
    maxArr.push(Math.max(...arr))
  }

  return maxArr

```

- 하지만 에러가 발생했는데, 다음과 같은 입력이 주어진 경우 `[[1,2,3,5],[5,6,7,100],[4,3,2,1]]` 결과값이 최고점이 되지 않기 때문입니다.

- 첫 행에서 최대 값을 선택하고 다음 행부터 이전 행과 같은 열에 있지 않은 최대의 수를 선택하면 결과가 5-7-4로 19가 됩니다. 하지만 실제 결과가 최대가 되는 경우은 3-100-4로 107이 되는 경우입니다.

- 따라서 다음 행의 모든 열에서 이전 행의 다른 열의 원소 중에서 어떠한 값을 더했을 때 최대가 되는지를 계산해주는 방식으로 합을 누적해서 문제를 해결할 수 있습니다.

- 예를 들어, `[[1,2,3,5],[5,6,7,100],[4,3,2,1]]`가 입력으로 주어진다면, 두번째 행의 첫번째 열 5는 첫번째 행의 첫번째 열인 1을 제외한 2, 3, 5를 거쳐 도착할 수 있고 2, 3, 5를 각각 더해주면 7, 8 ,10가 될 수 있습니다.

- 이 경우 최대가 되는 경우가 10이기 때문에 두번째 행의 첫번째 열의 원소를 10으로 바꾸어줍니다

- 이 방식을 다른 열에도 적용하면 두번째 행은 [10,11,12,103]이 됩니다

- 합이 누적되기 때문에 다음행에도 똑같은 방식으로 계산해준다면, 최대가 되는 값을 반환할 수 있습니다

- 전체 코드

```javascript
function solution(land) {
  for (let i = 0; i < land.length - 1; i++) {
    land[i + 1] = findMax(land[i], land[i + 1]);
  }
  // 마지막 행의 가장 큰 값을 반환해준다
  return Math.max(...land[land.length - 1]);
}

function findMax(arr1, arr2) {
  let maxArr = []; // 최대가 되는 행을 반환하는 배열
  for (let i = 0; i < arr2.length; i++) {
    let arr = [];
    for (let j = 0; j < arr1.length; j++) {
      if (i !== j) arr.push(arr2[i] + arr1[j]);
      else arr.push(arr2[j]);
    }
    maxArr.push(Math.max(...arr));
  }

  return maxArr;
}
```
