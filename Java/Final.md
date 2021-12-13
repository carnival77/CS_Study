# Final

### 정의

> 여러 컨텍스트에서 단 한 번만 할당될 수 있는 entity를 정의할 때 사용  
> = 한번 초기화 한다음 변경할 수 없음

### 특징

- 총 3곳에서 사용가능
    - final class
        - 상속자체가 불가능
        - 여러 상수값을 모아놓은 클래스에 사용 (상속할 이유가 없으므로)   
        - Util 형식의 클래스에서 사용 (어플리케이션 전역에서 사용하므로)
        
    <br>
  
    - final method
        - 상속받은 클래스에서 오버라이드( 재정의 ) 불가능 
        - 구현한 코드의 변경을 원치 않을떄 사용
      
    <br>

    - final variable
        - 원시타입
            - 한번 초기화된 변수는 변경할 수 없는 상수값이 됨
                ```
                final int i = 1;
                
                //x = 3; 값을 초기화한다음 새로운 값을 할당할 수 없음
                ```

        - 객체 타입
            - `final` 로 선언한 객체에 새로운 참조값을 지정할수는 없지만 **객체의 속성은 변경가능**
                ```
                final Pet pet = new Pet();
                 //pet = new Pet(); 다른 객체로 변경할수 없음
                pet.setWeight(3); //객체 필드는 변경할 수 있음
                ```

            <br>

        - 메서드 인자
            - 메서드 안에서 변수값을 변경할 수 없음
                ```
                public class Pet {
              
                    int weight;
              
                    public void setWeight(final int weight) {
                        //weight = 1; final 인자는 메서드안에서 변경할 수 없음
                    }
                }
                ```

        <br>

        - 클래스 필드(멤버변수, 전역변수)
            - final 키워드를 클래스 필드에 붙이면 생성자 호출시 한번만 초기화 할수 있다는 것을 의미
            ```
            public class Zoo {

                protected final int animal;
          
                //static 과 함께 쓰일경우
                //protected static final int animal = 0;
            
                public Zoo(int animal) {
                    this.animal = animal;
                }
            
                public static void main(String[] args) {
                    Zoo zoo = new Zoo(100);
                    //생성자 호출시 초기화 되었으므로 새로운 값을 할당할 수 없음
                    //zoo.animal = 200; 
                }
            
            }
            ```
            - `static` 키워드와 같이 선언했다면 값과 함께 선언했을떄 초기화 - **정적 초기화 블록에서**
            - 그렇지 않다면 생성자 메서드 안에서 초기화 - **인스턴스 초기화 블록에서**

            <br>

            #### 정적 초기화 블록 vs 인스턴스 초기화 블록

            #### 코드
            ```
             public class Zoo {

                final int animal;
                
                {
                    System.out.println("인스턴스 초기화 블록");
                    animal = 100;
                    System.out.println("animal : " + animal);
                }
                
                static {
                    System.out.println("정적 초기화 블록");
                }
                
                public Zoo() {
                    System.out.println("생성자 호출");
                }
                
                public static void main(String[] args) {
                    Zoo zoo = new Zoo();
                    Zoo zoo1 = new Zoo();
                }   
             }
            ```
            
            <br>
                
            #### 결과
            
            ```
            정적 초기화 블록
            인스턴스 초기화 블록
            animal : 100
            생성자 호출
                    
            인스턴스 초기화 블록
            animal : 100
            생성자 호출
          
            ```
          
            인스턴스 초기화 블록은 **객체를 생성할 때마다**, **부모 생성자 이후에 실행**, **생성자보다 먼저 실행됨** 일때 실행되며,  
            
            정적 초기화 블록은 **클래스 로드시 한번만** 블록이 실행된다.

<br>

- 혼동할 수 있는 키워드
    - `finally` : `try-catch`에서 예외처리의 발생 유무와 관계없이 무조건 실행해야하는 부분을 작성할떄 사용
    - `finalize` : 객체가 소멸될때 호출되는 **메소드**. 거의 사용하지 않음.
    

<br>

참고 자료
- https://blog.advenoh.pe.kr/java/자바에서-final에-대한-이해/


<br><br>