You can also create more than one object of a class within a single statement. The following code snippet shows the creation of multiple objects of a class:

```
```cpp
#include<iostream.h>

class Student
{
    // body of a class
};
/* Creating more than one instance of a class */
int main()
{
    Student object1, object2, object3, object4;
    return 0;
}
```
```

Another way to create more than one object of a class is shown in the following code snippet:

```
```cpp
#include<iostream.h>

/* Creating multiple instances of a class */
int main()
{
class Student
{
    // body of a class
} object1, object2, object3, object4;
return 0;
}
```
```

Both the preceding code snippets perform the same task, that is creating multiple objects object1, object2, object3, and object4 of the Student class.

You can also create pointer type objects. A pointer is a variable that stores the memory address of any variable. A pointer object is initialized with the help of the new operator and is destroyed with the delete operator. The following code snippet shows the allocation and de-allocation of a pointer object of a class using the new and delete operators, respectively:

```
```cpp
#include<iostream.h>

class Student
{
    // body of a class
};
```
```