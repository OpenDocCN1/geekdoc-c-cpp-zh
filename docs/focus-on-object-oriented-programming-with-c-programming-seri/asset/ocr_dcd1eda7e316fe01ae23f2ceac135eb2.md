# Multiple Inheritance Homework

+   1. As part of a military video game, a designer has created a vehicle class hierarchy. The base class is `Vehicle`, and it has `AirVehicle`, `LandVehicle`, and `SeaVehicle` as derived classes. The class `SeaPlane` inherits from both `AirVehicle` and `SeaVehicle`. Specifically, what **design issues** had to be considered in developing the `SeaPlane` class?

+   2. What is the distinction between an **abstract base class** and a **virtual base class**?

+   3. Give the output for the following program without executing the code.

```
class A {
    protected:
        int fa;
    public:
        A(int va = 0) : fa(va) {
            cout << "A constructor " << endl;
        }
        A(const A& va) : fa(va.fa) {
            cout << "A copy constructor " << endl;
        }
        ~A() {
            cout << "A destructor" << endl;
        }
        A& operator=(const A& va) {
            cout << "A = operator" << endl;
            fa = va.fa;
            return *this;
        }
};
```