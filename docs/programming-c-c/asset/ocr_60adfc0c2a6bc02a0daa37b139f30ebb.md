```
struct Point {
    int x = 0; // COMPILER ERROR: cannot initialize members here
    int y = 0; // COMPILER ERROR: cannot initialize members here
};
```

The reason for above error is simple, when a data type is declared, no memory is allocated for it. Memory is allocated only when variables are created.

Structure members can be initialized using curly braces '{}'.

For example, following is a valid initialization.

```
struct Point {
    int x, y;
}
int main() {
    // A valid initialization. member x gets value 0 and y
    // gets value 1. The order of declaration is followed.
    struct Point p1 = {0, 1};
}
```

# Following one is the other example.

Like a variable of any other data type, structure variable can also be initialized at compile time.

```
struct Patient {
    float height;
    int weight;
    int age;
}
struct Patient p1 = {180.75,73,23};//initialization
```