What would be the output of the following code? (Be careful to look at how each function is defined and exactly what is called in each function call.)

```
#include<iostream>
#include<string>
using namespace std;

class airplane {
public:
    float weight;
    string name;

    void print_name() {
        cout << "For the airplane " << name << ",";
    }
    virtual void print_info() {
        cout << "weight is: " << weight << endl;
    }
};

class jet : public airplane {
public:
    int numengines;

    void print_name() {
        cout << "For the jet " << name << ",";
    }

    void print_info() {
        cout << "weight is: " << weight << " " and there are " << numengines << " engines"<< endl;
    }
};

void print_plane_data(airplane &a) {
    a.print_name();
    a.print_info();
}

void print_plane_data2(airplane &a) {
    airplane privateplane;
    jet commercialplane;
    privateplane.name = "A123";
    privateplane.weight = 3000.0;
    commercialplane.name = "B456";
    commercialplane.weight = 10000.0;
    commercialplane.numengines = 4;
    privateplane.print_name();
    privateplane.print_info();
    commercialplane.print_name();
    commercialplane.print_info();
    print_plane_data(commercialplane);
    print_plane_data2(commercialplane);
}

int main() {
```

Lecture 20 | Object-Oriented Programming with Polymorphism