- 접두사인지 확인하기 위해서 비교하는 문자열 중 짧은 문자열의 길이만큼 두 문자열을 비교하였습니다

```python
def solution(phone_book):


    for i in range(len(phone_book)-1):
        for j in range(i+1, len(phone_book)):
            if int(phone_book[i]) > int(phone_book[j]):
                min_len = len(phone_book[j])
            else:
                min_len = len(phone_book[i])

            if phone_book[i][:min_len] in phone_book[j][:min_len]:
                return False

    return True

```
