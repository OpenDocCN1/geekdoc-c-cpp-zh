
![](img/7b01f9dd5d5d33f16ee27a44427cd56e_148_0.png)

**Figure 3.6 The mock object**

A *mock* is a spy. It returns test-specific values in order to drive the system under test through desired pathways, and it remembers what was done to it. However, a mock also knows what to expect and will pass or fail the test on the basis of those expectations.

![](img/7b01f9dd5d5d33f16ee27a44427cd56e_151_0.png)

**Figure 3.7 The fake**

Long ago, in the late 1970s, I worked for a company that built a system that was installed into telephone company facilities. This system tested telephone lines. There was a central computer at the service center that communicated over modem links to computers we installed in the switching offices. The computer in the service center was called the SAC (service area

```
    dialog.show();
    boolean success = dialog.submit("user", "good password");
    assertTrue(success);
}
```

These two tests use the same `FakeAuthenticator` but pass it a different password. The tests expect that *bad password* will fail the login attempt and that *good password* will succeed.

The code for `FakeAuthenticator` should be easy to envision:

[Click here to view code image](#)

```java
public class FakeAuthenticator implements Authenticator {
    public Boolean authenticate(String username, String password)
    {
        return (username.equals("user") &&
                password.equals("good password"));
    }
}
```

The problem with fakes is that as the application grows, there will always be more conditions to test. Consequently, the fakes tend to grow with each new tested condition. Eventually, they can get so large and complex that they need tests of their own.

I seldom write fakes because I don’t trust them not to grow.

## The TDD Uncertainty Principle

To mock or not to mock, that is the question. Actually, no. The question really is *when* to mock.

There are two schools of thought about this: the London school and the Chicago school, which are addressed at the end of this chapter. But before we get into that, we need to define why this is an issue in the first place. It is an issue because of the *TDD uncertainty principle*.

To help us understand this, I want you to indulge me in a playful bit of “going to extremes.” What follows is not something you would ever really do, but it illustrates quite nicely the point I’m trying to make.

Imagine that we want to use TDD to write a function that calculates the trigonometric sine of an angle represented in radians. What’s the first test?

Remember, we like to start with the most degenerate case. Let’s test that we can calculate the sine of zero:

[Click here to view code image](#)

```java
public class SineTest {
    private static final double EPSILON = 0.0001;
    @Test
    public void sines() throws Exception {
        assertEquals(0, sin(0), EPSILON);
    }

    double sin(double radians) {
        return 0.0;
    }
}
```

Now, if you are thinking ahead, this should already bother you. This test does not constrain anything other than the value of `sin(0)`.

What do I mean by that? I mean that most of the functions we write using TDD are so constrained by the growing set of tests that there comes a point where the function will pass any other test we can pose. We saw that in the prime factors example and the bowling game example. Each test narrowed the possible solution until finally the solution was known.

But here, the `sin(r)` function does not look to behave that way. The test for `sin(0) == 0` is correct, but it does not appear to constrain the solution beyond that one point.

This becomes much more evident when we try the next test. What should that test be? Why not try sin(π)?

[Click here to view code image](#)

```java
public class SineTest {
    private static final double EPSILON = 0.0001;
    @Test
    public void sines() throws Exception {
        assertEquals(0, sin(0), EPSILON);
        assertEquals(0, sin(Math.PI), EPSILON);
    }

    double sin(double radians) {
        return 0.0;
    }
}
```

Once again, we have that feeling of being unconstrained. This test doesn’t seem to add anything to the solution. It gives us no hint of how to solve the problem, so let’s try π/2:

[Click here to view code image](#)

```java
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
```

This fails. How can we make it pass? Again, the test gives us no hint about how to pass it. We could try to put some horrible `if` statement in, but that will just lead to more and more `if` statements.

At this point, you might think that the best approach would be to look up the Taylor series for sine and just implement that.

$$x - \frac{x^3}{3!} + \frac{x^5}{5!} - \frac{x^7}{7!} + \cdots$$

That shouldn’t be too hard:

[Click here to view code image](#)

```java
public class SineTest {
    private static final double EPSILON = 0.0001;
    @Test
    public void sines() throws Exception {
        assertEquals(0, sin(0), EPSILON);
        assertEquals(0, sin(Math.PI), EPSILON);
        assertEquals(1, sin(Math.PI/2), EPSILON);
    }

    double sin(double radians) {
        double r2 = radians * radians;
        double r3 = r2 * radians;
        double r5 = r3 * r2;
        double r7 = r5 * r2;
        double r9 = r7 * r2;
        double r11 = r9 * r2;
        double r13 = r11 * r2;
        return (radians - r3/6 + r5/120 - r7/5040 + r9/362880 -
                r11/39916800.0 + r13/6227020800.0);
    }
}
```

This passes, but it’s pretty ugly. Still, we ought to be able to calculate a few other sines this way:

[Click here to view code image](#)

```java
public void sines() throws Exception {
    assertEquals(0, sin(0), EPSILON);
    assertEquals(0, sin(Math.PI), EPSILON);
    assertEquals(1, sin(Math.PI/2), EPSILON);
    assertEquals(0.8660, sin(Math.PI/3), EPSILON);
    assertEquals(0.7071, sin(Math.PI/4), EPSILON);
    assertEquals(0.5877, sin(Math.PI/5), EPSILON);
}
```

Yes, this passes. But this solution is ugly because it is limited in precision. We should take the Taylor series out to enough terms that it converges to the limit of our precision. (Note the change to the EPSILON constant.)

[Click here to view code image](#)

```java
public class SineTest {
    private static final double EPSILON = 0.00000001;
    @Test
    public void sines() throws Exception {
        assertEquals(0, sin(0), EPSILON);
        assertEquals(0, sin(Math.PI), EPSILON);
        assertEquals(1, sin(Math.PI/2), EPSILON);
        assertEquals(0.8660254038, sin(Math.PI/3), EPSILON);
        assertEquals(0.7071067812, sin(Math.PI/4), EPSILON);
        assertEquals(0.5877852523, sin(Math.PI/5), EPSILON);
    }

    double sin(double radians) {
        double result = radians;
        double lastResult = 2;
        double m1 = -1;
        double sign = 1;
        double power = radians;
        double fac = 1;
        double r2 = radians * radians;
        int n = 1;
        while (!close(result, lastResult)) {
            lastResult = result;
            power *= r2;
            fac *= (n+1) * (n+2);
            n += 2;
            sign *= m1;
            double term = sign * power / fac;
            result += term;
        }

        return result;
    }

    boolean close(double a, double b) {
        return Math.abs(a - b) < .0000001;
    }
}
```

Okay, now we’re cooking with gas. But wait? What happened to the TDD? And how do we know that this algorithm is really working right? I mean, that’s a lot of code. How can we tell if that code is right?

I suppose we could test a few more values. And, yikes, these tests are getting unwieldy. Let’s refactor a bit too:

Click here to view code image
