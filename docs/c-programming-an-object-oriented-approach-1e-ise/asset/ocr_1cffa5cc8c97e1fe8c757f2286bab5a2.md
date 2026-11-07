**Table 6.1  Function call**

| Group | Name | Operator | Expression | Pred | Assoc |
|---|---|---|---|---|---|
| postfix | function call | (...) | name (expr, ...) | 18 | → |

The return type is integer. There are two parameters of type integer. The body is a compound statement, as we have seen in the *main* function in previous chapters.

# Function Declaration

The **function declaration** (also called **function prototype**) is only the header of the function followed by a semicolon. The parameter names are optional; the types are required. The function declaration is used to show how the function should be called. It tells us what goes into the function and what comes out of it without defining the action performed by the function.

# EXAMPLE 6.2

The following shows the declaration of the function defined in Example 6.1. We have given two versions, with and without the names of the parameters.

```
int larger (int first, int second);        // With the names of the parameters
int larger (int);                          // Without the names of the parameters
```

# Function Call

A **function call** is a postfix expression that invokes a function to do its job. As with the expressions we learned in previous chapters, we need to know the syntax of this expression to call it. It belongs to the postfix group (like the postfix-increment and postfix-decrement expressions). Table 6.1 shows the position of the function call expression with relation to other expressions as discussed in Appendix C. Figure 6.3 shows more information about a function call expression.

If we compare the syntax of the function call with other postfix expressions, such as postfix-increment or postfix-decrement, we see that the operand in this case is a name (the name of the function). The operator is a pair of parentheses with a list of zero or more values. A function call can have a side effect, a return value, or both. If it has only a side effect, it needs to be used as an expression statement. If it returns a value (with or without a side effect), it can be used in any situation where a value is needed. Our larger function is called as *larger (value1, value2)*, as shown in the next example.

![](bbox=[0.38, 0.812, 0.624, 0.907])

**Figure 6.3**  Function call operator