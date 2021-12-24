# Chapter 8. 예외처리 

### 1.1 - 1.2 프로그램 오류
프로그램 실행중 어떤 원인에 의해서 오작동을 하거나 비정상적으로 종료되는 경우를 일컫는 말   
발생시점에 따라 3가지로 나눌 수 있음


- **컴파일 에러(Compile error)** : 컴파일 할 때 발생하는 에러


- **런타임 에러(Runtime error)** : 프로그램 실행도중 발생하는 에러
  

- **논리적 에러(Logical error)** : 컴파일, 실행 모두 이상없지만 의도된 것과 다르게 동작하는 것
  
컴파일시 컴파일러가 소스코드( * . java) 파일에 대한 기본검사를 하고 오류가 없다면 클래스 파일( * . class) 이 생성됨  
컴파일시에는 아무런 문제가 없었지만 실행중에 발생하는 에러는 컴파일러가 찾을 수 없기 때문에 추가적인 처리가 필요하다.

런타임시 발생하는 오류는 크게 
- **에러(Error)** : 프로그램 코드에 의해서 수습될 수 없는 **심각한 오류**
- **예외(Exception)** : 프로그램 코드에 의해서 수습될 수 있는 **다소 미약한 오류**

<br>

#### 예외 클래스 계층도

<div align="center">
  <img src="https://user-images.githubusercontent.com/65614734/147367596-87390261-cea1-4691-a1bd-6997802f168e.png">
</div>

책에서 명시한대로   
`RuntimeException` 클래스와 그 자손 클래스들을 `RuntimeException 클래스들` 로,
`RuntimeException` 클래스를 제외한 나머지 클래스들을 `Exception 클래스들` 로 명시하겠다.

<br>

`RuntimeException 클래스들` 은 주로 **프로그래머의 실수에 의해 발생될 수 있는 예외**
- 배열 범위를 벗어나는 경우 - `ArrayIndexOutOfBoundsException`
- `null` 을 참조하는 경우 - `NullPointerException`
- 정수를 0으로 나누는 경우 - `ArithmeticException`

`Exception 클래스들` 은 주로 **외부의 영향으로 발생하는 오류**
- 존재하지 않는 파일의 이름을 입력한 경우 - `FileNotFoundException`
- 클래스 이름을 잘못 적은 경우 - `ClassNotFoundException`
- 입력한 데이터의 형식이 잘못된 경우 - `DateFormatException`


### 예외 처리하기 `try-catch` 문

#### 예외 처리 
정의 :  프로그램 실행시 발생할 수 있는 예기치 못한 예외의 발생에 대비한 코드를 작성하는 것  
목적 :  프로그램의 비정상적 종료를 막고, 정상적인 실행상태를 유지할 수 있도록 하는 것

> 예외와 어레 모두 실행(Runtime) 시 발생하는 오류이다.
> 예외를 처리하지 못할시 JVM의 예외처리기(UncaughtExceptionHandler) 가 예외의 원인을 화면에 출력한다.

#### 코드

```

    try { 
        //예외발생할 가능성이 있는 문장 
        
    }catch(Exception1 e1) { 
        //Exception1이 발생했을 경우, 이를 처리하지 위한 문장을 적는다. 
        
    }catch(Exception2 e2) { 
        //Exception2이 발생했을 경우, 이를 처리하지 위한 문장을 적는다.
         
    }catch(ExceptionN eN) { 
        //ExceptionN이 발생했을 경우, 이를 처리하지 위한 문장을 적는다.
         
    }finally{ 
        //예외발생여부에 관계없이 수행되어야 하는 구문.
         
    }

```

예외가 발생하면 발생한 부분의 `Exception` 클래스가 출력되므로 원인와 위치를 할 수 있다.

<br><br>

