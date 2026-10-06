# 4.3 Constructor and Destructor — 125

has a constructor, the compiler will automatically insert the calling code on the constructor at the place where the new object is defined. So we often say the "constructor is automatically called where the object is defined".

If a class has no constructor, the compiler will automatically generate a default constructor – with no parameters and doing nothing. If a class has defined a constructor (with parameters or not), the compiler will not generate any other constructor.

In the Clock class, there is no constructor. Thus the compiler will generate a default constructor for the class, while the constructor does nothing. So why do we need a constructor that does nothing? So why do we need a constructor? That's because calling the constructor of an object during its creation is a necessary behavior in a C++ program. If the programmer defines a proper constructor, an object of class Clock will receive an initial time value during its creation. Now we modify class Clock as follows:

```
class Clock {
public:
    Clock(int NewH, int NewM, int NewS); //constructor
    void SetTime(int NewH, int NewM, int NewS);
private:
    int Hour, Minute, Second;
};
```

Implementation of constructor:

```
Clock::Clock(int NewH, int NewM, int NewS) {
    Hour= NewH;
    Minute= NewM;
    Second= NewS;
}
```

Let's see what the constructor does when creating the object:

```
int main() {
    Clock c (0,0,0);
    c.ShowTime();
    c.SetTime(8,30,30);
}
```

When creating object c, the constructor is called implicitly and the actual parameters will be used as the initial values.