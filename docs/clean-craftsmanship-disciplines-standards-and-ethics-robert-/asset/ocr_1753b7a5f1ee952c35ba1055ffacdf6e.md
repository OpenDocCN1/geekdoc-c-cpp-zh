```
~~~
    }

    double sin(double radians) {
        return 0.0;
    }
}
~~~
```

Once again, we have that feeling of being unconstrained. This test doesn’t
seem to add anything to the solution. It gives us no hint of how to solve the
problem, so let’s try π/2:

[Click here to view code image](#)

```
~~~
public class SineTest {
    private static final double EPSILON = 0.0001;
    @Test
    public void sines() throws Exception {
        assertEquals(0, sin(0), EPSILON);
        assertEquals(0, sin(Math.PI), EPSILON);
        assertEquals(1, sin(Math.PI/2), EPSILON);
    }
    double sin(double radians) {
        return 0.0;
    }
}
~~~
```

This fails. How can we make it pass? Again, the test gives us no hint about
how to pass it. We could try to put some horrible `if` statement in, but that
will just lead to more and more `if` statements.

At this point, you might think that the best approach would be to look up
the Taylor series for sine and just implement that.

$$x - \frac{x^3}{3!} + \frac{x^5}{5!} - \frac{x^7}{7!} + \cdots$$

That shouldn’t be too hard:

[Click here to view code image](#)

```
~~~
public class SineTest {
    private static final double EPSILON = 0.0001;
    @Test
~~~
```