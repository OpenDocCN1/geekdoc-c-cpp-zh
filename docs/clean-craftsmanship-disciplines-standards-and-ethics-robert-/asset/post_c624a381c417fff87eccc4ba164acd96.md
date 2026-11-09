
We begin, as always, with a failing test. If you are wondering why I’m using BigInteger, it is because Fibonacci numbers get big very quickly.

Click here to view code image

```java
public class FibTest {
  @Test
  public void testFibs() throws Exception {
    assertThat(fib(0), equalTo(BigInteger.ONE));
  }

  private BigInteger fib(int n) {
    return null;
  }
}
```

We can make this pass by using the Nil → Constant transformation.

Click here to view code image

```java
private BigInteger fib(int n) {
  return new BigInteger("1");
}
```

Yes, I thought the use of the String argument was odd too; but that’s the Java library for you.

The next test passes right out of the box:

Click here to view code image

```java
@Test
public void testFibs() throws Exception {
  assertThat(fib(0), equalTo(BigInteger.ONE));
  assertThat(fib(1), equalTo(BigInteger.ONE));
}
```

The next test fails:

Click here to view code image

```java
@Test
public void testFibs() throws Exception {
  assertThat(fib(0), equalTo(BigInteger.ONE));
  assertThat(fib(1), equalTo(BigInteger.ONE));
  assertThat(fib(2), equalTo(new BigInteger("2")));
}
```

We can make this pass by using Unconditional → Selection:

Click here to view code image

```java
private BigInteger fib(int n) {
    if (n > 1)
        return new BigInteger("2");
    else
        return new BigInteger("1");
}
```

This is perilously close to being more specific than general, though it titillates me with the potential for negative arguments to the `fib` function.

The next test tempts us to go for the gold:

Click here to view code image

```java
assertThat(fib(3), equalTo(new BigInteger("3")));
```

The solution uses Statement → Recursion:

Click here to view code image

```java
private BigInteger fib(int n) {
    if (n > 1)
        return fib(n-1).add(fib(n-2));
    else
        return new BigInteger("1");
}
```

This is a very elegant solution. It’s also horrifically expensive in terms of time¹⁰ and memory. Going for the gold too early often comes at a cost. Is there another way we could have done that last step?

- 10. fib(40) == 165580141 took nine seconds to compute on my 2.3GHz MacBook Pro.

Of course there is:

Click here to view code image

```java
private BigInteger fib(int n) {
    return fib(BigInteger.ONE, BigInteger.ONE, n);
}
```

```java
private BigInteger fib(BigInteger fm2, BigInteger fm1, int n) {
    if (n>1)
        return fib(fm1, fm1.add(fm2), n-1);
    else
        return fm1;
}
```

This is a nice tail-recursive algorithm that is tolerably fast.^11

- 11. fib(100) == 573147844013817084101 in 10ms.

You might think that last transformation was just a different application of Statement → Recursion, but it wasn't. It was actually Selection → Iteration. In fact, if the Java compiler would deign to offer us tail-call-optimization,^12 it would translate almost exactly to the following code. Note the implied if->while.

- 12. Java, Java, wherefore art thou Java?

Click here to view code image

```java
private BigInteger fib(int n) {
    BigInteger fm2 = BigInteger.ONE;
    BigInteger fm1 = BigInteger.ONE;
    while (n>1) {
        BigInteger f = fm1.add(fm2);
        fm2 = fm1;
        fm1 = f;
        n--;
    }
    return fm1;
}
```

I took you on that little diversion to make an important point:

> *Rule 14: If one transformation leads you to a suboptimal solution, try a different transformation.*

This is actually the second time we have encountered a situation in which a transformation led us to a suboptimal solution and a different transformation produced much better results. The first time was back in the sort kata. In that case, it was the Value → Mutated Value transformation

## 5 Refactoring

