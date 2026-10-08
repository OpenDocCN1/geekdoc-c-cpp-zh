![](bbox=[0.248, 0.75, 0.822, 0.235])

# 13.1.2 Accessing Struct Members

Accessing struct members involves the dot (.) operator followed by the member's name. For example:

```
#include <stdio.h>

struct Person {
    char name[10];
    int age;
    float height;
};

int main() {
    // Declare and initialize struct variables
    struct Person person1 = {"Sarah", 20, 1.65f};
    struct Person person2 = {"Adam", 25, 1.80f};

    // Print first struct data
    printf("Name: %s\n", person1.name);
    printf("Age: %d\n", person1.age);
    printf("Height: %f\n", person1.height);

    // Print second struct data
    printf("Name: %s\n", person2.name);
    printf("Age: %d\n", person2.age);
    printf("Height: %f\n", person2.height);

    return 0;
}
```

Here, we access the name, age, age, and height members of the person struct and assign values to them.