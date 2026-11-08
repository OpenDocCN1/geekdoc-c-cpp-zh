# Designated initialization

```
```cpp
struct Point2D{
    int x;
    int y;
};

class Point3D{
public:
    int x;
    int y;
    int z;
};

int main(){

    Point2D point2D {.x = 1, .y = 2};
    // Point2D point2D {.y = 2, .x = 1};          // error
    Point3D point3D {.x = 1, .y = 2, .z = 2};
    // Point3D point3D {.x = 1, .z = 2}           // {1, 0, 2}

    std::cout << "point2D: " << point2D.x << " " << point2D.y << "\n";
    std::cout << "point3D: " << point3D.x << " " << point3D.y << " " << point3D.z
              << "\n";

}
```
```

The arguments for the instances of Point2 and Point3D are explicitly named. The output of the program is identical to the output of the previous one. The commented-out lines 16 and 18 are quite interesting. Line 16 would give an error because the order of the designators does not match the declaration order of the data members. As for line 18, the designator for y is missing. In this case, y is initialized to 0, such as when using braced initialization list {1, 0, 2}.

# 3.2.3 constexpr and constinit

The new `constexpr` specifier added in C++20 creates an immediate function. For an immediate function, each invocation of the function must produce a compile-time constant expression. An immediate function is implicitly a constexpr function but not necessarily the other way around.