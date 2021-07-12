# Static을 사용하는 이유?

## 1. 메모리의 효율성을 높일 수 있다.

```java
public class HousePark  {
    String lastname = "박";

    public static void main(String[] args) {
        HousePark p1 = new HousePark();
        HousePark p2 = new HousePark();
    }
}
```

위 코드를 보면 같은 클래스를 만들고 객체를 생성하면 `객체마다 객체변수 lastname을 저장하기 위한 메모리를 별도로 할당해야 한다.` 하지만 가만히 생각해 보면 HousePark 클래스의 lastname은 어떤 객체이던지 동일한 값인 "박"이어야 하기 때문에 객체가 생성할때마다 lastname을 별도로 할당 시키는 일은 상당히 비효율적이다. 이렇게 항상 값이 변하지 않는 경우라면 static 사용시 메모리의 이점을 얻을 수 있다.

```java
public class HousePark  {
    static String lastname = "박";

    public static void main(String[] args) {
        HousePark pey = new HousePark();
        HousePark pes = new HousePark();
    }
}
```

위 코드 처럼 변수 앞에 static 키워드를 붙이면 자바는 메모리 할당을 딱 한번만 하게 된다.

```java
public class Counter  {
    int count = 0;
    Counter() {
        this.count++;
        System.out.println(this.count);
    }

    public static void main(String[] args) {
        Counter c1 = new Counter();
        Counter c2 = new Counter();
    }
}
```

위 코드를 돌리면 다음과 같은 결과값이 출력된다.

```
1
1
```

이유는 객체가 생성될 때마다 count 변수가 따로 메모리에 할당받기 때문에 다른 주소를 가리킨다.

```java
public class Counter  {
    static int count = 0;
    Counter() {
        this.count++;
        System.out.println(this.count);
    }

    public static void main(String[] args) {
        Counter c1 = new Counter();
        Counter c2 = new Counter();
    }
}
```

count 변수에 static 키워드를 추가하면 메모리 할당을 딱 한번만 하기 때문에 같은 메모리를 가리키고 있으므로 count 변수를 공유하게 된다.

결과값은 다음과 같다.

```
1
2
```

## 2. 유틸리티 성 메소드(== 실시간으로 결과를 알려주는 메소드) 를 작성할 때 좋다.

```java
public class Counter  {
    static int count = 0;
    Counter() {
        this.count++;
    }

    // static method
    public static int getCount() {
        return count;
    }

    public static void main(String[] args) {
        Counter c1 = new Counter();
        Counter c2 = new Counter();

        System.out.println(Counter.getCount());
    }
}
```

위 코드 처럼 `count 변수 값을 실시간으로 알려주는 메소드`를 작성할 때 유용하다.  
`static method`는 다른 메소드에서 `클래스명.스태틱메소드명()` 으로 호출할 수 있기 때문이다.  
주의할 점은 static method 안에서는 `인스턴스 변수 접근이 불가능하다.` 접근을 원한다면 `앞에 static 키워드를 붙여줘야한다.`
