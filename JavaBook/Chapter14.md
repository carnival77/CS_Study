# 14장 Lambda 와 Stream

## 람다식
람다식의 도입으로 객체지향언어인 자바를 함수형 언어도 될수있도록 해줬다. 메서드를 하나의 식으로 표현한 것이다.
메서드를 람다식으로 표현하면 메서드의 이름과 반환값이 얻어지므로 익명함수 라고도 한다.


- 람다식 자체만으로 메서드이 역할을 할 수 있음
- 메서드의 매개변수로 전달할 수 있음
- 메서드의 결과로 반환될 수 있음  

**람다식으로 인해 메서드를 변수 처럼 다루는 것이 가능**

<br>

### 람다식 작성하기 

<br>

#### 기본형
```
    (매개변수 선언) -> {
         ...
    }
```

- 예시

    ```
        (int a, int b) -> {
            return a > b ? a : b; 
        }
        
        →
        
        (int a, int b) -> {
            return a > b ? a : b;
        }
        
    ```

<br>

#### 특징

<br>

-  혹은 return 문 대신 expression 으로 사용할 수도 있다.
    ``` 
        (int a, int b) -> a > b ? a: b
    ```

<br>

- 매개변수의 타입은 추론이 가능할 경우 생략이 가능한데 둘 중 하나만 생략하는 것은 불가능하다.
    ```
        (a, b) -> a > b ? a : b
    ```
  
<br>

- 매개변수가 하나뿐이면 괄호() 생략 가능하다.
    ```
        a -> a*a     //OK
        int a -> a*a //에러
    ```

<br>

- 중괄호{} 안의 문장이 하나 일때는 중괄호{} 생략가능하지만 return문일경우 중괄호{} 생략 불가능하다.

    ```
        (String name, int i) -> System.out.println(name+"="+i)
    ```

<br>

### 함수형 인터페이스
람다식은 메서드와 동등한 것이 아니라 익명클래스의 객체와 동등하다. 참조변수의 타입은 클래스 또는 
인터페이스여야 하며 람다식과 동등한 메서드가 정의되어 있는 것이어야 한다.


기존의 인터페이스를 구현한 객체의 생성은 

```
    
      interface MyFunction  {
        public abstract int max(int a, int b);
      }
      
      
    // MyFunction 인터페이스를 구현한 익명클래스 객체 생성
      MyFunction f = new MyFunction() {
        public int max (int a, int b);
          return a > b ? a : b;
        }
      }
      
      //익명 객체의 메서드 호출
      int big = f.max(5, 3);  
  
```

<br>

이런 식으로 이루어지지만 람다식을 사용하면 좀더 간편하게 생성할 수 있다.

```

      MyFunction f = (int a, int b) -> a > b ? a : b;
      int big = f.max(5, 3); // 익명객체의 메서드를 호출
      
```

이것은 람다식도 실제로는 익명 객체이고, MyFunction 인터페이스를 구현한 익명 객체의 메서드 
max()와 람다식의 매개변수의 타입과 개수, 반환값이 일치하기 때문에 가능한 것이다. 



단, 함수형 인터페이스에는 람다식과 인터페이스가 1:1로 연결되기 때문에 **오직 하나의 추상 
메서드만 정의되어 있어야 한다.** 하지만 static 메서드와 default 메서드의 개수에는 제약이 없다. 
**`@FunctionalInterface` 를 붙이면 컴파일러가 함수형 인터페이스를 올바르게 정의하였는지 확인해준다.**  


<br>


함수형 인터페이스로 람다식을 참조할 수 있지만, 람다식의 타입이 함수형 인터페이스의 타입과 일치하는 것은 아니다.  람다식은 익명 객체이고 
익명 객체는 타입이 없다. 정확히는 타입이 있지만 컴파일러가 임의로 이름을 정하기 때문에 알 수 없다. 그러므로 아래와 같이 형변환이 필요하다.

```
    MyFunction f = (MyFunction) (()->{});
```

람다식은 MyFunction인터페이스를 직접 구현하지 않았지만, 이 인터페이스를 구현한 클래스의 객체와 완전히 동일하기 때문에 위와 같은 
형변환을 허용한다. 그리고 이 형변환은 생략 가능하다.

람다식은 이름이 없을 뿐 분명히 객체인데도, Object 타입으로 형변환 할 수 없다. 람다식은 오직 함수형 인터페이스로만 형변환이 가능하다. 
굳이 Object 타입으로 형변환하려면 아래와 같이 먼저 함수형 인터페이스로 변환해야 한다.


```
    Object obj = (Object)(MyFunction)(()->{});
    String str = (Object)(MyFunction)(()->{})).toString();
```

<br>

### java.util.function 패키지
자주 쓰이는 형식의 메서드를 함수형 인터페이스로 정의해놓은 패키지이다.

