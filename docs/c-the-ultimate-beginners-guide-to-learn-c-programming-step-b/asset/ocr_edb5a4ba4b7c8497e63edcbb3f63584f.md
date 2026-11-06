```
}
}
}
```

The code gives the following output:

```
x greater than 10
The value of x is : 15
```

The *if* condition evaluated to a false, hence the statement within the *else* block has been executed. You must have noticed that part outside the two blocks has been executed in both cases. That is what happens.

# else...if Statement

In some cases, we may be in need of checking a multiple number of conditions. In such a case, we can use the *else if* statement. It takes the syntax given below:

```
if(boolean_expression a) {
    /* Runs if the boolean expression a is true */
}
else if( boolean_expression b) {
    /* Runs if the boolean expression b is true */
}
else if( boolean_expression c) {
    /* Runs if the boolean expression c is true */
} else {
    /* to run if none of above conditions is true */
}
```

Here is an example:

```
using System;

namespace DecisionMaking {
    class ElseIfStatement {
        static void Main(string[] args) {
```