# 13장 Thread

Process 는 실행중인 프로그램을 말하는데 OS 프로세스는 프로그램을 수행하는 데 필요한 데이터와, 메모리 등의 자원 
그리고 쓰레드로 구성되어 있다. **프로세스의 자원으로 실제로 작업을수행하는 것이 쓰레드이다**.모든 프로세스에는 
최소한 하나 이상의 쓰레드가 존재하는데 둘 이상의 쓰레드를 가진 프로세스를 멀티 쓰레드 프로세스라고 한다.

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
`Thread` 클래스를 상속받거나 `Runnable` 인터페이스를 구현하는 방법 2가지가 있는데 `Runnable` 
인터페이스를 구현하는 방법이 더 재사용성이
좋은 객체지향적 방법이다. 인터페이스의 구현을 위해서는 추상메서드인 `run()` 메소드만 구현해주면 된다.

<br>

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

- `Thread` 를 상속받은 경우 `Thread` 를 상속받은 자손 클래스의 인터페이스를 생성해야하는 반면, `Runnable` 
  인터페이스를 구현한 경우 `Runnable` 
  인터페이스를 구현한 클래스의 인스턴스를 생성하고 `Thread` 클래스의 생성자의 매개변수로 제공해야한다.

  
- 쓰레드의 이름은 생성자나 `setName(String name)` 메서드를 통해서 지정할 수 있으며 지정하지 않았을경우 
  `Thread-번호` 의 형식으로 이름이 정해진다. 
 
 
- 생성한 쓰레드는 `start()` 메서드를 호출해야 실행가능하며 자신의 차례가 된 쓰레드부터 실행된다.


- 한번 실행된 쓰레드는 다시 실행될 수 없으며 다시 실행하려면 다시 호출해야한다.

<br>


## 3. start() 와 run()
위에 있는 코드를 보면 알수있듯이 쓰레드의 실행은 `run()` 메소드가 아닌  `start()` 메소드의 호출로 이루어진다. 
왜 각각의 구현한 클래스 내부에 있는 `run()` 메소드가 아닌  `start()` 일까? 

쓰레드는 6가지 상태 - `NEW`, `RUNNABLE`, `BLOCKED`, `WAITING`, `TIME_WAITING`, `TERMINATED` 가 있는데 
쓰레드의 실행시 `NEW` 상태가 아니면 `IllegalThreadStateException()` 예외를 호출하며 비정상적으로 종료된다. 
반면, `run()`은 `Runnable` 
인스턴스가 `null` 값이 
아니면된다.

여기서 알 수 있는것은 `run()`은 단순히 메서드를 호출하는 반면, `start()`는 쓰레드가 실행가능한지 체크를 한다는 것이다. 
만약 `start()` 메소드에
의해 실행가능하다고 판단이되면 

1. 새로운 호출 스택(call stack)을 생성하고
2. `run()` 매서드를 새로운 스택에서 호출하여 작업하고 
3. 스케줄러가 정한 순서에 따라 호출 스택이 번갈아 실행된다.

<br>


> - 메인 메서드의 작업을 하는 쓰레드를 메인 쓰레드라고 한다.
> - 사용중인 쓰레드가 하나도 없을떄 프로그램은 종료된다.
> 

<br>

## 4. 싱글쓰레드와 멀티쓰레드

싱글쓰레드와 멀티쓰레드로 두개의 작업을 수행한 시간을 비교해보면 멀티쓰레드의 속도가 약간 느린데, 그것은 쓰레드를 전환하는 
`context-switching` 때문에 그렇다. 만약 계산 같은 단순한 작업이면 싱글쓰레드 환경에서의 작업이 더 효율적이다.

<br>

> `context-switching` 시 이전작업의 진행상태, 다음 작업의 위치등의 정보를 저장하기 위한 시간이 소모된다.

<br>

만약, 두개의 쓰레드가 각각 싱글 코어, 멀티 코어로 환경에서 동시에 작업하는 경우,  
싱글 코어환경에는 한 쓰레드의 작업이 끝나야 다른 쓰레드가 해당 자원을 가지고 작업을 할 수 있으므로 작업이 겹치지 않지만,   
멀티코어인 경우 동시에 여러 쓰레드를 번갈아 작업하는데 충분한 자원이 있기 때문에 작업이 겹칠 수 있다.
그러므로 두 쓰레드가 서로 다른 자원을 사용하는 경우에는 싱글 쓰레드 프로세스보다 멀티 쓰레드 프로세스가 더 효율적이다.

