however, is to put them all at the top of the class. I see no reason to follow
any other convention. The important thing is for the instance variables to be
declared in one well-known place. Everybody should know where to go to
see the declarations.

Consider, for example, the strange case of the `TestSuite` class in JUnit
4.3.1. I have greatly attenuated this class to make the point. If you look
about halfway down the listing, you will see two instance variables declared
there. It would be hard to hide them in a better place. Someone reading this
code would have to stumble across the declarations by accident (as I did).

```
```java
public class TestSuite implements Test {
    static public Test createTest(Class<? extends TestCase> theClass,
                                  String name) {
        ...
    }

    public static Constructor<? extends TestCase>
    getTestConstructor(Class<? extends TestCase> theClass)
    throws NoSuchMethodException {
        ...
    }

    public static Test warning(final String message) {
        ...
    }

    private static String exceptionToString(Throwable t) {
        ...
    }

    private String fName;

    private Vector<Test> fTests= new Vector<Test>(10);

    public TestSuite() {
    }
}
```
```