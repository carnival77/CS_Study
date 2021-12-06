# JVM - Java Virtual Machine

자바 코드를 ( **고수준** )  컴퓨터가 이해하고 실행할 수 있는 바이트코드로( **저수준** ) 변환( **컴파일** )하는 프로그램

<br><br>

## 특징

 - JVM의 역할을 애플리케이션을 클래스 로더를 통해 읽어 들여 자바 API와 함께 실행    
   <br>
    **API?**

    > API (Application Programming Interface) 는 응용 프로그램을 운영체제나 프로그램에서 사용할 수 있도록 프로그램과 운영체제 혹은 프로그램을 연결시켜주는 인터페이스를 뜻한다.
 
- 자바 API는 컴퓨터에서 자바를 사용할 수 있도록 도와주는 프로그램이다.

    즉, JVM 은 자바와 OS 사이의 **중개자 역할**을 한다. 또한 메모리관리, Garbage Collector 역할을 한다.  

  
- JVM 이 있기 때문에 운영체제가 달라도 운영체제별로 다르게 구현된 JVM을 통해서 자바를 사용할 수 있다.  
  → 운영체제에 종속되지 않는다.

<br><br>

## 자바 프로그램 실행순서

<br>

<div align="center">
  <img src="https://user-images.githubusercontent.com/65614734/144752745-4cbe928c-e254-4d20-b3f5-794f288f8310.png" width="70%">
</div>

<br>

1. 프로그램이 실행되면 JVM은 OS로부터 이 프로그램이 필요로하는 메모리를 할당받는다.  
    JVM은 이 메모리를 용도에 따라 여러 영역으로 나누어 관리한다.
   
   
2. 자바 컴파일러가(`javac`)가 자바 소스코드 (`.java`) 를 읽어들여 자바 바이트코드( `.class`) 로 변환시킨다.  
   <br>

3. `Class Loader` 를 통해 class 파일들을 JVM으로 로딩한다.  
   <br>

4. 로딩된 class 파일들은  `Execution engine`을 통해 해석된다.  
   <br>

5. 해석된 바이트코드는 `Runtime Data Area` 에 배치되어 실질적인 수행이 이루어지게된다.  
   <br>

<br>

## JVM 구성요소

<br>

### Class Loader

- JVM 내로 클래스 (`.class`) 파일을 로드하고 링크를 통해 배치하는 작업을 수행  
  → 로딩된 클래스들을 `Runtime Data Area` 에 배치됨
  

- 자바는 동적 로드, 즉 컴파일타임이 아니라 런타임에 클래스를 처음으로 참조할 때 해당 클래스를 로드하는데 이때 `Class Loader` 가 동적로드를 담당  
  → 클래스를 처음으로 참조할 때 해당 클래스를 로드하고 링크  
  

- jar 파일 내 저장된 클래스들을 JVM 위에 탑재하고 사용하지 않는 클래스들을 메모리에서 삭제 (컴파일러 역할)
    
    **Jar?**
    > Java Archive. 여러개의 **자바 클래스 파일**과, 클래스들이 이용하는 관련 리소스(텍스트, 그림 등) 및 메타데이터를 하나의 파일로 모아서 자바 플랫폼에 응용 소프트웨어나 라이브러리를 배포하기 위한 소프트웨어 패키지

<br>    

### Execution Engine (실행 엔진)

- 클래스를 실행시키는 역할  

  
- Class Loader가 JVM내의 런타임 데이터 영역에 바이트 코드를 배치시키고 이것을 실행엔진에 의해 실행  

  
- 자바 바이트 코드를 명령어 단위로 읽어서 실행  

  
- 고수준의 언어를 저수준의 언어로 바꾸는 작업을 해주는 곳 - 두가지 방법으로 변환    
    <br>
    
    #### Interpreter
    - 바이트 코드 명령어를 하나씩 읽어서 해석하고 실행
    - 하나씩 읽어서 해석하고 실행하기 때문에 **해석은 빠르지만** **인터프리팅 결과는 느림**  
    <br>
      
    #### JIT(Just - In - Time)
  
    - 인터프리터의 단점을 보완하기 위해 도입된 것  
    
    - 인터프리터 방식으로 실행하다가 적절한 시점에 바이트코드 전체를 컴파일하여 네이티브 코드로 변경하고, 이후에는 해당 메서드를 더 이상 인터프리팅하지 않고 네이티브 코드로 직접 실행하는 방식

    - 네이티브 코드는 캐시에 보관하기 때문에 한번 컴파일된 코드를 빠르게 수행되기 때문에 한번 컴파일된 코드는 계속 빠르게 수행  
    → JIT 컴파일러를 사용하는 JVM들은 해당 메서드들의 수행빈도를 체크하고 일정수준을 넘을때만 컴파일을 수행
      
    <br>
  
    **Native Code?**
    > 바이트 코드와 반대되는 개념으로 CPU와 OS가 직접 실행할 수 있는 코드. C, C++ 들이 해당됨
    
    


