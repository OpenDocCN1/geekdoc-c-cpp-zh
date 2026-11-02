We may also overload operators. Let us look at an example. Here is a record type for the coordinates of a point on a plane and two point variables:

```
```text
type Point is    -- Cartesian coordinates of a point
   record
      X_Coord : Float;
      Y_Coord : Float;
   end record;
```
```

```
```text
P1 : Point;
P2 : Point;
```
```

The following function, that overloads the <= operator, may be used to determine whether the Left point is the same distance from or closer to the origin than the Right point. Notice that we must enclose the operator symbols in double quotes.

```
```text
function "<=" (Left : in Point; Right : in Point) return Boolean is
   -- Returns True when Left is the same distance from
   -- or closer to the origin than Right
   Left_Squared  : Float;
   Right_Squared : Float;
begin
   Left_Squared := Left.X_Coord ** 2 + Left.Y_Coord ** 2;
   Right_Squared := Right.X_Coord ** 2 + Right.Y_Coord ** 2;
   return Left_Squared <= Right_Squared; -- Calls <= for Float numbers
end "<=";
```
```

Finally, some code that calls function "<= ". The call may be made as either an infix operator or a normal function call (prefix operator). When the function call syntax is used, the operator must be enclosed in double quotes.

```
```text
-- Function called as an infix operator
if P1 <= P2 then
   Put_Line ("P1 is not further from the origin than P2");
else
   Put_Line ("P1 is further from the origin than P2");
end if;
```
```

```
```text
-- "Normal" function call
if "<=" (P1, P2) then ...
```
```