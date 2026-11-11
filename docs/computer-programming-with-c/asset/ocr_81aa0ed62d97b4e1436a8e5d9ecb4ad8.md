The variable b1 is now called as an ‘object’ of a structure Book. The object memory of b1 will contain members id, title, author and price as shown in the Figure 9.3. Note that, these members are present in the object memory of b1 because we have defined them inside the structure Book.

![](bbox=[0.185, 0.192, 0.879, 0.39])

**Figure 9.3:** Object memory of b1

> **NOTES**
> 
> Specifying keyword struct while creating an object of a structure is mandatory in C but optional in C++. In C++, you can also create an object b1 by omitting keyword struct as shown in the statement below:
> 
> `Book b1;`
> 
> Since structures are supported by both C and C++, we will add keyword struct in all the programs written in this chapter. We will ensure that the program works on C as well as C++ compilers. If you are a C++ programmer adding a keyword struct makes your programs backward compatible with C and hence it's a good practice to add it, anyways. If you are a C programmer you have no choice; you have to add keyword struct while creating objects of structure.

The total memory required for object b1 should be calculated as addition of the memory required by integer member id (which is 2 bytes), character pointer title (which is 2 bytes), character pointer author (which is 2 bytes) and float member price (which is 4 bytes). Therefore, the total memory required by each object of the structure will be 10 bytes as shown in the Figure 9.4. We assume title and author as near pointers and hence consider them of 2 byte each.

![](bbox=[0.365, 0.738, 0.591, 0.875])

Total memory required for object b1 = **10 bytes**

**Figure 9.4:** Memory required for object b1