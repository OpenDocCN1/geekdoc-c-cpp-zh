# **Dive 14**

# **Structs and Objects**

> > “Object-oriented programming is an exceptionally bad idea which could only have originated in California.”  
> Edsger Dijkstra

Apart from the array, the struct is the only other sophisticated data structure that C provides. As things turn out, the array and the struct are enough for most things. At the most basic level, the struct is the C implementation of the data record, but the data record is also where object-oriented programming starts. This might seem surprising, but it is true that in most languages there is little difference between an object and a record. To understand C’s approach, the all purpose struct, let’s start with the basics.

# **The Struct**

You were probably introduced to the struct, short for “structure”, as a sort of array that allows different types as elements. For example:

```
```
struct{
int myfield1;
float myfield2;
} myStruct;
```
```

This creates a struct with two fields – one an int and the other a float. These fields are grouped into the structure in the same way as elements are in an array – except that they are of different types. Of course, you access the fields using the familiar dot notation:

```
```python
myStruct.myfield1 = 42;
myStruct.myfield2 = 4.2;
```
```

This declaration is of the standard form:

```
```python
type variable;
```
```

where *type* is the complete struct definition and the *variable* is the name at the end of the type.