## 자바 메모리 구조 
---

### 힙(Heap)
- 객체들이 저장되는 영역 
- 가바지 컬렉션이 이루어지는 주요 영역
### 스택(Stack)
- 메서드 호출 시 지역 변수들이 저장되는 영역 
- 원시타입 리터럴 값이 저장되는 영역
- 각 쓰레드별로 하나 씩 생성됨
### 메서드(Method) 영역
- 클래스 구조와 메서드 코드, static 변수 및 상수 풀 등이 저장되는 영역
- 클래스의 내부 메서드는 메서드 영역에서 공통으로 관리 및 실행 (여러개 생성 x)

❗️ **상수풀이란 **

```java

    String str1 = "Hello";
    String str2 = "Hello";

    System.out.println(str1 == str2); // true
    
```
**❗️ 상수풀 장점**

- 메모리 절약
동일한 문자열 리터럴은 상수 풀에 한 번만 저장되므로, 메모리 사용을 줄임
- 속도 향상
문자열 비교 시 참조를 비교하는 것이 값 자체를 비교하는 것보다 빠름
---
## 스택과 큐 자료구조 

![](https://velog.velcdn.com/images/boram0415/post/be25bc50-3e32-4ab0-9d30-2c1ace90b66a/image.png)

**Stack 후입 선출(LIFO, Last In First Out)**
나중에 넣은 것이 가장 먼저 나오는 것
**Queue 선입 선출(FIFO, First In First Out)**
가장 먼저 넣은 것이 가장 먼저 나오는 것

---
## 스택 영역과 힙 영역 



![](https://velog.velcdn.com/images/boram0415/post/d08aa686-9bdb-4120-968f-81249d5aeb05/image.png)

- 스택 내부에서 method1() 메서드가 실행이 되어 내부의 전역변수중 참조변수가 힙 영역에 만들어진 인스턴스를 가르킴 


![](https://velog.velcdn.com/images/boram0415/post/1b54f2e1-ce2f-45b9-8be0-9d03b82a3b06/image.png)

- method1() 종료 후 참조하는 곳이 없어진 인스턴스는 GC 대상임 

❗️ 힙 영역 외부가 아닌, 힙 영역 안에서만 인스턴스끼리 서로 참조하는 경우에도 GC의 대상이 됨 
ㅤ
## static 변수와 메서드
---
### Static 변수(클래스 변수,정적 변수)
`클래스 수준에서 관리`
- Static 변수는 클래스에 속하며, 클래스의 모든 인스턴스가 이 변수를 공유

`메모리 할당`
- 클래스가 처음 로드될 때 메서드 영역(Method Area)에 한 번만 할당

`공유 자원`
- 모든 인스턴스가 동일한 Static 변수를 공유하기 때문에, 하나의 인스턴스가 이 변수를 변경하면 
다른 인스턴스에서도 변경 됨

`접근 방식`
- 클래스명으로 직접 접근. ex) ClassName.staticVariable
- 인스턴스명으로도 접근 가능하지만, 변수의 구분을 위해 권장x
    
`초기화`
- Static 변수는 클래스가 로드될 때 초기화되며, 초기화 블록이나 static 초기화 블록에서 초기값을 설정 가능

----
### Static 메서드(클래스 메서드)

`클래스 수준에서 관리`
- Static 메서드는 클래스에 속하며, 객체 인스턴스와 무관하게 호출 가능

`인스턴스 변수 사용 불가`
- Static 메서드는 인스턴스 변수나 인스턴스 메서드를 직접 사용 불가
- Static 변수와 Static 메서드만 사용 가능

`접근 방식`
- 클래스명으로 직접 접근. ex) ClassName.staticMethod()
- 인스턴스명으로도 호출 가능하지만, 권장 x 

`주요 용도`
- 유틸리티 메서드나 공통 로직을 구현하는 데 사용 됨

`오버라이딩 불가`
- Static 메서드는 인스턴스 메서드가 아니기 때문에 상속받은 클래스에서 오버라이딩 불가
하지만, 같은 이름의 static 메서드를 다시 정의하여 사용 가능 ( 이를 “숨김(hiding)“이라고 함 )



```java
// static 메서드의 정적바인딩 예시 코드
class Parent {
    public static void staticMethod() {
        System.out.println("Parent's static method");
    }
}

class Child extends Parent {
    public static void staticMethod() {
        System.out.println("Child's static method");
    }
}

public class Main {
    public static void main(String[] args) {
        Parent obj = new Child();
        obj.staticMethod(); // Parent의 staticMethod가 호출.
    }
}
```

--- 
### 변수와 생명주기 

`지역 변수`  
메서드 내에서 선언된 변수로, 스택 영역에 저장되며 해당 메서드가 종료될 때 함께 제거

`인스턴스 변수` 
클래스의 인스턴스(객체)마다 개별적으로 유지되며, 힙 영역에 저장 됨 
GC가 동작하기 전까지는 객체와 함께 존재하므로 생명 주기가 일반적으로 지역 변수보다 길다

`클래스 변수` 
클래스 내에서 static 키워드로 선언된 변수로, 메서드 영역에 저장됩니다. 클래스가 JVM에 로딩될 때 생성되며, JVM이 종료될 때까지 유지됩니다. 따라서 가장 긴 생명 주기를 가집니다.

---



#### 📗 Java 프로그램 실행 과정
1. JVM이 OS로부터 프로그램 실행을 위해 필요한 메모리를 할당받음
2. Java 컴파일러(javac)가 Java 소스코드(.java)를 읽어들여 바이트코드(.class)로 변환
3. Class Loader를 통해 class 파일들을 JVM에 로딩함
4. Execution Engine을 통해 class 파일들이 해석됨
5. 해석된 바이트코드는 Runtime Data Areas에 배치되어 수행이 이루어짐



