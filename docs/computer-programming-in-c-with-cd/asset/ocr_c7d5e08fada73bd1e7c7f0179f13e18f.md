```
cout << "How many numbers do you want to enter ?";
cin >> num;
// create an object of AddingNumber class and compute the sum of numbers
AddingNumbers addnum (num);
addnum.input();
addnum.additionDisplay();
}
```

# Output:

```
How many numbers do you want to enter ?5
Enter a number at the position [ 0 ] ? 10
Enter a number at the position [ 1 ] ? 20
Enter a number at the position [ 2 ] ? 30
Enter a number at the position [ 3 ] ? 40
Enter a number at the position [ 4 ] ? 50
Sum of the numbers = 150
```

In Listing 18, the following code snippet creates an instance (or an object) addnum of the AddingNumbers class dynamically by using the new operator:

```
AddingNumbers addnum (num);
```

The object, addnum, is initialized with the num variable. The input() function accepts a number from a user, which indicates how many numbers are provided by a user. The additionDisplay() function adds all the number elements and displays their sum. When performing dynamic initialization of objects, it is important to note that the data members should not be initialized (pointer variable must be NULL). The parameterized constructor must allocate the right amount of memory resources. The program must have a destructor to release all the allocated memory.

# TEST YOUR KNOWLEDGE

+   Q4. Create a program that can convert:
+   - Meters into centimeters and vice-versa
+   - Feet into inches and vice-versa

Ans:

```
#include<iostream.h>

class db;
class dm
{
    private :
        float m,cm;
    public:
        dm():m(0.0),cm(0.0)
```