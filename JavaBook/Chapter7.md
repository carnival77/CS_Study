## 1. 상속 (inheritance)

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#11-%EC%83%81%EC%86%8D%EC%9D%98-%EC%A0%95%EC%9D%98%EC%99%80-%EC%9E%A5%EC%A0%90)1.1 상속의 정의와 장점

상속이란 기존의 클래스를 재사용하여 새로운 클래스를 작성하는 것이다.  
상속을 통해서 클래스를 작성하면 적은 양의 코드로 새로운 클래스를 작성할 수 있고, 코드를 공통적으로 관리할 수 있기 때문에 코드의 추가 및 변경이 매우 용이하다.

```text
조상 클래스 — 부모(parent)클래스, 상위(super)클래스, 기반(base)클래스
자손 클래스 — 자식(child)클래스, 하위(sub)클래스, 파생된(derived)클래스

- 생성자와 초기화 블럭은 상속되지 않는다. 멤버만 상속된다.
- 자손 클래스의 멤버 개수는 조상 클래스보다 항상 같거나 많다.
```

**상속을 구현하는 방법**은

새로 작성하고자 하는 클래스의 이름 뒤에

상속받고자 하는 클래스 이름을

**'extends'와 함께** 써주면 됩니다.

**ex)**

#### **class Parent { }**

#### **class Child** **extends Parent** **{ }**

위의 Parent 클래스와 Child 클래스는

서로 **상속 관계에 있다**고 하며,

Parent 클래스는 **'조상 클래스'**,

Child 클래스는 **'자손 클래스'**라고 합니다.

