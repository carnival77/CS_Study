# Garbage Collector

- 유효하지 않은 메모리 (Garbage) 를 정리해주는 기능
- JVM의 Heap 영역은 2가지를 전제(Weak Generational Hypothesis)로 설계되었는데,
  
    <br>
  
    1. 대부분의 객체는 금방 접근 불가능한 상태(Unreachable)가 된다.
    2. 오래된 객체에서 새로운 객체로의 참조는 아주 적게 존재한다.

그렇기 때문에 오랫동안 남아있는 객체와 금방 사라지는 객체를 구분하기 위해 Young, Old 두가지 영역으로 나누어 설계되었다.

