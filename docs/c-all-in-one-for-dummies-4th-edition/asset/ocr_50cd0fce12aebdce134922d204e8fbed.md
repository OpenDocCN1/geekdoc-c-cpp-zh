functions without having to use pointers. The following function (found in the CompoundData example) shows how to return a structure:

```
```cpp
Point3D StartingPoint(float x) {
    Point3D start;
    start.x = x;
    start.y = x * 2;
    start.z = x * 3;
    return start;
}
```
```

This function relies on the Point3D struct defined in the preceding section, “Equating structures.” The following code shows how to use this function:

```
```cpp
int main() {
    Point3D MyPoint = StartingPoint(5.2);
    Point3D OtherPoint = StartingPoint(6.5);

    cout << MyPoint.x << endl;
    cout << MyPoint.y << endl;
    cout << MyPoint.z << endl;
    cout << endl;
    cout << OtherPoint.x << endl;
    cout << OtherPoint.y << endl;
    cout << OtherPoint.z << endl;
}
```
```

These cout statements produce the following output:

```
```
5.2
10.4
15.6

6.5
13
19.5
```
```

Note that StartingPoint() creates a local variable, start, of type Point3D. This variable isn’t a pointer or reference. The return is an unmodified start. Calling StartingPoint() copies the value of the returned structure into variables in main(), first MyPoint and then OtherPoint.