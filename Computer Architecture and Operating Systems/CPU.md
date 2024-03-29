# CPU

-   컴퓨터 시스템을 이루는 3대 구성 : CPU, 메모리, 디스크
    -   운영체제의 3대 기능 : CPU 관리, 메모리 관리, 디스크 관리



-   폰 노이만 구조
    -   컴퓨터의 기본 골격 : CPU, 메모리, 디스크 , I/O
        -   특징 
            -   명령어/ 데이터 로드 / 실행/ 저장을 순차적으로 수행
            -   데이터/ 프로그램 메모리를 하나의 버스로 접근하는 구조.
        -   중앙처리장치를 통해 연산을 수행하는 구조
            -   CPU(중앙처리 장치)는 각종 연산을 수행하고 기억장치에 기억되어 있는 명령어들을 수행하는 컴퓨터 시스템을 이루는 핵심 부품.

## CPU의 속도 : Hz & Clock

-   대개 컴퓨터의 성능은 CPU의 속도와 메모리 용량으로 표현 가능.
-   **Hz(헤르츠) = CPU의 속도 단위**
    -   통신분야에서 사용되는 주파수와 동일한 의미.
        -   1초에 몇 번이나 진동하는가
        -   **1Hz : 1초에 한번 왕복 운동이 반복됨**
        -   예시) **100 Hz 는 어떠한 현상이 1 초에 100 번을 반복 혹은 진동됐다는 의미**

-   CPU 일정한 속도로 동작하기 위해서는 일정한 간격으로 전기적
    펄스를 공급함
    -   **이 전기적 신호가 초당 CPU 에 공급되는 횟수**라는 개념에서 Hz 라는 단위를 쓴다.
-   **Clock**  = 시스템내의 **CPU 에 전기적으로 공급되는 신호**
    -   주기적으로 일정한 시그널을 보내주는 칩
    -   Clock 에서는 일정 볼트로 주기적으로 신호를 발생함
        -   그러면 CPU 는 이 신호를 받고 데이터를 주거나 받고 처리하게 하게 됨.
    -   이 신호(Clock) 한번에 의해서 CPU 에서 한 개의 명령이 처리된다.
    -   반복적인 신호가 들어올 때마다 명령어를 수행하기 때문에 **(Clock 신호가) 빠르게 들어온다는 것**은 결국 **빠른 속도의 처리 능력을 갖는 시스템을 의미하는 것**

-   CPU 의 속도를 Hz 로 나타내고 이 Hz 가 높으면 속도가 빠른 성능의 CPU 가 되는 것.



## CPU의 구성도

-   **산술/논리 연산 장치(ALU), 제어 장치와 레지스터**로 구성되어 있음.
    -   산술 : 덧셈을 수행하는 것.
    -   제어장치 : 시그널을 통해서 데이터 흐름을 통제하는 것
    -   레지스터 : CPU 내부의 메모리
-   그림1-1.cpu 내부의 기본 구조

![image-20221020142736012](C:\TIL\Computer Architecture and Operating Systems\asset\image-20221020142736012.png)