If you put just one equal sign in your statements, most C++ compilers will not give you an error — though a statement like `x = 10` is not really a condition! Instead, `x = 10` is an assignment, setting the variable x to 10. When code contains such a statement, the result of the evaluation is always the same, regardless of the value that x has.

+   * The operator that tests for inequality is an exclamation mark followed by an equal sign. For the condition `x != 10`, the condition evaluates as true only if x is not equal to 10 (x is equal to something other than 10).
+   * When you're testing for greater-than or less-than conditions, the condition `x > 10` is not true if x is 10. The condition `x > 10` is true only if x is actually greater than, but not equal to, 10. To also test for x being equal to 10, you have two choices:
+       * If you're working with integers, you can test whether `x > 9`. In that case, the condition is true if x is 10, or 11, or 12, and so on.
+       * You can use the greater-than-or-equal-to operator to determine equality `x >= 10`. This condition also is true if x is 10, 11, and so on.

To test for all numbers greater than or equal to 10, the condition `x > 9` works only if you're working with integers. If you're working with floating-point numbers (refer to Book I, Chapter 3, for information on the types of numbers you can work with in C++), the statement `x > 9` won't work like you want. The number 9.1 is greater than 9, and it's not greater than or equal to 10. So if you want greater than or equal to and you're not working with integers, use the `>=` operator.

# Combining multiple evaluations

When you make evaluations for application decisions, you may have more than one condition to evaluate. For example, you might say, "If I get a million dollars, or if I decide to go into debt up to my eyeballs, then I will buy that Lamborghini." In this case, you would buy the car under two conditions, and either can be true. Combining conditions like this is called an or situation: If this is true or if that is true, something happens.

To evaluate two conditions together in C++, you write them in the same statement and separate them with the or symbol (`||`), which looks like two vertical bars. Other programming languages get to use the actual word or, but C++ uses the strange, unpronounceable symbol that we call *The Operator Previously Known As Or*. The following statement shows it performing live:

```
`(i < 10 || i > 100)`
```

This condition is useful for some kinds of range checking where you want to exclude the middle of a range and check only for the extremes. In this case, an i value of 50 (the middle of the range) would evaluate to false. If you use the or operator (`||`), accidentally ending up with a condition that is always true is easy. For example, the condition `(x < 100 || x > 0)` is always