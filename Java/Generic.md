<h3> 제네릭이란? </h3>

- 제네릭(Generic)은 클래스 내부에서 사용할 데이터 타입을 **외부에서 지정**하는 기법을 의미한다. – 생활코딩

- 지네릭스는 다양한 타입의 객체들을 다루는 메서드나 컬렉션 클래스에 **컴파일 시의 타입체크**를 해주는 기능이다. – 자바의 정석

<h3> 장점 </h3>

- 형변환이 필요없다. (객체의 타입을 컴파일 시에 체크하기 때문에)

- 타입안정성이 보장된다. (객체의 타입을 컴파일 시에 체크하기 때문에)

- 코드가 간결해진다.

- 코드의 재사용성이 높아진다.

<h3> 예시 </h3>

- 제네릭을 사용한 ArrayList

```java
ArrayList<String> listStr = new ArrayList<>();
ArrayList<Integer> listInt = new ArrayList<>();
listStr.add("string");
String str1 = list.get(0); // 타입변환이 필요없음.
```

- 제네릭을 사용하지 않은 ArrayList

```java
ArrayList list = new ArrayList();
list.add("string");
String str2 = (String) list.get(0); // 타입변환이 필요함.
```

- 직접 생성

```java
class MyClass <T> { ... }
interface MyInterface <T> { ... }
```

- 일반적으로 사용되는 타입 인자 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1dee6e6b-0b56-4d39-af63-8e97715f8714/Untitled.png)

<h3> 사용할 수 없는 경우 </h3>

- 제네릭으로 배열을 생성할 수 없다.

- static 변수를 제네릭으로 사용할 수 없다.
