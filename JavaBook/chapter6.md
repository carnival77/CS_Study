# 1. 객체지향언어

### 1.1. 객체지향언어의 기본 개념

`실제 세계는 사물(객체)로 이루어져 있으며, 발생하는 모든 사건들은 사물간의 상호작용이다.`  


### 1.2 객체지향언어

`객체지향언어는 기존의 프로그래밍언어와 다른 완전히 새로운 것이 아니라, 기존의 프로그래밍 언어에 몇 가지 새로운 규칙을 추가한 보다 발전된 형태의 것이다.`  
규칙들을 이용해서 코드 간에  `서로 관계를 맺어줌으로써`  보다 유기적으로 프로그램을 구성하는 것이 가능해졌다.

```text
객체지향언어의 주요 특징

1. 코드의 재사용성이 높다.
    - 새로운 코드를 작성할 때 기존의 코드를 이용하여 쉽게 작성할 수 있다.
2. 코드의 관리가 용이하다.
    - 코드간의 관계를 이용해서 적은 노력으로 쉽게 코드를 변경할 수 있다.
3. 신뢰성이 높은 프로그래밍을 가능하게 한다.
    - 제어자와 메서드를 이용해서 데이터를 보호하고 올바른 값을 유지하도록 하며, 
            코드의 중복을 제거하여 코드의 불일치로 인한 오동작을 방지할 수 있다.

=> 객체지향의 가장 큰 장점은 '코드의 재사용성이 높고 유지보수가 용이하다'는 것이다.
=> 객체지향개념을 학습할 때 재사용성과 유지보수 그리고 중복된 코드의 제거, 신뢰성이라는 키워드를 기억하자.
```

# 2. 클래스와 객체

### 2.1. 클래스와 객체의 정의와 용도

클래스란?

-   클래스의 정의: 객체를 정의해 놓은 것(틀)
-   클래스의 용도: 객체를 생성하는데 사용된다.

사전적 정의

-   객체의 정의: 실제로 존재하는 것. 사물 또는 개념
-   객체의 용도: 객체가 가지고 있는 기능과 속성에 따라 다름
    -   유형 객체: 책상, 의자, 자동차, TV 등등
    -   무형 객체: 수학 공식, 프로그램 에러와 같은 논리나 개념


클래스와 객체의 관계는  **제품 설계도와 제품과의 관계**라고 할 수 있으며,

클래스는 단지 객체를 생성하는데 사용될 뿐 객체 그 자체는 아닙니다.

즉, 먼저 **클래스로부터** **객체를 생성하는 과정이 선행**되어야 합니다.

ex) **TV 설계도(클래스) ↔ TV(객체)**

프로그래밍에서 객체는 클래스에 정의된 내용대로 메모리에 생성된 것을 뜻한다.

설계도(클래스)를 작성해두면 복잡한 제품 및 부품(객체)도 쉽게 만들 수 있다.

객체를 사용한다는 것은 객체가 가지고 있는 속성과 기능을 사용한다는 뜻이다.

JDK에는 많은 수의 유용한 클래스가 기본적으로 제공되어 원하는 기능을 쉽게 작성할 수 있다.

### 2.2. 객체와 인스턴스

인스턴스화 — 클래스로부터 객체를 만드는 과정  
인스턴스 — 어떤 클래스로부터 만들어진 객체를 그 클래스의 인스턴스라 한다.

```text
클래스 ==인스턴스화==> 인스턴스(객체)
```

-   책상은 객체다.
-   책상은 책상 클래스의 인스턴스다.

객체와 인스턴스는 같은 의미를 가지기 때문에 엄격히 구분할 필요는 없지만, 문맥에 따라 구분해서 사용하는 것이 좋다.

### 2.3. 객체의 구성요소

객체는 다수의 속성 및 기능을 가진다. 이러한 속성, 기능을 멤버(구성원, member)라고 한다. 객체는 `속성과 기능의 집합`이다.

-   속성(property): 멤버변수
-   기능(function): 메소드

### 2.4. 인스턴스의 생성과 사용

	클래스명 변수명;

클래스의 객체를 참조하기 위한 참조변수를 선언

	변수명 = new 클래스명( );

new 연산자로 클래스의 객체를 생성 후, 객체의 주소를 참조변수에 저장. (메모리의 빈 공간에 생성)

> 인스턴스는 참조 변수를 통해서만 다룰 수 있으며, 참조변수의 타입은 인스턴스의 타입과 일치해야 한다.

#### 예제 6_1

