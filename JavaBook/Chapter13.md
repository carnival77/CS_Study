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
좋은 객체지향적 방법이다. 인터페이스의 구현을 위해서는 추상메서드인 `run()` 메서드만 구현해주면 된다.

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
위에 있는 코드를 보면 알수있듯이 쓰레드의 실행은 `run()` 메서드가 아닌  `start()` 메서드의 호출로 이루어진다. 
왜 각각의 구현한 클래스 내부에 있는 `run()` 메서드가 아닌  `start()` 일까? 

쓰레드는 6가지 상태 - `NEW`, `RUNNABLE`, `BLOCKED`, `WAITING`, `TIME_WAITING`, `TERMINATED` 가 있는데 
쓰레드의 실행시 `NEW` 상태가 아니면 `IllegalThreadStateException()` 예외를 호출하며 비정상적으로 종료된다. 
반면, `run()`은 `Runnable` 
인스턴스가 `null` 값이 
아니면된다.

여기서 알 수 있는것은 `run()`은 단순히 메서드를 호출하는 반면, `start()`는 쓰레드가 실행가능한지 체크를 한다는 것이다. 
만약 `start()` 메서드에
의해 실행가능하다고 판단이되면 

1. 새로운 호출 스택(call stack)을 생성하고
2. `run()` 매서드를 새로운 스택에서 호출하여 작업하고 
3. 스케줄러가 정한 순서에 따라 호출 스택이 번갈아 실행된다.

<br>


> - 메인 메서드의 작업을 하는 쓰레드를 메인 쓰레드라고 한다.
> - 사용중인 쓰레드가 하나도 없을때** 프로그램은 종료된다.
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


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **생성자** / **메서드**
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

일반 쓰레드와 다르게 다른 일반 쓰레드의 작업을 돕는 보조적인 역할을 수행하는 쓰레드이다. 일반 쓰레드의 보조역할을 하기 때문에
일반 쓰레드가 모두 종료되면 자동으로 데몬 쓰레드도 종료된다.  이점을 제외하고는 일반 쓰레드와 다르지 않다. 

<br>

> 데몬 쓰레드의 예시 : 가비지 컬렉터, 워드프로세서의 저장, 화면자동갱신

<br>

데몬 쓰레드는 무한루프와 조건문을 통해 특정 조건 만족시에 작업을 수행하게 작성하며 실행하기전에 `setDaemon(true)` 를 
호출하기만 하면된다. 나머지 작성방법과 실행방법은 일반 쓰레드와 같다. 데몬 쓰레드가 생성하 쓰레드는 자동적으로 데몬 쓰레드가 된다.

```

public class ThreadEx3 implements Runnable {

    static boolean autoSave = false;

    public static void main(String[] args) {

        Thread t = new Thread(new ThreadEx3());
        t.setDaemon(true);
        //호출
        t.start();

        for (int i = 1; i <= 10; i++) {
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
            }
            System.out.println(i);

            if (i == 5)
                autoSave = true;
        }

        System.out.println("프로그램을 종료합니다.");
    }

    public void run() {
        while (true) {
            try {
                Thread.sleep(3 * 1000);
            } catch (InterruptedException e) {
            }

            if (autoSave) {
                autoSave();
            }
        }
    }

    public void autoSave() {
        System.out.println("작업파일이 자동저장되었습니다.");
    }
    

}


```

<br>

눈여겨 봐야할곳은 데몬 쓰레드를 실행하기 전에 쓰레드를 생성한 부분과 데몬 쓰레드를 호출한 부분이다. 작업이 없을때는 대기하다가
작업이 생기면 작업하고 작업이 끝나면 다시 대기하는 데몬 쓰레드의 특징 덕분에 데몬 쓰레드가 무한히 작동하지 않는다.

<br>

```

        Thread t = new Thread(new ThreadEx3());
        t.setDaemon(true);
        t.start();
        
```

<br>

현재 실행, 대기상태, 즉 작업이 완료되지않은 모든 쓰레드의 호출스택을 출력하려면 `getAllStackTraces()` 메서드를 사용하면 
된다.


<br>

## 8. 쓰레드의 실행제어
쓰레드 프로그래밍은 동기화(synchronization) 과 스케줄링(scheduling) 때문에 하는 것이 쉽지않다. 효율적인 멀테쓰레드 
프로그램을 만들기 위해서는 스케줄링을 통해 주어진 자원과 시간을 낭비없이 사용할 수 있도록 프로그래밍 해야한다.


#### 스케줄링 메서드

- `static void sleep(long millis)`
  `static void sleep(long millis, int nanos)`   
  : 지정된 시간동안 쓰레드를 일시정지시키고 지정한 시간이 지나고 나면 자동적으로 다시 실행대기상태가 된다.
  

