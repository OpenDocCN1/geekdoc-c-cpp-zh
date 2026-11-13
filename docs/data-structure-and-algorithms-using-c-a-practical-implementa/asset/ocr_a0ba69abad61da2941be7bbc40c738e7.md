# Member Function

A member function of a class is a function that has its definition or its prototype within the class definition like any other variable. It operates on any object of the class of which it is a member, and has access to all the members of a class for that object.

# Example :

```
class print
{
private:
    int x;
public:
    void display()
    {
        cout<<"\n Enter the number";
        cin>>x;
        cout<<"THE ENTERED NUMBER IS "<<x;
    }
};
```

The function display() is kept in the public section because by using this only one can print the value of x but x is in the private category so any one want to display a number is bound to use the display(). This is the benefit of the class.

# Difference between the class and structure

| Class | Structure |
| :--- | :--- |
| The Keyword class is used | The Keyword struct is used |
| It provides the inheritance, polymorphism | It does not provide these concepts |
| By default the members of class are private. | By default the members of structure are public. |
| Data abstraction is supported | Not supported |

# Declaration of an OBJECT

The object is an instance of a class. Through the object one can use the members of the class.

Syntax : class_name object_name;