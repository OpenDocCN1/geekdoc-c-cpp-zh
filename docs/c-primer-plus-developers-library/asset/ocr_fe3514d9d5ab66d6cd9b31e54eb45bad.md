```
~~~cpp
    x = y = mag = ang = 0.0;
    mode = RECT;
}
~~~
```

If the third argument is RECT or if it is omitted (in which case the prototype assigns a default value of RECT), the inputs are interpreted as rectangular coordinates, whereas a value of POL causes them to be interpreted as polar coordinates:

```
~~~cpp
Vector folly(3.0, 4.0);        // set x = 3, y = 4
Vector foolery(20.0, 30.0, VECTOR::POL);   // set mag = 20, ang = 30
~~~
```

The identifier POL has class scope, so class definitions can just use the unqualified name. But the fully qualified name is VECTOR::VECTOR::POL because POL is defined in the Vector class, and Vector is defined in the VECTOR namespace. Note that the constructor uses the private methods set_mag() and set_ang() to set the magnitude and angle values if you provide x and y values, and it uses the private set_x() and set_y() methods to set x and y values if you provide magnitude and angle values. Also note that the constructor delivers a warning message and sets the state to RECT if something other than RECT or POL is specified.

Now it may seem rather difficult to sneak something other than RECT or POL to the constructor because the third argument is type VECTOR::Mode. A call such as the following won't compile because an integer like 2 can't implicitly be converted to an enum type:

```
~~~cpp
Vector rector(20.0, 30.0, 2);   // type mismatch - 2 not an enum type
~~~
```

Still, the resourceful and curious user could try something like the following to see what happens:

```
~~~cpp
Vector rector(20.0, 30.0, VECTOR::Mode (2));   // type cast
~~~
```

In this case, he gets admonished.

Next, the operator<<() function uses the mode to determine how values are displayed:

```
~~~cpp
// display rectangular coordinates if mode is RECT,
// else display polar coordinates if mode is POL
std::ostream & operator<<(std::ostream & os, const Vector & v)
{
    if (v.mode == Vector::RECT)
        os << "(x,y) = (" << v.x << ", " << v.y << ")";
    else if (v.mode == Vector::POL)
    {
        os << "(m,a) = (" << v.mag << ", "
            << v.ang * Rad_to_deg << ")";
    }
    else
        os << "Vector object mode is invalid";
    return os;
}
~~~
```