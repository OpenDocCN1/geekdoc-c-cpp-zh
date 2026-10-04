Each declaration will have 2 parts: a variable type, followed by a variable name. In your code, there are 4 variables being declared. Each one is of integer, and they have different names: carb_grams, fat_grams, and calories (which is the variable you're looking to calculate).

As long you follow the rules, choosing the names for variables is up to you. Choosing good variable names is one of the most important things you can do to make your code understandable—to yourself and others.

```
// Program 2_3
// Using floating-point-
variables
#include<iostream>
using namespace std;
int main() {
float carb_grams;
float protein_grams;
float fat_grams;
carb_grams = 30;
protein_grams = 5;
fat_grams = 15;
float calories = 4 * carb_grams + 9 * protein_grams + fat_grams;
cout << "There are " << calories << " calories in this dish" << endl;
}
```

To avoid int over and over, you can put all of your declarations on one line. Just beginning to let the computer determine the type for all the variables on that line: int.

So, as you choose names, choose names that give a clear sense of the meaning of what variable is intended to hold. Do not choose names that are too short or too long. Also, try to be consistent in your names: For example, if you pick a name like carb_grams, you should pick fat_grams rather than grams_of_fat.

Then, you can just list all of variables you want to declare, separated by commas.

If you wanted to get more precise and use decimals for the number of grams or calories in your program,

# Exercise 1

Which of the following would be OK to use as variable names?

A decimal is called a floating point because the location of the decimal points around: Compare the decimal in 1.1 with 99.999.

To designate a variable as a floating-point type, use float.

So, you'd just go through your program and replace int with a float (g).

+   tank_capacity
namespace
something
length2
left foot
account
Success!
i
2nd_account

Once you've declared variables, whether they are integers or floats, you will need to use them—to store information in that box of memory and look at it later.

Click here to see the solution.