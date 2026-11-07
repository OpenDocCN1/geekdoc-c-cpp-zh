>, <, >= and <=, and the equality operators == and !=. Each decision tested precisely one condition. To test multiple conditions while making a decision, we performed these tests in separate statements or in nested if or if...else statements.

C++ provides logical operators that are used to form more complex conditions by combining simple conditions. The logical operators are && (logical AND), || (logical OR) and ! (logical NOT, also called logical negation).

# Logical AND (&&) Operator

Suppose that we wish to ensure that two conditions are both true before we choose a certain path of execution. In this case, we can use the && (logical AND) operator, as follows:

```
if ( gender == 1 && age >= 65 )
    ++seniorFemales;
```

This if statement contains two simple conditions. The condition gender == 1 is used here to determine whether a person is a female. The condition age >= 65 determines whether a person is a senior citizen. The simple condition to the left of the && operator evaluates first. If necessary, the simple condition to the right of the && operator evaluates next. As we’ll discuss shortly, the right side of a logical AND expression is evaluated only if the left side is true. The if statement then considers the combined condition.

```
gender == 1 && age >= 65
```

This condition is true if and only if both of the simple conditions are true. Finally, if this combined condition is indeed true, the statement in the if statement’s body increments the count of seniorFemales. If either (or both) of the simple conditions are false, then the program skips the incrementing and proceeds to the statement following the if. The preceding combined condition can be made more readable by adding redundant parentheses:

```
( gender == 1 ) && ( age >= 65 )
```

> **Common Programming Error 5.10**
> 
> Although 3 < x < 7 is a mathematically correct condition, it does not evaluate as you might expect in C++. Use ( 3 < x && x < 7 ) to get the proper evaluation in C++.

Figure 5.15 summarizes the && operator. The table shows all four possible combinations of false and true values for expression1 and expression2. Such tables are often called truth tables. C++ evaluates to false or true all expressions that include relational operators, equality operators and/or logical operators.

| expression1 | expression2 | expression1 && expression2 |
|---|---|---|
| false | false | false |
| false | true | false |
| true | false | false |
| true | true | true |

Fig. 5.15 | && (logical AND) operator truth table.