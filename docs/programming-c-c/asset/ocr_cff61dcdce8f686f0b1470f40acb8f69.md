# Object

An Object is an identifiable entity with some characteristics and behaviour. An Object is an instance of a Class. When a class is defined, no memory is allocated but when it is instantiated (i.e., an object is created) memory is allocated. To use the data and access functions defined in the class, you need to create objects.

Syntax:

```
ClassName ObjectName;
class sekhar
{
    char name[20];
    int id;
public:
    void getdetails(){}
};
int main()
{
    sekhar a1; // a1 is a object
}
```

Object take up space in memory and have an associated address like a record in Pascal or structure or union in C.

When a program is executed, the objects interact by sending messages to one another.

Each object contains data and code to manipulate the data. Objects can interact without knowing details of each other's data or code, it is sufficient to know the type of message accepted and type of response returned by the objects.

# DATA MEMBERS AND MEMBER FUNCTIONS IN C++

"Data Member" and "Member Functions" are the new names/terms for the members of a class, which are introduced in C++ programming language.

The variables which are declared in any class by using any fundamental data types (like int, char, float, etc.) or derived data type (like class, structure, pointer,