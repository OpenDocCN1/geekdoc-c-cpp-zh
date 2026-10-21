+   5. An enumeration type is converted to the first of `int`, `unsigned int`, `long`, or `unsigned long` that accommodates the range of the enumerators.
+   6. If either operand is of type `unsigned long`, the other is converted to `unsigned long`.
+   7. If one operand is of type `long` and the other is of type `unsigned int`, then both operands are converted to type `unsigned long`.
+   8. If either operand is of type `long`, the other is converted to type `long`.

This looks and reads as though it is incredibly complicated, but the basic principle is to always convert the value that has the type that is of a more limited range to the type of the other value. This maximizes the likelihood of being able to accommodate the result. You could try these rules on a hypothetical expression to see how they work. Suppose that you have a sequence of variable declarations as follows:

```
double value = 31.0;
int count = 16;
float many = 2.0f;
char num = 4;
```

Also suppose that you have the following rather arbitrary arithmetic statement:

```
value = (value - count) * (count - num) / many + num / many;
```

You can now work out what casts the compiler will apply in the execution of the statement.

The first operation is to calculate (value - count). Rule 1 doesn’t apply but Rule 2 does, so the value of count is converted to double and the double result 15.0 is calculated.

Next (count - num) must be evaluated, and here the first rule in sequence that applies is Rule 4, so num is converted from char to int and the result 12 is produced as a value of type int.

The next calculation is the product of the first two results, a double 15.0 and an int 12. Rule 2 applies here, and the 12 is converted to 12.0 as double, and the double result 180.0 is produced.

This result now has to be divided by many, so Rule 2 applies again, and the value of many is converted to double before generating the double result 90.0.

The expression num/many is calculated next, and here Rule 3 applies to produce the float value 2.0f after converting the type of num from char to float.

Lastly, the double value 90.0 is added to the float value 2.0f for which Rule 2 applies, so after converting the 2.0f to 2.0 as double, the final result of 92.0 is stored in value.

In spite of the preceding sequence reading a bit like The Auctioneer’s Song, you should get the general idea.

# Casts in Assignment Statements

As you saw in example Ex2_05.cpp earlier in this chapter, you can cause an implicit cast by writing an expression on the right-hand side of an assignment that is of a different type to the variable on the