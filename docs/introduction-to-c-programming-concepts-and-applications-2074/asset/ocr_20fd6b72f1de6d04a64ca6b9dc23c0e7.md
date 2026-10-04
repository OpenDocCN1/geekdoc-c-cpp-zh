If you had also wanted to be able to define an integer times a lightbulb, you'd have had to define a separate operator (e). Then, you could multiply 2 times a lightbulb (37).

```
lightbulb operator *(int increase_factor, lightbulb bulb) {
    lightbulb ans;
    ans.watts_used = bulb.watts_used * increase_factor;
    ans.lumens = bulb.lumens * increase_factor;
    ans.temperature = bulb.temperature;
    return ans;
}

int main() {
    lightbulb bulba, bulb b;
    bulb b = 2 * bulba;
    cout << bulb b.watts_used << " " << bulb b.lumens << " " << bulb b.temperature << endl;
}
```

Also, if you had not made the member elements public, then you couldn't have written the multiplication operator. It would not have been possible to access private member variables of the object from outside the function. Instead, you'd have had a compilation error.

So, it's more common for operators to be defined within a class. That way, you can access all the elements of the class without accessors and mutators.

In Program 17_10, the member values have been made private, but a print_vals function has been added that prints all the member variables to the console, separated by spaces (f). This will let you print the values of the member variables from outside the class.

The main routine is set up in a very similar way as before, with the only difference being that you're calling the print_vals function because the member variables of the lightbulb class are private (g).

```
// Program 17_10
// Operator example - defining inside a class
#include<iostream>
using namespace std;

class lightbulb {
    int watts_used;
    int lumens;
    int temperature;

public:
    lightbulb() {
        watts_used = 60;
        lumens = 900;
        temperature = 2700;
    }

    lightbulb operator *(int increase_factor) {
        lightbulb ans;
        ans.watts_used = watts_used * increase_factor;
        ans.lumens = lumens * increase_factor;
        ans.temperature = temperature;
        return ans;
    }

    void print_vals() {
        cout << watts_used << " " << lumens << " " << temperature << endl;
    }
};

int main() {
    lightbulb bulba, bulb b;
    bulb b = bulba * 2;
    bulb b.print_vals();
}
```