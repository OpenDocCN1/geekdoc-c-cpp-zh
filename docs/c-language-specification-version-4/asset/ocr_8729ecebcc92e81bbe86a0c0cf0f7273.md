meaning of a name is always the same within a given block, switch block, for-, foreach- or using-statement, or anonymous function.

The example

```
class Test
{
    double x;
    void F(bool b) {
        x = 1.0;
        if (b) {
            int x;
            x = 1;
        }
    }
}
```

results in a compile-time error because x refers to different entities within the outer block (the extent of which includes the nested block in the if statement). In contrast, the example

```
class Test
{
    double x;
    void F(bool b) {
        if (b) {
            x = 1.0;
        }
        else {
            int x;
            x = 1;
        }
    }
}
```

is permitted because the name x is never used in the outer block.

Note that the rule of invariant meaning applies only to simple names. It is perfectly valid for the same identifier to have one meaning as a simple name and another meaning as right operand of a member access (§7.6.4). For example:

```
struct Point
{
    int x, y;
    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```

The example above illustrates a common pattern of using the names of fields as parameter names in an instance constructor. In the example, the simple names x and y refer to the parameters, but that does not prevent the member access expressions this.x and this.y from accessing the fields.

# 7.6.3 Parenthesized expressions

A parenthesized-expression consists of an expression enclosed in parentheses.

```
parenthesized-expression:
    ( expression )
```