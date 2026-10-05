# 13 • Structures and Unions 387

```
return &v[i]; /* If the code is found, the function
terminates and the address of that structure is returned. */
}
```

```
return nullptr; /* If the code reaches that point, it means that the
product is not found and the function returns nullptr. */
```

**C.13.6** Define the structure Coord with the coordinates of a point (e.g., x and y). Define the
structure type Rectangle with two structures of type Coord (e.g., Point_A and Point_B).
Write a function that takes parameters as the two endpoints of a rectangle. Each endpoint
be a structure of type Coord. The function should calculate and return the area of the rectangle.
Write a program that uses this Rectangle to read the coordinates of a rectangle's diagonal and uses
function to display its area.

```
#include <iostream>
using std::cout;
using std::cin;
```

```
struct Coord
{
    double x;
    double y;
};
```

```
struct Rectangle
{
    Coord point_A; // First diagonal point.
    Coord point_B; // Second diagonal point.
};
```

```
double rect_area(const Coord *c1, const Coord *c2);
```

```
int main()
{
    Rectangle rect;

    cout << "Enter the x and y coords of the first point: ";
    cin >> rect.point_A.x >> rect.point_A.y;

    cout << "Enter the x and y coords of the second point: ";
    cin >> rect.point_B.x >> rect.point_B.y;

    cout << "Area:" << rect_area(&rect.point_A, &rect.point_B) << '\\n';
    return 0;
}
```

```
double rect_area(const Coord *c1, const Coord *c2)
{
    double base, height;

    if(c1->x > c2->x)
        base = c1->x - c2->x;
    else
        base = c2->x - c1->x;
}
```