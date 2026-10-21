# OUTPUT :

+   Enter a number
+   Vijay Nath Pandey
+   Enter a number
+   Madhuri Pandey
+   Enter a number
+   Anjana Pandey
+   Enter a number
+   Man Mohan Pandey
+   Enter a number
+   Hari Mohan Pandey
+   Enter a number
+   Ranjana Pandey

+   The names are
+   Name : = Vijay Nath Pandey
+   Name : = Madhuri Pandey
+   Name : = Anjana Pandey
+   Name : = Man Mohan Pandey
+   Name : = Hari Mohan Pandey
+   Name : = Ranjana Pandey

# EXPLANATION :

In the program we have created a pointer to an array of object which is created dynamically in the statement demo * ptr = new demo [S]; The address of array is saved in temporary variable temp as demo *temp = ptr; In the for loop we take names from the user in string s and initialize each dynamically created object using statement ptr[i] = demo (s); The entered names are displayed back using for loop as : for(i=0;i<S;i++) temp++ -> show()

Initially we assigned ptr to temp and now we make use of it. As temp contains address of the first object, initially show is called for the first object then temp is incremented as temp++, now temp points to the second object and show for second object is displayed and so on.

We could simply make use of ptr for calling the show functions. Why did we take another pointer temp ? The answer is simple. If we had used pointer ptr for displaying names by a call to show in the end would be pointing somewhere else in the memory and not to the base address of the array. Through it would be ok for this program but if you have to make use of ptr later some where in the program then you would not be getting object using ptr.

```
/*PROG 10.5 INITIALIZING ARRAY OF OBJECTS DYNAMICALLY */
#include <iostream.h>
#include <conio.h>
```