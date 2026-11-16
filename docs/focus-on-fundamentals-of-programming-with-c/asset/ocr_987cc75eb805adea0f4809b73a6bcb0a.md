# Nesting Structures

C allows us to nest structures, i.e., to define structures within other structures. For example, suppose we want to keep track of the dimensions of various rooms in a house. We can first define a Distance struct as follows:

```
typedef struct {
    int feet;
    float inches;
} Distance;
```

We can now define a Room struct that contains Distance variables as its components:

```
typedef struct {
    Distance length; width;
} Room;
```

We now initialize each of the fields of the struct variables:

```
int main(void) {
    Room bedroom, kitchen;

    bedroom.length.feet = 25;
    bedroom.length.inches = 6;
    bedroom.width.feet = 20;
    bedroom.width.inches = 8.5;

    kitchen.length.feet = 15;
    kitchen.length.inches = 3.25;
    kitchen.width.feet = 10;
    kitchen.width.inches = 6;

    return 0;
}
```