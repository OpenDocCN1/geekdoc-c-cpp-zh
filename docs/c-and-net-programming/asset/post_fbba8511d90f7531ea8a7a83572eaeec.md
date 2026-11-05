
**Example**

```csharp
enum number
{
    value0,
    value1,
    value2,
}
number num = (number)1;
int no = (int)num;
```

## 7. When to use enumeration

When class methods take a custom option as an argument, then enumeration can be used because it is a lot more efficient and is better programming practice.

## Two Marks Questions with Answers

### Q.1 How will you differentiate between a Class and a Struct?

Ans.: Although both class and structure are user-defined data types, they are different in several fundamental ways. A class is a reference type and stores on the heap. Struct, on the other hand, is a value type and is, therefore, stored on the stack. While the structure doesn't support inheritance and polymorphism, the class provides support for both. A class can be of an abstract type, but a structure can't. All members of a class are private by default, while members of a struct are public by default. Another distinction between class and struct is based on memory management. The former supports garbage collection while the latter doesn't.

Given below are the differences between a Class and a Struct:

| Sr. No. | Class | Struct |
|---|---|---|
| 1. | Supports Inheritance | Does not support Inheritance |
| 2. | Class is pass by reference (reference type) | Struct is pass by copy (value type) |
| 3. | Members are private by default | Members are public by default |
| 4. | Good for larger complex objects | Good for small isolated models |
| 5. | Can use garbage collector for memory management | Cannot use garbage collector and hence no memory management |

### Q.2 What is enum in C#?

Ans.: An enum is a value type with a set of related named constants often referred to as an enumerator list. The enum keyword is used to declare an enumeration. It is a primitive data type that is user-defined.

An enum type can be an integer (float, int, byte, double, etc.). But if you use it besides int it has to be cast.

An enum is used to create numeric constants in the .NET framework. All the members of enum are enum type. There must be a numeric value for each enum type.

The default underlying type of the enumeration element is int. By default, the first enumerator has the value 0, and the value of each successive enumerator is increased by 1.

```csharp
enum Dow {Sat, Sun, Mon, Tue, Wed, Thu, Fri};
```

### Q.3 Can you use tilde(~) with Enum in C#?

Ans.: Yes, you can use tilde(~) with Enum to flip the bits of its operand.

### Q.4 What is the advantage of structure in C#?

Ans.: Structures are stored on the stack, so there are some advantages of structures.

- Structures are created more quickly than heap-allocated.
- Structures are automatically deallocated when they go out of scope.
- Structures are value types so that we can easily copy value type variables on the stack memory.

### Q.5 When do we prefer the use of structs over classes?

Ans.: We prefer structure if it satisfies the following statements given below:

- To represent a single value.
- Size is smaller than 16 bytes.
- Immutable.
- For boxing.

## Long Answered Questions

- Q.1 What are the features of C# structures? (Refer section 7.1)
- Q.2 Define structures in C# along with their syntax. (Refer section 7.1)
- Q.3 Discuss classes versus structures in C#. (Refer section 7.1)
- Q.4 What is the purpose of enumeration? (Refer section 7.2)
- Q.5 What are the features of enumerations? (Refer section 7.2)

## Unit - 1

## CHAPTER - 8

## C# - OOP I - CLASSES AND OBJECTS

Syllabus: Object and Types - Classes and Structs.

| Section No. | Topic Name | Page No. |
|---|---|---|
| 8.1 | Classes and Objects, Constructor and Destructors, Types of Classes and Various Class Members | 8 - 2 |
| 8.2 | Method Overloading | 8 - 26 |
| 8.3 | Modifiers Readonly and Constant | 8 - 28 |
| 8.4 | Interfaces | 8 - 31 |
| 8.5 | Nested Classes | 8 - 33 |
|  | Two Marks Questions with Answers | 8 - 34 |
|  | Long Answered Questions | 8 - 38 |

## 8.1 Classes and Objects, Constructor and Destructors, Types of Classes and Various Class Members

### 8.1.1 Class

**Concept**

- 1. A class is a group of related methods and variables.

**Explanation**

