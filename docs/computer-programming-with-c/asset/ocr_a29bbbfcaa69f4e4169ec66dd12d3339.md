# # Chapter 3 | Operators and Type Casting

# ## 3.1 Overview

C/C++ has a dedicated set of special characters which can be used to perform operations on the data items. Each of these special characters represent as a specific operation to be performed to the compiler. For example, a symbol + is used to perform addition, and the symbol * is used to perform multiplication and so on. There are two properties associated with each of the operators so as to define the approach used for its evaluation:

+   1. Priority of the operator
+   2. Associativity of the operator

A **Priority** of the operator is a precedence associated with the operator. Every Operator is assigned a specific priority using which an operator must be resolved, so as to generate the result of the expression. Assigning priority to an operator helps in avoiding the **ambiguity** that may arise in the order of evaluation when a given expression consists of multiple operators. So as to understand the exact meaning of operator precedence, let us consider the expression below:

```
int p=10,q=5,r=2,s;
s=p+q*r;
```

After substituting the values of variables p, q, and r the expression that calculates the value of variable s can be rewritten as shown below:

```
s=10+5*2;
```

In the absence of operator precedence, the compiler will have two different options to generate the result of the above expression.

# ### 3.1.1 Option 1: Perform addition before multiplication (wrong option)

First perform the addition of two numbers 10 and 5, and then perform multiplication of the result with value 2. Hence, we will get the result of the expression as 30 as shown in Figure 3.1. Note that, this is a case where, we have evaluated the result of ‘addition’ before evaluating the result of ‘multiplication’. The order of evaluation is as shown in Figure 3.1.