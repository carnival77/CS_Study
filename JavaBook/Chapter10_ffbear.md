# Chapter 10. 날짜와 시간 & 형식화

## 1. 날짜와 시간 

### 1.1 Calendar 와 Date
날짜와 시간을 다룰 목적으로 만든 패키지 

#### Calendar 와 GregorianCalendar
`Calendar` 는 추상클래스 이므로 인스턴스를 생성해줘야한다. 태국일 경우에만 `BuddhistCalendar` 으로 생성해주고 그렇지않은 경우에는 전세계적으로 통용되는 양력인
`GregorianCalendar` 으로 생성해준다.  

```
Calendar calendar = new GregorianCalendar();
```


`Calendar` 가 추상클래스이므로 이렇게 나라에 따라 달력이나 시간이 다른 경우에도 알맞게 구현해서 사용할 수 있다.

<br>

#### Calendar 와 GregorianCalendar

`Calendar` 클래스에는 연도, 월, 일 같은 정보가 필드로 정의되어있어서 `인스턴스이름.get(Calendar.필드)` 로 원하는 값을 출력하거나 얻을 수 있다. 
주의할점은 `Calendar.MONTH`의 경우 1부터시작하는 것이 아니라 0부터 시작한다.
```
        Calendar calendar = Calendar.getInstance();

        System.out.println(calendar.get(Calendar.YEAR));                //2022
        System.out.println(calendar.get(Calendar.MONTH));               //0
        System.out.println(calendar.get(Calendar.DAY_OF_MONTH));        //7
```

`Date` 패키지는 `Calendar` 패키지 출시후 **Deprecated** 되었지만 여전히 필요로하는 메서드는 있다. 그럴경우 `Caldendar`를 `Date`로 변환해서 사용해야한다.
보통 날짜 와 날짜간 차이를 구하기 위해 초단위로 날짜를 변환해서 계산할때 사용한다. 

`getTimeInMillis` 는 밀리초의 차이를 반환하므로 초(sec)의 차이는 1000을 나눠주고 일(day) 의 차이는 24 * 60 * 60 의 값을 나눠준다.

```
        Calendar calendar = Calendar.getInstance();
        Calendar calendar1 = Calendar.getInstance();

        calendar1.set(2022, 0, 6);

        long milliSecDifference = calendar.getTimeInMillis() - calendar1.getTimeInMillis();
        long secDifference = (calendar.getTimeInMillis() - calendar1.getTimeInMillis()) / 1000;
        long dayDifference = (calendar.getTimeInMillis() - calendar1.getTimeInMillis()) / (1000 * 24 * 60 * 60 ) ;

        
        //작성 날짜인 1월 7일과 
        System.out.println(milliSecDifference);                         //86399994 
        System.out.println(secDifference);                              //86399
        System.out.println(dayDifference);                              //0
        
```




<br>



## 2. 형식화 클래스


<br>

## 3. Java.time 패키지


 
<br>

