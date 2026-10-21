```
```cpp
clrscr();

cout << "Enter the salary \n";
cIn >> s;

if(s >= 5000)
    incr(s,15);
else
    incr(s);

cout << "Salary with bonus=" << s << endl;
getch();
}

void incr(float & sal, float bonus_pr)
{
    sal = sal*(1+bonus_pr/100);
}
```
```

**OUTPUT :**  
Enter the salary  
7000  
Salary with bonus=8050

**EXPLANATION :** The function **incr** finds new salary after adding bonus to the original salary. If salary is **<5000** we provide a bonus of **10%** of **sal** else we provide bonus of **15%** of salary.

# 5.11 PONDERABLE POINTS

+   1. Based on the nature of creation there are two categories of function : **built-in and user-defined**.
+   
+   2. For all the built-in functions (also called library functions) prototype is stored in the header files and compiled code (which we cannot see) is stored in **.obj file** form in special files called library. One library may contain number of compiled functions.
+   
+   3. The functions which are predefined and supplied along with the compiler are known as *built-in function*.
+   
+   4. The function **main( )** can appear only once in a C program, because execution commences from the first statement in the **main ( )** function. If there is more than one **main( )** function, there will be a confusion while commencing the execution.