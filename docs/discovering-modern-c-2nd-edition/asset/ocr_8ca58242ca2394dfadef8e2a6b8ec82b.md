A concise class example is a type for representing complex numbers. Of course, there already exists such a class in C++ but for illustration purposes we write our own:

```
class complex
{
public:
double r, i;
};
```

The class contains variables to store the real and the imaginary parts of a complex number. A common mental picture for the role of a class definition is a blueprint. That is, we have not yet defined any single complex number. We only said that complex numbers contain two variables of type double which are named r and i. Now we are going to create Objects of our type:

Click here to view code image

```
complex z, c;
z.r = 3.5; z.i = 2;
c.r = 2; c.i = - 3.5;
std::cout << " z is (" << z.r << ", " << z.i << ")\n";
```

This snippet defines the objects z and c with variable declarations. Such declarations do not differ from intrinsic types: a type name followed by a variable name or a list thereof. The members of an object can be accessed with the dot operator . as illustrated above. As we can see, member variables can be read and written like ordinary variables—when they are accessible.

# 2.2.2 Accessibility

Each member of a class has a specified Accessibility. C++ provides three of them:

+   - public: accessible from everywhere;
+   - private: accessible only within the class; and
+   - protected: accessible in the class itself and its derived classes.

This gives the class designer good control of how the class users can work with each member. Defining more public members gives more freedom in