- `void join()` `void join(long millis)` `void join(long millis, int nanos)`  
  : 지정된 시간동안 쓰레드가 실행되도록 한다. 지정된 시간이 지나거나 작업이 종료되면 join()을 호출한 
    쓰레드로 다시 돌아와 실행을 계속한다.
 
 
- `void interrupt()` : sleep()이나 join()에 의해 일시정지상태인 쓰레드를 실행대기상태로 만든다. 해당 쓰레드에서는 
  `InterruptedException` 이 발생함으로써 일시정지상태를 벗어나게 한다.
  

- `void stop()` : 쓰레드를 즉시 종료시킨다. 교착상태에 빠지기 쉽기때문에 잘 사용하지 않는다.


- `void suspend()` : 쓰레드를 일시정지시킨다. `resume()` 을 호출하면 다시 실행대기 상태가 됩니다.


- `static void yield()` : 실행 중에 다른 쓰레드에게 양보하고 실행대기상태가 된다.

<br>

그리고 쓰레드에는 위에서 말한 5가지 상태가 있다.

- `NEW` : 쓰레드가 생성되고 아직 `start()` 가 호출되지 않은 상태
  

- `RUNNABLE` : 실행 중 또는 실행 가능한 상태
  

- `BLOCKED` : 동기화 블럭에 의해서 일시정지된 상태(lock 이 풀릴 까지 기다리는 상태)
  

- `WAITING`, `TIME_WAITING` : 쓰레드의 작업이 종료되지는 않았지만 실행가능하지 않은(unreachable) 일시정지 상태.
  `TIME_WAITING` 은 일시정지 시간이 지정된 경우를 의미한다.
  

- `TERMINATED` : 쓰레드의 작업이 종료된 상태

<br>


쓰레드의 생성부터 소멸까지의 과정을 샆려보면 다음과 같다.


<br>

1. 쓰레드를 생성하고 `start()` 를 호출하면 바로 실행되는 것이 아니라 실행대기열에 저장되어 자신의 차례가 될 때까지 기다려야 
   한다. 실행대기열은 큐(queue)와 같은 구조로 먼저 실행대기열에 들어온 쓰레드가 먼저 실행된다.


2. 실행대기상태에 있다가 자신의 차례가 되면 실행상태가 된다.


3. 주어진 실행시간이 다되거나 `yeild()` 를 만나면 다시 실행대기상태가 되고 다음 차례의 쓰레드가 실행상태가 된다.


4. 실행 중에 `suspend()`, `sleep()`, `wait()`, `join()`, `I/O block` 에 의해 일시정지상태가 될 수 있다. 
   `I/O block` 은 입출력작업에서 발생하는 지연상태를 말한다. 사용자의 입력을 기다리는 경우를 예로 들 수 있는데, 
   이런 경우 일시정지 상태에 있다가 사용자가 입력을 마치면 다시 실행대기상태가 된다.


5. 지정된 일시정지시간이 다되거나(time-out), `notify()`, `resume()`, `interrupt()`가 호출되면 일시정지 상태를 
   벗어나 다시 실행대기열에 저장되어 자신의 차례를 기다리게 된다.

   
6. 실행을 모두 마치거나 `stop()` 이 호출되면 쓰레드는 소멸된다.

1부터 6까지 번호를 붙였으나 번호의 순서대로 쓰레드가 수행되는 것은 아니다.

<br>

### 스케줄링 메서드 


#### `sleep(long millis)`, `static void sleep(long millis, int nanos)`
지정된 시간동안 쓰레드를 멈추게 한다. **millisecond 는 1000분의 1초 이고 nanosecond 는 10분의 1초 이다.**  
`sleep`에 의해 일시정지된 쓰레드는 지정시간이 다 되거나 `interrupt` 가 호출되면 다시 실행대기 생태가 되므로 
`try-catch`문으로 예외를 처리해줘야 한다.

```

    try {
            t1.sleep(2000);
    } catch (InterruptedException e) {
            e.printStackTrace();
    }

```

<br>

`sleep` 는 항상 현재 실행중이 쓰레드에 대해 동작하기 때문에 참조변수를 이용해서 호출하기 보다는 `Thread.sleep(2000)` 
같은 식으로 호출해야한다. (`static` 메서드이기 때문에 가능)


<br>


#### `interrupt()`, `interrupted()`
진행 중인 쓰레드의 작업이 끝나기 전에 취소시켜야할때 사용한다. 강제 종료하는 것이 아닌 작업을 멈추는 기능을 한다.  
`interrupt()`는 쓰레드 내부의 `interrupted` 변수을 바꾸지만, `interrupted()` 는 쓰레드에 의해 `interrupt()`
의 호출여부를 `boolean` 타입으로 반환한다.

