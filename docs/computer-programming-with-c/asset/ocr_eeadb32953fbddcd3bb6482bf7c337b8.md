We can access the attributes id, title, author, and price of each of the Book objects by using a membership operator ‘.’ (DOT) using the following notation given below:

```
```
<ObjectName>.<MemberName> = <value>;
```
```

For example, if the title of first Book is ‘C++’, second Book is ‘Java’, and the third Book is ‘Fortran’ then we can individually initialize the member variable title for each of the objects b1, b2, and b3 as shown in the following:

```
```
b1.title="C++";
b2.title="Java";
b3.title="Fortran";
```
```

The state of the objects b1, b2, and b3 after initializing the member title for each of them is as shown in Figure 9.7.

![](bbox=[0.27, 0.327, 0.79, 0.675])

**Figure 9.7:** Initialization of member variable title for each of the objects

> > **NOTES**
> >
> > In actuality title and author are **pointers** which points to the character array that store the string value. Hence the strings “C++”, “Java” and “Fortran” are actually stored in the character array created **external to the object** as shown in Figure 9.8. Hence the size of each book object remains 10 bytes immaterial of the number of characters in the string.