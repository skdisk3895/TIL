# String 자료형에서의 equals(String str) VS ==

1. `equals`는 `메소드`이고, `==` 은 `연산자`이다.
2. `equals`는 `값 자체`로만 비교하지만 `==`은 `주소값`으로 비교를 한다.

## 코드

```java
public class main {
    public static void main(String args[]) {
        String a = "aaa";
        String b = a;
        String c = new String("aaa");


        System.out.println(a == b);  // true
        System.out.println(a.equals(b));  // true
        System.out.println(a == c);  // false
        System.out.println(a.equals(c));  // true
        System.out.println(b == c);  // false
        System.out.println(b.equals(c));  // true
    }
}

```
