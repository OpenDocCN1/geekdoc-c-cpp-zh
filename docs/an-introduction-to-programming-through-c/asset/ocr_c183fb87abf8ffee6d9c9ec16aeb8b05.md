# 15.1.5  Linked structures

Here is a trickier example.

```
```cpp
struct Student{
    int rollno;
    Student* bestFriend;
};
```
```

The intention of the definition should be clear; in each student structure, we wish to store a pointer to the best friend of that student. But for this we have had to use the name Student inside its own definition! However it does not cause a problem. A pointer to a struct needs the same amount of memory no matter what is inside the struct. Thus using the new definition we can allocate memory for a Student object easily: we just need to allocate whatever is needed for an int and for a pointer.¹

We can use this to link students to their best friends as in the program below.

```
```cpp
int main(){
    Student s1, s2, s3;
    s1.rollno = 1;
    s2.rollno = 2;
    s3.rollno = 3;
    s1.bestFriend = &s2;
    s2.bestFriend = &s3;
    s3.bestFriend = &s2;

    cout << s1.bestFriend->rollno << endl;
    cout << s1.bestFriend->bestFriend->rollno << endl;
}
```
```

Thus after creating instances s1, s2, s3, we set them respectively to have roll numbers 1, 2, 3. Then we set s1’s best friend to be s2, s2’s best friend to be s3, and s3’s best friend to be also s2. Thus the first print statement will print 2, while the second will print 3.

We will see detailed examples of such linked structures later.

# 15.2  Structures and functions

It is possible to pass structure variables to functions. The key point to be noted is that the name of a structure variable denotes the content of the associated memory, like ordinary numerical variable names, and unlike the name of an array, which denotes the address of the associated memory. Thus structures behave like ordinary variables as far as passing to functions and being returned from functions.

> ¹ The following definition is not allowed, of course:
> 
> ```cpp
> struct Student{ int rollno; Student friend; };
> ```
> 
> This will require a Student object to contain an internal Student object, and the internal Student object to contain a Student object, and so on. In other words we are defining an infinite object! This is not allowed.