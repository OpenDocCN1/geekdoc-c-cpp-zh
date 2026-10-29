# Point of Information

# Accessor Methods

An accessor method is any non-constructor member method that accesses a class's private data members. For example, the showDate() method in the Date class is an accessor method. These methods are extremely important because they provide a means of displaying private data members' stored values.

When you construct a class, make sure to provide a complete set of accessor methods. Each accessor method doesn't have to return a data member's exact value, but it should return a useful representation of the value. For example, if the date 12/25/2012 is stored as a long integer member variable in the form 20122512, an accessor method could display this value. A more useful representation, however, is 12/25/12 or December 25, 2012.

Destructors are called automatically when an object goes out of existence and are meant to "clean up" any undesirable effects the object might leave. Generally, these effects occur only when an object contains a pointer member.

# Arrays of Objects

The importance of default constructors becomes evident when arrays of objects are created. Because a constructor is called each time an object is created, the default constructor provides an efficient way of initializing all objects to the same state.

Declaring an array of objects is the same as declaring an array of any built-in type. For example, the following declaration creates five objects named theDate[0] through theDate[4]:

```
Date theDate[5];
```

Member methods for each of these objects are called by listing the object name followed by a dot (.) and the method. Program 10.4 shows using an array of objects, which includes cout statements in both the constructor and destructor. As this program's output shows, the constructor is called for each declared object, followed by five member method calls to showDate(), followed by five destructor calls. The destructor is called when the objects go out of scope. In this case, the destructor is called when the main() function stops execution.