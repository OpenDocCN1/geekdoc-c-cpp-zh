![](bbox=[0.23, 0.085, 0.73, 0.295])

Fig. 5.2 ⇨ Representation of a class

```
item x;    // memory for x is created
```

creates a variable x of type item. In C++, the class variables are known as objects. Therefore, x is called an object of type item. We may also declare more than one object in one statement. Example:

```
item x, y, z;
```

The declaration of an object is similar to that of a variable of any basic type. The necessary memory space is allocated to an object at this stage. Note that class specification, like a structure, provides only a template and does not create any memory space for the objects.

Objects can also be created when a class is defined by placing their names immediately after the closing brace, as we do in the case of structures. That is to say, the definition

```
class item
{
    .....
    .....
    .....
} x,y,z;
```

would create the objects x, y and z of type item. This practice is seldom followed because we would like to declare the objects close to the place where they are used and not at the time of class definition.

# Accessing Class Members

As pointed out earlier, the private data of a class can be accessed only through the member functions of that class. The main() cannot contain statements that access number and cost directly. The following is the format for calling a member function: