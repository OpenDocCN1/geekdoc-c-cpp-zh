The function below initializes the fields of the `struct`:

```
void initialize (Elevator *e) {
  e->floorSelected = 0;
  e->floorNumber = 0;
}
```

We create another function to select the floor:

```
void selectFloor(Elevator *e, int floor) {
  e->floorSelected = floor;
}
```

We can see that everywhere we want to use the `Elevator` structure, we must dereference a pointer. We are forced to use pointers rather than passing the `Elevator` struct by value because we are modifying variables outside the scope of the function. Passing the `Elevator` struct by value would simply make a local variable!

# C++ Structs

Let's see how we might solve the same problem in C++.

We know that a type has characteristics and behavior. C++ implements a type as an extended `struct` that contains function declarations as well as data declarations. Collectively, these are called members:

+   - function members
+   - data members

Data members represent the state (characteristics) of the variable, and function members represent the operations (behavior) that can be performed on the data members.