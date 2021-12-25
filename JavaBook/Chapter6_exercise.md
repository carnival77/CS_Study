### **연습문제**

**6-1. 다음과 같은 멤버변수를 갖는** **Student클래스를 정의하시오.**

![](https://blog.kakaocdn.net/dn/dtryKm/btqS3JFgVR0/MOFqQkAitSC2v3LumdKfFk/img.png)

연습문제 6_1 문제

![](https://blog.kakaocdn.net/dn/dTWZZ7/btqS90GbHUn/NS88QpNKWwkaOIVg3g2A70/img.png)

연습문제 6_1 정답

**6-2. 다음과 같은 실행결과를 얻도록** **Student클래스에 생성자와 info()를** **작성하시오.**

![](https://blog.kakaocdn.net/dn/zDqIx/btqS3aQEjkt/j2IJgLAYKlVaYUYAPxb630/img.png)

연습문제 6_2 정답

**6-3. 연습문제 6-1에서 정의한 Student클래스에**

**다음과 같이 정의된 두 개의 메서드 getTotal( )과** **getAverage( )를 작성하시오.**

**(1) getTotal( )**

**- 메서드 명 : getTotal**

**- 기능 : 국어(kor), 영어(eng), 수학(math)의**

**점수를 모두 더해서 반환**

**③ 반환타입 : int**

**④ 매개변수 : 없음**

**(2) getAverage( )**

**- 메서드 명 : getAverage**

**- 기능 : 국어(kor), 영어(eng), 수학(math)의**

**총점을 과목수로 나눈 평균을 구함.**

**(소수점 둘째 자리에서 반올림)**

**- 반환타입 : float**

**- 매개변수 : 없음**

![](https://blog.kakaocdn.net/dn/bTbCVR/btqS4MuXS5h/6wr4vvh67YcHtMNuL47f60/img.png)

연습문제 6_3 정답

**6-4. 두 점의 거리를 계산하는** **getDistance( )를 작성하시오.**

**※ 두 점 (x, y)와 (x1, y1) 사이의** **거리를 구하는 공식**

![](https://blog.kakaocdn.net/dn/bRyDhY/btqSX7f3BgW/kfQ04fg17DaZUDahI8MH80/img.png)

**※ 제곱근 계산 메서드**

#### **Math.sqrt(double a)**

![](https://blog.kakaocdn.net/dn/cOJMLG/btqS29K1zv4/w1JFnSopHkyeQ9kn5GKYe1/img.png)

연습문제 6_4 정답

**6-5. 다음의 코드에 정의된 변수들을** **종류별로 구분해서 적으시오.**

![](https://blog.kakaocdn.net/dn/cpsafU/btqS6YIFiVs/pXv9wetwqRusJVx4TTM0wk/img.png)

연습문제 6_5 문제

**정답**

**- 클래스 변수(static 변수)**

static int width;

static int height;

**- 인스턴스 변수**

int kind;

int num;

**- 지역변수**

int k

int n

PlayintCard card

**6-6. 연습문제 6-4에서 작성한 클래스메서드** **getDistance( )를 MyPoint클래스의** **인스턴스메서드로 작성하시오.**

![](https://blog.kakaocdn.net/dn/vGvVl/btqS1VlUhE4/T1myo23W7JwBYmVRT9udIk/img.png)

연습문제 6_6 정답

**6-7. 다음은 컴퓨터 게임의 병사(marine)를** **클래스로 정의한 것이다.**

**이 클래스의 멤버중에** **static을 붙여야 하는 것은 어떤 것들이고** **그 이유는 무엇인가?**

**(단, 모든 병사의 공격력과 방어력은 동일)**

![](https://blog.kakaocdn.net/dn/3u12P/btqTcQXCkJA/UL7h2pLYAsOm5Ip1KHvz10/img.png)

연습문제 6_7 문제

**정답**

멤버변수 weapon, armor

매서드 weaponUp( ), armor( )

모든 Marine의 인스턴스가 동일한 값을

가져야 하기 때문입니다.

**6-8. 다음 중 생성자에 대한 설명으로 옳지 않은 것은? (모두 고르시오)**

**① 모든 생성자의 이름은 클래스의** **이름과 동일해야한다.**

**② 생성자는 객체를 생성하기 위한 것이다.**

**③ 클래스에는 생성자가 반드시** **하나 이상 있어야 한다.**

**④ 생성자가 없는 클래스는 컴파일러가** **기본 생성자를 추가한다.**

**⑤ 생성자는 오버로딩 할 수 없다.**

**정답 :** ②, ⑤

**해설**

② 생성자는 객체를 초기화하기 위한 것이며,

객체를 생성하는 연산자는 new입니다.

⑤ 생성자도 오버로딩이 가능합니다.

매개변수가 있는 생성자를

여러 개 정의할 수 있습니다.

**6-9. 다음 중 this에 대한 설명으로 맞지 않는 것은? (모두 고르시오)**

**① 객체 자신을 가리키는 참조변수이다.**

**② 클래스 내에서라면 어디서든** **사용할 수 있다.**

**③ 지역변수와 인스턴스 변수를** **구별할 때 사용한다.**

**④ 클래스 메서드 내에서는 사용할 수 없다.**

**정답 :** ②

**해설**

② this는 인스턴스 자신의 주소를 저장하고

있으며, 모든 인스턴스 메서드에 숨겨진 채로

존재하는 지역변수입니다.

그러므로 인스턴스 메서드 내에서만

사용가능 합니다.

**6-10. 다음 중 오버로딩이 성립하기 위한 조건이 아닌 것은? (모두 고르시오)**

**① 메서드의 이름이 같아야 한다.**

**② 매개변수의 개수나 타입이 달라야 한다.**

**③ 리턴타입이 달라야 한다.**

**④ 매개변수의 이름이 달라야 한다.**

**정답 :** ③, ④

**해설**

오버로딩의 조건

① 매서드의 이름이 같아야 한다.

② 매개변수의 개수 또는 타입이 달라야 한다.

③ 리턴타입은 오버로딩에 아무런

영향을 주지 않는다.

**6-11. 다음 중 아래의 add메서드를** **올바르게 오버로딩 한 것은?  (모두 고르시오)**

**long add(int a, int b) { return a+b; }**

**① long add(int x, int y) { return x+y;}**

**② long add(long a, long b) { return a+b;}**

**③ int add(byte a, byte b) { return a+b;}**

**④ int add(long a, int b) { return (int)(a+b);}**

**정답 :** ②, ③, ④

**해설**

오버로딩의 조건

① 매서드의 이름이 같아야 한다.

② 매개변수의 개수 또는 타입이 달라야 한다.

③ 리턴타입은 오버로딩에 아무런

영향을 주지 않는다.

**6-12. 다음 중 초기화에 대한 설명으로 옳지 않은 것은? (모두 고르시오)**

**① 멤버변수는 자동 초기화되므로 초기화하지** **않고도 값을 참조할 수 있다.**

**② 지역변수는 사용하기 전에 반드시** **초기화해야 한다.**

**③ 초기화 블럭보다 생성자가 먼저 수행된다.**

**④ 명시적 초기화를 제일 우선적으로** **고려해야 한다.**

**⑤ 클래스 변수보다 인스턴스 변수가** **먼저 초기화된다.**

**정답 :** ③, ⑤

**해설**

멤버변수의 초기화 순서

① 클래스 변수(cv) 초기화

→ 인스턴스 변수(iv) 초기화

② 자동 초기화 → 명시적 초기화(간단)

→ 초기화 블럭, 생성자(복잡)

**6-13. 다음 중 인스턴스 변수의 초기화** **순서가 올바른 것은?**

**① 기본값→명시적초기화→초기화블럭→생성자**

**② 기본값→명시적초기화→생성자→초기화블럭**

**③ 기본값→초기화블럭→명시적초기화→생성자**

**④ 기본값→초기화블럭→생성자→명시적초기화**

**정답 :** ①

**해설**

인스턴스 변수의 초기화 순서

자동 초기화 → 명시적 초기화(간단)

→ 초기화 블럭, 생성자(복잡)

**6-14. 다음 중 지역변수에 대한 설명으로** **옳지 않은 것은?** **(모두 고르시오)**

**① 자동 초기화되므로 별도의 초기화가 필요없다.**

**② 지역변수가 선언된 메서드가 종료되면 지역변수도 함께 소멸된다.**

**③ 메서드의 매개변수로 선언된 변수도 지역변수이다.**

**④ 클래스 변수나 인스턴스 변수보다 메모리 부담이 적다.**

**⑤ 힙(heap)영역에 생성되며 가비지 컬렉터에 의해 소멸된다.**

**정답 :** ①, ⑤

**해설**

① 지역변수는 자동으로 초기화 되지

않으므로, 사용하기 전에 반드시

적절한 값으로 초기화를 해야 합니다.

⑤ 지역변수는 호출스택(call stack)에

생성됩니다.

**6-15. 호출스택이 다음과 같은 상황일 때** **옳지 않은 설명은?** **(모두 고르시오)**

![](https://blog.kakaocdn.net/dn/bfQsXx/btqS4NglDJD/pEvgArwN9gF8T2wtNBhKJ0/img.png)

연습문제 6_15 문제

**① 제일 먼저 호출스택에 저장된 것은** **main메서드 이다.**

**② println메서드를 제외한 나머지** **메서드들은 모두 종료된 상태이다.**

**③ method2메서드를 호출한 것은** **main메서드이다.**

**④ println메서드가 종료되면** **method1메서드가 수행을 재개한다.**

**⑤ main-method2-method1-println의** **순서로 호출되었다.**

**⑥ 현재 실행중인 메서드는 println뿐이다.**

**정답 :** ②

**해설**

② 호출스택의 제일 위에 있는 메서드가 현재

수행중인 메서드이며, 호출스택 안의 나머지

메서드들은 대기상태입니다.

**6-16. 다음 코드의 실행 결과를 예측하여 적으시오.**

![](https://blog.kakaocdn.net/dn/bAB5pv/btqS6XJMeb7/Cf2aBHQLk5mOGtNvKGlbQ1/img.png)

연습문제 6_12 문제

**정답**

ABC123

After change : ABC123

**해설**

![](https://blog.kakaocdn.net/dn/76pOu/btqS3a4azkG/7GUfdKjWPFV51QYi73pKK1/img.png)

change 메서드 수행 중

① change 메서드의 지역변수인 str에

주소값 0x100이 저장되며,

문자열 "ABC123"을 참조하게 되지만,

서로 다른 영역에 존재하므로

이름은 같지만 분명히 다른 변수입니다.

② change 메서드의 문자열 덧셈연산인

'str += "456"'을 통해 새로운 문자열인

"ABC123456"이 생성되고,

새로운 문자열의 주소가 변수 str에

저장됩니다.

※ String객체(문자열)은 읽을 수만 있을 뿐

내용을 변경할 수 없습니다.

**6-17. 다음과 같이 정의된 메서드를 작성하고** **테스트하시오.**

**- 메서드명 : shuffle**

**- 기능**

**① 주어진 배열에 담긴 값의 위치를 바꾸는**

**작업을 반복하여 뒤섞이게 한다.**

**② 처리한 배열을 반환한다.**

**- 반환타입 : int[ ]**

**- 매개변수 : int[ ] arr**

**(정수값이 담긴 배열)**

![](https://blog.kakaocdn.net/dn/cfc3hd/btqSX8F4K4W/4kTAKXuWZM5GOmkHcLEKF0/img.png)

연습문제 6_17 정답(1)

![](https://blog.kakaocdn.net/dn/OiiTY/btqS3ab1TaK/XVCr6g4olZxEnWfA1gfUaK/img.png)

연습문제 6_17 정답(2)

**6-18. 다음과 같이 정의된 메서드를 작성하고** **테스트하시오.**

**- 메서드명 : isNumber**

**- 기능**

**① 주어진 문자열이 모두 숫자로만**

**이루어져있는지 확인한다.**

**② 모두 숫자로만 이루어져 있으면 true를**

**반환하고, 그렇지 않으면 false를 반환한다.**

**③ 만일 주어진 문자열이 null이거나**

**빈 문자열 ""이라면 false를 반환한다.**

**- 반환타입 : boolean**

**- 매개변수 : String str**

**(검사할 문자열)**

![](https://blog.kakaocdn.net/dn/bev01D/btqS3a4aHg7/8arCFgrKnKYmUKQp88bkbk/img.png)

연습문제 6_18 정답

**6-19. Tv클래스를 주어진 로직대로 완성하시오.**

**완성한 후에 실행해서 주어진 실행결과와** **일치하는지 확인하라.**

![](https://blog.kakaocdn.net/dn/IgfqP/btqS9ZAxv3b/5RDoy2jWeP8KIUFTyhGKhK/img.png)

연습문제 6_19 Tv클래스

![](https://blog.kakaocdn.net/dn/bOUIQv/btqSZwNtCn7/ZhRFNpnCiqr0zl9Cz0UXA0/img.png)

연습문제 6_19 결과

**6-20. 다음과 같이 정의된 메서드를 작성하고** **테스트하시오.**

**- 메서드명 : max**

**- 기능**

**① 주어진 int형 배열의 값 중에서**

**제일 큰 값을 반환한다.**

**② 만일 주어진 배열이 null이거나**

**크기가 0인 경우,**

**-999999를 반환한다.**

**- 반환타입 : int**

**- 매개변수 : int[ ] arr**

**(최댓값을 구할 배열)**

![](https://blog.kakaocdn.net/dn/cWVmv4/btqS1UN6ImI/WAiytxwAK23NEdH9kSRkMK/img.png)

연습문제 6_20 정답

**6-21. 다음과 같이 정의된 메서드를 작성하고** **테스트하시오.**

**- 메서드명 : abs**

**- 기능 : 주어진 값의 절대값을 반환한다.**

**- 반환타입 : int**

**- 매개변수 : int value**

![](https://blog.kakaocdn.net/dn/RT74o/btqTcRa9Edq/uYhFKCCoSIMPJ82cecP0v1/img.png)

연습문제 6_21\
