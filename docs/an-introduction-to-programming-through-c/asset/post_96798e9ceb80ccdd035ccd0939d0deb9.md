
## 15.1.3  Pointers to Structures and ->

The “address of” operator & defined in Section 9.8.1 and the dereferencing operator * defined in Section 9.8.3 work as you might expect with structures. Here is an example. Assuming the definition of Circle as above, we might write

```
Circle c1={{1,2},3}, *cptr;
cptr = &c1;
(*cptr).radius = 5;
```

The first statement declares cptr to be of type Circle*, i.e. pointer to Circles. The second statement stores the address of c1 in cptr, which we often refer to as “sets cptr to point to c1”. The third statement dereferences it so that *cptr really means c1, and then the radius member of this is set to 5.

C++ provides the operator -> where x->y means (*x).y. Hence (*cptr).radius could instead be written as cptr->radius, which you will agree is easier to read.

## 15.1.4  Pointers as structure members

It is possible to have pointers as members of a struct. For example, we might have an alternate way to represent structures as follows.

```
struct Circle2{
    double radius;
    Point *cptr;
};
```

where Point is as before. Thus we could write

```
Point p1 = {10.0,20.0};
Circle2 cc1, cc2;
cc1.radius = 5;
cc2.radius = 6;
cc1.cptr = &p1;
cc2.cptr = &p1;
```

Thus we have created cc1 and cc2 to be circles of radii 5, 6 respectively, both centered at the point p1. Say we wanted to get the x coordinate of the center. For this we would write cc1.cptr->x, which would evaluate to 10.0 as you would expect. Note further that if you write

```
cc2.cptr->y = 25;
```

it would change the y coordinate of p1, and hence of the center of both the circles.

## 15.1.5  Linked structures

Here is a trickier example.

```cpp
struct Student{
    int rollno;
    Student* bestFriend;
};
```

The intention of the definition should be clear; in each student structure, we wish to store a pointer to the best friend of that student. But for this we have had to use the name Student inside its own definition! However it does not cause a problem. A pointer to a struct needs the same amount of memory no matter what is inside the struct. Thus using the new definition we can allocate memory for a Student object easily: we just need to allocate whatever is needed for an int and for a pointer.¹

We can use this to link students to their best friends as in the program below.

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

Thus after creating instances s1, s2, s3, we set them respectively to have roll numbers 1, 2, 3. Then we set s1’s best friend to be s2, s2’s best friend to be s3, and s3’s best friend to be also s2. Thus the first print statement will print 2, while the second will print 3.

We will see detailed examples of such linked structures later.

## 15.2  Structures and functions

It is possible to pass structure variables to functions. The key point to be noted is that the name of a structure variable denotes the content of the associated memory, like ordinary numerical variable names, and unlike the name of an array, which denotes the address of the associated memory. Thus structures behave like ordinary variables as far as passing to functions and being returned from functions.

> ¹ The following definition is not allowed, of course:
>
> ```cpp
> struct Student{ int rollno; Student friend; };
> ```
>
> This will require a Student object to contain an internal Student object, and the internal Student object to contain a Student object, and so on. In other words we are defining an infinite object! This is not allowed.

We first consider an example for our Point structure as defined above. The function below returns a Point that is the midpoint of the line joining two given points. It is followed by a main program that uses it.

```
// Point as defined earlier
Point midpoint(Point a, Point b){
    Point mp;
    mp.x = (a.x+b.x)/2;
    mp.y = (a.y+b.y)/2;
    return mp;
}
```

```
int main(){
    Point p1 = {0.0, 0.0}, p2 = {100.0, 200.0}, p3;
    p3 = midpoint(p1, p2);
    cout << midpoint(midpoint(p1,p2), p2).x << endl;
}
```

The function calls above execute essentially as per the description in Section 9.1. Consider the call midpoint(p1,p2). First, an activation frame is created. Then the values of the arguments p1,p2 are copied to the corresponding parameters a,b in the activation frame. Then the local variable mp is created. Then its members x,y respectively are set to the averages of the corresponding members of a,b. Thus mp.x, mp.y will get the values 50, 100. Then, mp will be returned. Note that returning a structure means copying its value to the main program. To receive this value, in the main program a temporary variable of type Point will be created. After the returned value is placed in the temporary variable, we are free to do whatever we like with it. In the second statement of the main program, we are merely copying the value of the temporary variable to the variable p3. However, we can do essentially everything with this variable that can be done using any variable. We see this in the last statement. The call midpoint(p1,p2) will return the point (50,100). The temporary variable which holds this is then passed as an argument to another call to midpoint. This call will return the midpoint of the points (50,100) and (100,200). Thus it will return the point (75,150). This point will be stored in a temporary structure, and finally we take its x member, which gets printed. Thus 75 will get printed.²

We can also use call by reference (Section 9.7). Suppose we want to shift a given point by some amount dx,dy in the x,y directions respectively. Then the following function is natural to write.

```
void move(Point &p, double dx, double dy){
    p.x += dx;
    p.y += dy;
}
```

Notice that we are passing the first argument, the point, by reference. Thus the point p in the body will be deemed to refer to same variable that is passed as the first argument in the calling program. Thus the x,y members of that variable will get modified.

> ²Note that temporary variables are created also with ordinary numerical variables. For example, when you write a = z + sin(x)*y, temporary variables will be created to hold the value of sin(x).

## 15.2.1  const reference parameters

It is desirable to pass structures to functions by reference even if we don’t want them modified. This is because when passed by value, the entire structure must be copied. Copying takes time. This can be a significant overhead for a large structure such as Book defined above.³ However, some subtle issues arise when passing parameters by reference. For example, suppose we passed the parameters to our midpoint function by reference as follows.

```
Point midpoint(Point const &a, Point const &b){
    Point mp;
    mp.x = (a.x+b.x)/2;  mp.y = (a.y+b.y)/2;
    return mp;
}
```

We have not only made the parameters be reference parameters, but also declared them const, i.e. asserted that they will not change during execution. Since the function midpoint does not modify the points a,b, it is clearly a good idea to declare our intent explicitly and mark the parameters const. Indeed, if a parameter is marked const, then it improves readability because a human reader can tell at a glance that it will not be modified.

However, the const keyword serves another important purpose. Suppose we did not mark the parameters const. Then the first call in our main program above, midpoint(p1,p2) would be compiled fine, but for the call midpoint(midpoint(p1,p2),p2) the compiler would flag an error! If a parameter is a non-const reference parameter, the compiler assumes that you wish to modify it in the code. But if you wish to modify it, then the corresponding argument must not be a compiler generated temporary structure which is considered to be a constant. So if you do indeed pass a temporary structure such as midpoint(p1,p2), the compiler suspects that you have perhaps made a programming error (over paranoidly, perhaps) and tells you so. But if the parameter is marked const, then the compiler knows that you are passing the parameter by reference only to avoid copying.

## 15.2.2  Passing pointers to structures

Note finally that you can pass structures to functions using a pointer and then dereference the pointer in the body to access the members of the structure. But it is considered better to use references (const if appropriate).

## 15.3  Representing vectors from physics

In Chapter 17 we will see a program which deals with motion in 3 dimensional space. This program will deal considerably with 3 dimensional vector quantities such as positions, velocities, and accelerations. So we will design a structure which makes it convenient to represent such quantities.

A vector in 3 dimensions can be represented in many ways. For example, we could consider it in Cartesian coordinates, or in so called spherical coordinates, or cylindrical

> ³In addition, the activation frame of the called structure will also have to have memory allocated to store the structure. This increases the total memory requirement of the program.