|함수형 인터페이스     |                  메서드|                                              설명|
|-----------------|----------------------|-------------------------------------------------|
java.lang.Runnable|void run()            |매개변수도 없고, 반환값도 없음
Supplier          |T get()	             |매개변수는 없고, 반환값만 있음
Consumer          |void accept(T t)      |Supplier와 반대로 매개변수만 있고, 반환값이 없음
Function          |R apply(T t)          |일반적인 함수. 하나의 매개변수를 받아서 결과를 반환
Predicate         |boolean test(T t)     |조건식을 표현하는데 사용. 매개변수는 하나, 반환 타입은 boolean
BiConsumer        |void accept(T t, U u) |두개의 매개변수만 있고, 반환값이 없음
BiPredicate       |boolean test(T t, U u)|조건식을 표현하는데 사용됨. 매개변수는 둘, 반환값은 boolean
BiFunction        |R apply(T t, U u)     |두개의 매개변수를 받아서 하나의 결과를 반환
UnaryOperator     |T apply(T t)          |Function 의 자손, Function 과 달리 매개변수와 결과의 타입이 같다. 
BinaryOperator    |T apply(T t, T t)     |BiFunction 의 자손, BiFunction 과 달리 매개변수와 결과의 타입이 같다.
<br>

- `Predicate` 는 리턴값이 `boolean` 이라는 점만 함수와 다르다. 
- 매개변수가 2개인 함수형 인터페이스는 이름 앞에 ‘Bi’가 붙는다.
- `Supplier` 는 매개변수는 없고 반환값만 존재하는데 메서드는 두 개의 값을 반환할 수 없으므로 `BiSupplier` 가 없다.
- 두개 이상의 매개변수를 갖는 함수형 인터페이스가 필요하다면 직접 만들어서 써야한다.
  ex) 
  ```
       @FunctionalInterface
       interface TriFunction<T, U, V, R>{
            R apply(T t, U u, V v);
       } 
  
  ```

<br>

### Function 의 합성과 Predicate 의 결합

#### Function 의 합성
두 람다식을 합성해서 새로운 람다식을 만들 수 있다. 함수 f, g가 있을 때 
- `f.andThen(g)` f를 먼저 적용하고 g 적용 
- `f.compose(g)` g를 먼저 적용하고 f 적용.

    ```
        //문자열을 숫자로 변환하는 함수 
        Function<String, Integer> f = (s) -> Integer.parseInt(s, 16);
        
        //숫자를 2진 문자열로 변환하는 함수
        Function<Integer, String> g = (i) -> Integer.toBinaryString(i);
        
        //두 함수를 합성
        Function<String, String> h = f.andThen(g);
        Function<Integer, Integer> h = f.compose(g);
    
    ```

<br>

#### Predicate 의 결합
여러 `Predicate` 를 `and()`, `or()`, `negate()` 으로 연결해서 하나의 새로운 `Predicate`를 만들 수 있다.  
두 대상을 비교할때는 static 메서드인 `isEqual()` 를 사용해서 비교할 수 있다. `isEqual()` 의 매개변수로 비교대상을 하나 
지정하고, 또 다른 비교대상은 `test()` 의 매개변수로 지정한다.


<br>

### 메서드 참조
람다식이 하나의 메서드만 호출하는 경우, 메서드 참조를 통해 더 간결하게 표현할 수 있다. 생략된 부분은 컴파일러가 우변 혹은 좌변에서 
알아낼 수 있다.

**기존 방법** : `Function<String, Integer> f = (String s) -> Integer.parseInt(s);`  
**메서드 참조** : `Funcation<String, Integer> f = Integer::parseInt;`

ex) 
```
    //기존
    BoFunction<String, String, Boolean> f = (s1, s2) -> s1.equals(s2);
    
    //메서드 참조
    BoFunction<String, String, Boolean> f = String::equals;
    
```
두개의 `String` 을 받아서 `Boolean` 을 반환하는 클래스는 다른 클래스에도 존재할 수 있으므로 클래스 이름은 반드시 필요하다.


메서드 참조를 할 수 있는 다른경우는 이미 생성된 객체의 메서드를 람다식에서 사용한 경우에는 클래스 이름 대신 그 객체의 참조변수를 적어서
사용할 수 있다.
```

  MyClass obj = new MyClass();
  Function<String, Boolean> f = (x) -> obj.equals(x); 
  Function<String, Boolean> f2 = obj::equals;
   
```

|종류 |람다 |메서드 참조 |
|---|---|---|
|static 메서드참조   |(x) -> ClassName.method(x)| ClassName::method|
|인스턴스 메서드참조    |(obj, x) -> obj.method(x)| ClassName::method|
|특정 객체 인스턴스 참조|(x) -> obj.method(x)| obj::method|

> 하나의 메서드만 호출하는 람다식은 `클래스이름::메서드이름` 또는 `참조변수::메서드이름`으로 바꿀 수 있다.


<br>


생성자를 호출하는 람다식도 메서드 참조로 변환 가능하다. 매개변수가 있는 생성자라면 매개변수의 개수에 따라 알맞은 
함수형 인터페이스를 사용해야한다.

```
  Supplier<MyClass> s = () -> new MyClass();  // 람다식
  Supplier<MyClass> s = MyClass::new; // 메서드 참조
```

<br>

배열을 생성할 때는 다음과 같이 작성한다.

```
  Function<Integer, int[]> f = x -> new int[x]; // 람다식
  Function<Integer, int[]> f2 = int[]::new; // 메서드 참조
```

<br>



```
  Function<Integer, int[]> f = x -> new int[x]; // 람다식
Function<Integer, int[]> f2 = int[]::new; // 메서드 참조
```

<br>

## 스트림


<br><br>
