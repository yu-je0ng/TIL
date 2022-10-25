# Bitwise Operators

-   코딩 테스트를 하던 중 &와 and의 차이를 알지 못해 계속 오류가 발생하였음.
-   bit연산자와 그와 비슷하게 헷갈리는 것들에 대해 정리함.



## is와 ==

-   is
    -   identity 연산자
    -   참조 비교(refernce comparsion)
-   ==
    -   비교 연산자
    -   값 비교(value comparison)

```py
no1_1 = 1
no1_2 = 1
str1_1 = 'teemo'
str1_2 = 'teemo'

no1_1 == no1_3 # True
str1_1 == str1_2 # True
str1_1 is str1_2 # True
```

```py
no2_1 = 257
no2_2 = 257
str2_1 = "temmo is the cutest chamption in league of legends"
str2_2 = "temmo is the cutest chamption in league of legends"

no2_1 == no2_2 # True
no2_1 is no2_2 # False
str1_1 == str1_2 # True
str1_1 is str1_2 # False
```

```py
id(no1_1) #4297375104
id(no1_2) #4297375104
id(no2_1) #4301496976
id(no2_2) #4301496720
```

-   id 매소드는 객체의 주소값과 매칭되는 유니크한 int값을 반환함.
    -   값이 1이었던 두 변수(no1_1, no1_2)는 주소 값이 동일함.
    -   값이 257이었던 두 변수(no2_1,no2_2)는 주소 값이 다름.
-   **is는 주소값을 비교하여 같으면 True, 다르면 False를 반환함.**
    -   python에서 int의 경우 -5 ~ 256까지의 작은 숫자들은 파이썬 내부적으로 캐시되어 있어 다른 변수에 같은 값을 넣어도 같은 메모리 주소를 참조함.
        -   **python integer caching**
            -   파이썬에서 -5 ~ 256에 해당하는 작은 수들은 할당할 때는 이미 존재하는 오브젝트의 레퍼런스를 참조함.
    -   string의 경우 'teemo'와 같이 짧은 건 동일 주소에 할당되지만, 긴 문장의 경우 다른 주소로 할당됨.



## and와 &

-   and
    -   논리 연산자
    -   True, False 연산
    -   [docs](https://docs.python.org/2/reference/expressions.html#boolean-operations)에 나온 and연산자의 설명
        -   *The expression x and y first evaluates x; if x is false, its value is returned; otherwise, y is evaluated and the resulting value is returned.*
        -   **x and y 가 있으면 x가 False면 x를 반환하고, x가 True면 y값을 반환함.**
-   &
    -   비교 연산자
    -   **bitwise 연산자**



```py
8 & 10 # 8
8 and 10 # 10
```

-   8 & 10을 이진수로 표현하면  1000 & 1010과 같은데 
    -   이 결과는 1000이 되므로 8이 반환됨.
-   0을 제외한 모든 숫자는 True이므로, 8 and 10은 8이 True이고 10이 반환됨.

```py
0 and 100 # 0
100 and 0 # 0
```

-   0 and 100과 100 and 0은 0이 False이므로 0이 반환

```py
not 100 # False
not 0 # True
```





## or과 |

-   or

    -   논리 연산자

    -   True, False 연산
    -   [docs](https://docs.python.org/2/reference/expressions.html#boolean-operations)에 나온 or연산자의 설명
        -   *The expression x and y first evaluates x; if x is false, its value is returned; otherwise, y is evaluated and the resulting value is returned.*
        -    **x and y 가 있으면 x가 False면 x를 반환하고, x가 True면 y값을 반환함.**

-   |

    -   비교 연산자

    -   **bitwise 연산자**



```py
8 or 10 # 8
8 | 10 # 10
```

-   8 or 10 은 8이 True이므로 8이 반환 
-   8 | 10 은 이진수로 표현하면 1000 | 1010 이고, 이 결과는 1010이 되므로 10이 반환

```py
0 or 100 # 100
100 or 0 # 100
```

-   0 or 100 과 100 or 0 은 0이 False고 100이 True이므로 100이 반환



## not 과 ~

-   not

    -   논리 연산자

    -   True, False 연산

-   ~
    -   비교 연산자
    -   bitwise 연산자

```python
not 7 # False
not 0 # True
```

-   7은 True니까 not 7은 반대인 False가 반환
-   0은 False니까 not 0은 반대인 True가 반환

```py
~7 # -8
~0 # -1
```

-   ~7은 이진수로 나타내면 ~0111
    -   ~는 0은 1, 1은 0이 되므로
    -   1000이고 십진법으론 -8이 됨(보수가 됨.)
-   ~0은 0의 보수인 -1이 반환



## Bitwise AND operator

**<u>Returns 1 if both the bits are 1</u> else 0.**

-   bit가 모두 1이면 1을 반환, 아니면 0을 반환.

```py
a = 10 = 1010 (Binary)
b = 4 =  0100 (Binary)

a & b = 1010
         &
        0100
      = 0000
      = 0 (Decimal)
```



## Bitwise OR operator

**<u>Returns 1 if either of the bit is 1</u> else 0.**

-   두 bit중 하나라도 1이면, 1을 반환.

```py
a = 10 = 1010 (Binary)
b = 4 =  0100 (Binary)

a | b = 1010
         |
        0100
      = 1110
      = 14 (Decimal)
```



## Bitwise NOT operator

**Returns one’s complement of the number.**

-   보수를 반환

```py
a = 10 = 1010 (Binary)

~a = ~1010
   = -(1010 + 1)
   = -(1011)
   = -11 (Decimal)
```



## Bitwise XOR operator

**Returns 1 if one of the bits is 1 and the other is 0 else returns false.**

-   하나의 비트가 1일때 다른 비트가 0이면 1을 반환.

```py
a = 10 = 1010 (Binary)
b = 4 =  0100 (Binary)

a ^ b = 1010
         ^
        0100
      = 1110
      = 14 (Decimal)
```









---

# 참고자료

[[python\] is와 == / and와 & / or과 ⎪ - Onsil's blog (onsil-thegreenhouse.github.io)](https://onsil-thegreenhouse.github.io/programming/python/2017/10/22/operator/)

[[기본원리\] 2진수의 음수표현법! (namsieon.com)](https://namsieon.com/229)

[Python Operators - GeeksforGeeks](https://www.geeksforgeeks.org/python-operators/#:~:text=Python Operators 1 OPERATORS%3A Are the special symbols.,the value on which the operator is applied.)

[Python Bitwise Operators - GeeksforGeeks](https://www.geeksforgeeks.org/python-bitwise-operators/)
