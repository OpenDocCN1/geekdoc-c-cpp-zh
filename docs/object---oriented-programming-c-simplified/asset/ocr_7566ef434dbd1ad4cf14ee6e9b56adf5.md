```
OUTPUT :
IN FIRST_FUN OF FIRST
num := 30
```

**EXPLANATION** : In the function show1 we pass object f by reference. So s in function show1 and f in main are same. In the function we call first_fun function which sets the value of num to 30. Later when we call function show2 and pass object f by value the same value of num is displayed.

# 6.8.1 Demerits of Friend Function

+   1. **Friend** function cannot access the class members and functions directly, they need to have a class object which using dot can call the members of the class.
+   2. Creating friend classes and functions defy the idea of encapsulation and create exception in the ways of data hiding.
+   3. Usages of many friend functions some times make you think to redesign your program.
+   4. **Friend** functions are conceptually messy and potentially lead to spaghetti-code situations as numerous friend functions muddy the clear boundaries between classes.

# 6.9 STATIC CLASS MEMBERS

Static variables are those variables which persist even after control returns from the functions. In terms of static members as class members they are the members which are one for a class and not one for an object. We know that functions of which belong to class only. Static members can be either functions or static data. They are also known as class variables as they belong to whole of the class.

# 6.9.1 Static Member Functions

Let’s discuss static function first. Note several points about static member’s functions :

+   1. Static functions are functions which are made static by placing keyword static before function definition in side the class.
+   2. All static function of class must be defined inside the class. You cannot separate the declaration and definition of a static member function.
+   3. Static functions are one for class and you can call them as.
+   4. In a static function only static data members, other static variables or other static function can be used.
+   5. Though static member function is called using class name with :: operator. It can be called explicitly using objects of the class.

```
/*PROG 6.45 DEMO OF STATIC FUNCTION VER 1*/

#include <iostream.h>
#include <conio.h>
```