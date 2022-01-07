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

#### Date 와 Calendar 의 변환

`Calendar` 클래스에는 연도, 월, 일 같은 정보가 필드로 정의되어있어서 `인스턴스이름.get(Calendar.필드)` 로 원하는 값을 출력하거나 얻을 수 있다. 
주의할점은 `Calendar.MONTH`의 경우 1부터시작하는 것이 아니라 0부터 시작한다.


```

        Calendar calendar = Calendar.getInstance();

        System.out.println(calendar.get(Calendar.YEAR));                //2022
        System.out.println(calendar.get(Calendar.MONTH));               //0
        System.out.println(calendar.get(Calendar.DAY_OF_MONTH));        //7
```

<br>

`Date` 패키지는 `Calendar` 패키지 출시후 **Deprecated** 되었지만 여전히 필요로하는 메서드는 있다. 그럴경우 `Caldendar`를 `Date`로 변환해서 사용해야한다.
보통 날짜 와 날짜간 차이를 구하기 위해 초단위로 날짜를 변환해서 계산할때 사용한다.


```
Date date = new Date(calendar.getTimeInMillis());
```

<br>

`getTimeInMillis` 는 밀리초의 차이를 반환하므로 초(sec)의 차이는 1000을 나눠주고 일(day) 의 차이는 24 * 60 * 60 의 값을 나눠준다.

<br>

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
        System.out.println(dayDifference);                              //0 하루에 해당하는 86400 초를 넘지 않아서 0으로 출력
        
```




<br>

`Calendar` 클래스의 각 필드에 값을 추가하면 `add(field name, amount)` 와 `roll(field name, amount)` 를 사용하면된다.
둘의 차이점은 `roll` 메서드는 다른 필드에 영향을 미치지 않는다.

``` 

        Calendar calendar1 = Calendar.getInstance();
        Calendar calendar2 = Calendar.getInstance();
        calendar1.set(2022, 0, 31);
        calendar2.set(2022, 0, 31);
           
        //roll
        System.out.println(calendar1.get(Calendar.MONTH) + 1 + " / " + calendar1.get(Calendar.DATE)); 
        calendar1.roll(Calendar.DATE, 2);
        System.out.println(calendar1.get(Calendar.MONTH) + 1 + " / " + calendar1.get(Calendar.DATE));
        
        //add
        System.out.println(calendar2.get(Calendar.MONTH) + 1 + " / " + calendar2.get(Calendar.DATE)); 
        calendar1.add(Calendar.DATE, 2);
        System.out.println(calendar2.get(Calendar.MONTH) + 1 + " / " + calendar2.get(Calendar.DATE));
        
        
        //출력
        
        //1 / 31
        //1 / 2
        //1월 33일은 존재하지 않으므로 자동으로 1월 2일로 변경되었다.
        
        //1 / 31
        //2 / 2
        //1월 31일의 이틀뒤인 2월 2일로 자동 변경되었다.
        
```

<br>

하지만 만약 변경하려는 날짜가 월(month) 의 말일(end of month) 일때는 `DATE`에 영향을 미칠 수 있다.

```

        calendar1.set(2022, 0, 31);
        
        System.out.println(calendar1.get(Calendar.MONTH) + 1 + " / " + calendar1.get(Calendar.DATE));
        calendar1.roll(Calendar.Month, 1);
        System.out.println(calendar1.get(Calendar.MONTH) + 1 + " / " + calendar1.get(Calendar.DATE));
        
         //출력
        
        //1 / 31
        //2 / 28
        //자동으로 2월의 말일로 변경되었다.
    
```

<br><br>

#### 기타 메소드

- `boolean isLeapYesr(int year)` : 매개변수가 윤년인지 아닌지 판변해주는 메소드
- `int dayDiff(int y1, int m1, int d1, int y2, int m2, int d2)` : 두 눌짜간의 차이를 일단위로 변환
- `int getDayOfWeek(int year, int month, int day)` : 지정한 날짜의 요일을 1~7로 반환 (1이 일요일)
- `String convertDayToDate(int day)` : 일단위의 값을 년월일의 문자열로 변환
- `int convertDateToDay(int year, int month, int day)` : 년월일을 일단위로 변환

<br><br>

## 2. 형식화 클래스

숫자나 날짜 등등을 원하는 형식으로 변환하는 것을 도와주는 클래스이다.

### 2.1 DecimalFormat
형식화 클래스중 숫자를 형식화할떄 사용하거나 일정한 형식의 텍스트를 숫자로 변환할때 사용한다.

#### 사용되는 기호

- `0` : 10진수 숫자(값이 없으면 0)
- `#` : 10진수 숫자
- `.` : 소수점
- `-` : 음수 부호
- `.` : 단위 구분자
- `E` : 지수기호
- `;` : 패턴 구분자
- `%` : 퍼센트
- `‰` : 퍼밀(퍼센트 x 10)
- `₩` : 통화기호
- `'` : escape 문자

