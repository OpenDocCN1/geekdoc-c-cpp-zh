# Display 3.9 A Global Named Constant (part of 2)

```
1 //Computes the area of a circle and the volume of a sphere.
2 //Uses the same radius for both calculations.
3 #include <iostream>
4 #include <cmath>
5 using namespace std;

6 const double PI = 3.14159;

7 double area(double radius);
8 //Returns the area of a circle with the specified radius.

9 double volume(double radius);
10 //Returns the volume of a sphere with the specified radius.

11 int main()
12 {
13     double radiusOfBoth, areaOfCircle, volumeOfSphere;

14     cout << "Enter a radius to use for both a circle\n"
15         << "and a sphere (in inches): ";
16     cin >> radiusOfBoth;

17     areaOfCircle = area(radiusOfBoth);
18     volumeOfSphere = volume(radiusOfBoth);

19     cout << "Radius = " << radiusOfBoth << " inches\n"
20         << "Area of circle = " << areaOfCircle
21         << " square inches\n"
22         << "Volume of sphere = " << volumeOfSphere
23         << " cubic inches";

24     return 0;
25 }
26 
27 double area(double radius)
28 {
29     return (PI * pow(radius, 2));
30 }

31 double volume(double radius)
32 {
33     return ((4.0/3.0) * PI * pow(radius, 3));
34 }
```