<br>



## 5. 쓰레드의 우선순위
쓰레드 클래스 내부에 있는 `priority` 속성을 통해 1 ~ 10 까지 우선순위 지정할 수 있다.   
`setPriority(int newPriority)` 로 값을 변경하고 `getPriority()` 로 값을 반환한다.

> 높은 우선순위를 준 쓰레드에게 더 많은 실행시간과 실행기회가 주어지고 더 빠른 속도의 작업완료를 기대할 수 있지만 
> 무조건 높은 우선순의를 주면 더 많은 실행시간과 실행기회가 주어지는 것은 아니다.


<br>

## 6. 쓰레드 그룹

쓰레드 그룹은 서로 관련된 쓰레드를 그룹으로 다루기 위한 것이다. 여러 관련있는 쓰레드들은 폴더로 묶어서 관리할 수 있다.


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 생성자 / 메서드
- `ThreadGroup(String name)` :	지정된 이름의 새로운 쓰레드 그룹을 생성
- `ThreadGroup(ThreadGroup parent, String name)` : 지정된 쓰레드 그룹에 포함되는 새로운 쓰레드 그룹 생성
- `int activeCount()` : 쓰레드 그룹에 포함된 활성상태에 있는 쓰레드의 수를 반환
- `int activeGroupCount()` : 쓰레드 그룹에 포함된 활성상태에 있는 쓰레드 그룹의 수를 반환
- `void checkAccess()` : 현재 실행중인 쓰레드가 쓰레드 그룹을 변경할 권한이 있는지 체크
- `void destroy()` : 쓰레드 그룹과 하위 쓰레드 그룹까지 모두 삭제한다.
  

- `int enumerate(Thread[] list)`                       
  `int enumerate(Thread[] list, boolean recurse)`   
  `int enumerate(ThreadGroup[] list)`   
  `int enumerate(ThreadGroup[] list, boolean recurse)`   
   쓰레드 그룹에 속한 쓰레드 또는 하위 쓰레드 그룹의 목록을 지정된 배열에 담고 그 개수를 반환 두 번째 매개변수인 
  recurse의 값을 true로 하면 하위 쓰레드 그룹에 쓰레드 또는 쓰레드 그룹까지 배열에 담는다.
  

- `int getMaxPriority()` : 쓰레드 그룹의 최대우선순위를 반환
- `String getName()` : 쓰레드 그룹의 이름을 반환
- `ThreadGroup getParent()` : 쓰레드 그룹의 상위 쓰레드그룹을 반환
- `void interrupt()` : 쓰레드 그룹에 속한 모든 쓰레드를 interrupt
- `boolean isDaemon()` : 쓰레드 그룹이 데몬 쓰레드그룹인지 확인
- `boolean isDestroyed()` : 쓰레드 그룹이 삭제되었는지 확인
- `void list()` : 쓰레드 그룹에 속한 쓰레드와 하위 쓰레드그룹에 대한 정보를 출력
- `boolean parentOf(ThreadGroup g)` : 지정된 쓰레드 그룹의 상위 쓰레드그룹인지 확인
- `void setDemon(boolean daemon)` : 쓰레드 그룹을 데몬 쓰레드그룹으로 설정, 해제
- `void setMaxPriority(int pri)` : 쓰레드 그룹의 최대우선순위를 설정

<br>

쓰레드를 그룹에 포함시키려면 `Thread` 생성자를 사용해야 한다. 
<br>

```

            Thread(ThreadGroup group, String name);
            Thread(ThreadGroup group, Runnable target);
            Thread(ThreadGroup group, Runnable target, String name);
            Thread(ThreadGroup group, Runnable target, String name, long stackSize);
            
```

<br>


모든 쓰레드들은 반드시 쓰레드 그룹에 포함되어 있어야하므로 만약 생성자를 통해 그룹은 지정하지 않은 쓰레드는 기본적으로 자신을 
생성한 쓰레드와 같은 쓰레드 그룹에 속하게 된다.  
자신이 속한 쓰레드를 반환하려면 `ThreadGroup getThreadGroup()` 
를 사용한다. 쓰레드 그룹에 의해 쓰레드가 처리되지않은 예외에 의해 실행이 종료되었다면 자동으로 `uncaughtException` 이 
호출된다.


<br>

## 7. 데몬 쓰레드

<br>

## 8. 쓰레드의 실행제어


