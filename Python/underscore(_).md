# ❗ Python Underscore

-   Python에서 underscore은 스네이크 표기법이나 변수 또는 함수명을 위해 사용될 뿐만아니라 다양한 의미를 가지고 있음.
    -   for _ in range(10) 또는 \_\_init__(self)등 익숙하게 보았지만 제대로 정리하기 위해 해당 글을 작성함.
-   Python에서 underscore은 크게 5가지 경우로 상용됨.
    -   인터프리터(Interpreter)에서 마지막 값을 저장할 때
    -   값을 무시하고 싶을 때
    -   변수나 함수명에 특별한 의미 또는 기능을 부여하고자 할 때
    -   국제화(Internationalization, i18n)/ 지역화(Localization, I10n)함수로써 사용할 때
    -   숫자 리터럴값의 자릿수 구분을 위한 구분자로써 사용할 때



## 1. 인터프리터에서 사용되는 경우

-   파이썬 인터프리터에선 마지막으로 실행된 결과값이 _라는 변수에 저장됨.

    -   이는 표준 CPython 인터프리터에서 먼저 사용되었으며 다른 파이썬 인터프리터 구현체에서도 동일하게 사용가능함.

    ```
    >>> 10
    10
    >>> _
    10
    >>> _*3
    30
    >>> _/2
    5.0
    >>> 3
    3
    >>> _
    3
    ```

    

##  2. 값을 무시하고 싶을 때

-   어떤 특정 값을 무시하기 위한 용도로 사용됨.

    -   값이 필요하지 않거나 사용되지 않는 값을 _에 할당하면 됨.

    ```
    # 언패킹시 특정값을 무시
    >>> x, _, y = (1, 2, 3) 
    >>> x
    1
    >>>y
    3
    
    # 여러개의 값 무시하려면 *을 붙여서 사용함.
    >>> x, *_, y = (1, 2, 3, 4, 5)
    >>> x 
    1
    >>> y
    5
    ```

    -   변수가 0, 1, 2, 3, 4 값을 가지고 반목을 수행함.
        -   실제로 사용되지 않기 때문에 "_" 를 사용함.

    ```python
    for _ in range(5): # 단순히 5번 반복할 목적으로
        print('hello world')
        
    # 결과
    hello world
    hello world
    hello world
    hello world
    hello world
    
    ```

    ```py
    for _ in range(3): # _를 i로 바꿔서 보면 우리에게 익숙한 표현식일 것이다.
        print(_)
    # 결과
    0
    1
    2
    ```

    ```py
    def values():
        return (1,2,3,4) # 튜플을 반환
    a, b, _, _ = values() # 반환된 튜플 값중 2개만 필요할 경우
    ```

    ```py
    >>> print(a, b)
    1 2
    ```

    

    

## 3. 특별한 의미의 네이밍을 하는 경우

-   파이썬에서 가장 많이 사용되는 것을 볼 수 있음.
    -   4가지의 언터스코어를 활용한 네이밍 컨벤션(파이썬 컨벤션 가이드라인:PEP8)

### `_single_leading_underscore`

-   주로 한 모듈 내부에서만 사용하는 private 클래스/함수/변수/메서드를 선언할 때 사용하는 컨벤션

-   이 컨벤션으로 선언하게 되면 `from module import *`시 " _ "로 시작하는 것들은 모두 임포트에서 무시된다. 

    -   그러나, 파이썬은 진정한 의미의 private을 지원하고 있지는 않기 때문에 private을 완전히 강제할 수는 없다. 즉, **위와 같은 임포트문에서는 무시되지만 직접 가져다 쓰거나 호출을 할 경우엔 사용이 가능하다**. 그래서 “weak internal use indicator"라고 부르기도 한다.

    ```py
    _internal_name = 'one_module' # private 변수
    _internal_version = '1.0' # private 변수
    ```

    ````py
    class _Base: # private 클래스 
        _hidden_factor = 2 # private 변수
        def __init__(self, price):
            self._price = price
    
        def _double_price(self): # private 메서드
            return self._price * self._hidden_factor
    
        def get_double_price(self):
            return self._double_price()
    ````

    

### `single_trailing_underscore_`

-   파이썬 키워드와의 충돌을 피하기 위해 사용하는 컨벤션. (많이 사용되지 않음)

```py
Tkinter.Toplevel(master, class_='ClassName') # class와의 충돌을 피함
list_ = List.objects.get(1) # list와의 충돌을 피함
```



### `__double_leading_underscores`

-   컨벤션이라기보단 하나의 문법적인 요소. 

-   더블 언더스코어는 클래스 속성명을 *맹글링*하여 <u>클래스간 속성명의 충돌을 방지</u>하기 위한 용도로 사용됨. 

    -   *맹글링이란, 컴파일러나 인터프리터가 변수/함수명을 그대로 사용하지 않고 일정한 규칙에 의해 변형시키는 것을 말함*

