We begin, as always, with a failing test. If you are wondering why I’m using BigInteger, it is because Fibonacci numbers get big very quickly.

Click here to view code image

```
~~~java
public class FibTest {
  @Test
  public void testFibs() throws Exception {
    assertThat(fib(0), equalTo(BigInteger.ONE));
  }

  private BigInteger fib(int n) {
    return null;
  }
}
~~~
```

We can make this pass by using the Nil → Constant transformation.

Click here to view code image

```
~~~java
private BigInteger fib(int n) {
  return new BigInteger("1");
}
~~~
```

Yes, I thought the use of the String argument was odd too; but that’s the Java library for you.

The next test passes right out of the box:

Click here to view code image

```
~~~java
@Test
public void testFibs() throws Exception {
  assertThat(fib(0), equalTo(BigInteger.ONE));
  assertThat(fib(1), equalTo(BigInteger.ONE));
}
~~~
```

The next test fails:

Click here to view code image

```
~~~java
@Test
public void testFibs() throws Exception {
  assertThat(fib(0), equalTo(BigInteger.ONE));
  assertThat(fib(1), equalTo(BigInteger.ONE));
~~~
```