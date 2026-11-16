We can now modify our `Elevator` class as follows:

```
class Elevator {
    private:
        int floorSelected;
        int floorNumber;
    public:
        Elevator() {
            floorSelected = 0;
            floorNumber = 0;
        }
        Elevator (int selected, int number) {
            floorSelected = selected;
            floorNumber = number;
        }
        void selectFloor(int floor) {
            floorSelected = floor;
        }
        void go() {
        }
};

int main() {
    Elevator a;
    Elevator b(7, 2);

    a.selectFloor(7);
    a.go();
    return 0;
}
```

Remember that the constructor with no arguments is again called the default constructor and is called by the compiler when no arguments are available. Calling a constructor with arguments is simply a matter of adding an argument list after the object name.

Note: once you create a constructor taking arguments, you must also explicitly declare and define the default constructor if you want to declare any class instances that would employ the default constructor. Remember, the constructors that would employ the default constructor. Remainder, the constructors also automatically perform certain other initializations.

Constructors are pretty amazing when you think about it. Whoever writes language compilers (for C, C++, Java, etc.) must execute the equivalent of a constructor when the user defines a variable. If you define an `int`, for example, somewhere there's a constructor allocating 4 bytes of memory for it. If we can write our own constructors, we can start to take over some of the tasks of a