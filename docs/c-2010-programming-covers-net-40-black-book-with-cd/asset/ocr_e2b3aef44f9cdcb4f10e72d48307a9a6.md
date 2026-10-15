example, you can assign true, false, or null value to Boolean variables. In addition, you can use a collection of user-defined nullable types supported by the .NET Framework.

# Enumeration Type

Enumerations are the user-defined integer data types that are declared using the enum keyword. Using enumeration, you can define a set of named integral constants that can be assigned to a variable. For example, you might have a program that models a traffic light. Traffic lights have three possible states—the green light indicating go, the yellow light indicating get prepared to stop, and the red light indicating stop. A traffic light can have only one of these states at a time, implying that the traffic light can be only red, yellow, or green at a time. In such a case, you can define enumeration type variable and assign 3 values to it. The following code snippet shows how to create enumeration type:

```
enum TrafficLight
{Red, Green, Yellow}
```

To use the enumerated type, you need to declare a variable of the new enumeration type, as shown in the following code snippet:

```
TrafficLight t1;
```

The TrafficLight enumeration can take any of the three values, Red, Green, and Yellow; i.e. enumeration can take only those values that are defined while creating the enumeration type, as shown in the following code snippet:

```
t1 = TrafficLight.Red;
t1 = TrafficLight.Green;
t1 = TrafficLight.Yellow;
```

Enumerations, by default, begin with the value of 0 for the first entry. However, you can modify this value by entering a different value for the first entry, as shown in the following code snippet:

```
enum TrafficLight
{
Red=1, Green, Yellow
}
```

Let’s take a look at reference types in C#.

# Reference Types

C# also provides types that are passed by references to calling functions, known as reference types. Variables that refer to the objects store the reference of the actual data. In reference types, any changes made in the new copy modify the old copy to which the object is referenced. The reference types use heap to store the references instead of the actual data. In C#, heap is called managed heap, as it manages and maintains a pointer to the address where the next object is to be allocated. Initially, the pointer is addressed to the heap’s base address, and when the first reference is created, the memory is allocated at the base address. When the next object is created in an application, the garbage collector allocates memory for it in the address space just next to the first object and continues to allocate memory for all the newly created objects. C# provides some built-in reference types, which are as follows:

+   dynamic type — Performs the type checking of the dynamic type variable at run time instead of compile time. You can add any type of value in the dynamic type variable. This type is similar to the object type; the difference is that the type checking of the variable of object type is performed at compile time. The following code snippet shows how to declare a dynamic type variable:

```
dynamic dyn = 10;
```

+   object Type — Enables you to assign values of any type to the variables of object type. Object is an alias for the predefined System.Object class. The object type is the ultimate base class for the other types in Common Type System (CTS), such as value types, reference types, predefined types, and user-defined types. All these types are derived directly or indirectly from the object type. The object type can be assigned a value of any other types, but before assigning a value it requires the type conversion. When a value type is converted to the object type, the process is known as boxing and on the contrary, when an object type is converted to the value type, the process is known as unboxing. The following code snippet shows the use of object type:

```
object x;
x=15; //boxing
```