- 주어진 budget에 최대한 가까운 값을 만들기 위해 리스트 안의 숫자들을 더해주는 문제입니다

- 따라서 오름차순으로 정렬을 해준다음에 budget을 넘어설 때 까지 숫자들을 하나씩 더해주고 budget을 넘어서는 경우 총 몇개의 숫자가 리스트에 있는지를 반환해줍니다

```python
def solution(d, budget):

    d.sort()
    arr = []
    for i in range(len(d)):
        if(d[i] + sum(arr) <= budget):
            arr.append(d[i])
        else:
            break

    return len(arr)
}
```