![](https://blog.kakaocdn.net/dn/7aGhs/btqS1UN30nv/AWwFWgoHfJA8pbz59HaTL0/img.png)

#### 예제 6_2
![](https://blog.kakaocdn.net/dn/8w91b/btqS1VzoPiv/nCeqfKbSSNzAc8aurxRQhK/img.png)


#### 예제 2

```
public class Tv {
    String color; // 색상
    boolean power; // 전원
    int channel; // 채널

    public void power() {
        this.power = !power; // 전원 토글
    }

    public void channelUp() {
        channel++; // 채널 증가
    }

    public void channelDown() {
        channel--; // 채널 감소
    }
}
```

```
Tv tv; // 참조변수 생성
tv = new Tv(); // 인스턴스 생성, 객체의 주소를 참조변수에 저장 (메모리의 빈 공간에 생성)

tv.channel = 7;
System.out.println(tv.channel);

tv.channelDown();
System.out.println(tv.channel);
```



### 2.5. 객체 배열

객체 역시 배열로 만드는 것이 가능하다.

```
Tv[] tvArr = new Tv[3]; // 3개의 객체 참조변수 배열 생성
```

주의할 점은 위 코드는 참조변수를 위한 공간만 생성됐을뿐, 객체는 아직 생성되지 않았다.

```
// 객체 생성
tvArr[0] = new Tv();
tvArr[1] = new Tv();
tvArr[2] = new Tv();
```

또는 선언 및 초기화를 한번에 할 수 있다.

```
Tv[] tvArr = {new Tv(), new Tv(), new Tv()};
```

또는 객체가 너무 많은 경우 반복문을 이용할 수 있다.

```
Tv[] tvArr = new Tv[100];

for(int i=0; i<tvArr.length; i++) {
    tvArr[i] = new Tv();
}
```

### 2.6. 클래스의 또 다른 정의

#### 2.6.1. 데이터의 변화

```text
1. 변수 — 하나의 데이터를 저장할 수 있는 공간
2. 배열 — 같은 종류의 여러 데이터를 하나의 집합으로 저장할 수 있는 공간
3. 구조체 — 서로 관련된 여러 데이터를 종류에 관계없이 하나의 집합으로 저장할 수 있는 공간
4. 클래스 — 데이터와 함수의 결합 (구조체 + 함수)
```
프로그래밍 언어에서 제공하는 자료형(`primitive type`) 외에 프로그래머가 서로 관련된 변수들을 묶어서 하나의 타입으로 새로 추가하는 것을 `사용자정의 타입(user-defined type)`이라고 한다.

#### 2.6.2. 접근 제어자

[접근 제어자](https://github.com/carnival77/CS_Study/blob/main/Java/%EC%A0%91%EA%B7%BC%20%EC%A0%9C%EC%96%B4%EC%9E%90.md)

접근 제어자를 통해서 변수 값의 제한을 걸어, 보다 정확한 데이터를 유지할 수 있다.

Time을 예를들어보면 시간은 0 ~ 23 의 범위를 가지고, 분과 초는 0 ~ 59 범위를 가진다.

```
public class Time {
    private int hour;
    private int minute;
    private float second;

    // Constructor
    public Time () {}

    // Access methods
    public int getHour() {
        return hour;
    }

    public void setHour(int hour) {
        if (hour < 0 || 23 < hour) return;
        this.hour = hour;
    }

    public int getMinute() {
        return minute;
    }

    public void setMinute(int minute) {
        if (minute < 0 ||  minute > 59) return;
        this.minute = minute;
    }

    public float getSecond() {
        return second;
    }

    public void setSecond(float second) {
        if (second < .0f || second > 59.99f) return;
        this.second = second;
    }

    // 데이터 확인을 위한 메소드
    @Override
    public String toString() {
        return "Time{" +
                "hour=" + hour +
                ", minute=" + minute +
                ", second=" + second +
                '}';
    }
}
```

### 2.7. **한 파일에 여러 클래스 작성하기**

**하나의 소스파일**에 **하나의 클래스만을 정의하는 것이 보편적**이지만, **둘 이상의 클래스를 정의하는 것도 가능**합니다.

이 때, 주의해야 할 점은 아래와 같습니다.

#### (1) public class가 있는 경우

소스파일의 이름은 반드시 public class의 이름과 일치해야 합니다.

※ 대소문자를 구분하므로, 대소문자까지 일치해야 합니다.

#### (2) public class가 하나도 없는 경우

소스파일의 이름은 소스파일 내의 어떤 클래스의 이름으로 해도 상관없습니다.

# 3. 변수와 메소드

### 3.1. 선언 위치에 따른 변수의 종류

변수에는 클래스 변수, 인스턴스 변수, 지역 변수 총 3개가 있다. 변수의 종류를 결정짓는 중요한 요소는 `변수의 선언된 위치` 이다.

![](https://blog.kakaocdn.net/dn/bgvZ7p/btqS6YaNLHE/jVkzQjeU174EzxjVxk3w0k/img.png)

선언위치에 따른 변수의 종류

```
class Variables {
    int iv; // instance variable 인스턴스 변수
    static int cv; // class variable 클래스 변수

    void method() {
        int lv = 0; // local variable 지역 변수
    }
}
```

-   인스턴스 변수
    
    -   클래스 영역에 선언
    -   `인스턴스가 생성될 때 만들어진다`  .
    -   인스턴스마다 고유한 상태를 유지해야 하는 속성의 경우, 인스턴스 변수로 선언한다.
-   클래스 변수
    
    -   클래스 영역에 선언
    -   `클래스가 메모리에 로딩 될 때 생성되어 프로그램이 종료될 때 까지 유지된다`.
    -   클래스 변수를 선언하는 방법은 인스턴스 변수 앞에 static 키워드 붙인다.
    -   인스턴스 변수와 달리 모든 인스턴스가  `공통된 저장공간(변수)을 공유`한다.
    -   인스턴스를 생성하지 않고도 언제라도 바로 사용할 수 있다.
    
    ```java
    Book.saleCount  // 클래스이름.클래스변수
    ```
    
-   지역 변수
    
    -   메서드 내에 선언되어 메서드 내에서만 사용 가능하다.
    -   메서드가 종료되면 소멸된다.

### 3.2. 클래스 변수와 인스턴스 변수

**인스턴스 변수**는 **인스턴스가 생성될 때 마다 생성**되므로 인스턴스마다 **다른 값을 유지**할 수 있지만,

**클래스 변수**는 **모든 인스턴스가 하나의 저장공간을 공유**하므로, **항상 공통된 값**을 갖는다.

예를 들어, 트럼프 카드가 있을때

```
class Card {
    String kind; // 문양 (instance variable)
    int number; // 숫자 (instance variable)

    static int width = 100; // 넓이 (class variable)
    static int height = 250; // 높이 (class variable)
}
```

**인스턴스 변수(개별 속성) : 숫자와 무늬**

**클래스 변수(공통 속성) : 크기(폭 * 높이)**

모든 카드의 넓이와 높이는 공통된 값을 가지니 클래스 변수로 선언, 문양이랑 숫자는 카드마다 다른 값을 가지므로 인스턴스 변수로 선언하는 것이 좋다.

예제 6_3

![](https://blog.kakaocdn.net/dn/AENS6/btqS6XQtXl7/nXeaYzGtNyyakF2G8xzWmK/img.png)


### 3.3. 메소드

#### 3.3.1. 메소드란?

**메서드(method)**는 **특정 작업을 수행하는 일련의 문장들을 하나로 묶은 것**이며, 기본적으로 **함수와 유사**합니다.

메서드는 크게 두 부분, **'선언부(header, 머리)'와 '구현부(body, 몸통)'**으로 이루어져 있으며, **메서드를 정의한다는 것은 선언부와 구현부를 작성하는 것을 의미**합니다.

#### 메서드의 구조

![](https://blog.kakaocdn.net/dn/mwtZH/btqS6YV77YY/gzHtDwCiLVfeJM3c3hkDO0/img.png)

#### 3.3.2. **메서드의 선언부**

메서드의 선언부는 '메서드의 이름'과 '매개변수 선언', '반환타입'으로 구성되어 있으며,

메서드가 작업을 수행하기 위해 어떤 값들을 필요로 하고 작업의 결과로 어떤 타입의 값을 반환하는지에 대한 정보를 제공합니다.

#### **(1) 매개변수 선언 (parameter declaration)**

**매개변수**는 **메서드가 작업을 수행하는데 필요한 값들(입력)을 제공받기 위한 것**입니다.

**필요한 값의 개수만큼 변수를 선언**하며 각 변수 간의 구분은 쉼표','를 사용합니다.

#### **(2) 반환타입(return type)**

메서드의 작업수행 결과(출력)의 **'반환값(return value)'의 타입**을 적습니다. **반환값이 없는 경우, 'void'**를 적어야 합니다.

#### 3.3.3. 메서드의 구현부

메서드의 선언부 다음에 오는 괄호{ }를 **'메서드의 구현부'**라고 하며, **메서드를 호출했을 때 수행될 문장**들을 넣습니다.

#### **(1) return문**

메서드의 반환타입이 'void'가 아닌 경우, 구현부{ } 안에 'return 반환값;'이 반드시 포함되어야 합니다.

return문은 작업을 수행한 결과인 반환값을 호출한 메서드로 전달하는데, 이 값의 타입은 반환타입과 일치하거나 적어도 자동 형변환이 가능한 것이어야 합니다.

return문은 **단 하나의 값만 반환**할 수 있습니다.

#### **(2) 지역변수(local variable)**

**지역변수(local variable)**는 메서드 내에 선언된 변수를 말하며, **매개변수**도 메서드 내에 선언된 것으로 간주되므로 지역변수입니다.

#### 3.3.4. 메서드의 호출

메서드를 호출해야만 구현부{ }의 문장들이 수행되며, 메서드를 호출하는 방법은 아래와 같습니다.

#### **메서드이름 (값1, 값2, ...);**

#### (1) 인수(argument)와 매개변수(parameter)

메서드를 호출할 때 괄호( ) 안에 지정해준 값들을 '인수(argument)' 또는 '인자'라고 하며, 인자의 개수와 순서는 호출된 메서드에 선언된 매개변수와 일치해야 합니다.

인수는 메서드가 호출되면서 매개변수에 대입되므로, 인자의 타입은 매개변수의 타입과 일치하거나 자동 형변환이 가능한 것이어야 합니다.

static 메서드는 같은 클래스 내의 인스턴스 메서드를 호출할 수 없다. ⇒ 클래스가 메모리에 로딩되는 시점에 인스턴스 존재하지 않을 수 있기 때문이다. 인스턴스 생성하여 사용 가능하다.

### 3.3.5. 메서드의 실행 흐름

![](https://blog.kakaocdn.net/dn/lIl5i/btqSZwUaDYo/FnqFCOvwisFGX4xm2v9b91/img.png)

#### 메서드의 실행 흐름

① main메서드에서 메서드 add를 호출합니다.
인수 1L과 2L가 메서드 add의 매개변수 a, b에 각각 복사(대입)됩니다.

② 메서드 add의 괄호{ }안에 있는 문장들이 순서대로 수행됩니다.

③ 메서드 add의 모든 문장이 실행되거나, return문을 만나면, 호출한 메서드(main메서드)로 되돌아와서 이후의 문장들을 실행합니다.

### 3.3.6. 메서드의 실행 흐름 예제

#### 예제 6_4

![](https://blog.kakaocdn.net/dn/cqwDtv/btqS9ZN2p9L/09QHKwaeUi2OIxz8v1o6BK/img.png)


### 3.3.7. return문

**return문**은 현재 실행중인 메서드를 종료하고 호출한 메서드로 되돌아갑니다.

반환값의 유무에 관계없이 **모든 메서드에는 적어도 하나의 return문이 있어야 하며,**

반환타입이 void인 경우, **컴파일러가 메서드의 마지막에 'return;'을 자동적으로 추가**해주었기 때문에 생략이 가능합니다.

### 3.3.8. 반환값

**return문의 반환값**으로 **주로 변수**가 오며, 'x+y'와 같은 **수식**이 올 수도 있습니다. 이 때, **수식을 계산한 결과가 반환**됩니다.


#### 메서드를 사용하는 이유

#### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch06-oop-1/#i-%EB%86%92%EC%9D%80-%EC%9E%AC%EC%82%AC%EC%9A%A9%EC%84%B1)i. 높은 재사용성

-   한번 만들어 놓은 메서드를 몇 번이고 호출할 수 있다.

#### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch06-oop-1/#ii-%EC%A4%91%EB%B3%B5%EB%90%9C-%EC%BD%94%EB%93%9C%EC%9D%98-%EC%A0%9C%EA%B1%B0)ii. 중복된 코드의 제거

-   반복되는 문장들을 메서드로 작성한다.
-   전체 소스 길이가 짧아진다.
-   변경사항 발생했을 때 수정해야할 코드의 양이 줄어든다. (메서드 내용만 수정하면 됨)

#### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch06-oop-1/#iii-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%A8%EC%9D%98-%EA%B5%AC%EC%A1%B0%ED%99%94)iii. 프로그램의 구조화

-   큰 규모의 프로그램에서는 문장들을  `작업단위`로 나눠서 여러 개의 메서드에 담아 프로그램의 구조를 단순화시키는 것이 필수적이다.
-   처음에 프로그램을 설계할 때  `내용이 없는 메서드를 작업단위로 만들어 놓고`, 하나씩 완성해가는 것도 프로그램을 구조화 하는 좋은 방법이다.


#### 3.3.2. 메소드의 유효성 검사

메소드 구현부를 작성하기 전에 제일 먼저 할 것은 매개변수에 대한 유효성 검사를 하는 것이다. (프로그램이 비정상적으로 종료되는 것을 막기 위해)

> 호출하는 쪽에서 알아서 적절한 값을 넘겨주겠지 라는 생각은 절대로 가져선 안된다.

### 3.4. JVM의 메모리 구조

응용프로그램이 실행되면 JVM은 시스템으로부터 프로그램을 수행하는데 필요한 메모리를 할당 받는다. 그리고, 메모리를 용도에 따라 여러 영역으로 나눠서 관리한다.

**주요 3가지 영역**

1.  method area
    
    -   프로그램 실행 중에 어떤 클래스가 사용되면, JVM은 해당 클래스의 클래스 파일(*.class)을 읽고 분석하여 클래스에 대한 정보를 이곳에 저장한다.
    -   클래스 변수(class variable) 또한 이 영역에 함께 생성된다.
2.  호출스택 (call stack)
    
    -   메소드가 호출되면 해당 메소드에 필요한 메모리가 할당된다. 이 메모리는 메소드가 실행되는 동안 지역변수(매개변수 포함)들과 연산의 중간 결과 등을 저장하는데 사용된다.
    - `컴파일 타임에 크기 결정`된다.

3.  heap
    
    -   인스턴스가 생성되는 공간. 프로그램 실행 중 생성되는 모든 인스턴스는 이곳에 저장된다.
    - `런타임에 크기가 결정`된다.
    -   인스턴스 변수(instance variable)도 이 영역에 생성된다.
    - 가비지 컬렉터에 의해 관리된다.

#### 3.4.1. call stack의 특징

-   메소드가 호출되면 수행에 필요한 만큼의 메모리를 스택에 할당 받는다.
-   메소드가 수행을 마치고나면 사용했던 메모리를 반환하고 스택에서 제거된다.
-   호출스택의 제일 위에 있는 메소드가 현재 실행중인 메소드이다.
-   아래에 있는 메소드가 바로 위의 메소드를 호출한 메소드이다.

![](https://blog.kakaocdn.net/dn/xhd7X/btqSZxS9hTZ/g3IAvZi7ZMT9iT4Zkzh4J0/img.png)

#### 예제 6_5

![](https://blog.kakaocdn.net/dn/NY0o8/btqTcRhSu6m/w7e9ew9NkrmXXuQz83YWB1/img.png)


**① ~ ②**

JVM에 의해서 main메서드가 호출됨으로써, 프로그램이 시작됩니다.
호출스택에는 main메서드를 위한 메모리 공간이 할당되고, main메서드의 코드가 수행됩니다.

**③**

main메서드에서 println( )을 호출한 상태입니다.

아직 main메서드가 끝난 것은 아니므로 호출스택에 대기상태로 남아있고, println( )의 수행이 시작되어 화면에 "Hello"를 출력합니다.

**④**

println( )메서드의 수행이 완료되어 호출스택에서 사라지고 main메서드로 되돌아가 println( ) 이후부터 수행을 재개합니다.

**⑤**

main메서드에 더 이상 수행할 코드가 없으므로, 호출스택은 완전히 비워지고 프로그램은 종료됩니다.

### 3.5. 기본형 매개변수와 참조형 매개변수

-   기본형 매개변수: 변수의 값을 읽을 수만 있다. (Read Only)
-   참조형 매개변수: 변수의 값을 읽고 변경할 수 있다. (Read & Write)

메소드의 매개변수를 기본형으로 선언하면 단순히 값을 복사하여 넘긴다. 하지만, 참조형인 경우에는 주소값을 복사하여 넘기기 때문에 값을 변경하는 것이 가능하다.

```
public class Parameter {
    private int x;
    private int y;

    // Constructor
    public Parameter() {}
    public Parameter(int x, int y) {
        this.x = x;
        this.y = y;
    }

    // Access methods
    public int getX() {
        return x;
    }

    public void setX(int x) {
        this.x = x;
    }

    public int getY() {
        return y;
    }

    public void setY(int y) {
        this.y = y;
    }

    // 기본형 매개변수 변경하는 메소드
    public static void changePrimitiveParam(int num) {
        num += 10;
    }

    // 참조형 매개변수 변경하는 메소드
    public static void changeReferenceParam(Parameter param) {
        param.setX(100);
        param.setY(200);
    }

    @Override
    public String toString() {
        return "Parameter{" +
                "x=" + x +
                ", y=" + y +
                '}';
    }
}
```

```
// 기본형 매개변수는 바뀌지 않는다. (Read only)
System.out.println("기본형(primitive) 매개변수 값 변경");
int z = 10;
System.out.println("변경 전 z: " + z);
Parameter.changePrimitiveParam(z);
System.out.println("변경 후 z: " + z);

// 참조형 매개변수는 바뀔 수 있다. (Read & Write)
System.out.println("참조형(Reference) 매개변수 값 변경");
final Parameter param = new Parameter();
System.out.println("변경 전 Parameter: " + param.toString());
Parameter.changeReferenceParam(param);
System.out.println("변경 후 Parameter: " + param.toString());
```

결과

```
기본형(primitive) 매개변수 값 변경
변경 전 z: 10
변경 후 z: 10
참조형(Reference) 매개변수 값 변경
변경 전 Parameter: Parameter{x=0, y=0}
변경 후 Parameter: Parameter{x=100, y=200}
```
기본형 매개변수 예제


![](https://blog.kakaocdn.net/dn/cJUmei/btqS4NACZ9K/KFQOQvDvkOQm7zbHaP3P71/img.png)

#### 예제 6_6

![](https://blog.kakaocdn.net/dn/mOojv/btqS4Ngjtmh/xuuOcgR8bj29IMUKPPWVGK/img.png)

예제 6_6 호출스택

**①**

change메서드가 호출되면서 'd.x'가 change메서드의 매개변수 x에 복사됩니다.

**②**

change메서드에서 x의 값을 1000으로 변경합니다.

**③**

change메서드가 종료되면서 매개변수 x는 스택에서 제거됩니다.

#### 참조형 매개변수 예제

![](https://blog.kakaocdn.net/dn/xiH6m/btqSX8F2Ysj/HJ5rMpMJeZ411k1Gc6vHc0/img.png)

예제 6_7

![](https://blog.kakaocdn.net/dn/pFtWW/btqTcRa7z2a/odDQk1thQ2mPkdL9rpaBPK/img.png)

예제 6_7 호출스택

**①**

change메서드가 호출되면서 참조변수 d의 값(주소)이 매개변수 d에 복사되며, 매개변수 d에 저장된 주소값으로 x에 접근이 가능합니다.

**②**

change메서드에서 매개변수 d로 x의 값을 1000으로 변경합니다.

**③**

change메서드가 종료되면서 매개변수 d는 스택에서 제거됩니다.

#### 참조형 반환 타입 예제

매개변수뿐만 아니라 **반환타입도 참조형이 될 수 있으며, 모든 참조형 타입의 값인 '객체의 주소'가 반환**됩니다.

![](https://blog.kakaocdn.net/dn/Pe6iD/btqSX8eXb29/gmdH0YIxtbAmJcmHo6qKKk/img.png)

예제 6_8

![](https://blog.kakaocdn.net/dn/bWjzjC/btqS29KZYsg/ePmRymhlPw8vijbMeGQgOK/img.png)

예제 6_8 호출스택(1)

![](https://blog.kakaocdn.net/dn/GV0Ii/btqS6Yokb88/uFIJVDSjC9Y9pHM3JzQz7k/img.png)

예제 6_8 호출스택(2)

### 3.6. 재귀호출(recursive call)

메소드의 내부에서 메소드 자신을 다시 호출 하는 것을 재귀호출(recursive call)이라 한다.

```text
void method() {
    method();  // 재귀호출
}
```

재귀호출과 반복문은 서로 유사한점이 많아서 변환이 가능하다.

반복문은 그저 같은 문장을 반복해서 호출하지만, 재귀 호출은 매개변수 복사와 종료, 복귀할 메모리 주소 저장 등 추가적으로 필요한 요소가 많다. 그래서 반복문보다 재귀호출의 수행시간이 더 오래걸린다.

재귀호출을 사용하는 이유는 논리적 간결함 때문이다. 논리적으로 간결하게 표현이 가능한 경우, 비효율적이더라도 오류를 줄이고 단순한 구조로 바꿀 수 있다.

### 3.7. 클래스 메소드(static 메소드)와 인스턴스 메소드

-   인스턴스 메소드는 인스턴스 변수와 관련된 작업을 하는, 즉 인스턴스 변수를 필요로 하는 메소드일때 정의한다.
-   클래스 메소드는 인스턴스와 관계없이 공통으로 사용되는 메소드일때 정의한다.

무조건 인스턴스를 사용하지 않는다고 클래스 메소드를 만드는 것은 아니지만, 특별한 이유가 없는 한 클래스 메소드로 만드는것이 일반적이다.

**정리**

1.  클래스를 설계할 때, 멤버변수 중 모든 인스턴스에 공통으로 사용하는 것에는 static을 붙인다.
2.  클래스 변수(static 변수)는 인스턴스를 생성하지 않아도 사용할 수 있다.
	-  static이 붙은 클래스 변수는  `클래스가 메모리에 올라갈 때 이미 자동적으로 생성`되기 때문이다.
3.  클래스 메소드(static method)는 인스턴스 매개변수를 사용할 수 없다.
	-   인스턴스 생성 없이 호출 가능하므로, 클래스 메서드가 호출되었을 때 인스턴스가 존재하지 않을 수도 있다.
4.  메소드 내에서 인스턴스 변수를 사용하지 않는다면 static을 붙이는 것을 고려한다.
	-   static 메서드는 메서드 호출 시간이 짧아지므로 성능이 향상된다. 인스턴스 메서드는 실행 시  `호출되어야 할 메서드를 찾는 과정`이 추가적으로 필요하기 때문에 시간이 더 걸린다.
	
```java
- 클래스의 멤버변수 중 모든 인스턴스에 공통된 값을 유지해야 하는 것이 있는지 살펴보고 있으면, static을 붙여준다. 
- 작성한 메서드 중에서 인스턴스 변수나 인스턴스 메서드를 사용하지 않는 메서드에 static을 붙일 것을 고려한다.
```

```
public class MyMath {
    static int add(int x, int y) {
        return  x + y;
    }

    static int subtract(int x, int y) {
        return x - y;
    }

    static double multiply(double x, double y) {
        return x * y;
    }

    static double divide(double x, double y) {
        return x / y;
    }
}
```

```
MyMath.add(1, 3)
MyMath.subtract(10, 5)
MyMath.multiply(1, 2)
MyMath.divide(10, 5)
```

### **static 메서드와 인스턴스 메서드 예제**

![](https://blog.kakaocdn.net/dn/bBQ5u3/btqS4MPgGj1/GQWG7wHVQqyGwEPG5tmTJ0/img.png)

#### 예제 6_9

### 3.8. 클래스 멤버와 인스턴스 멤버간의 참조와 호출


같은 클래스에 속한 멤버들 간에는 별도의 인스턴스를 생성하지 않고도 서로 참조 또는 호출이 가능하다. 단, `클래스멤버가 인스턴스 멤버를 참조 또는 호출`하고자 하는 경우에는 인스턴스를 생성해야 한다.  
그 이유는 `인스턴스 멤버가 존재하는 시점에 클래스 멤버는 항상 존재`하지만, `클래스 멤버가 존재하는 시점에 인스턴스 멤버가 존재하지 않을 수도` 있기 때문이다.

```

public class MemberCall {
    private int iv = 10;
    private static int cv = 20;

    private int iv2 = cv; // 인스턴스 변수에서 클래스 변수를 사용할 수 있음
//    private static int cv2 = iv2; // 반대로, 클래스 변수에 인스턴스 변수를 사용할 수 없음.

    // Methods
    public static void staticMethod() {
        System.out.println("cv: " + cv);
//        System.out.println("iv: " + iv); // 클래스 메소드에서 인스턴스 변수를 사용할 수 없음

        // 인스턴스를 생성해서 사용
        MemberCall memberCall = new MemberCall();
        System.out.println("memberCall.iv: " + memberCall.iv);
    }

    public void instanceMethod() {
        System.out.println("cv: " + cv); // 클래스 변수 사용 가능
        System.out.println("iv: " + iv); // 인스턴스 변수 사용 가능
    }

    public static void staticMethod2() {
        staticMethod(); // 클래스 메소드 사용 가능
//        instanceMethod(); // 클래스 메소드에서 인스턴스 메소드 사용 불가
    }

    public void instanceMethod2() {
        // 둘다 사용가능
        staticMethod();
        instanceMethod();
    }
}
```

정리

-   클래스 멤버는 언제나 참조 또는 호출이 가능하다.
-   인스턴스 멤버는 객체가 생성되지 않았을 수 있기 때문에, 언제나 호출이 가능한 것은 아니다.
-   인스턴스 멤버끼리는 참조 또는 호출이 가능하다.

# 4. 오버로딩 (overloading)

### 4.1. 오버로딩?

한 클래스 내에 같은 이름의 메서드를 여러 개 정의하는 것을 `오버로딩`이라고 한다. 이름은 같지만 매개변수의 개수 또는 타입이 다르다. 하나의 메서드 이름으로 여러 기능을 구현하기 때문에 붙여진 이름.

### 4.2. 오버로딩의 조건

1.  메소드의 이름이 같아야 한다.
2.  매개변수의 개수 또는 타입이 달라야 한다.

> 주의. 반환 타입은 오버로딩을 구현하는데 아무런 영향을 주지 못한다. 즉, 오버로딩은 매개변수에 의해서만 구분 될 수 있다.

### 4.3. 오버로딩의 예

대표적인 예로 println() 메소드를 들 수 있다.

```
System.out.println() ...
System.out.println(boolean x) ...
System.out.println(char x) ...
System.out.println(char[] x) ...
System.out.println(double x) ...
System.out.println(float x) ...
System.out.println(int x) ...
System.out.println(long x) ...
System.out.println(Object x) ...
System.out.println(String x) ...
```

```
public static int add (int x, int y) {
    return x + y;
}

public static long add(long x, int y) {
    return x + y;
}

public static long add(int x, long y) {
    return x + y;
}

public static long add(long x, long y) {
    return x + y;
}
```

```
final int intX = 10, intY = 20;
final long longX = 100_000L, longY = 200_000L;

Stream.of(
    add(intX, intY),
    add(longX, intY),
    add(intX, longY),
    add(longX, longY)
).forEach(System.out::println);
```

![](https://blog.kakaocdn.net/dn/8rwjm/btqS1VMXHRK/1VLfrArQxg9A3Xb2HGkTHk/img.png)

예제 6_10

## 4.4. 오버로딩의 장점

-   기억하기 쉽고 이름도 짧게 할 수 있어서 오류의 가능성을 줄일 수 있다.
-   메서드의 이름만 보고도 ‘이 메서드들은 이름이 같으니, 같은 기능을 하겠구나’라고 쉽게 예측 가능.
-   메서드의 이름을 절약할 수 있다.

오버로딩이 없다면, 근본적으로 같은 역할을 하는 메소드지만 각각 다른 이름을 사용해서 메소드를 생성해야하는 불편함이 있다.

예를들어서,

```
System.out.println() ...
System.out.printlnBoolean(boolean x) ...
System.out.printlnChar(char x) ...
System.out.printlnCharArr(char[] x) ...
...
```

System.out.println() 메소드는 근본적으로 콘솔에 매개변수를 출력하는 역할을 하지만, 오버로딩이 없다면 위처럼 모두 다른 이름으로 메소드를 정의해야한다.

메소드 이름이 같음으로서 우리는 "같은 기능을 하는 메소드구나" 라고 예상할 수 있다.

## 4.5. 가변인자(varargs)와 오버로딩

매개 변수 개수가 고정된 것이 아닌, 동적으로 지정하고 싶을 때 "타입... 변수명" 과 같이 표현한다.

가변인자 외에도 매개변수가 더 있다면, `가변인자를 매개변수 중에서 제일 마지막에 선언`해야 한다. 가변인자인지 아닌지를 구별할 방법이 없기 때문에 허용하지 않는다.  
가변인자는 내부적으로 배열을 이용한다. 가변인자로 선언된 메서드는 호출할 때마다 배열이 새로 생성된다. (비효율)

예를들어, concatenate(문자를 합치는 기능) 메소드를 구현할 때, 가변인자를 이용하면 편리하다.

가변인자를 사용하지 않는 경우

```
concat(String delim, String str1, String str2)
concat(String delim, String str1, String str2, String str3)
concat(String delim, String str1, String str2, String str3, String str4)
```


가변인자를 사용하는 경우
```java
public static String concat(String delim, String... strs) {
    final StringBuffer sb = new StringBuffer();

    Stream.of(strs)
            .filter(str -> !str.isEmpty())
            .forEach(str -> sb.append(str + delim));

    return sb.toString();
}
```

```
Stream.of(
        MyString.concat("/", "Hello,", "Java", ""),
        MyString.concat("/", "Hello,", "Java", "", "!"),
        MyString.concat("/", "Hello,", "Java", "", "!", "!")
).forEach(System.out::println);
```

> 주의. 가변인자를 이용한 오버로딩 메소드는 구별되지 못하는 경우가 발생하기 쉽기 때문에 가변인자를 이용한 오버로딩을 하지 않는 것이 좋다.

# 5. 생성자 (Constructor)

### 5.1. 생성자란?

생성자는 인스턴스가 생성될 때 호출되는 인스턴스 초기화 메소드이다. 인스턴스 변수의 초기화 작업에 주로 사용되며, `인스턴스 생성 시에 실행되어야 할 작업`을 위해서도 사용된다.

1.  생성자의 이름은 클래스의 이름과 같아야 한다.
2.  생성자는 리턴 값이 없다.

생성자도 오버로딩이 가능하다. 예를들어,

```
public class Card {
    private String kind; // 무늬
    private int number; // 숫자

    private static int width = 100; // 가로 길이
    private static int height = 250; // 세로 길이

    // Constructor
    public Card() {} // 매개변수가 없는 생성자

    public Card(String kind, int number) {      // 매개변수가 있는 생성자
        this.kind = kind;
        this.number = number;
    }

    ...
}
```

#### 5.1.1. 인스턴스가 만들어지는 과정

주의할 점. 연산자 new가 인스턴스를 생성하는 것이지, 생성자(Constructor)가 인스턴스를 생성하는 것이 아니다.

```
Card card = new Card();
```

1.  연산자 new에 의해서 메모리(heap)에 Card 클래스의 인스턴스가 생성된다.
2.  생성자 Card()가 호출되어 수행된다.
3.  연산자 new의 결과로, 생성된 Card 인스턴스의 주소가 반환되어 참조변수 card에 저장된다.

### 5.2. 기본 생성자 (Default Constructor)

생성자를 성성하지 않더라도 컴파일러는 자동적으로 기본 생성자를 만들어준다.

컴파일을 할 때, .java 파일에 생성자가 없다면

```
클래스이름() {}
```

위와같이 기본 생성자를 생성해준다. (반대로 생성자가 있다면 생성해주지 않는다.)

```
class Card {
    ...

    Card(String kind, int number) {
        ...
    }

    ...
}

// 호출부분
Card card = new Card(); // 컴파일 에러 발생.
```

이미 매개변수가 있는 생성자가 있기 때문에, 컴파일러는 기본 생성자(Card())를 생성하지 않는다.

즉, 기본생성자가 컴파일러에 의해 추가되는 경우는 클래스에 생성자가 하나도 없는 경우이다.



![](https://blog.kakaocdn.net/dn/bsgLaP/btqTcPLa5G9/s1Hk3nKLYnM6Tzjqh3a9Tk/img.png)

예제 6_11



![](https://blog.kakaocdn.net/dn/RFheu/btqS4MuXFbo/aCYe1yyGlqoSnke5zhQhV1/img.png)

예제 6_12

### 5.3. 생성자에서 다른 생성자 호출하기 - this(), this

같은 클래스의 멤버들 간에 서로 호출할 수 있는 것처럼 생성자 간에도 호출이 가능하다. 단, 2가지 규칙을 지켜야한다.

-   생성자의 이름으로 클래스 이름 대신에 this 키워드를 사용한다.
-   한 생성자에서 다른 생성자를 호출할 때는 반드시 첫줄에서만 호출이 가능하다.

#### 다른 생성자를  `첫 줄에서만 호출 가능한 이유`

⇒ 생성자 내에서 초기화 작업 도중에 다른 생성자를 호출하게 되면, 호출된 다른 생성자 내에서도 멤버변수들의 값을 초기화 할 것이므로  `다른 생성자를 호출하기 이전의 초기화 작업이 무의미해질`  수 있기 때문이다.


`this`  는 참조변수로 인스턴스 자신을 가리킨다. this를 사용할 수 있는 것은 인스턴스 멤버뿐이다. static 메서드에서는 this를 사용할 수 없다. static 메서드가 호출된 시점에 인스턴스가 존재하지 않을 수도 있기 때문이다.  
생성자를 포함한 모든 인스턴스 메서드에는 자신이 관련된 인스턴스를 가리키는 참조변수 this가 지역변수로 숨겨져 있다.

```
public class Car {
    private String color; // 색상
    private String gearType; // 변속기 종류 - 오토 or 수동
    private int door; // 문의 개수

    // Constructor
    public Car(String color, String gearType, int door) {
        this.color = color;
        this.gearType = gearType;
        this.door = door;
    }

    public Car() {
        this("white", "auto", 4);
    }

    public Car(String color) {
        this(color, "auto", 4);
    }
}
```

```
// 실행부
Stream.of(
        new Car().toString(),
        new Car("pink").toString(),
        new Car("black", "manual", 6).toString()
).forEach(System.out::println);
```

위에서 this.color는 인스턴스 변수를 뜻하고, color는 매개변수를 뜻한다.

####  예제
![](https://blog.kakaocdn.net/dn/Zb6r8/btqTcPRVXlY/MHleLSil4ulfIB2HVr7DQk/img.png)


예제 6_13

정리

-   this는 인스턴스 자신을 가리키는 참조변수, 인스턴스의 주소가 저장되어 있다.
-   this(), this(매개변수)는 생성자를 뜻한다. 같은 클래스의 다른 생성자를 호출할 때 사용한다.

# 6. 변수의 초기화

### 6.1. 변수의 초기화

지역변수는 사용전에 반드시 초기화를 해야한다.

```
int i;
int j = i; // 컴파일러 에러.
```


선언과 동시에 적절한 값으로 초기화 하는 것이 바람직하다.  
멤버변수는 초기화를 하지 않아도 자동적으로  `변수의 자료형에 맞는 기본값으로 초기화`가 이루어진다. 지연변수는 사용하기 전에 반드시 초기화를 해야 한다.

```text
멤버변수(클래스변수와 인스턴스변수)와 배열의 초기화는 선택적이지만, 지역변수의 초기화는 필수적이다.

멤버변수의 초기화 방법
1. 명시적 초기화 (explicit initialization)
2. 생성자 (constructor)
3. 초기화 블럭 (initialization block)
	- 인스턴스 초기화 블럭 : 인스턴스 변수 초기화
  - 클래스 초기화 블럭 : 클래스(static) 변수 초기화
```




### 6.2. 멤버변수의 초기화

#### 6.2.1. 명시적 초기화 (Explicit initialization)

선언과 동시에 초기화를 하는 방법을 명시적 초기화라고 한다.

```
class Car {
    int door = 4; // 기본형 변수의 초기화
    Engine e = new Engine(); // 참조형 변수의 초기화
}
```

#### 6.2.2. 초기화 블럭(initialization block)

-   클래스 초기화 블럭: 클래스 변수의 복잡한 초기화에 사용된다.
-   인스턴스 초기화 블럭: 인스턴스 변수의 복잡한 초기화에 사용된다.

배열과 같이 초기화 과정이 복잡한 경우 초기화 블럭을 사용하면 좋다.

```
public class InitBlock {

    static { /* 클래스 초기화 블럭 */ }

    { /* 인스턴스 초기화 블럭 */ }

}
```

인스턴스 변수의 초기화는 보통 생성자 초기화를 이용하고, 공통으로 수행되는 코드의 경우 인스턴스 초기화 블럭을 이용한다.

```
// 인스턴스 초기화 블럭을 이용하여 공통 부분을 제거
{
    count++;
    serialNo = count;
}

Car() {
    // count++;         // 중복되는 코드
    // serialNo = count;
    color = "White";
    gearType = "Auto";
}

Car(String color, String gearType) {
    // count++;
    // serialNo = count;
    this.color = color;
    this.gearType = gearType;
}
```

> 코드의 중복을 제거하는 것은 코드의 신뢰성을 높여준다. 그리고 오류의 발생 가능성을 줄여준다는 장점이 있다. 프로그래머는 코드의 중복을 최대한 제거하기 위해 노력해야 한다.
#### 멤버변수의 초기화 예제 1

![](https://blog.kakaocdn.net/dn/clbYpR/btqS9Zgeaf5/4veHnpcrVxjBQURLxXlWJ1/img.png)

위의 예제와 같이 **인스턴스 초기화 블럭은 클래스 내에 블럭{ }을 만들고 내부에 코드를 작성**하면 되며,

**클래스 초기화 블럭은 인스턴스 초기화 블럭 앞에 static을 덧붙이기**만 하면 됩니다.

이와 더불어 위의 예제의 실행결과와 같이 **클래스 초기화 블럭은 처음 메모리에 로딩될 때 한번만 수행**되지만, **인스턴스 초기화 블럭은 인스턴스가 생성될 때마다 수행**됩니다.

#### 멤버변수의 초기화 예제2

![](https://blog.kakaocdn.net/dn/bBoz8A/btqSZx6CuOO/znWdS0fb8h2UebwSh0ZWQK/img.png)

예제 6_15


### 6.3. 멤버변수의 초기화 시기와 순서

시점

-   클래스 변수의 초기화 시점: 클래스가 처음 로딩될 때 단 한번 초기화 된다.
-   인스턴스 변수의 초기화 시점: 인스턴스가 생성될 때마다 인스턴스 별로 초기화가 이루어진다.

순서

-   클래스 변수의 초기화 순서: 기본값 -> 명시적 초기화 -> 클래스 초기화 블럭
-   인스턴스 변수의 초기화 순서: 기본값 -> 명시적 초기화 -> 인스턴스 초기화 블럭 -> 생성자

클래스가 실행되는 시점에 메모리에 로딩된다. 이미 메모리에 로딩되어 있다면 다시 로딩하지 않는다. (클래스 멤버가 한번만 호출되는 이유)




  
  
## Reference 
1. [https://hongku.tistory.com/391](https://hongku.tistory.com/391) [IT에 취.하.개.]
2. https://im-yeobi.io/posts/java/book/standard-of-java/ch06-oop-1/
3. https://amacoding.tistory.com/8?category=954151
4. https://amacoding.tistory.com/9?category=954151