`while` 문과 조합해서 사용할 수 있다.

```
    while(!interrupted()){
            ...
    }
```

<br>

- `interrupt()` 는 쓰레드의 `interrupt` 상태를 `false` → `true` 상태로 변경
  

- `isInterrupt()` : 쓰레드의 `interrupt` 상태를 반환
  

- `interrupted()` : 쓰레드의 `interrupt` 상태를 반환 후 **false 로 변경**

쓰레드를 `WAITING` 상태로 만드는 `sleep()`, `wait`, `join` 에 의해 일시정지 상태가 되었을댸 `interrupt()` 를
호출하면 `InterruptException` 이 발생하고 실행대기상태인 `RUNNABLE` 상태가 된다.

<br>

#### `suspend()`, `resume()`, `stop()`

`suspend` 는 `sleep` 처럼 쓰레드를 멈추게 하고 `suspend` 에 의해 정지된 쓰레드는 `resume` 을 호출해야 다시 실행대기
상태가 된다. `suspend` 와 `stop` 는 쓰레드를 제어하기 가장 쉬운 방법이지만 교착 생태(`deadlock`) 를 일으키기 쉬워서
`stop` 은 `deprecated` 되었다.


#### yield()

다음 차례의 쓰레드에게 주어진 실행시간을 양보하는 메서드 이다. 만약 1초의 실행시간을 할당 받은 쓰레드가 0.5초 동안 작업을 수행하고
`yield()` 메서드가 호출되면 나머지 0.5초 동안은 실행대기상태로 된다. `yield` 와 `interrupt` 를 적절히 사용하면 효율적인
프로그래밍을 할 수 있다. 


#### join()
쓰레드가 현재 하던 작업을 잠시 멈추고 다른 쓰레드가 지장된 시간동안 작업을 수행하도록 할때 사용한다. 만약 시간을 지정하지 않는다면 
해당 쓰레드가 작업을 마칠 때까지 기다린다. 작업중에 다른 쓰레드의 작업이 먼저 수행되어야할 필요가 있을 사용한다. `join`도 
`interrupt` 에 의해 대기상태에서 벗어날 수 있다. `sleep` 과 유사하지만 `join` 은 현재 쓰레드가 아닌 특정 쓰레드에 대해 
동작한다는 점이 다르다.


<br>

## 9. 쓰레드의 동기화

싱글 쓰레드 환경에서는 하나의 쓰레드가 프로세서의 모든 자원을 사용하기 때문에 별 문제가없지만 멀티쓰레드는 환경에서는 여러 쓰레드가
프로세르의 자원을 공유하기 때문에 서로의 작업에 영향을 줄 수도 있다. 그래서 임계 영역 - `critical area` 과 잠금 - `lock`
을 사용한다. 

공유 데이터를 사용하는 코드 영역을 임계 영역으로 지정해놓고, 공유 데이터가 가지고 있는 `lock` 을 획득해 단 하나의 쓰레드만 
이 영역내의 코드를 수행할 수 있게 잠근다. 그리고 해당 쓰레드가 임계영역 내의 작업이 끝다면 다시 `lock` 으로 잠그고 다음 
쓰레드만 접근할수 있게 한다.이렇게 한 쓰레드가 진행중인 작업을 다른 쓰레드가 간섭하지 못하도록 맏는 것을 동기화 - 
`synchronization` 이라고 한다. 

### synchronized 를 이용한 동기화
`synchronized` 키워드는 임계영역을 설정하는데 사용된다.  

1. `synchronized` 키워드를 메서드 앞에 붙혀서 메서드 전체를 임계영역으로 설정  
   쓰레드는 `synchronized` **메서드가 호출된 시점부터 해당 메서드가 포함된 객체의 `lock` 을 얻어 작업을 수행하고, 작업이 
   끝나면 `lock` 을 반환한다.**
   

2. 메서드 내의 코드 일부를 `{ }` 으로 감싸고 블럭 앞에 `synchronized(참조변수)` 를 붙이는것  
   침조변수는 `lock` 을 걸고자 하는 객체를 참조하는 것이어야 한다. 이 블럭을 `synchronized` 블럭이라고 하는데 
   **이 블럭의 영역 안으로 들어가면서 부터 thread 는 지정된 객체의 `lock` 을 얻게 되고 블럭을 벗어나면 `lock` 
   을 반납한다.**

<br>

