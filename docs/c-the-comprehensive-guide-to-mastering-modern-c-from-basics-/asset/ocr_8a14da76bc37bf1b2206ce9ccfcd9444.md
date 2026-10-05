greater than or equal to >=, less than or equal to <=, equal to ==, and not equal to !=.

+   - number > 100 && number < 200
With the Boolean AND &&, you check if both expressions are true.

+   - x < 0 || y < 0
The Boolean OR || fits when at least one condition should be met.

+   - x == y+1
You can perform arithmetic calculations before a comparison.

+   - (x > 0 || y > 0) && (maxx < 100 || maxy < 100)
Parenthesize complex expressions if necessary.

+   - !(x < y)
With the operator ! for not, you negate a Boolean expression; true becomes false and vice versa.

With this repertoire, you are already well-equipped for the if condition.

There is another useful form of the if statement, which you can also see in Figure 8.2:

if( Condition ) Statement1 else Statement2

This implements: “Execute either Statement1 or Statement2.” The Statement2 is called the else branch of the if statement. Thus,

```
if(x > 1) {
    std::cout << "x is greater than 1" << std::endl;
}
if(!(x > 1)) { // test alternative
```