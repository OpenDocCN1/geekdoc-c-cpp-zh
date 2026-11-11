```
```cpp
rat operator *(rat R)
{
rat temp;
temp.Num= Num*R.Num;
temp.Den= R.Den* Den;
return temp;
}

void display()
{
cout<<Num<<Den;
}
};

void main()
{
clrscr();
rat R1(2,3),R2(3,4),R3;
R3=R1+R2;
R3.display();
R1-R2;
R1.display();
R3=R1*R2;
R3.display();
R1/R2;
R1.display();

getch();
}
```
```

**Q25.** Implement a class named ‘Matrix’ having following members.

+   **Private members:**
+   
+    a. A two dimensional array variable A of 10 X 10 integer elements
+    b. Number of rows and columns of the array – M and N

+   **Public members** are to be incorporated as member functions and the list is as follows:
+   
+    a. Function for reading a matrix from console
+    b. Function for display of Matrix
+    c. Function for addition of two matrices
+    d. Function which over loads multiplication operator (*) for Multiplication of two conformable matrices.