```
```cpp
// call rectangle area.
shape->area();
// store the address of Triangle
shape = &tri;
// call triangle area.
shape->area();
return 0;
}
```
```

When you've completed compiling the code above and given it some time to run, you should see the parent class area's result there. However, both portions will be kept blank.

The compiler will set the call of the function area once as the version that is declared in our base class, resulting in this erroneous output. This is known as the static linkage or the static resolution of the function call. What this implies for us is that the function call will be corrected before we even start working with the software. Because the area() function is set during the compilation of the program, this may also be referred to as the early binding. However, we must now take a different path and make some minor changes to our software. In this case, we'll use the virtual keyword to precede the definition of the area() method in our Shape class.

The following is how this code will appear:

```
```cpp
Shape as a class
protected:

class Shape {
protected:
int width, height;
public:
Shape( int a = 0, int b = 0) {
width = a;
height = b;
}
virtual int area() {
cout << "Parent class area :" <<endl;
return 0;
}
}
```
```

It will give us a little different outcome in the process once we can make this minor alteration, compile, and then run the code again. Instead, we'll obtain the Triangle class area and the Rectangle class area.

Instead of looking at the type of the pointer, the compiler will look at the contents of the pointer. Because the addresses of our rec and tri objects will be kept in the *shape, here is where the appropriate region of our function will be called up. As you can see, each of the child classes with which we will work will have a different implementation of our function area. We are typically able to deal with polymorphism in this manner. You may also create several classes with the same function name and even the same arguments, but to make this work, you'll need to use a different implementation. Another thing we'll be able to do here is work with the virtual function. This will be a function from a base class that may be defined with the "virtual" keyword, as we