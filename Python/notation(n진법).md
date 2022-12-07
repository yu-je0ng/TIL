# python 진법 변환



## n진수 -> 10진수

- 결과 값은 모두 string
- python에서는 기본적으로 int()라는 함수를 지원함.
  - `int(string, base)`
- 위와 같은 형식으로 사용하며, base에는 진법(notation)을 넣으면 됨.

```py
>>> print(int('101',2))
5
>>> print(int('202',3))
20
>>> print(int('303',4))
51
>>> print(int('404',5))
104
>>> print(int('505',6))
185
>>> print(int('ACF',16))
2767
```



## 10진수 -> 2, 8, 16진수

- 2, 8, 16진수는 bin(), oct(), hex() 함수를 지원함

```py
>>> print(bin(11))
0b1011
>>> print(oct(11))
0o13
>>> print(hex(11))
0xb
```

- 진법의 표시를 지우려면 인덱싱 처리하면 됨.

```py
>>> print(bin(11)[2:])
1011
>>> print(oct(11)[2:])
13
>>> print(hex(11)[2:])
b
```



### 10진수 -> n진수

- 지원하는 함수가 없어 divmod 함수로사용자정의 함수를 만들어야 함.

  - divmod 함수 : `divmod(x, y)`

    - 두 숫자를 인자로 전달 받아 첫번째 인자를 두번째 인자로 나눈 몫과 나머지를 tuple형식으로 반환함.

      ```py
      >>> divmod(8,3)
      (2, 2)
      >>> divmod(8,3)
      (2, 2)
      >>> divmod(4,2)
      (2, 0)
      >>> divmod(10,-3)
      (-4, -2)
      >>> divmod(-10,-3)
      (3, -1)
      >>> divmod(1.8,2)
      (0.0, 1.8)
      >>> divmod(5,0.4)
      (12.0, 0.19999999999999973)
      ```

```py
def solution(n, q):
    rev_base = ''

    while n > 0:
        n, mod = divmod(n, q)
        rev_base += str(mod)

    return rev_base[::-1] 
    # 역순인 진수를 뒤집어 줘야 원래 변환 하고자하는 base가 출력
    
>>> print(solution(45, 3))
1200
```



## n진수 -> n진수

- 위에서 정의했던 사용자정의 함수와 int함수를 이용.

  ```py
  >>> print(solution(int('c',16),4)) # 16진수인 C를 4진수로 바꾸는것
  30
  >>> print(solution(int('4',6),3))  # 6진수인 4를 3진수로 바꾸는것
  11
  >>> print(solution(int('21',3),7)) # 3진수인 21을 7진수로 바꾸는것
  10
  >>> print(solution(int('15',9),5)) # 9진수인 15를 5진수로 바꾸는것
  24
  ```

  