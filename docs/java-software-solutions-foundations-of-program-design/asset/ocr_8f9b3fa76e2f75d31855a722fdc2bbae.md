```
if (num1 >= num2)
{
    System.out.print (" red ");
    System.out.print (" orange ");
}
if ((num1 + 5) >= num2)
    System.out.print (" white ");
else
    if ((num1 + 10) >= num2)
    {
        System.out.print (" black ");
        System.out.print (" blue ");
    }
    else
        System.out.print (" yellow ");
System.out.println(" green ");
```

+   a. Assuming the value of num1 is 5 and the value of num2 is 4?
+   b. Assuming the value of num1 is 5 and the value of num2 is 12?
+   c. Assuming the value of num1 is 5 and the value of num2 is 27?

SR 5.12 Write an expression that will print a message based on the value of the int variable named temperature. If temperature is equal to or less than 50, it prints “It is cool.” on one line and “Dress warmly.” on the next. If temperature is greater than 80, it prints “It is warm.” on one line and “Dress coolly.” on the next. If temperature is in between 50 and 80, it prints “It is pleasant.” on one line and “Dress pleasantly.” on the next.

# 5.3 Comparing Data

When comparing data using boolean expressions, it’s important to understand some nuances that arise depending on the type of data being examined. Let’s look at a few key situations.

# Comparing Floats

An interesting situation occurs when comparing floating point data. Two floating point values are equal, according to the == operator, only if all the binary digits of their underlying representations match. If the compared values are the results of