```
                double num = 12345678.89;
     
                "0",                     // 1234568
                "0.0",                   // 1234567.9
                "0000000000.0000",       // 0001234567.8900

                "#",                     // 1234568
                "#.#",                   // 1234567.9
                "##########.####",       // 1234567.89

                "#.#",                   // 1234567.9

                "-#.#",                  // -1234567.9
                "#.#-",                  // 1234567.9-

                "#,###.##",              // 1,234,567.89
                "#,####.##",             // 123,4567.89

                "#E0",                   // 1.23456789E6
                "0E0",                   // 1E6
                "##E0",                  // 1.23456789E6
                "00E0",                  // 12E5
                "####E0",                // 123.456789E4
                "0000E0",                // 1235E3
                "#.#E0",                 // 1.2E6
                "0.0E0",                 // 1.2E6
                "0.000000000E0",         // 1.234567890E6
                "00.00000000E0",         // 12.34567890E5
                "000.0000000E0",         // 123.4567890E4
                "#.#########E0",         // 1.23456789E6
                "##.########E0",         // 1.23456789E6
                "###.#######E0",         // 1.2345679E6

                "#,###.##+;#,###.##-",   // 1,234,567.89+

                "#.#%",                  // 123456789%

                "#.#\u2030",             // 1234567890‰

                "\u00A4 #,###",          // ₩ 1,234,568

                "'#'#,###",              // #1,234,568
                "''#,###"                // '1,234,568


```

<br>

혹은 `NumberFormat` 에 정의된 `parse(String)` 메소드를 사용해서 문자열에서 숫자로 변환할 수 있다.

```
        DecimalFormat df = new DecimalFormat("0.0");
        Number n = df.parse("123.456");
        
        //123.456
```

<br>

### 2.2 SimpleDateFormat
날짜를 출력할때 사용하는 메소드이며 좀더 편리하게 출력하게 도와준다. 마찬가지로 추상클래스이기 때문에 `SimpleDateFormat` 
인스턴스를 생성하고 원하는 형식을 넣으면 그에 맞는 형태로 출력된다.

- `G` : 연대 (BC, AD)
- `y` : 년도 
- `M` : 월 (1~12)  
- `w` : 해당 년도의 몇 번째 주 (1~53)
- `W` : 해당 월의 몇 번째 주 (1~5) 
- `D` : 해당 연도의 몇 번째 일 (1~366) 
- `d` : 해당 월의 몇 번째 일 (1~31) 
- `F` : 해당 월의 몇 번째 요일 (1~5)
- `E` : 요일 (월~일) Sat a 오전/오후 (AM, PM)
- `H` : 시간 (0~23) 21 h 시간 (1~12) 
- `K` : 시간 (0~11)
- `k` : 시간 (1~24)
- `m` : 분 (0~59)
- `s` : 초 (0~59)
- `S` : 1/1000초 (0~999)
- `z` : 타임존(RFC 822) (ex : KST+0900 )
- `Z` : 타임존 (ex : +0900 ) 

<br>

```

        Date today = new Date();
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
        SimpleDateFormat sdf1 = new SimpleDateFormat("yy년 MM월 dd일 E요일");
        SimpleDateFormat sdf2 = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss SSS");
        SimpleDateFormat sdf3 = new SimpleDateFormat("yyyy-MM-dd hh:mm:ss a");


        System.out.println(sdf.format(today));
        System.out.println(sdf1.format(today));
        System.out.println(sdf2.format(today));
        System.out.println(sdf3.format(today));
        
        //출력
        // 2022-01-08
        // 22년 01월 08일 Sat요일
        // 2022-01-08 01:16:37 278
        // 2022-01-08 01:16:37 AM
                
```

<br>

`Calendar` 와 `Date`클래스와도 조합할 수 있는데 `Date` 인스턴스만 `format` 메서드에 사용될수 있기 때문에 변환을 해줘야한다.

```

        Calendar cal = Calendar.getInstance();
        cal.set(2021, 1, 1);

        //변환
        Date day = cal.getTime();
        SimpleDateFormat sdf4 = new SimpleDateFormat("yy년 MM월 dd일 E요일");
        System.out.println(sdf4.format(day));
        
        //출력
        // 21년 02월 01일 Mon요일

```

<br>

문자열을 Date 인스턴스로 변환할 수 도 있다.

```

        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
        Date day = sdf.parse("2021-01-01");
        System.out.println(sdf.format(day));
        
        //출력
        // 2021-01-01
        
```



<br><br>

## 3. Java.time 패키지


<br><br>

 
<br>

