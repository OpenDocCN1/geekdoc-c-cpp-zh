```
~~~java
    assertEquals(0, sin(Math.PI), EPSILON);
    assertEquals(1, sin(Math.PI/2), EPSILON);
    assertEquals(0.8660254038, sin(Math.PI/3), EPSILON);
    assertEquals(0.7071067812, sin(Math.PI/4), EPSILON);
    assertEquals(0.5877852523, sin(Math.PI/5), EPSILON);
}
~~~
```

```
~~~java
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
~~~
```

```
~~~java
boolean close(double a, double b) {
    return Math.abs(a - b) < .0000001;
}
}
~~~
```

Okay, now we’re cooking with gas. But wait? What happened to the TDD? And how do we know that this algorithm is really working right? I mean, that’s a lot of code. How can we tell if that code is right?

I suppose we could test a few more values. And, yikes, these tests are getting unwieldy. Let’s refactor a bit too:

Click here to view code image