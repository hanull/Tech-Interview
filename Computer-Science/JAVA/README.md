# JAVA
## [캐스팅](#캐스팅)
- 캐스팅이란?

## [박싱(boxing), 언박싱(unboxing)](#박싱(boxing),-언박싱(unboxing))
- 박싱(boxing), 언박싱(unboxing)

## [String & StringBuilder & StringBuffer](#String-&-StringBuilder-&-StringBuffer)
- String & StringBuilder & StringBuffer 차이점

## [스레드](#스레드)
- 스레드란?
- 스레드의 실행을 start()를 사용하는 이유는?

## [컴파일 과정 & JVM](#컴파일-과정-&-JVM)
- 자바 컴파일 과정을 설명해주세요
- JVM이란?

## [call by value & call by reference 차이](#💡-call-by-value-&-call-by-reference-차이)
- call by value & call by reference 차이

## 캐스팅
### 캐스팅에 대해 설명해주세요.
타입 변환을 말한다. 
- 업캐스팅
    - 서브 클래스의 객체가 수퍼 클래스 타입으로 형변환 되는 것을 말한다.
- 다운캐스팅
    - 업캐스팅 된 것을 다시 원상태로 되돌리는 것을 말한다.

## 박싱(boxing), 언박싱(unboxing)
### 💡 박싱(boxing), 언박싱(unboxing)이란?
기본 타입의 데이터를 래퍼 클래스의 인스턴스로 변화하는 과정을 박싱(boxing), 래퍼 클래스의 인스턴스에 저장된 값을 다시 기본 타입의 데이터로 꺼내는 과정을 언박싱(unboxing)이라고 한다.

## String & StringBuilder & StringBuffer
### 💡 String & StringBuilder & StringBuffer 차이점을 설명해주세요.
- String
    - String은 immutable하다. 즉, 한 번 생성되면 변경될 수 없고, 할당된 메모리 공간이 변하지 않는다.
    - 문자열 추가, 수정, 삭제가 빈번하게 발생하는 경우 가비지가 생성되어 힙메모리 부족으로 성능에 영향을 끼치게 된다.
- StringBuilder & StringBuffer
    - String과 달리 가변성이다. 즉, 메모리에 추가, 삭제가 가능하다.
    - 따라서 문자열의 추가, 수정, 삭제가 빈번하게 발생하는 경우 StringBuilder, StringBuffer를 사용하는 것이 좋다.
    - StringBuilder와 StringBuffer의 차이는 동기화 유무이다.
    - StringBuilder
        - 동기화 보장하지 않음
        - 멀티 스레드 환경에 적합하지 않다
        - 단일 스레드에의 성능은 더 좋다
    - StringBuffer
        - 동기화 보장
        - 멀티 스레드 환경에 안전함

## 스레드
### 💡 스레드란?
프로그램 실행 단위를 말한다. 동시 처리를 위해 사용한다. Runnable interface, Thread Class 를 통해 생성한다.


### run()이 아닌 start()를 사용하는 이유?
start()는 동시성을 위해서 call stack 내에 새로운 메모리를 할당받고 실행한다.


## 컴파일 과정 & JVM
### 💡 자바 컴파일 과정을 설명해주세요.
1. 자바 소스코드(.java)를 작성한다.
2. 컴파일러에 의해 소스파일를 바이트코드(.class)로 컴파일한다.
3. 컴파일된 바이트코드를 JVM의 클래스로더(Class Loader)에 의해 JVM 내로 로드된다.
4. 실행엔진(Execution Engine)에 의해 기계어로 해석되어 메모리(Runtime Data Area)에 배치되게 된다.
5. 실행 엔진은 인터프리터(Interpreter), JIT(Just-In-Time) 컴파일러가 있다.

### 💡 JVM이란?
- JVM이란 자바 가상 머신의 약자를 줄여 부르는 용어이다.
- 자바와 OS사이에서 중개자 역할을 수행하여 OS에 독립적인 플랫폼을 갖게 해준다. 즉 OS 의 메모리 영역에 직접적으로 접근하지 않고 JVM 이라는 가상 머신을 이용해서 간접적으로 접근한다. 
- GC를 통해서 프로그램의 메모리 관리를 알아서 해준다. 

### 💡 call by value & call by reference 차이
결론부터 말하면 자바는 `call by Value` 이다.
- call by value
    - 함수의 인자로 전달되는 타입이 기본형(원시 자료형)인 경우 값을 넘기게 되어있다. 이 경우 메모리에는 함수를 위한 별도의 공간이 생성되고 이는 함수 종료 시 사라진다. 따라서 함수 안에서 해당 인자의 값을 변경하더라도 원본 값은 바뀌지 않는 특징이 있다.

```java
public static void main(String[] args) {
    int a = 10;
    int b = 20;
    swap(a, b);
    System.out.println("a = " + a + ", " +  "b = " + b);
}

private static void swap(int a, int b) {
    int tmp = b;
    b = a;
    a = tmp;
}
```

```
a = 10, b = 20
```

- call by reference
    - 참조형(참조 타입)인 경우, 변수가 가지는 값이 주소 값이므로 Call by Value에 의해 주소 값이 전달된다. 따라서 함수 안에서 해당 인자의 값을 변경하게 되면 원본 값도 바뀌게 되는 특징이 있다.

```java
public static void main(String[] args) {
    int[] array = {10, 20};
    multiply(array, 10);
    for (int num : array) {
        System.out.println(num);
    }
}

private static void multiply(int[] array, int num) {
    for (int i = 0; i < array.length; i++) {
        array[i] *= num;
    }
}
```

```
100
200
```

