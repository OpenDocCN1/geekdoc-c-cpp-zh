# 7.09 Short Answer Poll – Correct Answer

Using pencil and paper, write an ARRAY statement to define a temporary lookup table named Country with three elements, each two characters long. Initialize the elements to AU, NZ, and US. Refer to the syntax below.

```
ARRAY array-name{subscript} $<length>
<array-elements> <initial-value-list>;
```

```
array Country{3} $ 2 temporary_ ('AU', 'NZ', 'US');
```