# Garbage Collector

- 유효하지 않은 메모리 (Garbage) 를 정리해주는 기능
- JVM의 Heap 영역은 2가지를 전제(Weak Generational Hypothesis)로 설계되었는데,
  
    <br>
  
    1. 대부분의 객체는 금방 접근 불가능한 상태(Unreachable)가 된다.
    2. 오래된 객체에서 새로운 객체로의 참조는 아주 적게 존재한다.

그렇기 때문에 오랫동안 남아있는 객체와 금방 사라지는 객체를 구분하기 위해 `Young`, `Old` 두가지 영역으로 나누어 설계되었다.

<br>

<div align="center">
  <img src="https://user-images.githubusercontent.com/65614734/144907772-00544efb-9578-465b-a122-8d69a58e051e.png" width="70%">
</div>

<br>


### Young Generation

- 새롭게 생성된 객체가 할당(Allocation)되는 영역
- 대부분의 객체가 금방 Unreachable 상태가 되기 때문에, 많은 객체가 `Young` 영역에 생성되었다가 사라진다.
- `Young` 영역에 대한 가비지 컬렉션(Garbage Collection)을 `Minor GC` 라고 부른다.

    #### Minor GC
    - 새롭게 생성된 객체는 `Eden` 영역에 할당되고 `Eden` 영역에 꽉 차면 `Minor GC` 가 발생한다.
    - 사용중인 객체는 `Survivor` 영역으로 이동하고 사용되지 않는 메모리는 해체되는데, 두개의 `Survivor` 영역중 한개의 영역에만 데이터가 존재해야한

    <br>

    #### Young 영역의 동작 순서
    1. 새로 생성된 객체가 `Eden` 영역에 할당된다.
    
    <br>
    
    2. 객체가 계속 생성되어 `Eden` 영역이 꽉차게 되고 `Minor GC`가 실행된다.
        1. `Eden` 영역에서 사용되지 않는 객체의 메모리가 해제된다.

        2. `Eden` 영역에서 살아남은 객체는 1개의 `Survivor` 영역으로 이동된다.
    
    <br>
  
    3. 1~2번의 과정이 반복되다가 `Survivor` 영역이 가득 차게 되면 `Survivor` 영역의 살아남은 객체를 다른 `Survivor` 영역으로 이동시킨다.(1개의 `Survivor` 영역은 반드시 빈 상태가 된다.)

    <br>       

    4. 이러한 과정을 반복하여 계속해서 살아남은 객체는 `Old` 영역으로 이동(Promotion)된다.

    <br>

`Old` 영역으로 보내는 객체를 판단하는 기준은 `Minor GC` 에서 객체들의 생존횟수를 의미하는 age를 `Object Header` 에 기록하고, 이 age를 보고 이동여부를 결정한다.

<br>

<div align="center">
  <img src="https://user-images.githubusercontent.com/65614734/144907769-9dae2e7f-46a7-4e6c-884a-e8a468a4dd8a.png" width="70%">
</div>


<br>

### Old Generation

- `Young` 영역에서 Reachable 상태를 유지하여 살아남은 객체가 복사되는 영역
- 복사되는 과정에서 대부분 `Young` 영역보다 크게 할당되며, 크기가 큰 만큼 가비지는 적게 발생한다.
- Old 영역에 대한 가비지 컬렉션(Garbage Collection)을 `Major GC` 또는 `Full GC`라고 부른다. 

    <br>    

    #### Major GC
    - `Young` 영역에서 오래 살아남은 객체들은 `Old` 영역으로 이동하는데 객체들이 계속 promotion 하여 Old 영역의 메모리가 부족해지만 `Major GC` 가 발생한다. 
    - Old 영역은 일반적으로 Young 영역보다 크기때문에 시간이 오래 걸리고 stop-the-world 가 발생한다.


<br>

### Garbage Collection 알고리즘
여러가지 방식이 있는데 기본적인 원리는 같다.

1. Heap 내에 있는 객체중 가비지를 찾아내서 메모리를 회수
   

2. 가비지의 판단은 **reachability** / **unreachability** 로 판단
- Heap 영역내에 있는 객체가 유효한 참조가 있으면 **reachability**
- 그렇지 않으면 **unreachability**

<br>

<div align="center">
  <img src="https://user-images.githubusercontent.com/65614734/144907765-a3f9b27c-398e-4e5b-98f2-5fb6d7e49186.png" width="70%">
</div>


<br>

객체가 객체를 참조하고 그 객체가 또 다른 객체를 참조하는 참조 사슬이 형성될때 사슬의 최초 객체를 Root Set 이라고 한다.

