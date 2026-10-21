+   5. The arguments of **friend** functions are usually objects of the class to which it is a **friend**.
+   6. A **friend** function not being a member function of class is called as a normal function.
+   7. A **friend** function can be **friend** of more than one class.
+   8. A function of one class can be a **friend** of another class.
+   9. We can have whole class as a **friend** of another class
+   10. We use **friend** function usually with multiple classes but can used with single class also.
+   11. A **friend** function can be declared in the **public or private** visibility mode without affecting its meaning.
+   12. There can be any number of **friend** functions of a class.

The general syntax of creating a **friend** function as a **friend** class is :

```
class demo
{
  data members :
  public :
    members functions;
  // friend function declaration
  friend data_type function_name (parameters);
};
data_type function_name (parameters)
//definition
{
  function definition;
}
```

Now, let’s have some programs which make use of friend keyword.

```
/*PROG 6.37 DEMO OF FRIEND FUNCTION WITH SINGLE CLASS VER 1*/

#include <iostream.h>
#include <conio.h>
class demo
{
  int f x;
  public :
  void inputf(int x)
{
f x = x;
}
```