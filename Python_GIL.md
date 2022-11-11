# Python_GIL

[공식문서](https://wiki.python.org/moin/GlobalInterpreterLock)



[참고자료 : 블로그](https://hongl.tistory.com/240)

[참고자료2 : 블로그](https://seongonion.tistory.com/117)



**CPython** (파이썬의 표준구현을 CPython이라고 함.)

-   소스 코드를 구문 분석해서 8비트 명령어로 이루어진 바이트코드(파이썬 3.6부터는 16비트 명령어를 사용함_워드코드)로 변환
-   스택 기반 인터프리터를 통해 바이트코드를 실행함

-   **바이트코드 인터프리터**에는 파이썬 프로그램이 실행되는 동안 일관성 있게 유지해야 하는 상태가 존재함.

-   CPython은 스레드 세이프하지 않는 메모리 관리를 쉽게 하기 위해, **GIL(Global Interpreter Lock)**이라는 방법으로 여러 개의 스레드의 메모리 접근을 제한하는 형태로 일관성을 강제로 유지함.
    -   즉, 여러 개의 스레드가 병렬로 존재하더라도 실제로는 특정 순간에 하나의 스레드만 동작함.

![GIL (Global Interpreter Lock), Multi-Threading](https://blog.kakaocdn.net/dn/NMZMc/btq7Fh10ids/ldqiHOn73U62KEfO6USX40/img.png)

**GIL**

-   상호배제 락(mutual exclusive lock, mutex) 형식
-   한 스레드가 다른 스레드의 실행을 중간에 인터럽트시키고 제어를 가져오지 못하게 방지함.
    -   독립적으로 메모리 영역을 할당받는 프로세스와 달리 프로세스 내에서 stack 메모리만 각각 할당받고 나머지 메모리는 공유하는 방식.
        -   스레드간 인터럽트가 발생하면 전역변수, garbage collector 참조변수 등의 인터프리터 상태가 오염될 수 있음.
        -   따라서 CPython은 멀티 스레드라 하더라도 GIL을 이용해 하나의 스레드만 자원을 독점하게 하여 인터프리터 상태가 제대로 유지되고 바이트코드 명령어들이 제대로 실행되게 함.
-   스레드 세이프를 위한 GIL의 사용은 태생적으로 속도 향상을 위한 멀티 스레딩을 동시에 할 수 없음.
    -   python에서도 "threading" 모듈로 멀티 스레드를 지원하지만 GIL로 인해 여러 스레드 중 하나만 진행 가능함.



**파이썬에서의 멀티 스레드 사용**

파이썬에서 멀티 스레딩을 하는 것이 무조건 불리하지 않음.

**GIL은 파이썬의 런타임과의 상호작용 여부에 의해 영향을 받음.**

따라서, 파이썬 런타임과 상호작용을 하는 CPU-Bound 작업들에서는 GIL이 계속 영향을 주기 때문에 멀티 스레드를 이용하더라도 성능 향상을 기대하기 힘든 반면, **I/O-Bound 작업에선 극적이진 않더라도 어느 정도의 성능 향상을 기대할 수 있음.**

-    I/O-Bound : 프로그램 실행 중 I/O 인터럽트 발생 시 파이썬은 GIL을 release함.
    -   이 때, 단일 스레드라면 I/O 작업이 완료될 때까지 다른 작업들이 block되지만, 
    -   멀티 스레드를 사용한다면 기존 실행 중이던 스레드가 GIL을 release하자마자 다른 스레드가 곧바로 GIL을 넘겨받게 되므로, I/O 작업 처리 시 발생하는 딜레이들을 줄일 수 있음.
    -   그 외에도, 파이썬의 Numpy 라이브러리를 이용한 number crunching 작업도 GIL 밖에서 처리됨



----



## CPU bound, IO bound

[참고자료](https://taes-k.github.io/2021/06/05/cpu-io-bound/)

[참고자료 : I/O](https://chelseafandev.github.io/2021/07/13/os-io-system/)



**Burst**

어떤 특정된 기준(criterion)에 따라 한 단위로서 취급되는 연속된 신호(signal) 또는 데이터의 모임.

어떤 현상이 짧은 시간에 집중적으로 일어나는 현상.

또는 주기억 장치의 내용을 캐시 기억 장치에 블록 단위로 한꺼번에 전송하는 것.

-   `CPU burst`는 프로세스 내에서 `CPU 명령`작업이 연속된 작업을 의미
-   `IO burst`는 로컬 혹은 네트워크등의 `I/O wait` 작업이 연속되는것을 의미
-   프로세스는 수행과정중에 `CPU burst`, `I/O burst` 가 계속 변경되면서 수행되며 프로세스 작업의 종류에 따라 `CPU burst`가 일어나는 시간이 달라짐
    -   이때 일반적으로 `CPU burst`가 많이 일어나는 작업을 `CPU bound process` 라고 부름



**CPU Bound process**

`CPU`의 주 목적에 부합하는 `연산`처리가 많은 프로세스에서 `CPU burst`가 많이 일어남

-   예시) 데이터 마이닝, 이미지 프로세싱, 암호화폐 마이닝

-   성능 향상
    -   CPU 성능 향상 _ 높은 클럭의 CPU 사용
    -   CPU 병렬 처리 _ 멀티코어 프로세서 추가
    -   (머신러닝_CPU연산이 많이 발생) _ `Many-core processor`인 `GPU`를 사용



**IO Bound process**

I/O : 입출력 처리

-   I/O란 하드웨어 장치를 통한 입출력 정보를 컴퓨터에서 구동 중인 어플리케이션에서 컨트롤하고자 할 때 사용하는 일종의 인터페이스

-   성능향상
    -   (로컬 저장소에 대한 `I/O wait`가 많은 작업)_하드웨어 교체`(HDD -> SSD)`
    -   로컬 저장소보다 빠른 `memory`를 활용
    -   `Non-blocking I/O`를 통해 쓰로풋을 향상