Heap 영역의 객체들은 총 4가지 경우에 대해 참조를 하게되는데 이중 2, 3, 4 는 Root Set 이고 Reachability 를 판단하는 기준이 된다.

1. 힙 내의 다른 객체에 의한 참조
2. Java 스택, 즉 Java 메서드 실행 시에 사용하는 지역변수와 파라미터들에 의한 참조
3. 네이티브 스택(Java Native Interface) 에 의해 생성된 객체에 의한 참조
4. 메서드 영역의 정적변수에 의한 참조

<br>

### Serial GC

- Serial GC 의 Young 영역에서는 **Mark & Sweep** 이 일어나지만 Old 영역에서는 **Compact** 과정이 추가된다.  
  

- Heap 영역을 정리하기 위한 단계로 유요한 객체들이 연속되게 쌓이도록 힙의 가장 앞 부분부터 채워서 객체가 존재하는 부분과 객체가 존재하지 않는 부분으로 나누는 것
  

- 하지만 서버의 CPU 코어가 1개일때 사용하기 위해 개발되었으므로 CPU 코어가 여러개일 경우는 피해야한다.  

<br>

### Parallel GC

- 처리 과정은 Serial GC와 동일하지만 Parallel GC는 여러 개의 쓰레드를 통해 Parallel하게 GC를 수행함으로써 GC의 오버헤드를 상당히 줄여준다
  

- 멀티 프로세서 또는 멀티 쓰레드 머신에서 중간 규모부터 대규모의 데이터를 처리하는 애플리케이션을 위해 고안되었으며, 옵션을 통해 애플리케이션의 최대 지연 시간 또는 GC를 수행할 쓰레드의 갯수 등을 설정해줄 수 있다.
  

- Java8 까지 Default Garbage Collector 로 사용되었으나 추후 대체되었다.

<br>

### CMS(Concurrent Mark Sweep) GC

- Parallel GC와 마찬가지로 여러 개의 쓰레드를 이용한다. 하지만 기존의 Serial GC나 Parallel GC와는 다르게 Mark Sweep 알고리즘을 Concurrent하게 수행하게 된다.

  #### Concurrency(병행성, 동시성) vs Parallelism(병렬성)
  
  <br>

  <div align="center">
    <img src="https://user-images.githubusercontent.com/65614734/144907776-f3e6d3eb-a841-493d-921f-888989572bde.png" width="50%">
  </div>


  <br>
  
  > Concurrency : 동시에 실행되는 것 같이 보이는 것                                                                      
  > Parallelism : 실제로 동시에 여러 작업이 처리되는 것

  <br>

- 애플리케이션의 지연 시간을 최소화 하기 위해 고안
  

- 다른 GC 방식보다 메모리와 CPU를 더 많이 필요
  

- Java9 버젼부터 deprecated 되었고 결국 Java14에서는 사용이 중지

<br>

#### Serial GC vs Parallel GC vs CMS GC

<br>

<div align="center">
  <img src="https://user-images.githubusercontent.com/65614734/144907763-eb7441f3-d5fa-435b-ba3e-51816fb8c851.png" width="70%">
</div>


<br>

### G1(Garbage First) GC

- CMS GC를 대체하기 위해 개발되었고, Java7부터 지원되기 시작
  

- Region(지역)이라는 개념을 새로 도입하여 Heap을 균등하게 여러 개의 지역으로 나누고, 각 지역을 역할과 함께 논리적으로 구분하여(Eden 지역인지, Survivor 지역인지, Old 지역인지) 객체를 할당

<br>

<div align="center">
  <img src="https://user-images.githubusercontent.com/65614734/144907759-2754ecc5-b18d-40ee-8c39-455ad829b1da.png" width="35%">
</div>


<br>

- Humonguous는 Region 크기의 50%를 초과하는 객체를 저장하는 Region을 의미
  

- Availabe/Unused는 사용되지 않은 Region을 의미
  

- 어떠한 GC 방식보다 처리 속도가 빠르며 큰 메모리 공간에서 멀티 프로레스 기반으로 운영되는 애플리케이션을 위해 고안
  

- Java9부터 Default Garbage Collector로 사용


<br><br>

이미지출처
- https://asfirstalways.tistory.com/159?category=660807
- https://mangkyu.tistory.com/119

<br>

참고 자료
- https://asfirstalways.tistory.com/158
- https://d2.naver.com/helloworld/1329
- https://d2.naver.com/helloworld/329631
- https://mangkyu.tistory.com/118
- https://mangkyu.tistory.com/119

<br><br>



