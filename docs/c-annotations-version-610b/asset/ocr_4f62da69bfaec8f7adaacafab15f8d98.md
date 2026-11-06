![](bbox=[0.223, 0.042, 0.655, 0.252])

Figure 3.1: Private data and public interface functions of the class Person.

member functions which are defined in the `struct`: these are the functions `setName`, `setAddress` etc.. As an illustration consider the following code:

```
```cpp
Person fbb;

fbb.setName("Frank");        // OK, setName is public
strcpy(fbb.d_name, "Knarf"); // error, x.d_name is private
```
```

Data integrity is implemented as follows: the actual data of a `struct Person` are mentioned in the structure definition. The data are accessed by the outside world using special functions that are also part of the definition. These member functions control all traffic between the data fields and other parts of the program and are therefore also called ‘interface’ functions. The thus implemented data hiding is illustrated in Figure 3.1. The members `setName` and `setAddress` are declared with `char const *` parameters. This indicates that the functions will not alter the strings which are supplied as their arguments. Analogously, the members `name` and `address` return `char const *s`: the compiler prevents callers of those members from modifying the information made accessible through the return values of those members.

Two examples of member functions of the `struct Person` are shown below:

```
```cpp
void Person::setName(char const *n)
{
    strncpy(d_name, n, 79);
    d_name[79] = 0;
}

char const *Person::name()
{
    return d_name;
}
```
```

The power of member functions and of the concept of data hiding results from the abilities of member functions to perform special tasks, e.g., checking the validity of the data. In the above example `setName` copies only up to 79 characters from its argument to the data member name, thereby avoiding a buffer overflow.

Another illustration of the concept of data hiding is the following. As an alternative to member functions that keep their data in memory a library could be developed featuring member functions storing data on file. To convert a program storing `Person` structures in memory to one that stores the data on disk no special modifications are required. After recompilation and linking the program to a new