### `wait()` 와 `notify()`
`synchronized` 키워드로 `lock` 을 걸면 공유 데이터를 보호할수 있지만 `lock` 을 가진 쓰레드가 작업 끝날때까지 다른
쓰레드는 작업을 할 수 없는 점을 보완하는 메서드이다.

#### `wait(long timeout)`
동기화된 임계영역의 코드를 수행하다가 작업을 더이상 진행할 상황이 아니면 `wait()` 를 호출하여 쓰레드가 `lock` 을 반납하고 
기다리게 한다.(`waiting poll` 에 넣는다. ) 그리고 나중에 작업을 진행할 수 있는 상황이 되면 `notify()` 를 호출하여 
다시 `lock` 을 얻어서 작업을 진행할 수 있게 된다. 지정 시간동만 기다리며, 지정 시간이 자난 뒤에는 자동으로 `notify()` 
가 호출된다.

#### `notify()`
대기중이던 쓰레드 중 임의의 쓰레드에게 통지를 준다. 통지를 받은 쓰레드는 `lock` 을 얻을 수 있다.  

#### `notifyAll()`
기다리던 모든 쓰레드에게 통지를 준다. 하지만 `lock` 을 얻는 쓰레드는 한개다. 

세 메서드 모두 `Object` 에 정의되어 있고 `synchronized` 블록에서만 사용할 수 있다. 

<br>

### `Lock` 과 `Condition` 을 이용한 동기화
만약 `notify()` 를 통해 `waiting pool` 에 있는 쓰레드중 하나의 쓰레드만 통지를 받는다면 마지막에 남겨질 쓰레드는 오랜
시간을 기다려야 한다. (starvation 현상) 그것을 개선하기 위한 클래스들이다. 


### `Lock`

`synchronized` 를 통한 동기화는 자동으로 `lock`을 걸고 푸는 점은 편하지만 같은 메서드 안에서만 걸 수 있다는 단점이 
있는데 그럴때 `Lock` 을 사용한다. `Lock` 클래스는 3가지가 있다. 

- ##### `ReentrantLock` 
    특정 조건에서 `lock` 을 풀고 나중에 다시 `lock` 을 얻고 임계영역으로 들어와 이후의 작업을 수행할 수 있게한다. 베타적인
    `lock` 이라서 무조건 `lock` 이 있어야 임계영역의 코드를 수행할 수 있다.


- ##### `ReentrantReadWriteLock`
    읽기를 위한 `lock`과 쓰기를 위한 `lock`을 제공하며 읽기 `lock` 이 걸려있으면 다른 쓰레드가 읽기 `lock` 을 중복해서
    걸고 읽을 수 있고 쓰기도 마찬가지지만 읽기 `lock` 이 걸려있는데 쓰기 `lock`을 거는것은 불가능하다.


- ##### `StampedLock`
    `lock`을 걸거나 해지할때 스탬프를 사용하며 `낙관적 읽기 lock`(Optimistic reading lock) 이 추가되었다. 기존에 
    읽기 `lock` 이 걸려있으면 쓰기 `lock`을 얻기위해서는 읽기 `lock`이 풀릴때까지 기다려야 했지만 `낙관적 읽기 lock` 은
    쓰기 `lock` 에 의해 바로 풀린다. 그래서 낙관적 읽기에 실패하면, 읽기 `lock`을 얻어서 다시 읽어 와야 한다.
    **무조건 읽기 `lock`을 걸지 않고, 쓰기와 읽기가 충돌할 때만 쓰기가 끝난 후에 읽기 `lock`을 거는 것이다.**

<br>



`ReentrantLock` 은 boolean 을 매개변수로 받는데 `true` 값을 주면 가장 오래 기다린 쓰레드가 `lock`을 획득할 수 있다.
그리고 `synchronized` 와 다르게 수동으로 `lock()` 메서드와 `unlock()` 메서드를 통해서 수동으로 `lock` 을 관리해줘야 
한다. **`lock` 을 걸었다면 푸는 것을 잊지 말것!** `try-catch-finally` 구문을 활용하면 좀더 편하게 관리할 수 있다.


기존의 starvation 현상을 방지하게 위해서 `Condition` 클래스의 `await()` , `signal()` 를 사용할 수 있는데 쓰레드를 
구분하지 않고 공유 객체의 `waiting pool` 에 넣는 `wait()` 와 `notify()` 와는 다르게 각각의 `waiting pool` 을 
만들어서 기다리게 하므로 기아현상을 줄일수있다.  

<br>

### volatile

요즘 대부분의 멀티 코어 프로세서가 있는 컴퓨터들은 메모리에서 읽어온 값을 캐시에 저장하고 사용하는데 값의 변경 여부는 체크하지않고







<br><br>

