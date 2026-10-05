# Introduction to C++

Alternatively, we can use the -> operator to access the members of a structure. The -> operator consists of the - and > characters. Here is another version of the previous program:

```
int main() {
    Student *ptr, stud;

    ptr = &stud;
    ptr->name = "somebody";
    ptr->grd = 6.7;
    std::cout << ptr->name << ' ' << ptr->grd << '\n';
    return 0;
}
```

The expression ptr->name is equivalent to (*ptr).name and the expression ptr->grd is equivalent to (*ptr).grd (also equivalent to ptr[0].grd). Therefore, both programs output: somebody 6.7
Between the two ways of using the pointer to access the members of a structure, I find it more expressive and easier to use the -> operator.

+   Pointer arithmetic works the same as the ordinary pointers. For example, if a structure pointer is increased by one value it will be increased by the size of the structure it points to.

# Array of Structures

An array of structures is an array whose elements are structures. Its typical use is to store information about many items, like the data of a company's employees or students' data or the products of a warehouse. In fact, an array of structures may be used as a simple database. For example, with the statement:

```
Student stud[100];
```

the variable stud is declared as an array of 100 elements where each element is a structure of type Student. Array of structures can be initialized when declared. For example, given the declaration:

```
struct Student {
    string name;
    int code;
    float grd;
}
```

An initialization example is:

```
Student stud[3] = {{"nick sterg", 150, 7.3}, {"john theod", 160, 5.8}, {"peter karast", 170, 6.7}};
```

The initialization is done in the same way as initializing a two-dimensional array. The initial values for each structure are enclosed in braces, separated by comma. For example, stud[0].name becomes "nick sterg", stud[1].code becomes 160 and stud[2].grd becomes 6.7. The braces around each structure can be omitted; however, I prefer to use them to make clearer the initialization of each structure. As the usual, the compiler will compute the number of elements if the [] is empty.