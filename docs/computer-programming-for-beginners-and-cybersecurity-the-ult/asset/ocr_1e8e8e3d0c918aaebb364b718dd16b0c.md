```
```java
public class forArrayDemo {
    public static void main(String args[]) {
        int [] numberArray = {100, 300, 500, 700, 900};
        for(int i : numberArray ) {
            System.out.print( i );
            System.out.print(",");
        }
        System.out.print("\n");
    }
}
```
```

# Exception Hierarchy

Java has an inbuilt class named java.lang.Exception and all the exceptions fall under this class. All the exception classes are subclasses of this class. Moreover, the Throwable class is the superclass of the exception class. Another subclass of the Throwable class is the Error class. All the errors like stack overflow described above fall under this Error class.

The Exception class has two subclasses, namely RuntimeException class and IOException class. A list of the methods, for which definitions are available in Java, as part of the Throwable class, is given below.

```
```java
public String getMessage()
```
```

When called, this message returns a detailed description of the exception that has been encountered.

```
```java
public Throwable getCause()
```
```