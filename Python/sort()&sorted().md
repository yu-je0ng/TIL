## sort()

- 리스트를 정렬된 상태로 변경
- 리스트만을 위한 메소드
- 오름차순 정렬 : sort()
- 내림차순 정렬 : sort(reverse=True)

```
a = [1,9, 3, 4, 2, 7, 5]

a.sort()
print(a)
> [1, 2, 3, 4, 5, 7, 9]

a.sort(reverse=True)
print(a)
> [9, 7, 5, 4, 3, 2, 1]
```



## sorted()

- 기존의 리스트를 변경하는 것이 아니라 정렬의 새로운 리스트를 반환
- 어떤 이터러블 객체도 받을 수 있다
  - (ex 딕셔너리 객체도 받을 수 있음)
- 오름차순 정렬 : sorted()
- 내림차순 정렬 : sorted(reverse=True)

```
b = {3: 'D', 2: 'B', 5: 'B', 4: 'E', 1: 'A'}
sorted(b)
> [1, 2, 3, 4, 5]

sorted(b, reverse=True)
> [5, 4, 3, 2, 1]
```



##  sorted()함수와 lambda함수

### 인덱스로 정렬하기 

- key인자에 함수를 넘겨주면 해당 함수의 반환값을 비교하며 순서대로 정렬한다.
  - 오름차순 정렬 : sorted(a, key=lambda x:x[0])
  - 내림차순 정렬 : sorted(a, key=lambda x:-x[0])

```
c = [(1, 2), (0, 1), (5, 1), (5, 2), (3, 0)]

# 인자 없이 그냥 sorted()만 쓰면, 리스트 아이템의 각 요소 순서대로 정렬한다.
c_1 = sorted(c)
> [(0, 1), (1, 2), (3, 0), (5, 1), (5, 2)]

# key인자에 함수를 넘겨주면 해당 함수의 반환값을 비교하여 순서대로 정렬한다.
c_2 = sorted(c, key = lambda x : x[0])
> [(0, 1), (1, 2), (3, 0), (5, 1), (5, 2)]

c_3 = sorted(c, key = lambda x : x[1])
> [(3, 0), (0, 1), (5, 1), (1, 2), (5, 2)]
```

```
# 아이템 첫번째 인자를 기준으로 오름차순으로 먼저 정렬하고, 
# 그 안에서 다음 두 번째 인자를 기준으로 내림차순으로 정렬한다.
d = [(1, 3), (0, 3), (1, 4), (1, 5), (0, 1), (2, 4)]
d_1 = sorted(d, key = lambda x : (x[0], -x[1]))
> [(0, 3), (0, 1), (1, 5), (1, 4), (1, 3), (2, 4)]
```



### 문자열 인덱스로 정렬하기.

```py
def solution(strings, n):
    return sorted(strings, key= lambda x : x[n])
strings = ["sun", "bed", "car"]

solution(strings, 0)
> ['bed', 'car', 'sun']
solution(strings, 1)
> ['car', 'bed', 'sun']
solution(strings, 2)
> ['bed', 'sun', 'car']
```

```py
# n 인덱스의 값이 중복되는 경우 다음 인덱스의 문자로 정렬하기.
def solution_1(strings, n):
    return sorted(sorted(strings, key= lambda x : x[n]))
    
solution_1(strings, 0)
> ['bed', 'car', 'sun']
solution_1(strings, 1)
> ['bed', 'car', 'sun']
solution_1(strings, 2)
> ['bed', 'car', 'sun']
```

```py
students = [('홍길동', 3.9, 20220101), ('김철수', 3.0, 20220102), ('김문식', 4.1, 20220103)]

sorted(students, key=lambda students :students[2])
> [('홍길동', 3.9, 20220101), ('김철수', 3.0, 20220102), ('김문식', 4.1, 20220103)]
sorted(students, key=lambda students :students[2], reverse=True)
> [('김문식', 4.1, 20220103), ('김철수', 3.0, 20220102), ('홍길동', 3.9, 20220101)]
```

