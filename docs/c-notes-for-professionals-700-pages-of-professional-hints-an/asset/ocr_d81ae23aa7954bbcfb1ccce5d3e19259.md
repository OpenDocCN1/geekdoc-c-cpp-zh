A struct can declare everything a class can declare, with a few exceptions:

+   - A struct cannot declare a parameterless constructor. struct instance fields can be set via a parameterized constructor or individually after struct construction. Private members can only be initialized by the constructor.
+   - A struct cannot declare members as protected, since it is implicitly sealed.
+   - Struct fields can only be initialized if they are const or static.

# Section 94.2: Struct usage

**With constructor:**

```
```
Vector v1 = new Vector();
v1.X = 1;
v1.Y = 2;
v1.Z = 3;

Console.WriteLine("X = {0}, Y = {1}, Z = {2}",v1.X,v1.Y,v1.Z);
// Output X=1,Y=2,Z=3

Vector v1 = new Vector();
//v1.X is not assigned
v1.Y = 2;
v1.Z = 3;

Console.WriteLine("X = {0}, Y = {1}, Z = {2}",v1.X,v1.Y,v1.Z);
// Output X=0,Y=2,Z=3

Point point1 = new Point();
point1.x = 0.5;
point1.y = 0.6;

Point point2 = new Point(0.5, 0.6);
```
```

**Without constructor:**

```
```
Vector v1;
v1.Y = 2;
v1.Z = 3;

Console.WriteLine("X = {0}, Y = {1}, Z = {2}",v1.X,v1.Y,v1.Z);
//Output ERROR "Use of possibly unassigned field 'X'

Vector v1;
v1.X = 1;
v1.Y = 2;
v1.Z = 3;

Console.WriteLine("X = {0}, Y = {1}, Z = {2}",v1.X,v1.Y,v1.Z);
// Output X=1,Y=2,Z=3

Point point3;
point3.x = 0.5;
point3.y = 0.6;
```
```

If we use a struct with its constructor, we aren't going to have problems with unassigned field (each unassigned field has null value).