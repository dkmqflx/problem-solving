- 캐릭터가 처음 걸어본 길의 길이를 구하는 문제입니다

- 따라서 방문하지 않은 길을 방문할 때 마다 추랍ㄹ점과 도착점을 리스트에 추가해주고, 만약 이미 방문한 길인 경우에는 리스트에 넣지 않습니다

- 여기서 주의할 점은 ‘UDU’처럼 왔던 길을 그대로 다시 내려왔다가 또 다시 올라가는 경우에는 단순히 시작점과 도착점을 비교해주면 리스트에 두개의 값이 저장됩니다 [[0,0], [0,1]], [[1,0], [0,0]]

- 이러한 경우가 생기는 것을 막기 위해 출발점과 도착점을 바꾸어도 해당 리스트에 추가 되어있는지를 확인해줍니다

- 추가적으로 좌표가 넘어가는 경우에는 출발점과 도착점이 같아지는 경우가 생기기 때문에 같은 경우에도 추가하지 않도록 합니다

```python
def solution(dirs):
    lst_check = []
    dirs_list = list(dirs)
    x = 0
    y = 0
    _x = 0
    _y = 0

    for d in dirs_list:
        if(d == 'U' and y<5):
            _y = y+1
        elif(d == 'D' and y>-5):
            _y = y-1
        elif(d == 'R' and x<5):
            _x = x+1
        elif(d == 'L' and x>-5):
            _x = x-1

        r_lst = list(reversed([[x,y], [_x, _y]])) # 출발점과 도착점을 바꾸어서도 비교해준다
        if [[x,y], [_x, _y]] not in lst_check and r_lst not in lst_check and [x,y] != [_x,_y]:
            lst_check.append([[x,y], [_x, _y]])
        x = _x
        y = _y



    return len(lst_check)
```
