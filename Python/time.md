# datetime 

- datetime package

  - datetime class :날짜와 시간을 함께 저장.

  - date class : 날짜만 저장

    ```
    from datetime import date
    date.today() # 오늘 날짜를 알 수 있는 매서드
    >>> datetime.date(2022, 12, 9)
    
    today.isoformat() # date 객체를 YYYY-MM-DD 형태의 문자열로 변환해줌.
    >>>> '2022-12-09'
    
    date.fromisoformat('2020-07-18') # YYYY-MM-DD 형태의 문자열을 date 객체로 변환해줌.
    >>> datetime.date(2020, 7, 18)
    ```

  - time class : 시간만 저장

  - timedelta class : 시간 구간 정보를 저장

## datetime 

```
>>> import datetime
>>> now = datetime.datetime.now()
>>> print(now)
2022-12-09 01:15:15.786001
```

- 다른 클래스와 달리  클래스 이름이 대문자로 시작하지 않음.

- datetime 클래스에는 객체를 생성하지 않고도 바로 클래스에서 사용할 수 있는 클래스 메서드라는 것을 제공함.

  - now 클래스 매서드는 컴퓨터의 현재 시각을 datetime 클래스 객체로 만들어 반환함.

    ```
    >>> print(type(now))
    <class 'datetime.datetime'>
    ```

  - 속성(attribute)

    ```
    >>> print(now)
    2022-12-09 01:15:15.786001
    >>> print(now.year) # year : 연도
    2022
    >>> print(now.month) # month : 월
    12
    >>> print(now.day) # day : 일
    9
    >>> print(now.hour) # hour : 시
    1
    >>> print(now.minute) # minute : 분
    15
    >>> print(now.second) # second : 초
    15
    >>> now.microsecond # micro seconds : 마이크로초(백만분의 일초)
    786001
    ```

  - 매서드(method)

    - weekday() : 요일반환

      ```
      >>> now.weekday 
      <built-in method weekday of datetime.datetime object at 0x000001EB3E8DAFC0>
      >>> now.weekday() # {0:월, 1:화, 2:수, 3:목, 4:금, 5:토, 6:일}
      4
      ```

      

    - strftime() : 문자열 반환

      ```
      >>> now.strftime("%A %d. %B %Y")
      'Friday 09. December 2022'
      >>> now.strftime("%H시 %M분 %S초")
      '01시 15분 15초'
      ```

      | 날짜 및 시간 지정 문자열 | 의미                                                   |
      | ------------------------ | ------------------------------------------------------ |
      | `%Y`                     | 앞의 빈자리를 0으로 채우는 4자리 연도 숫자             |
      | `%m`                     | 앞의 빈자리를 0으로 채우는 2자리 월 숫자               |
      | `%d`                     | 앞의 빈자리를 0으로 채우는 2자리 일 숫자               |
      | `%H`                     | 앞의 빈자리를 0으로 채우는 24시간 형식 2자리 시간 숫자 |
      | `%M`                     | 앞의 빈자리를 0으로 채우는 2자리 분 숫자               |
      | `%S`                     | 앞의 빈자리를 0으로 채우는 2자리 초 숫자               |
      | `%A`                     | 영어로 된 요일 문자열                                  |
      | `%B`                     | 영어로 된 월 문자열                                    |

    - strptime() : datetime 클래스 객체 반환

      - strptime(날짜와 시간 정보를 가진 문자열, 형식) 

      ```
      >>> datetime.datetime.strptime("2017-01-02 14:44", "%Y-%m-%d %H:%M")
      datetime.datetime(2017, 1, 2, 14, 44)
      >>> datetime.datetime.strptime("1997-11-27", "%Y-%m-%d").strftime("%Y년 %m월 %d일")
      '1997년 11월 27일'
      ```

      

    - date() : 날짜 정보만 가지는 `date` 클래스 객체 반환

      ```
      >>> now.date()
      datetime.date(2022, 12, 9)
      ```

      

    - time() : 시간 정보만 가지는 `time` 클래스 객체 반환

      ```
      >>> now.time()
      datetime.time(1, 15, 15, 786001)
      ```



## timedelta 

- 특정 시점의 기간을 구할 수 있음.

- 현재 날짜를 기준으로 5일 뒤의 날짜 구하는 코드

  ```
  import datetime as dt
  today = dt.date.today()
  print(today)
  >>> 2022-12-09
  
  a = dt.timedelta(days=5)
  print(today + a)
  >>> 2022-12-14
  ```

- 응용 - 산술 및 대소연산자 사용가능.

  ```
  from datetime import date, timedelta
  week = timedelta(weeks=1) # 7일
  >>> datetime.timedelta(days=7)
  
  next_week = date.today() + week
  >>> datetime.date(2022, 12, 16)
  
  two_weeks = week * 2
  >>> datetime.timedelta(days=14)
  
  # 대소 비교 
  week < two_weeks
  >>> True
  
  two_weeks == timedelta(weeks=2)
  >>> True
  
  # 다음주에서 2주전 날짜(==현재기준 저번주 날짜)
  last_week = next_week - two_weeks
  >>> datetime.date(2022, 12, 2)
  ```

  



# time

- time package

  - sleep : 실행을 잠시 멈추는 함수.

    ```
    import time
    time.sleep(5) #5초 동안 쉬었다가 다음 코드 실행.
    ```

  - time() : 현재 시간

    - 1970년 1월 1일 0시 0분 0초 이후 경과한 시간을 초 단위로 반환함.

    ```
    time.time()
    >>> 1670518465.397561
    ```

    



# module & package & library

### 함수

- 미리 정한 동작을 수행하는 코드를 묶은 것.

### 모듈(module)

- 전역변수, 함수, 클래스 등을모아 놓은 파일. 
  - 함수의 집합

### 패키지(package)

-  모듈의 집합

### 라이브러리(library)

- 패키지의 집합



# reference

https://datascienceschool.net/01%20python/02.15%20%ED%8C%8C%EC%9D%B4%EC%8D%AC%EC%97%90%EC%84%9C%20%EB%82%A0%EC%A7%9C%EC%99%80%20%EC%8B%9C%EA%B0%84%20%EB%8B%A4%EB%A3%A8%EA%B8%B0.html

https://taehyeki.tistory.com/142

https://greeksharifa.github.io/references/2021/05/18/time-datetime-usage/



https://losskatsu.github.io/programming/function-module-package/#2-%EB%AA%A8%EB%93%88