This discipline pursues two goals. First, every function should do *one thing*.<sup>5</sup> Second, your code should read like *well-written prose*.<sup>6</sup>

- 5. Martin, *Clean Code*, p. 7.
- 6. Martin, p. 8.

A function does *one thing* when no other function can be extracted from it. Therefore, in order that your functions all do *one thing*, you should extract and extract and extract until you cannot extract any more.

This will, of course, lead to a plethora of little tiny functions. And this may disturb you. You may feel that so many little tiny functions will obscure the intent of your code. You may worry that it would be easy to get lost within such a huge swarm of functions.

But the opposite happens. The intent of your code becomes much more obvious. The levels of abstraction become crisp and the lines between them clear.

Remember that languages nowadays are rich with modules, classes, and namespaces. This allows you to build a hierarchy of names within which to place your functions. Namespaces hold classes. Classes hold functions. Public functions refer to private functions. Classes hold inner and nested classes. And so on. Take advantage of these tools to create a structure that makes it easy for other programmers to locate the functions you have written.

And then choose good names. Remember that the length of a function’s name should be *inversely* proportional to the scope that contains it. The names of public functions should be relatively short. The names of private functions should be longer.

As you extract and extract, the names of the functions will get longer and longer because the purpose of the function will become less and less general. Most of these extracted functions will be called from only one place, so their purpose will be extremely specialized and precise. The names of such specialized and precise functions must be long. They will likely be full clauses or even sentences.

These functions will be called from within the parentheses of `while` loops and `if` statements. They will be called from within the bodies of those statements as well, leading to code that looks like this:

Click here to view code image

```java
if (employeeShouldHaveFullBenefits())
  AddFullBenefitsToEmployee();
```

It will make your code read like *well-written prose*.

Using the **Extract Method** refactoring is also how you will get your functions to follow *the stepdown rule.*⁷ We want each line of a function to be at the same level of abstraction, and that level should be one level below the *name* of the function. To achieve this, we extract all code snippets within a function that are below the desired level.

- 7. Martin, p. 37.

### Extract Variable

If **Extract Method** is the most important of refactorings, **Extract Variable** is its ready assistant. It turns out that in order to extract methods, you often must extract variables first.

For example, consider this refactoring from the bowling game in Chapter 2, “Test-Driven Development.” We started with this:

Click here to view code image

```java
@Test
public void allOnes() throws Exception {
  for (int i=0; i<20; i++)
    g.roll(1);
  assertEquals(20, g.score());
}
```

And we ended up with this:

Click here to view code image

```java
private void rollMany(int n, int pins) {
  for (int i = 0; i < n; i++) {
    g.roll(pins);
  }
}
```

```java
@Test
public void allOnes() throws Exception {
    rollMany(20, 1);
    assertEquals(20, g.score());
}
```

The sequence of refactorings was as follows:

- 1. **Extract Variable:** The `1` in `g.roll(1)` was extracted into a variable named `pins`.
- 2. **Extract Variable:** The `20` in `assertEquals(20, g.score());` was extracted into a variable named `n`.
- 3. The two variables were moved above the `for` loop.
- 4. **Extract Method:** The `for` loop was extracted into the `rollMany` function. The names of the variables became the names of the arguments.
- 5. **Inline:** The two variables were inlined. They had served their purpose and were no longer needed.

Another common usage for **Extract Variable** is to create an *explanatory variable*.<sup>8</sup> For example, consider the following if statement:

- 8. Kent Beck, *Smalltalk Best Practice Patterns* (Addison-Wesley, 1997), 108.

Click here to view code image

```java
if (employee.age > 60 && employee.salary > 150000)
    ScheduleForEarlyRetirement(employee);
```

This might read better with an explanatory variable:

Click here to view code image

```java
boolean isEligibleForEarlyRetirement = employee.age > 60 &&
                                       employee.salary > 150000;
if (isEligibleForEarlyRetirement)
    ScheduleForEarlyRetirement(employee);
```
