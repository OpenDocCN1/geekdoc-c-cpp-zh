```
```cpp
/* --------------------------------------- */
/* Default constructor */
/* Point::Point() */
{
    cout << "Constructing Point object, default: \\n";
    cout << " initializing to zero" << endl;
    xCoord = 0.0;
    yCoord = 0.0;
}
/* --------------------------------------- */
```
```

```
```cpp
/* --------------------------------------- */
/* This method returns the distance between two */
/* points in a plane. */
/* --------------------------------------- */
double Point::operator- (const Point& rhs) const
{
    double diffX, diffY, distance;
    diffX = rhs.xCoord - xCoord; // (x2-x1)
    diffY = rhs.yCoord - yCoord; // (y2-y1)
    distance = sqrt( pow(diffX,2) + pow(diffY, 2) );
    return distance;
}
/* --------------------------------------- */
```
```

```
```cpp
/* --------------------------------------- */
/* This method returns: */
/* true if two points are equal */
/* false if two points are not equal. */
/* * means that all corresponding data */
/* members are equal. */
/* --------------------------------------- */
bool Point::operator==(const Point& rhs) const
{
    if(rhs.xCoord == xCoord &&
       rhs.yCoord == yCoord )
    {
        return true;
    }
    else
    {
        return false;
    }
}
```
```

We have completed the definition of two binary operators for the Point class. These new operators are tested in program chapter3_3, provided below. We will use memory snapshots to illustrate the use of the overloaded operators as we trace the execution of the main program.

```
```cpp
/* --------------------------------------- */
/* Program chapter3_3 */
/* */
/* This program illustrates the use of the */
/* programmer-defined data type Point */
/* --------------------------------------- */
```
```