-   **파이썬의 맹글링 규칙**은 더블 언더스코어로 지정된 속성명 앞에 _ClassName을 결합하는 방식. 

    -   즉, ClassName이라는 클래스에서 __method라는 메서드를 선언했다면 이는 _ClassName\_\_method로 맹글링 된다.

    ```py
    class A:
        def _single_method(self):
            pass
    
        def __double_method(self): # 맹글링을 위한 메서드
            pass
    
    class B(A):
        def __double_method(self): # 맹글링을 위한 메서드
            pass
    
    print(dir(A())) 
    # ['_A__double_method', ..., '_single_method']
    print(dir(B())) 
    # ['_A__double_method', '_B__double_method', ..., '_single_method']
    
    # 서로 같은 이름의 메서드를 가지지만 오버라이드가 되지 않는다.
    ```

    -   더블 언더스코어로 지정된 속성명은 위와 같이 맹글링이 되기 때문에 일반적인 속성 접근인 `ClassName.__method`으로 접근이 불가능. 
        -   간혹, 이러한 특징으로 더블 언더스코어를 사용해 진짜 private처럼 보이게 하는 경우가 있는데 이는 private을 위한 것이 아니며 private으로의 사용도 권장되지 않음. ([Python Naming](http://python.net/~goodger/projects/pycon/2007/idiomatic/handout.html#naming))



### `__double_leading_and_trailing_underscores__`

-   스페셜 변수나 메서드(매직 메서드)에 사용되는 컨벤션이며, `__init__`, `__len__`과 같은 메서드들이 있음. 

    -   이런 형태의 메서드들은 어떤 특정한 문법적 기능을 제공하거나 특정한 일을 수행함. 

        -   `__file__` : **현재 파이썬 파일의 위치를 나타내는 스페셜 변수**
        -    `__eq__`  : **`a == b`라는 식이 수행될 때 실행되는 스페셜 메서드**
        -   `__init__` : **클래스의 인스턴스가 생성될 때 처음으로 실행되는 메서드**

    -   사용자가 직접 만들 수도 있지만 그런 경우는 정말 거의 없으며, 일부 스페셜 메서드의 경우 직접 수정하거나 하는 일은 빈번히 있을 수 있음.

        -   `__init__` : 인스턴스의 초기화 작업을 이 메서드의 내용으로 작성할 수 있음.

        ```py
        class A:
            def __init__(self, a): # 스페셜 메서드 __init__에서 초기화 작업을 한다.
                self.a = a
        
            def __custom__(self): # 커스텀 스페셜 메서드. 이런건 거의 쓸 일이 없다.
                pass
        ```

-   folder
    -   " __ init__.py "라는 파일이 있으면 그 폴더를 패키지로 만들 수 있음.

-   method

    -   __init__은 클래스의 생성자 함수이며, __add__ 함수는 연산자 오버로드용으로 사용됨.

    ```py
    class vector:
      def __init__(self, x,y,z):
        self.x = x
        self.y = y
        self.z = z
    
      def __add__(self, other):
        x_ = self.x + other.x
        y_ = self.y + other.y
        z_ = self.z + other.z
    
        return vector(x_,y_,z_)
    
      def show(self):
        print(f"x:{self.x}, y:{self.y}, z:{self.z}")
    
    
    v1 = vector(1,2,3)
    v2 = vector(4,5,6)
    v3 = v1 + v2
    
    >>> v3.show()
    x:5, y:7, z:9
    ```

    



## 4. 국제화(i18n)/지역화(l10n)함수로 사용되는 경우

-   어떤 특정한 문법적 규칙이라기보단 말 그대로 컨벤션임.

    -   " _ "가 국제화/지역화 함수라는 의미는 아니며, **i18n/l10n 함수를 _로 바인딩하는 C 컨벤션에서 유래된 컨벤션.**
    -   i18n/l10n 라이브러리인 `gettext`라는 파이썬 내장 라이브러리 API 문서에서도 이 컨벤션을 사용하고 있으며, i18n과 l10n을 지원하는 파이썬 웹 프레임워크인 Django의 공식 문서에서도 이 컨벤션을 소개하면서 사용하고 있음.

    ```
    # gettext 공식 문서 참고 : https://docs.python.org/3/library/gettext.html
    import gettext
    
    gettext.bindtextdomain('myapplication', '/path/to/my/language/directory')
    gettext.textdomain('myapplication')
    _ = gettext.gettext
    
    # ...
    
    print(_('This is a translatable string.'))
    ```

    ```
    from django.utils.translation import ugettext as _
    from django.http import HttpResponse
    
    def translate_view(request):
      translated = _('This string will be translated.')
      return HttpResponse(translated)
    ```

    

## 5. 숫자 리터럴 값의 자릿수 구분을 위한 구분자로써 사용할 때

-   Python 3.6에 추가된 문법으로 언더스코어로 숫자값을 좀 더 읽기 쉽도록 자릿수를 구분할 수 있음.

    ```py
    dec_base = 1_000_000
    bin_base = 0b_1111_0000
    hex_base = 0x_1234_abcd
    
    print(dec_base) # 1000000
    print(bin_base) # 240
    print(hex_base) # 305441741
    ```

    





# 참고자료

https://mingrammer.com/underscore-in-python/

https://syujisu.tistory.com/130

https://ebbnflow.tistory.com/255