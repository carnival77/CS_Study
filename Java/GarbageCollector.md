# Garbage Collector

- 유효하지 않은 메모리 (Garbage) 를 정리해주는 기능
- JVM의 Heap 영역은 2가지를 전제(Weak Generational Hypothesis)로 설계되었는데,
  
    <br>
  
    1. 대부분의 객체는 금방 접근 불가능한 상태(Unreachable)가 된다.
    2. 오래된 객체에서 새로운 객체로의 참조는 아주 적게 존재한다.

그렇기 때문에 오랫동안 남아있는 객체와 금방 사라지는 객체를 구분하기 위해 `Young`, `Old` 두가지 영역으로 나누어 설계되었다.


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

### Old Generation

- `Young` 영역에서 Reachable 상태를 유지하여 살아남은 객체가 복사되는 영역
- 복사되는 과정에서 대부분 `Young` 영역보다 크게 할당되며, 크기가 큰 만큼 가비지는 적게 발생한다.
- Old 영역에 대한 가비지 컬렉션(Garbage Collection)을 `Major GC` 또는 `Full GC`라고 부른다. 

    <br>    

    #### Major GC
    - `Young` 영역에서 오래 살아남은 객체들은 `Old` 영역으로 이동하는데 객체들이 계속 promotion 하여 Old 영역의 메모리가 부족해지만 `Major GC` 가 발생한다. 
    - Old 영역은 일반적으로 Young 영역보다 크기때문에 시간이 오래 걸리고 stop-the-world 가 발생한다.


<br>

### 동작방식

    1.  








