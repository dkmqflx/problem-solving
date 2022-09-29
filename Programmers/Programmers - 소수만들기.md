```python

from itertools import combinations

# 소수 확인하기 위한 함수
def prime_check(num):
    for i in range(2, num):
        if(num%i == 0):
            return False

    return True


def solution(nums):
    result = 0
    comb = list(combinations(nums, 3))
    for c in comb:
        if(prime_check(sum(list(c)))):
            result+=1

    return result


```
