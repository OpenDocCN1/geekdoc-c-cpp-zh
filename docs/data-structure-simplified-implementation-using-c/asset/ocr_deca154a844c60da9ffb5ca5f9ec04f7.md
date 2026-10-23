```
{
int marks1, marks2, marks3, marks4, marks5;
cout<<"enter marks1";
cin>>marks1;
cout<<"enter marks2";
cin>>marks2;
cout<<"enter marks3";
cin>>marks3;
cout<<"enter marks4";
cin>>marks4;
cout<<"enter marks5";
cin>>marks5;
return 0;
}
```

In the above program, we have observed that to store the marks of 05 different subjects, we have to create five distinct variables. Complexity of the above program will grow further upon increment of subjects. Correspondingly, to input the details of 100 students or more, there will be phenomenal growth in the complexity of the above program. To overcome such limitation, we need to evolve the aforementioned method in order to reduce the complexity at the same time to improve the programmer's productivity. Here the solutions lie with the usage of arrays. Once array is declared, space needed for an array is allocated contiguously. This space is allocated at the time of compilation.

Array can be defined as:

+   - Used to store, set of similar data types.
+   - In an array, elements are stored in continuous memory locations.
+   - Index, or subscript starts with 0.
+   - Size of the array should be constant.
+   - Character array terminates with the special symbols '\0', known as null.

Index is also known as subscript and starts from '0th' number. At index '0', first element is stored. Same has been illustrated in figure 2.2.

# 2.2.1 Declaration of an array

If we are intending to create an array that should be capable to store 10 elements. Consider that number to be stored is of integer type. To declare this array, following syntax can be used.

```
int number [10];
```