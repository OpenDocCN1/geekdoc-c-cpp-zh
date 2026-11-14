+   - Boolean:
+     * Comparison: <=, !=, ...
+     * Logic: && and ||
+   - Bitwise: ~, << and >>, &, ^, and |
+   - Assignment: =, +=, ...
+   - Program flow: function call, ?:, and ,
+   - Memory handling: new and delete
+   - Access: ., ->, [ ], *, ...
+   - Type handling: dynamic_cast, typedef, sizeof, alignof ...
+   - Error handling: throw

This section will give an overview of the operators. Some operators are better described elsewhere in the context of the appropriate language feature; e.g., scope resolution is best explained together with namespaces. Most operators can be overloaded for user types; i.e., we can decide which calculations are performed when one or multiple arguments in an expression are our types.

At the end of this section (Table 1-8), you will find a concise table of operator precedence. It might be a good idea to print or copy this page and pin it next to your monitor; many people do so and almost nobody knows the entire priority list by heart. Neither should you hesitate to put parentheses around sub-expressions if you are uncertain about the priorities or if you believe it will be more understandable for other programmers working with your sources. If you ask your compiler to be pedantic, it often takes this job too seriously and prompts you to add surplus parentheses assuming you are overwhelmed by the precedence rules. In Section C.2, we will give you a complete list of all operators with brief descriptions and references.

# 1.3.1 Arithmetic Operators

Table 1-2 lists the arithmetic operators available in C++. We have sorted them by their priorities, but let us look at them one by one.

The first kinds of operations are increment and decrement. These operations can be used to increase or decrease a number by 1. As they change the value of the number, they only make sense for variables and not for temporary results, for instance:

```
int i = 3;
+++; // i is now 4
const int j = 5;
+++j; // error, j is constant
(3 + 5)++; // error, 3 + 5 is only a temporary
```

In short, the increment and decrement operations need something that is modifiable and addressable. The technical term for an addressable data item is Lvalue (see Definition C-1