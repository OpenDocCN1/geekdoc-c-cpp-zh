functions. As we know, a constmember is a function prototype or function definition where the keyword const appears after the function's signature.

Whenever constobjects try to invoke nonconstmember functions, the compiler generates errors.

# 6.11 Destructors

A _destructor,_as the name implies, is used to destroy the objects that have been created by a constructor. Like a constructor, the destructor is a member function whose name is the same as the class name but is preceded by a tilde. For example, the destructor for the class integer can be defined as shown below:

```
~integer( ){}
```

A destructor never takes any argument nor does it return any value. It will be invoked implicitly by the compiler upon exit from the program (or block or function as the case may be) to clean up storage that is no longer accessible. It is a good practice to declare destructors in a program since it releases memory space for future use.

Whenever newis used to allocate memory in the constructors, we should use delete to free that memory. For example, the destructor for the matrixclass discussed above may be defined as follows:

```
matrix :: ~matrix( )
{
for(int i=0; i<d1;
delete p[i];
delete p;
}
```