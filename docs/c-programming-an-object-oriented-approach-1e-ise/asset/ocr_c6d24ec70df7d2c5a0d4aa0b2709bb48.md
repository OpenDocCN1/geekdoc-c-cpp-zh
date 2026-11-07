# 3.2 **TYPE CONVERSION**

We have discussed some arithmetic data types, some operators, and some expressions, but we need to remember that operators operate on data. We now need to answer two questions before we can find the return value and side effect (if any) of an arithmetic operation.

+   1. What happens when we apply an arithmetic operator to nonatomic data types such as Boolean or character? For example, what happens if we add two Boolean data items or multiply two characters?
+   2. When using binary operators, what happens if the operands are of different types? What is the type of the return value?

To answer these questions, we need to discuss two different processes: *implicit type conversion* and *explicit type conversion*. In the first process, the data types are implicitly changed to answer the above questions; in the second process, we force **type conversion**.

The C++ language provides a tool to test the type of any expression as shown below:

```
`typedef (expression).name()`
```

The expression is the one for which we need to know its type. The tool returns an abbreviation of the type (i.e. for **int**, for **double**, and so on). To use this tool, we need to include the `<typeinfo>` header file.

# 3.2.1 Implicit Conversion

Every time we use an operation on a data type for which that operation is not defined, the C++ compiler performs **implicit type conversion** before giving us the result. Implicit type conversion means changing the type of the operand(s) to another type on which the operation can be applied. This is done in two steps: *implicit type promotion* (promoting the type of the operand to a larger size) and *implicit type change* (changing the type of one operand to the other's type in a binary operation to make them of the same type). We discuss each step separately.

> **Implicit type conversion is done automatically by the compiler.**

# Implicit Type Promotion

**Implicit type promotion** is automatically applied to any operand to make it suitable for an arithmetic operation. This is done for two reasons. First, the type of the operand is not suitable for an arithmetic operation (Boolean and character). Second, there is no arithmetic operator defined for the type (**short** and **float**) because if we apply an arithmetic operator on a **short** or **float** value, the result may not fit in a **short** or **float** (think about multiplying two data items). To avoid these problems, the compiler applies five rules for implicit type promotion, as shown in Table 3.2.

| Rule | Original Type | Promoted Type |
|---:|---|---|
| 1 | `bool` | `int` |
| 2 | `char` | `int` |
| 3 | `short` | `int` |
| 3 | `unsigned short` | `unsigned int` |
| 4 | `float` | `double` |