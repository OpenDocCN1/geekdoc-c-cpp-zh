And, voilà — you have a singleton class! Here’s how it works: Whenever you need the single instance of the class, you don’t try to create it. (You’ll get a compile error! Yes, the compiler itself won’t let you do it.) Instead, you call the static method.

![](bbox=[0.163, 0.165, 0.227, 0.232])

The singleton pattern won’t prevent different programs on the same machine from creating multiple instances of the class (one for each application). This pattern works only within a single application. Consequently, if you need to ensure that a class isn’t instantiated more than once on a machine as a whole, you need to use some form of globally unique identifier at the operating system level, a topic that’s outside the scope of this book.

# Creating a singleton pattern class

It’s time to see the singleton pattern at work. Listing 4-1 from the Singleton example shows how to create such a class:

# LISTING 4-1 — Creating a Singleton Class

```
```cpp
class Planet {
private:
    static Planet *inst;
    Planet() {}
    ~Planet() {}
public:
    static Planet *GetInstance();
};

Planet *Planet::inst = 0;

Planet *Planet::GetInstance() {
    if (inst == 0) {
        inst = new Planet();
    }
    return inst;
}

int main() {
    Planet *MyPlanet = Planet::GetInstance();
    cout << "MyPlanet address: " << MyPlanet << endl;

    Planet *MyPlanet2 = Planet::GetInstance();
    cout << "MyPlanet2 address: " << MyPlanet2 << endl;
    return 0;
}
```
```