```
Destructor mvalue1
Constructor mvalue2
Destructor mvalue2
Destructor mvalue1
```

You see with Destructor mvalue1 that mvalue1 is cleaned up twice. This is the result of negligence in our code. We have already mentioned this: when passing a parameter by value, the object is copied. So you get a second object, and as such, it of course also be cleaned up again—including the corresponding destructor call.

The object in question was not created by calling our constructor; you would have seen that. No, for the purpose of copy there is a special constructor, the copy constructor. You can define it yourself—and you should in this case, because only then will our output be correct. The copy constructor of a class is exactly the constructor that has the current class as a constant reference to the argument.

```
// https://gndbolt.org/z/sGan39a8z
struct MyValue {
    static int counter;
    int number;
    string name_;
    Explicit MyValue(string name) // as before
        : number_(++counter), name_(name) {
        cout << set(number) << " << Constructor " << name_ << "\n";
    }
    MyValue(const MyValue &orig) // new copy constructor
        : number_(++counter), name_(orig.name_ + "-Copy") {
        cout << set(number) << " << Copy Constructor " << name_ << "\n";
    }
    ~MyValue() { // as before
        cout << set(number) << " << Destructor " << name_ << "\n";
    }
```