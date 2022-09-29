- skill 문자열이 주어졌을 때 skill_trees로 주어진 배열의 요소 중에서 주어진 조건을 만족하는 스킬트리 개수를 구하는 문제입니다

- 반복문을 사용해서 skill의 각 문자에 해당하는 문자가 있는지 확인하고, 해당하는 문자가 있는 경우 checkArr이라는 배열에 넣어줍니다. 이 배열은 skill과 비교해서 주어진 조건을 만족하는지 확인하기 위한 배열입니다

- 배열에 넣어줄 때는 비교하는 skill의 문자가 있는 배열의 요소의 인덱스 위치를 고려해주는데, 예를 들어 C라는 문자는 BACDE의 2번째 인덱스에 위치하는데 이 경우 checkArr의 2번째 인덱스에 C라는 문자를 넣어줍니다

- 반복이 끝나고 나면 checkArr을 문자열로 만든다음 skill에 문자열이 포함되는지 확인해줍니다

- 이 때 checkArr의 문자열에서 처음 문자열은 skill의 처음 문자열과 같아야 합니다

- 그리고 skill_trees에서 `["ASF"]`와 같이 skill과 중복되는 문자열이 없더라도 가능한 스킬트리가 되기 때문에 이 경우도 고려해서 코드를 작성해줍니다

```javascript
function solution(skill, skill_trees) {
  let result = 0;

  for (let i = 0; i < skill_trees.length; i++) {
    let checkArr = []; //ski
    for (let j = 0; j < skill.length; j++) {
      if (skill_trees[i].indexOf(skill[j]) !== -1)
        checkArr[skill_trees[i].indexOf(skill[j])] = skill[j];
      // skill_tress의 각 요소의 ㅂ
    }
    if (
      (skill.includes(checkArr.join('')) &&
        checkArr.join('')[0] === skill[0]) ||
      checkArr.length === 0
    )
      result += 1;
  }

  return result;
}
```