![](https://blog.kakaocdn.net/dn/BiSBX/btqSZxTcuaN/PlXzXPqC4nx4RcRHP0Ue3k/img.png)

Parent클래스와 Child클래스의 관계

위의 그림과 같이

**자손 클래스는 조상 클래스의**

**모든 멤버를 상속**받기 때문에,

Child 클래스는 Parent 클래스의

멤버들을 포함합니다.

그리고

**조상 클래스가 변경되면**

**자손 클래스는 자동적으로 영향**을 받지만,

**자손 클래스가 변경되는 것은**

**조상 클래스에 아무런 영향을 주지 못합니다.**

그러므로

**자손 클래스는 조상 클래스보다**

**같거나 많은 멤버**를 갖으며,

**상속을 거듭할수록**

**상속받는 클래스의 멤버 개수는**

**점점 증가**하게 됩니다.

이는 상속에 사용되는 키워드가

'extends'인 이유라고 할 수 있습니다.

### **02. 상속 예제**

![](https://blog.kakaocdn.net/dn/dxrWZb/btqS6XbWJ8L/HITcnoRVXGPfa1nJ6RsoWK/img.png)

예제 7_1

![](https://blog.kakaocdn.net/dn/L5aDD/btqS1VzrgXb/FwpCiRojHeudzSJWzCJhq1/img.png)

Tv클래스와 SmartTv클래스의 관계


#### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#q-private-%EC%A0%91%EA%B7%BC%EC%A0%9C%EC%96%B4%EC%9E%90%EB%A1%9C-%EC%A7%80%EC%A0%95%EB%90%9C-%EB%A9%A4%EB%B2%84%EB%8A%94-%EC%83%81%EC%86%8D%EB%90%98%EC%A7%80-%EC%95%8A%EC%A7%80-%EC%95%8A%EB%82%98-)Q. private 접근제어자로 지정된 멤버는 상속되지 않지 않나 ?

> 접근제어자가 private 또는 default인 멤버들은 상속되지 않는다기보다 상속은 받지만 자손 클래스로부터의  `접근이 제한`되는 것이다.

```text
자손 클래스의 인스턴스를 생성하면 조상 클래스의 멤버와 자손 클래스의 멤버가 합쳐진 하나의 인스턴스로 생성된다.
```

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#12-%ED%81%B4%EB%9E%98%EC%8A%A4%EA%B0%84%EC%9D%98-%EA%B4%80%EA%B3%84---%ED%8F%AC%ED%95%A8%EA%B4%80%EA%B3%84)1.2 클래스간의 관계 - 포함관계

클래스간의 포함관계를 맺어주는 것은 한 클래스의  `멤버변수로 다른 클래스 타입의 참조변수를 선언`하는 것을 뜻한다.  
단위클래스별로 코드가 작게 나뉘어 작성되어 있기 때문에 코드를 관리하는데도 수월하다.

![](https://blog.kakaocdn.net/dn/bjpWKz/btqSX7UJqdt/K67kVg3aQVjKqZ6kWnIX0K/img.png)

포함관계


### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#13-%ED%81%B4%EB%9E%98%EC%8A%A4%EA%B0%84%EC%9D%98-%EA%B4%80%EA%B3%84-%EA%B2%B0%EC%A0%95%ED%95%98%EA%B8%B0)1.3 클래스간의 관계 결정하기

```text
원(Circle)은 점(Point)이다. — Circle is a Point
원(Circle)은 점(Point)을 가지고 있다 — Circle has a Point

상속관계 : '~은 ~이다. (is-a)'
포함관계 : '~은 ~을 가지고 있다. (has-a)'
```

참조변수의 출력이나 덧셈연산자를 이용한 참조변수와 문자열의 결합에는  `toString`이 자동적으로 호출되어 참조변수를 문자열로 대치한 후 처리한다.  
toString() 메서드는 모든 클래스의 조상인 Object 클래스에 정의되어 있다.

```text
참조변수 card
System.out.println(card) == System.out.println(card.toString());
```

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#14-%EB%8B%A8%EC%9D%BC-%EC%83%81%EC%86%8D-single-inheritance)1.4 단일 상속 (single inheritance)

다른 객체지향언어인 C++에서는 여러 조상 클래스로부터 상속받는 것이 가능하나 다중 상속(multiple inheritance)을 허용하지만,  `자바에서는 단일 상속만을 허용`한다.

#### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#%EB%8B%A4%EC%A4%91-%EC%83%81%EC%86%8D%EC%9D%98-%EC%9E%A5%EC%A0%90)다중 상속의 장점

> 다중 상속을 허용하면 여러 클래스로부터 상속받을 수 있기 때문에 복합적인 기능을 가진 클래스를 쉽게 작성할 수 있다.

#### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#%EB%8B%A4%EC%A4%91-%EC%83%81%EC%86%8D%EC%9D%98-%EB%8B%A8%EC%A0%90)다중 상속의 단점

> 클래스간의 관계가 매우 복잡해진다. 서로 다른 클래스로부터 상속받은 멤버간의 이름이 같은 경우 구별할 수 있는 방법이 없다.

#### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#%EB%8B%A8%EC%9D%BC-%EC%83%81%EC%86%8D-%EC%9E%A5%EC%A0%90)단일 상속 장점

> 클래스 간의 관계가 보다 명확해지고 코드를 더욱 신뢰할 수 있게 만들어준다.

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#15-object-%ED%81%B4%EB%9E%98%EC%8A%A4---%EB%AA%A8%EB%93%A0-%ED%81%B4%EB%9E%98%EC%8A%A4%EC%9D%98-%EC%A1%B0%EC%83%81)1.5 Object 클래스 - 모든 클래스의 조상

Object 클래스는 모든 클래스 상속계층도의 최상위에 있는 조상 클래스이다.  
다른 클래스로부터 상속 받지 않는 모든 클래스들은 자동적으로 Object 클래스를 상속 받는다.

```java
컴파일러가 자동으로 extends Object 추가 
(이미 어떤 클래스로부터 상속받도록 작성된 클래스에 대해서는 컴파일러가 `extends Object` 추가하지 않는다.)

class Tv extends Object {
...
}
```

Object 클래스에는 toString(), equals()와 같은 모든 인스턴스가 가져야 할 기본적인 11개의 메서드가 정의되어 있다.

## [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#2-%EC%98%A4%EB%B2%84%EB%9D%BC%EC%9D%B4%EB%94%A9-overriding)2. 오버라이딩 (overriding)

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#21-%EC%98%A4%EB%B2%84%EB%9D%BC%EC%9D%B4%EB%94%A9%EC%9D%B4%EB%9E%80)2.1 오버라이딩이란?

조상 클래스로부터 상속받은 메서드의 내용을 변경하는 것을 오버라이딩이라고 한다.

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#22-%EC%98%A4%EB%B2%84%EB%9D%BC%EC%9D%B4%EB%94%A9%EC%9D%98-%EC%A1%B0%EA%B1%B4)2.2. 오버라이딩의 조건

자손 클래스에서 오버라이딩 하는 메서드는 조상 클래스의 메서드와

-   이름이 같아야 한다.
-   매개변수가 같아야 한다.
-   반환타입이 같아야 한다.

⇒ 선언부가 서로 일치해야 한다.

#### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#%EC%A0%9C%ED%95%9C%EB%90%9C-%EC%A1%B0%EA%B1%B4-%ED%95%98%EC%97%90%EC%84%9C%EB%A7%8C-%EB%8B%A4%EB%A5%B4%EA%B2%8C-%EB%B3%80%EA%B2%BD%ED%95%A0-%EC%88%98-%EC%9E%88%EB%8B%A4)제한된 조건 하에서만 다르게 변경할 수 있다.

1.  접근 제어자는 조상 클래스의 메서드보다  `좁은 범위로 변경 할 수 없다`.
2.  예외는 조상 클래스의 메서드보다 많이 선언할 수 없다.
3.  인스턴스 메서드를 static 메서드로 또는 그 반대로 변경할 수 없다.

#### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#q-%EC%A1%B0%EC%83%81-%ED%81%B4%EB%9E%98%EC%8A%A4%EC%97%90-%EC%A0%95%EC%9D%98%EB%90%9C-static-%EB%A9%94%EC%84%9C%EB%93%9C%EB%A5%BC-%EC%9E%90%EC%86%90-%ED%81%B4%EB%9E%98%EC%8A%A4%EC%97%90%EC%84%9C-%EB%98%91%EA%B0%99%EC%9D%80-%EC%9D%B4%EB%A6%84%EC%9D%98-static-%EB%A9%94%EC%84%9C%EB%93%9C%EB%A1%9C-%EC%A0%95%EC%9D%98%ED%95%A0-%EC%88%98-%EC%9E%88%EB%82%98)Q. 조상 클래스에 정의된 static 메서드를 자손 클래스에서 똑같은 이름의 static 메서드로 정의할 수 있나?

> 가능하다. 하지만 이것은  `각 클래스에 별개의 static 메서드를 정의한 것일 뿐`  오버라이딩이 아니다. 각 메서드는 클래스 이름으로 구별될 수 있으며, 호출할 때는 ‘참조변수.메서드이름()’ 대신 ‘클래스이름.메서드이름()‘으로 하는 것이 바람직하다.  `static 멤버들은 자신들이 정의된 클래스에 묶여있다`고 생각하면 된다.

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#23-%EC%98%A4%EB%B2%84%EB%A1%9C%EB%94%A9-vs-%EC%98%A4%EB%B2%84%EB%9D%BC%EC%9D%B4%EB%94%A9)2.3 오버로딩 vs 오버라이딩

```text
오버로딩(overloading) : 기존에 없는 새로운 메서드를 정의하는 것 (new)
오버라이딩(overriding) : 상속받은 메서드의 내용을 변경하는 것 (change, modify)
```

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#24-super)2.4 super

super는 자손 클래스에서 조상 클래스로부터 상속받은 멤버를 참조하는데 사용되는 참조변수이다. this와 마찬가지로 super 역시 static 메서드에서는 사용할 수 없고 인스턴스 메서드에서만 사용할 수 있다.

```java
class Parent {
	int x = 10;
}

class Child extends Parent {
int x = 20;

	void print() {
		System.out.println("this.x = " + this.x);    // 20
		System.out.println("super.x = " + super.x);  // 10
	}
}
```

![](https://blog.kakaocdn.net/dn/nNvCE/btqTfCSq9kk/VByMCLJLwQhzdCjf7kPFIk/img.png)

예제 7_2

![](https://blog.kakaocdn.net/dn/bdbQct/btqSZwNBkkh/wA7U9twLsRFvFOXkVxnYCk/img.png)

예제 7_3

같은 이름의 멤버변수가 조상 클래스와 자손 클래스 모두에 있으면 super와 this는 서로 다른 값을 참조하게 된다. 조상 클래스에 선언된 멤버 변수와 같은 이름의 멤버 변수를 자손 클래스에 중복 정의할 수 있다.

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#25-super---%EC%A1%B0%EC%83%81-%ED%81%B4%EB%9E%98%EC%8A%A4%EC%9D%98-%EC%83%9D%EC%84%B1%EC%9E%90)2.5 super() - 조상 클래스의 생성자

super()는 조상 클래스의 생성자를 호출하는데 사용된다. 자손 클래스의 인스턴스를 생성하면 자손의 멤버와 조상의 멤버가 모두 합쳐진 하나의 인스턴스가 생성된다.

생성자의 첫 줄에서 조상 클래스의 생성자를 호출해야 하는 이유는 자손 클래스의 멤버가 조상 클래스의 멤버를 사용할 수도 있으므로  `조상의 멤버들이 먼저 초기화 되어`  있어야 하기 때문이다.

```text
Object 클래스를 제외한 모든 클래스의 생성자 첫 줄에 생성자 this() 또는 super()를 호출해야 한다.
그렇지 않으면 컴파일러가 자동적으로 super()를 생성자의 첫 줄에 삽입한다.
```

![](https://blog.kakaocdn.net/dn/JbmwQ/btqSZwNEt6x/RBFINU5wvUlT2cj94S4xSk/img.png)

예제 7_4

인스턴스를 생성할 때는 클래스를 선택하는 것만큼 생성자를 선택하는 것도 중요하다.

```text
1. 클래스 — 어떤 클래스의 인스턴스를 생성할 것인가 ?
2. 생성자 — 선택한 클래스의 어떤 생성자를 이용해서 인스턴스를 생성할 것인가 ?
```

## [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#3-package%EC%99%80-import)3. package와 import

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#31-%ED%8C%A8%ED%82%A4%EC%A7%80-package)3.1 패키지 (package)

패키지란 클래스의 묶음이다. 패키지에는 클래스 또는 인터페이스를 포함시킬 수 있으며,  `서로 관련된 클래스들끼리 그룹 단위로 묶어`  놓음으로써 클래스를 효율적으로 관리할 수 있다.

```text
- 하나의 소스 파일에는 첫 번째 문장으로 단 한 번의 패키지 선언만을 허용한다.
- 모든 클래스는 반드시 하나의 패키지에 속해야 한다.
- 패키지는 점(.)을 구분자로 하여 계층구조로 구성할 수 있다.
- 패키지는 물리적으로 클래스 파일(.class)을 포함하는 하나의 디렉토리이다.
```

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#32-%ED%8C%A8%ED%82%A4%EC%A7%80%EC%9D%98-%EC%84%A0%EC%96%B8)3.2 패키지의 선언

```java
package 패키지명;
```

패키지 선언문은 반드시 소스 파일에서 주석과 공백을 제외한 첫 번째 문장이어야 한다.  
하나의 소스 파일에 단 한번만 선언될 수 있다.  
클래스명과 쉽게 구분하기 위해 소문자로 하는 것을 원칙으로 한다.

-   ‘\jre\classes\’
-   ‘\jre\lib\ext\’

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#33-import-%EB%AC%B8)3.3 import 문

import 문의 역할은 컴파일러에게 소스 파일에 사용된 클래스의  `패키지에 대한 정보를 제공`하는 것이다.

**import문**을 통해 **사용하고자 하는**

**클래스의 패키지를 미리 명시해주면**

**소스코드에 사용되는 클래스이름에서**

**패키지명 생략이 가능**합니다.

**import문의 역할**은

**컴파일러에게 소스파일에 사용된**

**클래스의 패키지에 대한 정보를**

**제공**하는 것이며,

**import문의 단축키**는

**'ctrl + shift + o'**  입니다.

import문은  **클래스 선언문 이전에 위치**하며,

**한 소스파일에 여러 번 선언**할 수 있습니다.

**import문을 선언하는 방법**은

아래와 같습니다.

#### **import 패키지명.클래스명;**

#### **import 패키지명.*;**

**※ '패키지명.*' : 지정된 패키지에 속하는 모든 클래스를**

**패키지명 없이 사용가능하며, 실행 시 성능상의 차이는 없습니다.**

### **16. static import문**

**static import문**을 사용하면

**static멤버를 호출할 때,**

**클래스 이름을 생략**할 수 있습니다.

![](https://blog.kakaocdn.net/dn/csVlBt/btqTcPECil9/Ewf51uMvlGZnKtmgKBijLk/img.png)

예제 7_6

```java
import java.lang.*;
```

`java.lang`  패키지는 매우 빈번히 사용되는 중요한 클래스들이 속한 패키지이기 때문에 따로 import문으로 지정하지 않아도 된다.

## [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#4-%EC%A0%9C%EC%96%B4%EC%9E%90-modifier)4. 제어자 (modifier)

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#41-%EC%A0%9C%EC%96%B4%EC%9E%90%EB%9E%80-)4.1 제어자란 ?

제어자는 클래스, 변수 또는 메서드의 선언부에 함께 사용되어 부가적인 의미를 부여한다.  
제어자들 간의 순서는 관계없지만 주로 접근 제어자를 제일 왼쪽에 놓는 경향이 있다.

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#42-static)4.2 static

-   static 멤버변수
    
    -   모든 인스턴스에 공통적으로 사용되는 클래스 변수가 된다.
    -   클래스변수는 인스턴스를 생성하지 않고도 사용 가능하다.
    -   클래스가 메모리에 로드될 때 생성된다.
-   static 메서드
    
    -   인스턴스를 생성하지 않고도 호출이 가능한 static 메서드가 된다.
    -   static 메서드 내에서는 인스턴스 멤버들을 직접 사용할 수 없다.


![](https://blog.kakaocdn.net/dn/JkXbP/btqTfDqmttS/1nZYvXkoTvIhEOSPtRJiE0/img.png)

static - 클래스의, 공통적인

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#43-final)4.3. final

-   클래스
    
    -   변경할 수 없는 클래스, 확장될 수 없는 클래스가 된다.
    -   final로 지정된 클래스는 다른 클래스의 조상이 될 수 없다.
-   메서드
    
    -   변경될 수 없는 메서드, final로 지정된 메서드는 오버라이딩을 통해 재정의 될 수 없다.
-   멤버변수, 지역변수
    
    -   변수 앞에 final이 붙으면, 값을 변경할 수 없는 상수가 된다.

![](https://blog.kakaocdn.net/dn/djzWmb/btqS3I7DnUC/wa5sRtK4SptY2sR6GNhso0/img.png)

final - 마지막의, 변경될 수 없는

대표적인 final 클래스는 String과 Math가 있다.

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#43-%EC%83%9D%EC%84%B1%EC%9E%90%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%9C-final-%EB%A9%A4%EB%B2%84-%EB%B3%80%EC%88%98%EC%9D%98-%EC%B4%88%EA%B8%B0%ED%99%94)4.3 생성자를 이용한 final 멤버 변수의 초기화

final이 붙은 변수는 상수이므로 일반적으로 선언과 초기화를 동시에 하지만, 인스턴스 변수의 경우  `생성자에서 초기화 되도록`  할 수 있다.

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#44-abstract---%EC%B6%94%EC%83%81%EC%9D%98-%EB%AF%B8%EC%99%84%EC%84%B1%EC%9D%98)4.4 abstract - 추상의, 미완성의

-   클래스 — 클래스에 사용되어 클래스 내에 추상 메서드가 존재한다는 것을 쉽게 알 수 있게 한다.
-   메서드 — 메서드의 선언부만 작성하고 실제 수행 내용은 구현하지 않은 추상 메서드를 선언하는데 사용된다.

![](https://blog.kakaocdn.net/dn/bYjQnd/btqS3ai3nOX/wkNYt0O5uHAIHK0AY8Cux0/img.png)

abstract - 추상의, 미완성의

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#45-%EC%A0%91%EA%B7%BC-%EC%A0%9C%EC%96%B4%EC%9E%90-access-modifier)4.5 접근 제어자 (access modifier)

접근 제어자는 멤버 또는 클래스에 사용되어, 해당하는 멤버 또는 클래스를 외부에서 접근하지 못하도록 제한하는 역할을 한다.  
클래스나 멤버변수, 메서드, 생성자에 접근 제어자가 지정되어 있지 않다면, 접근 제어자가 default 임을 뜻한다.

```shell
private : 같은 클래스 내에서만 접근이 가능하다.
default : 같은 패키지 내에서만 접근이 가능하다.
protected : 같은 패키지 내에서, 그리고 다른 패키지의 자손 클래스에서 접근이 가능하다.
public : 접근 제한이 없다.
```

접근 범위 : public > protected > default > private

![](https://blog.kakaocdn.net/dn/Luxhf/btqS6YB4zlp/cAZbcOmkGzpVi8z3vlzyr0/img.png)

접근 제어자(access modifier)

![](https://blog.kakaocdn.net/dn/diux82/btqS4Nt6Z2s/i0kaM2HMNCviiOQIzXpoAk/img.png)

접근 제어자(access modifier)

#### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#%EC%A0%91%EA%B7%BC-%EC%A0%9C%EC%96%B4%EC%9E%90%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%9C-%EC%BA%A1%EC%8A%90%ED%99%94)접근 제어자를 이용한 캡슐화

```shell
접근 제어자를 사용하는 이유
- 외부로부터 데이터를 보호하기 위해서
- 외부에는 불필요한, 내부적으로만 사용되는, 부분을 감추기 위해서
```

#### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#%EC%83%9D%EC%84%B1%EC%9E%90%EC%9D%98-%EC%A0%91%EA%B7%BC-%EC%A0%9C%EC%96%B4%EC%9E%90)생성자의 접근 제어자

생성자에 접근 제어자를 사용함으로써 인스턴스의 생성을 제한할 수 있다.  
생성자가 private인 클래스는 다른 클래스의 조상이 될 수 없다. 왜냐하면 자손 클래스의 인스턴스를 생성할 때 조상 클래스의 생성자를 호출해야만 하는데, 생성자의 접근 제어자가 private이므로 자손 클래스에서 호출하는 것이 불가능하기 때문이다.  `클래스 앞에 final을 추가하여 상속할 수 없는 클래스라는 것을 알리는 것이 좋다`.

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#46-%EC%A0%9C%EC%96%B4%EC%9E%90modifier%EC%9D%98-%EC%A1%B0%ED%95%A9)4.6 제어자(modifier)의 조합

```text
1. 메서드에 static과 abstract를 함께 사용할 수 없다.
static 메서드는 몸통이 있는 메서드만 사용할 수 있기 때문이다.

2. 클래스에 abstract와 final을 동시에 상용할 수 없다.
클래스에 사용되는 final은 클래스를 확장할 수 없다는 의미이고, 
abstract는 상속을 통해서 완성되어야 한다는 의미이므로 서로 모순되기 때문이다.

3. abstract 메서드의 접근 제어자가 private일 수 없다.
abstract 메서드는 자손 클래스에서 구현해주어야 하는데 접근 제어자가 private이면, 
자손 클래스에서 접근할 수 없기 때문이다.

4. 메서드에 private과 final을 같이 사용할 필요는 없다.
접근 제어자가 private인 메서드는 오버라이딩 될 수 없기 때문이다. 이 둘 중 하나만 사용해도 의미가 충분하다.
```

### **22. 캡슐화와 접근 제어자**

클래스나 멤버에  **접근 제어자를 사용하는 이유**는

**클래스의 내부에 선언된 데이터를 보호하기 위함**이며,

이를  **객체지향개념의 캡슐화(encapsulation)에**

**해당하는** **데이터 감추기(data hiding)**라고 합니다.

일반적으로  **private나 protected로 멤버변수를**

**제한하고** **public메서드를 제공**함으로써

**간접적으로 멤벼변수 값을** **다룰 수 있도록**

**하는 것이 바람직**합니다.

그래서

**보통 멤버변수의 값을 읽는 메서드**의 이름을

**'get멤버변수이름'**으로 하고  **'겟터(getter)'**라 하며,

**멤버변수의 값을 변경하는 메서드**의 이름을

**'set멤버변수이름'**으로 하고  **'셋터(setter)'**라 부릅니다.

## [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#5-%EB%8B%A4%ED%98%95%EC%84%B1-polymorphism)5. 다형성 (polymorphism)

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#51-%EB%8B%A4%ED%98%95%EC%84%B1%EC%9D%B4%EB%9E%80-)5.1 다형성이란 ?

객치지향개념에서 다형성이란  `여러 가지 형태를 가질 수 있는 능력`을 의미한다. 프로그래밍적으로는 한 타입의 참조변수로  `여러 타입의 객체를 참조`할 수 있도록 하는 것을 의미한다.  
조상 클래스 타입의 참조변수로 자손 클래스의 인스턴스를 참조할 수 있도록 한다.  
참조변수의 타입에 따라 사용할 수 있는 멤버의 개수가 달라진다.  
`자손타입의 참조변수로 조상타입의 인스턴스를 참조하는 것은 불가능하다.`  그 이유는 실제 인스턴스인 조상의 멤버 개수보다 자손타입의 참조변수가 사용할 수 있는 멤버 개수가 더 많기 때문이다.

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#52-%EC%B0%B8%EC%A1%B0%EB%B3%80%EC%88%98%EC%9D%98-%ED%98%95%EB%B3%80%ED%99%98)5.2 참조변수의 형변환

서로 상속관계에 있는 클래스 사이에서만 형변환 가능하다.

### **24. 참조변수의 형변환**

**참조변수의 형변환**은  **사용할 수 있는**

**멤버의 개수를 조절하기 위한 것**이며,

**서로 상속관계에 있는** **클래스**

**사이에서만 가능**합니다.

**자손타입에서 조상타입으로 형변환하는 경우,**

**형변환은 생략이 가능(Up-casting**)하지만

조상타입에서 자손타입으로 형변환하는 경우,

형변환은 생략이 불가능(Down-casting)합니다.

### **25. 참조변수의 형변환 예제**

![](https://blog.kakaocdn.net/dn/cx7CYl/btqThYWnYMv/wiEYw7twDETRjsJ5V9PdKk/img.png)

예제 7_7

```java
자손타입 => 조상타입(Up-casting) : 형변환 생략가능
자손타입 <= 조상타입(Down-casting) : 형변환 생략불가

Car car = null;
FireEngine fe = new FireEngine();
FireEngine fe2 = null;

car = fe;  // 업캐스팅
fe2 = (FireEngine)car;  // 다운캐스팅
```

Car타입의 참조변수 c를 Car타입의 조상인 Object타입의 참조변수로 형변환 하는 것은  `참조변수가 다룰 수 있는 멤버의 개수가 실제 인스턴스가 갖고 있는 멤버의 개수보다 적을 것이 분명`하므로 문제가 되지 않는다. 그래서 형변환을 생략할 수 있다.

![](https://blog.kakaocdn.net/dn/bkaxA9/btqTcPL9sQJ/0sGbjOiWOa8SykDJpvgnTK/img.png)

다형성(polymorphism)

![](https://blog.kakaocdn.net/dn/JTL8u/btqS4MP6cTf/ZreNbc6JKUpwniCoNT2TqK/img.png)

다형성(polymorphism)

참조변수의 형변환은 인스턴스에 아무런 영향을 미치지 않는다.  
단지 참조변수의 형변환을 통해서, 참조하고 있는 인스턴스에서 사용할 수 있는  `멤버의 범위(개수)를 조절`하는 것 뿐이다.  
`컴파일 시에는 참조변수 간의 타입만 체크하기 때문에 실행 시 생성될 인스턴스의 타입에 대해서는 전혀 알지 못한다. 참조변수가 가리키는 인스턴스의 자손타입으로 형변환은 허용되지 않는다. 그래서 참조변수가 가리키는 인스턴스의 타입이 무엇인지 확인하는 것이 중요하다.`

**조상타입의 참조변수로**

**자손타입의 인스턴스를 참조하는 경우**,

**조상 클래스의 멤버만 사용 가능**하며,

자손 클래스에 생성된 멤버는

사용이 불가능합니다.

이와 반대로

**자손타입의 참조변수로** **조상타입의**

**인스턴스를 참조하는 것은** **허용하지 않는데,**

이는  **자손타입의 참조변수가  사용할 수 있는**

**멤버의 개수가 조상의 멤버의 개수보다**

**많기 때문**입니다.

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#53-instanceof-%EC%97%B0%EC%82%B0%EC%9E%90)5.3 instanceof 연산자

참조변수가 참조하고 있는 인스턴스의 실제 타입을 알아보기 위해 instanceof 연산자를 사용한다.  
`어떤 타입에 대한 instanceof 연산의 결과가 true라는 것은 검사한 타입으로 형변환이 가능하다는 것을 뜻한다.`

**instanceof 연산자**는  **참조변수가 참조하는**

**인스턴스의 실제 타입을 확인하는데 사용**하며,

**연산의 결과**는  **boolean타입**으로  **참조변수가**

**검사한 타입으로 형변환이 가능하면 true**,

**형변환이 불가능하면 false를 반환**합니다.

### **27. 매개변수의 다형성**

**참조형 매개변수**는  **메서드 호출시,**

**자신과 같은 타입 또는 자손타입의**

**인스턴스를 넘겨줄 수 있습니다.**

자세한 내용은 예제를 통해 살펴보겠습니다.

### **28. 매개변수의 다형성 예제**

![](https://blog.kakaocdn.net/dn/bl9NnU/btqThZt9APy/70aghpFBiAULnMXMbixzq0/img.png)

예제 7_8 클래스

![](https://blog.kakaocdn.net/dn/bluJx5/btqS6YXnH1D/MKLoCLiBSrop2phfWtD1EK/img.png)

예제 7_8 결과

### **29. 여러 종류의 객체를 배열로 다루기**

조상타입의 참조변수로 자손타입의

객체를 참조하는 것이 가능하므로,

**조상타입의 참조변수 배열을 통해**

**공통의 조상을 가진 서로 다른 종류의**

**객체를 묶어서 다룰 수 있습니다.**

### **30. 여러 종류의 객체를 배열로 다루기 예제**

![](https://blog.kakaocdn.net/dn/IekQ9/btqTcQR8Zgm/CLOwiwfxKFV1T2ptbYclB1/img.png)

예제 7_9 클래스

![](https://blog.kakaocdn.net/dn/cqIrN9/btqTfDdP7j1/F9yKTnL344AC43YUPBVzv0/img.png)

예제 7_9 결과

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#54-%EC%B0%B8%EC%A1%B0%EB%B3%80%EC%88%98%EC%99%80-%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%EC%9D%98-%EC%97%B0%EA%B2%B0)5.4 참조변수와 인스턴스의 연결

멤버변수가 조상 클래스와 자손 클래스에 중복으로 정의된 경우, 조상타입의 참조변수를 사용했을 때는 조상 클래스에 선언된 멤버변수가 사용되고, 자손타입의 참조변수를 사용했을 때는 자손 클래스에 선언된 멤버변수가 사용된다.  
메서드는 참조변수의 타입에 관계없이 항상 실제 인스턴스의 메서드가 호출된다.  
`인스턴스 변수에 직접 접근(참조변수명.인스턴스변수명)하면, 참조변수의 타입에 따라 사용되는 인스턴스 변수가 달라질 수 있으므로 주의해야 한다.`

## [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#6-%EC%B6%94%EC%83%81-%ED%81%B4%EB%9E%98%EC%8A%A4-abstract-class)6. 추상 클래스 (abstract class)

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#61-%EC%B6%94%EC%83%81-%ED%81%B4%EB%9E%98%EC%8A%A4%EB%9E%80-)6.1 추상 클래스란 ?

클래스를 설계도에 비유한다면, 추상클래스는 미완성 설계도에 비유할 수 있다.  
클래스가 미완성이라는 것은 멤버의 개수에 관계된 것이 아니라, 단지 미완성 메서드(추상메서드)를 포함하고 있다는 의미이다.  
추상클래스로 인스턴스를 생성할 수 없다. 추상 클래스는 상속을 통해서 자손 클래스에 의해서만 완성될 수 있다.

```java
abstract class 클래스 이름 {
...
}
```

추상 메서드를 포함하고 있지 않은 클래스에도 키워드 ‘abstract’를 붙여서 추상클래스로 지정할 수 있다.

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#62-%EC%B6%94%EC%83%81-%EB%A9%94%EC%84%9C%EB%93%9C)6.2 추상 메서드

선언부만 작성하고 구현부는 작성하지 않은 채로 남겨둔 것이 추상 메서드이다.

```text
/* 주석을 통해 어떤 기능을 수행할 목적으로 작성하였는지 설명한다. */
abstract 리턴 타입 메서드 이름();
```

추상 클래스로부터 상속받는 자손 클래스는 오버라이딩을 통해 조상인 추상 클래스의  `추상 메서드를 모두 구현`해주어야 한다.

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#63-%EC%B6%94%EC%83%81-%ED%81%B4%EB%9E%98%EC%8A%A4%EC%9D%98-%EC%9E%91%EC%84%B1)6.3 추상 클래스의 작성

```text
'추상'의 사전적 의미
낱낱의 구체적 표상이나 개념에서 공통된 성질을 뽑아 이를 일반적인 개념으로 파악하는 정신 작용.
```

`추상화`  는 기존의 클래스의 공통 부분을 뽑아내서 조상 클래스를 만드는 것이다.  
상속 계층도를 따라 내려갈수록 클래스는 점점 기능이 추가되어  `구체화의 정도가 심해지며`, 상속 계층도를 따라 올라갈수록 클래스는  `추상화의 정도가 심해진다`.

```text
추상화 — 클래스간의 공통점을 찾아내서 공통의 조상을 만드는 작업
구체화 — 상속을 통해 클래스를 구현, 확장하는 작업
```

`abstract를 붙여서 추상 메서드로 선언하는 이유는 자손 클래스에서 추상 메서드를 반드시 구현하도록 강요하기 위해서`이다.

![](https://blog.kakaocdn.net/dn/cgtz6O/btqTlGOoy2C/zTyEul8KNjkYV5H2RhoUm1/img.png)

예제 7_10 클래스

![](https://blog.kakaocdn.net/dn/bL7bWU/btqThYPPG66/aSxMtOZ2riFPHwm04jApd1/img.png)

예제 7_10 결과

## [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#7-%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4-interface)7. 인터페이스 (interface)

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#71-%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EB%9E%80-)7.1 인터페이스란 ?

인터페이스는 추상 클래스보다 추상화 정도가 높아서, 추상 클래스와 달리 몸통을 갖춘 일반 메서드 또는 멤버 변수(상수만을 가진다.)를 구성원으로 가질 수 없다. (Java8부터 default 메소드를 이용하여 메소드 구현부에 함께 인터페이스에 선언할 수 있다.)

추상 클래스를 부분적으로만 완성된  `미완성 설계도`라고 한다면, 인터페이스는 구현된 것은 아무것도 없고 밑그림만 그려져 있는  `기본 설계도`라 할 수 있다.

**인터페이스**는 **일종의 추상클래스**이며,

추상클래스와 달리 **구현부를 갖춘 일반 메서드와**

**멤버변수를 구성원으로 가질 수 없으며,**

**오직 추상메서드와 상수만을 멤버로**

**가질 수 있기 때문에,**

**추상클래스보다 추상화 정도가**

**높다**고 할 수 있습니다.

추상클래스를 부분적으로만 미완성된

'미완성 설계도'라고 한다면,

**인터페이스는 밑그림만 그려져 있는**

**'기본 설계도'**라고 할 수 있으며,

**미리 정해진 규칙에 맞게 구현하도록**

**표준을 제시하는 역할**을 합니다.

**인터페이스를 작성하는 방법**은

**키워드 'class' 대신 'interface'를 사용**하는 것

외에는 클래스 작성과 동일하며,

**접근제어자**로  **public이나 (default)만 사용**합니다.

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#72-%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EC%9D%98-%EC%9E%91%EC%84%B1)7.2 인터페이스의 작성

```java
interface 인터페이스이름 {
	public static final 타입 상수이름 = 값;
	public abstract 메서드이름(매개변수목록);
}
```

#### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4-%EB%A9%A4%EB%B2%84-%EC%A0%9C%EC%95%BD%EC%82%AC%ED%95%AD)인터페이스 멤버 제약사항

> 모든 멤버변수는 public static final 이어야 하며, 이를 생략할 수 있다. 모든 메서드는 public abstract이어야 하며 이를 생략할 수 있다. (단, static 메서드와 default 메서드는 예외, Java8부터)

생략된 제어자는 컴파일 시에 컴파일러가 자동적으로 추가해준다.  
Java8 이전에는 인터페이스의 모든 메서드는 추상 메서드이어야 했다. Java8부터 인터페이스에 static 메서드와 default 메서드의 추가를 허용한다.

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#73-%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EC%9D%98-%EC%83%81%EC%86%8D)7.3 인터페이스의 상속

인터페이스는 인터페이스로부터만 상속받을 수 있다. 여러개의 인터페이스로부터 상속 가능하다.

```java
인터페이스는 클래스와 달리 Object 클래스와 같은 최고 조상이 없다.
interface Movable {
	void move(int x, int y);
}

interface Attackable {
	void attack(Unit u);
}

interface Fightable extends Movable, Attackable { 
	// move(int x, int y), attack(Unit u)을 멤버로 갖는다.
}
```

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#74-%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EC%9D%98-%EA%B5%AC%ED%98%84)7.4 인터페이스의 구현

추상 클래스와 같이 그 자체로는  `인스턴스를 생성할 수 없다`. 인터페이스에 정의된 추상 메서드의 구현체를 만들어주는 클래스를 작성해야 한다.  `implements`  키워드 사용.

```java
class 클래스이름 implements 인터페이스이름 {
	// 인터페이스에 정의된 추상 클래스를 구현한다.
}
```

구현하는 인터페이스의 메서드 중 일부만 구현한다면, abstract를 붙여서 추상클래스로 선언해야 한다.

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#75-%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%9C-%EB%8B%A4%EC%A4%91-%EC%83%81%EC%86%8D)7.5 인터페이스를 이용한 다중 상속

자바에서는 다중 상속을 허용하지 않는다.

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#76-%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%9C-%EB%8B%A4%ED%98%95%EC%84%B1)7.6 인터페이스를 이용한 다형성

자손 클래스의 인스턴스를 조상 타입의 참조 변수로 참조하는 것이 가능하다.  
리턴 타입이 인터페이스라는 것은 메서드가 해당 인터페이스를 구현한 클래스의 인스턴스를 반환한다는 것이다.

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#77-%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EC%9D%98-%EC%9E%A5%EC%A0%90)7.7 인터페이스의 장점

-   개발 시간을 단축시킬 수 있다.
-   표준화가 가능하다.
-   서로 관계없는 클래스들에게 관계를 맺어줄 수 있다.
    
    -   서로 아무런 관계가 없는 클래스들에게 하나의 인터페이스를 공통적으로 구현하도록 함으로써 관계를 맺어줄 수 있다.
-   독립적인 프로그래밍이 가능하다.
    
    -   클래스의 선언과 구현을 분리시킬 수 있다. 클래스와 클래스간의 직접적인 관계를 인터페이스를 이용해서 간접적인 관계로 변경하면, 한 클래스의 변경이 관련된 다른 클래스에 영향을 미치지 않는 독립적인 프로그래밍이 가능하다.

```java
interface Repairable { }

class SCV extends GroundUnit implements Repairable { //... }

class Tank extends GroundUnit implements Repairable { //... }

class Dropship extends AirUnit implements Repairable { //... }
```

위 3개의 클래스에는 같은 인터페이스를 구현했다는 공통점이 생겼다. 메서드의 매개변수로 Repairable 인터페이스를 구현한 클래스의 인스턴스만 받아들여질 것이다. void repair(Repairable r) { // 매개변수로 넘겨받은 유닛을 수리한다. }

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#78-%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EC%9D%98-%EC%9D%B4%ED%95%B4)7.8 인터페이스의 이해

그래서 인터페이스란 도대체 무엇인가 ?

```text
- 클래스를 사용하는 쪽(User)과 클래스를 제공하는 쪽(Provider)이 있다.
- 메서드를 사용(호출)하는 쪽(User)에서는 사용하려는 메서드(Provider)의 선언부만 알면 된다.(내용은 몰라도 된다.)
```

직접적인 관계의 두 클래스는 한 쪽(Provider)이 변경되면 다른 한 쪽(User)도 변경되어야 한다는 단점이 있다. 두 클래스 간의 관계를 간접적으로 변경하기 위해서는 먼저  `인터페이스를 이용해서 클래스 B(Provider)의 선언과 구현을 분리`해야 한다.

```java
클래스 A는 인터페이스 I하고만 직접적인 관계에 있기 때문에 클래스 B의 변경에 영향을 받지 않는다.

class A {
	methodA(I i) {
		i.methodB();
	}
}

interface I { 
	public abstract void methodB();
}

class B implements I {
	public methodB() {
		System.out.println("methodB in B class");
	}
}
```

[![인터페이스](https://im-yeobi.io/static/9065239c27fb26b26cd9da7c1c15fd07/f570d/007-oop-interface.png "인터페이스")](https://im-yeobi.io/static/9065239c27fb26b26cd9da7c1c15fd07/264f6/007-oop-interface.png)

```text
인터페이스 I는 실제 구현 내용(클래스 B)을 감싸고 있는 껍데기이며, 클래스 A는 껍데기 안에 어떤 알맹이(클래스)가 있는지 몰라도 된다.
```

인터페이스의 참조 변수로도 Obejct 클래스에 정의된 메서드들을 호출할 수 있다. 모든 객체는 Object 클래스에 정의된 메서드를 가지고 있을 것이기 때문에 허용하는 것이다.

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#79-default-%EB%A9%94%EC%84%9C%EB%93%9C%EC%99%80-static-%EB%A9%94%EC%84%9C%EB%93%9C)7.9 default 메서드와 static 메서드

Java 8부터 디폴트 메서드와 static 메서드도 인터페이스에 추가할 수 있다.

#### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#default-%EB%A9%94%EC%84%9C%EB%93%9C)default 메서드

인터페이스에 메서드를 추가한다는 것은 추상 메서드를 추가한다는 것이고, 이 인터페이스를 구현한 기존의 모든 클래스들이 새로 추가된 메서드를 구현해야 한다는 것을 의미한다.  
default 키워드를 붙이며, 추상 메서드와 달리 일반 메서드처럼 몸통{}이 있어야 한다.

```java
interface MyInterface {
	void method();
	default void newMethod() { }
}
```

-   default 메서드와 기존의 메서드 이름 중복되어 충돌하는 경우
    
    -   여러 인터페이스의 default 메서드 간의 충돌
	    -   인터페이스를 구현한 클래스에서 default 메서드를 오버라이딩 해야 한다.
    -   default 메서드와 조상 클래스의 메서드 간의 충돌
	    -   조상 클래스의 메서드가 상속되고, default 메서드는 무시된다.

![](https://blog.kakaocdn.net/dn/IVE2d/btqTqIrz7ZN/Lfk2RRlC1qsCQNgR1JIa11/img.png)

예제 7_11 클래스와 인터페이스

![](https://blog.kakaocdn.net/dn/bavQZC/btqTp3W65FW/9yc7CYGI9IT2LS82kG8h70/img.png)

예제 7_11 결과

## [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#8-%EB%82%B4%EB%B6%80-%ED%81%B4%EB%9E%98%EC%8A%A4-inner-class)8. 내부 클래스 (inner class)

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#81-%EB%82%B4%EB%B6%80-%ED%81%B4%EB%9E%98%EC%8A%A4%EB%9E%80-)8.1 내부 클래스란 ?

내부 클래스는 클래스 내에 선언된 클래스이다. 클래스에 다른 클래스를 선언하는 이유는 두 클래스가 서로 긴밀한 관계에 있기 때문이다.

```text
내부 클래스의 장점
- 내부 클래스에서 외부 클래스의 멤버들을 쉽게 접근할 수 있다.
- 코드의 복잡성을 줄일 수 있다.(캡슐화)
```

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#82-%EB%82%B4%EB%B6%80-%ED%81%B4%EB%9E%98%EC%8A%A4%EC%9D%98-%EC%A2%85%EB%A5%98%EC%99%80-%ED%8A%B9%EC%A7%95)8.2 내부 클래스의 종류와 특징

-   instance 클래스
    
    -   외부 클래스의 멤버변수 선언 위치에 선언. 외부 클래스의 인스턴스 멤버처럼 다루어진다.
-   static 클래스
    
    -   외부 클래스의 멤버변수 선언 위치에 선언. 외부 클래스의 static 멤버처럼 다루어진다. 특히 외부 클래스의 static 메서드에서 사용될 목적으로 선언된다.
-   local 클래스
    
    -   외부 클래스의 메서드나 초기화 블럭 안에 선언하며, 선언된 영역 내부에서만 사용될 수 있다.
-   anonymous 클래스
    
    -   클래스의 선언과 객체의 생성을 동시에 하는 이름 없는 클래스(일회용)

![](https://blog.kakaocdn.net/dn/5r7Ah/btqS90A9YRT/0obWO3jY3Ml3jc3kuO6pZK/img.png)

내부 클래스의 종류와 특징

### **44. 내부 클래스의 선언**

**내부 클래스의 선언위치는**

**변수의 선언위치와 동일**하며,

각 내부 클래스의  **선언 위치에 따라**

**변수와 동일한 유효범위(scope)와**

**접근성(accessibility)**을 갖습니다.

![](https://blog.kakaocdn.net/dn/2XYc5/btqTkgJLywD/HNCpVKDr8Jl8N55hycDyl1/img.png)

변수의 선언과 내부 클래스의 선언

### **45. 내부 클래스의 제어자와 접근성**

**내부 클래스**는

**외부 클래스의 멤버와 같이 간주**되고,

**인스턴스멤버와 static멤버 간의 규칙이**

**내부클래스에도 똑같이 적용**됩니다.

내부 클래스도 클래스이므로

**'abstract'나 'final'과 같은 제어자를 사용**할 수

있을 뿐만 아니라, 멤버변수들처럼  **'private'나**

**'protected'와 같은 접근제어자도**

**사용 가능**합니다.

자세한 내용은 예제를 통해 알아보겠습니다.

### **46. 내부 클래스의 제어자와 접근성 예제1**

**① 내부 클래스 중에서 스태틱 클래스만**

**static멤버를 가질 수 있습니다.**

**② final과 static이 동시에 붙은 변수는**

**상수(constant)이므로 모든 내부 클래스에서**

**정의가 가능합니다.**

![](https://blog.kakaocdn.net/dn/bzow07/btqTh0glZEI/TinhJr9THhFTilK3eQEC0k/img.png)

예제 7_12

### **47. 내부 클래스의 제어자와 접근성 예제2**

**"내부 클래스도 외부 클래스의 멤버로 간주되며,**

**동일한 접근성을 갖습니다."**

![](https://blog.kakaocdn.net/dn/Th63h/btqToxEoId0/iRG1eXqM03KLOLSzkLw6Zk/img.png)

예제 7_13

### **48. 내부 클래스의 제어자와 접근성 예제3**

**"내부 클래스에서 외부 클래스의 변수들에 대한**

**접근성을 보여주는 예제입니다."**

![](https://blog.kakaocdn.net/dn/nCUnk/btqTrSucDrr/uhCCz2KIwmvFNHAoamFxl1/img.png)

예제 7_14

### **49. 내부 클래스의 제어자와 접근성 예제4**

**"외부 클래스가 아닌 다른 클래스에서**

**내부 클래스를 생성하고 내부 클래스의**

**멤버에 접근하는 예제입니다."**

![](https://blog.kakaocdn.net/dn/cHB7Ny/btqTp3wf0pd/MIUfeXfyRPKRHUsyqZk4e1/img.png)

예제 7_15

### **50. 내부 클래스의 제어자와 접근성 예제5**

**"내부 클래스와 외부 클래스에**

**선언된 변수의** **이름이 같을 때,**

**변수 앞에 'this' 또는** **'외부클래스명.this'를**

**붙여서 서로 구별할 수 있습니다."**

![](https://blog.kakaocdn.net/dn/ZcxIw/btqTlGn0Fli/K5CCOsBeSkdkrzj9JKZGYk/img.png)

예제 7_16

### [](https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#85-%EC%9D%B5%EB%AA%85-%ED%81%B4%EB%9E%98%EC%8A%A4-anonymous-class)8.5 익명 클래스 (anonymous class)

다른 내부 클래스들과는 달리 이름이 없다. 클래스의 선언과 객체의 생성을 동시에 하기 때문에 오직 하나의 객체만을 생성할 수 있는 일회용 클래스이다.

```java
new 조상클래스이름() {
	// 멤버 선언
}

new 구현인터페이스이름() {
	// 멤버 선언
}
```

이름이 없기 때문에 생성자도 가질 수 없다. 오로지 단 하나의 클래스를 상속 받거나, 단 하나의 인터페이스만을 구현할 수 있다.

![](https://blog.kakaocdn.net/dn/lA3op/btqThYXw8kJ/P3yGeQe0BJquL2dY6mpk9k/img.png)

예제 7_17

### **52. 익명 클래스(anonymous class) 예제**

**"두 개의 독립된 클래스를**

**익명클래스로 변환하여 보다 쉽게**

**코드를 작성할 수 있습니다."**

![](https://blog.kakaocdn.net/dn/N8Wpv/btqTkgb4B8t/cKIWnsDFxUVpP89wAuND91/img.png)

예제 7_18 변환 전

![](https://blog.kakaocdn.net/dn/qWXuM/btqTlF3KqWG/Ozwk3wuQqAAXsjGgyBXc31/img.png)

7_19 변환 후


## Reference
1. https://kevinntech.tistory.com/11?category=917070
2. https://im-yeobi.io/posts/java/book/standard-of-java/ch07-oop-2/#21-%EC%98%A4%EB%B2%84%EB%9D%BC%EC%9D%B4%EB%94%A9%EC%9D%B4%EB%9E%80
3. https://amacoding.tistory.com/10
4. https://amacoding.tistory.com/11