<br>


### Garbage Collector 
[가비지 콜렉터](https://github.com/ffolabear/CS_Study/blob/main/Java/GarbageCollector.md)

<br>

### Runtime Data Area
프로그램을 수행하기 위해 OS에서 할당받은 메모리 공간

<br>

<div align="center">
  <img src="https://user-images.githubusercontent.com/65614734/144752740-464bbfdf-93f1-4bec-8706-ca9c244b7436.png" width="60%">
</div>

<br>


#### PC Register

- Thread 가 시작될때 생성되며 Thread가 생성될 때마다 생성되는 공간으로 Thread 마다 하나씩 존재
  

- Thread 가 어떤 부분을 어떤 명령으로 실행해야할지에 대한 기록을 하는 부분으로 현재 수행중이 JVM 명령의 주소를 갖는다.



<br>

#### JVM 스택 영역

- Thread의 수행 정보를 `stack-frame` 을 통해서 저장
  

- Java Virtual Machine Stacks는 Thread가 시작될 때 생성되며, 각 Thread 별로 생성되기 때문에 다른 Thread는 접근할 수 없음
  

- 메소드가 호출되면 스택에 쌓이고 호출이 종료될때 스택에 제거
  

- 프로그램 실행과정중 임시로 할당되었다가 메소드를 빠져나가면 바로 소멸되는 특성의 데이터를 저장하기 위한 영역



<br>

#### Native Method Stack

- 자바프로그램이 컴파일되어 생성된 바이트코드가 아닌 실제 실행할수 있는 기계어로 작성된 프로그램을 실행시키는 영역.  
  → 자바 언어가 아닌 다른 언어로 작성된 코드를 위한 영역
  

- Native Method는 별도의 스택에서 새로운 스택 프레임에 저장하는데, 이것은 JNI를 사용하여 JVM 내부에 영향을 주지 않기 위함이다. 

<br>

#### Method Area (= Class Area = Static Area)

- 모든 스레드가 공유하는 메모리 영역
  

- 클래스 정보를 처음 메모리 공간에 올릴때 초기화되는 대상을 저장하기 위한 메모리 공간
  

- 클래스, 인터페이스, 메소드, 필드, Static 변수 등 바이트 코드 등을 보관
  

- **Runtime Constant Pool** 을 통해서 상수자료형을 저장하여 참조하고 중복을 막는다.



<br>

#### Heap 

<div align="center">
  <img src="https://user-images.githubusercontent.com/65614734/144752744-d2f3bb1f-6c74-4f09-893b-6727314580d7.png" width="70%">
</div>

- 프로그램 상에서 런타임시 동적으로 할당하여 사용하는 영역  
  

- 객체를 저장하는 가상 메모리 공간이며 `new` 연산자로 생성된 객체와 배열을 저장
  

- New/Young Generation 에는 최초로 생성된 객체를 저장
  

- Tenured generation 에는 `Eden` 에서 넘어온 오래된 객체들이 저장
  

- Permanent Generation 에는 생성된 객체들의 정보의 주소값이 저장
    - Class loader 에 의해 load 되는 Class, Method 등에 대한 Meta 정보가 저장
    - Reflection을 사용하여 동적으로 클래스가 로딩되는 경우에 사용
      → Spring 사용시 이 영역에 대한 고려가 필요


<br><br>

이미지출처
- https://asfirstalways.tistory.com/158

참고 자료
- https://asfirstalways.tistory.com/158
- https://velog.io/@jsj3282/JVM%EA%B3%BC-%EC%9E%90%EB%B0%94-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EA%B5%AC%EC%A1%B0Runtime-Data-Area
- https://d2.naver.com/helloworld/1230


<br><br>