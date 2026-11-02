SPARK allows you to refine a postcondition in the body of a package to express it in terms of the private information available in the body. An implementation of Make_Circle that refines the postcondition in the specification using the Refined_Post aspect follows:

```
```ada
function Make_Circle (X, Y  : in Coordinate_Type;
                     Radius : in Radius_Type) return Circle
with Refined_Post =>
  (Make_Circle'Result.Center_X + Make_Circle'Result.Radius
     in Coordinate_Type and
   Make_Circle'Result.Center_X - Make_Circle'Result.Radius
     in Coordinate_Type and
   Make_Circle'Result.Center_Y + Make_Circle'Result.Radius
     in Coordinate_Type and
   Make_Circle'Result.Center_Y - Make_Circle'Result.Radius
     in Coordinate_Type)
is
  R : Radius_Type := Radius;
begin
  if R >= Coordinate_Type'Last - X then
    R := Coordinate_Type'Last - X;
  end if;
  if R >= X - Coordinate_Type'First then
    R := X - Coordinate_Type'First;
  end if;
  if R >= Coordinate_Type'Last - Y then
    R := Coordinate_Type'Last - Y;
  end if;
  if R >= Y - Coordinate_Type'First then
    R := Y - Coordinate_Type'First;
  end if;
  return (X, Y, R);
end Make_Circle;
```
```

The effect of Make_Circle is described in internal terms. The SPARK tools will generate verification conditions to show that the body of the subprogram honors the refined postcondition. In addition, the tools will generate a verification condition that shows that the precondition (if any), together with the refined postcondition, implies the publicly visible postcondition. This allows the refined postcondition to be stronger than the public postcondition (it can say more), but not weaker.

Callers of Make_Circle inside the package body will use the refined postcondition as it is written in terms of the private information of interest to them. The