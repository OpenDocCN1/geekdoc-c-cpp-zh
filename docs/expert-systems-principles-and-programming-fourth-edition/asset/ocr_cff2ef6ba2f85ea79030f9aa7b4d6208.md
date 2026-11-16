this expression in prefix form it will be useful to start by, 4. In general, any CLIPS expression to be evaluated can be entered at the top level. Most functions, such as the addition function, have a return value. This return value can be an integer, a float, a symbol, a string, or even a multifield value. Other functions, such as the facts and agenda commands, have no return value. Functions without a return value typically have what is called a side effect. The side effect of the facts command is to list the facts in the fact list.

The other arithmetic functions also work at the top level. The following output demonstrates the evaluation of some other expressions:

```
CLIPS> (+ 2 3)
5
CLIPS> (- 2 3)
-1
CLIPS> (* 2 3)
```