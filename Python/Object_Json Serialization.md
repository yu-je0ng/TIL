# 직렬화, 역직렬화

- 직렬화 
  - 객체에 저장된 데이터를 I/O 스트림에 쓰기(출력)위해 연속적인(serial)데이터로 변환하는 것.
- 역직렬화
  - I/O 스트림에서 데이터를 읽어서(입력) 객체를 만드는 것.
- 직렬화와 역직렬화는 객체를 파일로 저장하거나 네트워크를 통해 전송하기 위해 제공되는 기능임.
- 객체
  - 인스턴스 변수의 집합.
  - "객체를 저장/전송한다"는 것은 객체의 인스턴스 변숭의 값을 저장/전송하는 것과 동일함.
- 객체 직렬화는 JVM에서 자바 객체를 내보내는(출력하는) 간단한 방법임.
  - 직렬화된 객체는 파일로 저장하거나, 네트워크로 전송하거나, 다른 I/O 인터페이스에 내보낼 수 있음.  

## [JAVA] ObjectInputStream과 ObjectOutputStream

- 자바에서는 객체 직렬화, 역직렬화를 위해 ObjectInputStream과 ObjectOutputStream을 제공함.
  - 객체를 스트림에 쓰거나(출력) 읽는 기능(입력)을 제공하는 보조스트림(기반스트림 필요)
- **ObjectInputStream** extends OutputStream
  - 직렬화 : 스트림에 객체를 출력하기 위해 사용
  - writeObject()
- **ObjectInputStream** extends InputStream
  - 역직렬화 : 스트림으로부터 객체를 입력받기 위해 사용
  -  readObject() : Object로 리턴되므로 형변환 필요
- writeObject()/readObject()뿐만 아니라 primitive(기본, 원시) 타입에 대응하는 메소드도 제공됨.
  - 또 다른 보조 스트림 중 **DataInputStream/DataOutputStream**은 Object 타입을 제외하고 writeByte(), wirteChar(), writeUTF()나 readByte(), readChar(), readUTF()와 같이 기본적인 데이터 타입을 유지하며 읽거나 쓰는 기능을 제공하는데, 직렬화의 기반 개념이 된 스트림임.

## [PYTHON] Serialize

### 	 Json 직렬화

- 직렬화는 객체를 문자열로 변환하는 작업
- 파이썬에서는 기본 내장 라이브러리로 Json의 직렬화와 역직렬화를 수행할수 있음

```python
>>> import json
>>> post_list = [{ 'message' :  'hello'}]
>>> print(type(post_list))
<class 'list'>
>>> json_string = json.dumps(post_list)
>>> print(type(json_string))
<class 'str'>
>>> json_string
'[{"message": "hello"}]'
```

### 역직렬화

- 역직렬화는 문자열을 다시 객체로 변환하는 작업

```py
>>> json.loads(json_string)
[{'message': 'hello'}]
```





# 클래스, 객체, 인스턴스

## 클래스(Class)

- 개념
  - 객체를 만들어 내기 위한 설계도 혹은 틀
  - 연관되어 있는 변수와 매서드의 집합

## 객체(Object)

- 개념
  - 소프트웨어 세계에 구현할 대상
  - 클래스에 선언된 모양 그대로 생성된 실

- 특징
  - '클래스의 인스턴스(instance)'라고도 불림.
  - 객체는 모든 인스턴스를 대표하는 포괄적인 의미를 갖음.
  - oop의 관점에서 클래스의 타입으로 선언되었을 때 '객체'라고 부름

##  인스턴스(instance)

- 개념
  - 설계도를 바탕으로 소프트웨서 세계에 구현된 구체적인 실체
    - 즉, 객체를 소프트웨어에 실체화 하면 그것을 '인스턴스'라고 부른다.
    - 실체화된 인스턴스는 메모리에 할당된다.
- 특징
  - 인스턴스는 객체에 포함된다고 볼 수 있다.
  - oop의 관점에서 객체가 메모리에 할당되어 실제 사용될 때 '인스턴스'라고 부른다.
  - 추상적인 개념과 구체적인 객체 사이의 관계에 초첨을 맞출 경우에 사용한다.
    - '~의 인스턴스'의 형태로 사용된다.
    - 객체는 클래스의 인스턴스이다.
    - 객체 간의 링크는 클래스 간의 연관 관계의 인스턴스이다.
    - 실행 프로세스는 프로그램의 인스턴스이다.
  - 즉, 인스턴스라는 용어는 반드시 클래스와 객체 사이의 관계로 한정지어서 사용할 필요없다.
    - 인스턴스는 어떤 원본(추상적인 개념)으로부터 '생성된 복제본'을 의미한다.

```java
/* 클래스 */
public class Animal {
  ...
}
/* 객체와 인스턴스 */
public class Main {
  public static void main(String[] args) {
    Animal cat, dog; // '객체'

    // 인스턴스화
    cat = new Animal(); // cat은 Animal 클래스의 '인스턴스'(객체를 메모리에 할당)
    dog = new Animal(); // dog은 Animal 클래스의 '인스턴스'(객체를 메모리에 할당)
  }
}
```



## 클래스, 객체, 인스턴스의 차이

### 클래스(Class) VS 객체(Object)

- 클래스는 ‘설계도’, 객체는 ‘설계도로 구현한 모든 대상’을 의미한다.

### 객체(Object) VS 인스턴스(Instance)

- 클래스의 타입으로 선언되었을 때 객체라고 부르고, 그 객체가 메모리에 할당되어 실제 사용될 때 인스턴스라고 부른다.
- 객체는 현실 세계에 가깝고, 인스턴스는 소프트웨어 세계에 가깝다.
- 객체는 ‘실체’, 인스턴스는 ‘관계’에 초점을 맞춘다.
- 객체를 ‘클래스의 인스턴스’라고도 부른다.
- ‘방금 인스턴스화하여 레퍼런스를 할당한’ 객체를 인스턴스라고 말하지만, 이는 원본(추상적인 개념)으로부터 생성되었다는 것에 의미를 부여하는 것일 뿐 *엄격하게 객체와 인스턴스를 나누긴 어렵다.*

### 참고

- 추상화 기법
  1. **분류(Classification)**
     - **객체 -> 클래스**
     - 실재하는 객체들을 공통적인 속성을 공유하는 범부 또는 추상적인 개념으로 묶는 것
  2. **인스턴스화(Instantiation)**
     - **클래스 -> 인스턴스**
     - 분류의 반대 개념. 범주나 개념으로부터 실재하는 객체를 만드는 과정
     - 구체적으로 클래스 내의 객체에 대해 특정한 변형을 정의하고, 이름을 붙인 다음, 그것을 물리적인 어떤 장소에 위치시키는 등의 작업을 통해 인스턴스를 만드는 것을 말한다.
     - ‘예시(Exemplification)’라고도 부른다.
       

# reference

https://atoz-develop.tistory.com/entry/JAVA%EC%9D%98-%EA%B0%9D%EC%B2%B4-%EC%A7%81%EB%A0%AC%ED%99%94Serialization%EC%99%80-JSON-%EC%A7%81%EB%A0%AC%ED%99%94

https://gmlwjd9405.github.io/2018/09/17/class-object-instance.html