
```java
public static boolean isLeap(int year) {

    boolean c1, c2, c3;

    c1 = year % 4 == 0;

    c2 = year % 100 == 0;

    c3 = year % 400 == 0;

    boolean isLeap = false;

    if (c1 && !c2) {

        isLeap = true;

    } else if (c1 && c2 && c3) {

        isLeap = true;

    }

    return isLeap;

}
```
