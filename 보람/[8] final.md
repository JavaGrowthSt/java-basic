>   •	변수: 값이 한 번 할당되면 변경할 수 없음
	•	필드 (인스턴스 변수): 객체별로 한 번만 값 설정 가능
	•	참조형 변수: 참조값은 변경할 수 없지만, 참조하는 객체의 내용은 변경 가능
    
### [1] 초기화 방법     
#### 지역 변수
final로 선언된 지역 변수는 초기화된 후 값을 변경할 수 없음
반드시 선언과 동시에 초기화하거나, 생성자 또는 블록 내에서 초기화 해야 함
```java
public class MyClass {
    public void myMethod() {
        final int localVar = 10;
        // localVar = 20; // 컴파일 에러: 값 변경 불가
    }
}
```
#### 인스턴스 변수
final로 선언된 인스턴스 변수는 생성자에서 초기화한 후 값을 변경할 수 없음
```java
public class MyClass {
    final int instanceVar;
    
    public MyClass(int value) {
        this.instanceVar = value;
    }
}
```

#### 클래스 변수
final로 선언된 클래스 변수는 선언과 동시에 또는 정적 초기화 블록에서 초기화해야 하며, 
초기화된 후에는 값을 변경할 수 없음
```java
public class MyClass {
    static final int classVar = 100;
    static final int anotherVar;
    
    static {
        anotherVar = 200;
    }
}
```


### [2] final 메서드와 클래스

#### final 메서드
final로 선언된 메서드는 서브클래스에서 오버라이드할 수 없음 (코드 변경 안됨)


```java
public class ParentClass {
    public final void finalMethod() {
        // 구현 내용
    }
}

public class ChildClass extends ParentClass {
    // public void finalMethod() {
    //     // 컴파일 에러: 오버라이드 불가
    // }
}
```

#### final 클래스

final로 선언된 클래스는 다른 클래스가 상속할 수 없음 (클래스 확장 안됨)

```java
public final class FinalClass {
    // 구현 내용
}

// public class SubClass extends FinalClass {
//     // 컴파일 에러: 상속 불가
// }
```


### [3] static final (상수)
#### 상수(Constant)
- 단 하나만 존재하는 변하지 않는 고정된 값 ( `static final` 키워드를 사용 )
- 관례상 대문자를 사용하고 구분은 `_` (언더스코어)로 한다. ( 변수와 상수를 구분 )
- 필드를 직접 접근해서 사용 ( `예: ClassName.constantName` ) 
- 애플리케이션 전반에서 사용되기 때문에 `public` 를 자주 사용 ( 접근제어자를 이용해 제약을 줄 수 있음 )


```java
public class Constant {
    //수학 상수
    public static final double PI = 3.14;
    //시간 상수
    public static final int HOURS_IN_DAY = 24; 
    public static final int MINUTES_IN_HOUR = 60; 
    public static final int SECONDS_IN_MINUTE = 60; 
    //애플리케이션 설정 상수
    public static final int MAX_USERS = 1000;
}


```
#### static final 을 사용하는 이유

```java
//final 필드 - 필드 초기화 
public class FieldInit {
     static final int CONST_VALUE = 10;
     final int value = 10;
 }
```

![](https://velog.velcdn.com/images/boram0415/post/1a5d1274-ead0-415b-a9cd-a71f4cf47338/image.png)

FieldInit 클래스에서 final 필드를 필드 초기화로 설정하는 경우, 모든 인스턴스의 value 값은 동일값으로 초기화 됨 

새로운 인스턴스 생성 시 동일한 값을 가지는 `final int value` 객체가 메모리 상에 올라가 메모리 낭비를 유발

이를 해결하기 위해 static 영역을 사용하는 것이 좋음
static 필드를 사용하면 모든 인스턴스가 동일한 값을 공유하게 되어 메모리 낭비를 줄이고, 코드 중복을 피할 수 있음

### [4] 참조형 변수에 대한 final
참조형 변수에 final을 붙이면, 해당 변수가 가리키는 참조 주소는 변경 불가 하지만 
해당 참조가 가리키는 객체의 내용은 변경 가능 함
```java
public class MyClass {
    final List<String> list = new ArrayList<>();
    
    public void modifyList() {
        list.add("Hello"); // 객체의 내용 변경 가능
        // list = new ArrayList<>(); // 컴파일 에러: 참조 주소 변경 불가
    }
}
```