- 2. It is like defining a blueprint for a data type. A class is a blueprint that defines the attributes and behaviors of the objects that are created as instances of the class.
- 3. When a class is defined, this does not actually define any data, but it does define what the class name means. That is, what an object of the class consists of and what operations can be performed on that object.
- 4. Objects are instances of a class. The methods and variables that constitute a class are called members of the class. On this object, defined methods and variables are used. As many instances of a class can be created as per requirement of the application.
- 5. By having a class in a program one of the basic features of object-oriented programming is incorporated on the application.
- 6. **Data encapsulation** means that the class user or client code does not have direct access to the data. When working with the data, the client code must use clearly defined properties and methods accessed through an instance of the class.

Following are some of the **benefits of encapsulating** the data in the form of creation of class,

- 1. Preventing unauthorized access to the data.
- 2. Ensuring data integrity through error checking.
- 3. Creating read-only or write-only properties.
- 4. Isolating users of the class from changes in the implementation code.

### 8.1.2 Object

**Concept**

- 1. Object is an instance of a class that is created dynamically which represents runtime behavior of the class.

**Explanation**

- 2. Object is also a keyword that is an alias for the predefined type System.Object in the .NET framework.
- 3. C# allows objects to be defined which can be user-defined, reference or value type, but they all inherit directly or indirectly from System.Object. This inheritance is implicit so that the type of the object need not be declared with System.Object as the base class.
- 4. Objects are of class type and an object is created using the new keyword as, `object_name = new class_name();`
- 5. Object type is used for building generic routines. Because values of any type can be assigned to variables of object type, object type is used mostly in designing classes that handle objects of any type that allow code to be reused.
- 6. The non-generic collection classes in the .NET framework library, such as ArrayList, use object type to define various collections.
- 7. An object consists of instance members whose values make it unique in a similar set of objects.
- 8. When an object is instantiated, it is allocated with a block of memory and configured as per the blueprint provided by the class underlying the object.
- 9. Objects of value type are stored on the stack, while those of reference type are allocated on the heap.
- 10. As the execution of C# code is in the managed environment of .NET, wherein the garbage collector provides automatic memory reclamation, it is not necessary or possible to explicitly de-allocate memory that is allocated for objects.
- 11. Objects of value type are destroyed when they go out of scope, while reference type objects are destroyed in a non-deterministic manner until the last reference to them is removed.
- 12. The two operations related to objects created in C# are boxing and unboxing. Boxing implies the conversion of a value type to object and unboxing refers to the conversion from object to a value type.

### 8.1.3 Working with the Classes and Objects

**1. Creating and using a class**

**1.1 Defining Classes**

- 1. The class is defined using the keyword class followed by the name of the class.
- 2. The body of the class definition is enclosed by an opening and closing curly bracket.

**Example**

```csharp
class Book
{
}
```

**1.2 Field (Class Member Variable)**

**Concept**

- 1. Fields describe the real-world properties of the object and hold the state of the object.

**Explanation**

- 2. Objects describe things from the real world by using their **characteristics**, which are related to the problems solved in the program.
- 3. These characteristics of the real-world object would be encapsulated in the class in the form of variables.
- 4. When an object is created based on certain class definition, the values of the fields contain the characteristics of the created object (its state). These characteristics have different values for different objects.
- 5. **Declaring Fields in a Class**
  - 5.1) Apart from **Local variables** (these are the variables declared in the body of some method (or block)) and **Parameters** (these are the variables in parameter list passed to a method), the third type of variable is **field** or **instance variable**.
  - 5.2) Fields are declared in the body of the class which is always outside the body of a single method or constructor.
  - 5.3) General syntax for declaration of a field is,

```csharp
[<modifiers>] <field_type> <field_name>;
```

The **<modifiers>** describe the access level (described in the following section) of the field as well as other modifiers like 'const' etc. Modifiers are not mandatory for field declaration.

The **<field_type>** determines the type of a given field which can be primitive type (**byte, short, char** and so on), an array or also some class type (e.g. **Book** or **string**).

The **<field_name>** indicates the name of the field which follows the identifier's standard naming convention of C# specified in earlier chapter (**Refer chapter 2 – Section 2.6**).

- 6. **Scope of the field**

The **scope of a class field** is from the start of class declaration statement and it is until the ending closing bracket of the body of the class.
