![](bbox=[0.13, 0.1, 0.86, 0.5])

values. A string type is a composite type. A string value is composed of characters. We can access and use the individual characters making up a string. An atomic type is one whose values cannot be decomposed into smaller values. A character type is an atomic type. A character value cannot be decomposed into smaller values. Integers and real numbers are also atomic types.

# ### 2.3.1 Scalar Types

A scalar type is an atomic type with the additional property of ordering. We can compare scalar values with the relational operators (<, <=, >, and >=). Characters, integers, and real numbers are all scalar types.

One of the principles of object-oriented programming is the development of classes that accurately model the objects in the problem. We can apply this same approach to the design of our scalar types. By using scalar types that more accurately reflect the nature of the data in a problem we are solving, we can write better programs. One research study on the nature of costly software faults indicates that poor models of scalar quantities were responsible for nearly 90 percent of the errors in the cases studied (Eisenstadt, 1997; McCormick, 1997). Ada allows programmers to define their own scalar data types that accurately model the scalar values in the problem domain.