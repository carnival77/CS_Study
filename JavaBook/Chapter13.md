# 13장 Thread

Process 는 실행중인 프로그램을 말하는데 OS 프로세스는 프로그램을 수행하는 데 필요한 데이터와, 메모리 등의 자원 그리고 쓰레드로 구성되어 
있다. **프로세스의 자원으로 실제로 작업을수행하는 것이 쓰레드이다**.  
모든 프로세스에는 최소한 하나 이상의 쓰레드가 존재하는데 둘 이상의 쓰레드를 가진 프로세스를 멀티 쓰레드 프로세스라고 한다.

<br>

## 1. 멀티태스킹 vs 멀티쓰레드 

### 공통점
- 여러개의 작업울 동시에 실행
- 동시에 모든 프로세스를 작업하는 것이 아니라 time-division 방식으로 쪼개서 번갈아 작업

### 차이점

#### 멀티태스킹 
- CPU의 코어당 하나의 작업만 할수있으므로 동시에 처리되는 프로세스의 수는 CPU 코어의 수와 같다.
- **멀티태스킹은 동시에 여러 프로그램을 실행시키는 것**
    
    <br>

#### 멀티쓰레드
- 프로세의 수보다 쓰레드의 수가 항상 많으므로 동시에 처리되는 쓰레드의 수가 더 많다. (일반적으로)
- **멀티쓰레드는 하나의 프로그램을 여러개의 기능으로 나누어 이를 동시에 실행시키킄 것**

    ##### 멀티쓰레드의 장점
    - CPU의 사용률을 향상 시킨다.
    - 자원을 보다 효율적으로 사용할 수 있다.
    - 사용자에 대한 응답성이 향상된다.
    - 작업이 분리되어  코드가 간결해진다. 

<br>

## 2. 쓰레드의 구현과 실행
`Thread` 클래스를 상속받거나 `Runnable` 인터페이스를 구현하는 방법 2가지가 있는데 `Runnable` 인터페이스를 구현하는 방법이 더 재사용성이
좋은 객체지향적 방법이다. 인터페이스의 구현을 위해서는 추상메서드인 `run()` 메소드만 구현해주면 된다.

```

public class ThreadEx1{
    
    //자손클래스에서 Thread 클래스의 매서드를 직접 호출할 수 있음
    static class ThreadEx_1 extends Thread {

        public void run() {
            for (int i = 0; i < 5; i++) {
                System.out.println("Thread : " + getName());

            }

        }
    }
        
    //Thread 클래스의 `static` 메서드인 currentThread() 을 호출하여 쓰레드에 대한 참조를 얻어와야만 호출이 가능
    static class ThreadEx_2 implements Runnable {

        @Override
        public void run() {
            for (int i = 0; i < 5; i++) {
                System.out.println("Runnable : " + Thread.currentThread());

            }
        }

    }

    public static void main(String[] args) {

        ThreadEx_1 t1 = new ThreadEx_1();

        Runnable r = new ThreadEx_2();
        Thread t2 = new Thread(r);

        t1.start();
        t2.start();

    }

}

```
<br>

출력

    Thread : Thread-0  
    Thread : Thread-0   
    Thread : Thread-0  
    Thread : Thread-0  
    Thread : Thread-0  
    Runnable : Thread[Thread-1,5,main]  
    Runnable : Thread[Thread-1,5,main]  
    Runnable : Thread[Thread-1,5,main]  
    Runnable : Thread[Thread-1,5,main]  
    Runnable : Thread[Thread-1,5,main]  


<br>

- `Thread` 를 상속받은 경우 `Thread` 를 상속받은 자손 클래스의 인터페이스를 생성해야하는 반면, `Runnable` 인터페이스를 구현한 경우 `Runnable` 
  인터페이스를 구현한 클래스의 인스턴스를 생성하고 `Thread` 클래스의 생성자의 매개변수로 제공해야한다.

  
- 쓰레드의 이름은 생성자나 `setName(String name)` 메서드를 통해서 지정할 수 있으며 지정하지 않았을경우 
  `Thread-번호` 의 형식으로 이름이 정해진다. 
 
 
- 생성한 쓰레드는 `start()` 메서드를 호출해야 실행가능하며 자신의 차례가 된 쓰레드부터 실행된다.


- 한번 실행된 쓰레드는 다시 실행될 수 없으며 다시 실행하려면 다시 호출해야한다.

<br>


## 3. start() 와 run()

<br>

## 4. 싱글쓰레드와 멀티쓰레드

<br>

## 5. 쓰레드의 우선순위 

<br>

## 6. 쓰레드 그룹

<br>

## 7. 데몬 쓰레드

<br>

## 8. 쓰레드의 실행제어


