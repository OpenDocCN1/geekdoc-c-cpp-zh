Additionally, if you leave an element uninitialized, all elements that follow it must be uninitialized. You can't, for example, alternate initializing and not initializing array elements. For example, the following statement won't compile
float milesPerGallon[4] = { 44.4, , 11.6, 33.3 }; // won't compile

# Implicit Array Sizing

The following are examples of array sizing:
int testScore[] = { 74, 87, 91 };
float milesPerGallon[] = { 44.4, 22.3, 11.6, 33.3 };
char grades[] = { 'A', 'B', 'C', 'D', 'F' };
string strings[] = {"Sunday","Monday","Tuesday","Wednesday","Thursday","Friday","Saturday"};

The first array, *testScore*, allocates memory for three integers. Since the square brackets are blank, the compiler allocates memory based on the number of elements to the right side of the assignment statement.
Similarly, the second array, *milesPerGallon*, allocates memory for four floats, the third array, *grades*, allocates memory for five characters, and the fourth array, *days*, allocates memory for seven strings.
The compiler only allocates memory based on the number of elements to the right side of the assignment statement if square brackets are empty. Otherwise, memory is allocated based on the number in the square brackets. Thus, in the example, the declaration of the array *testScore* would allocate memory for five integers even though only three are in the initialization statement because memory allocation is determined by the number within the square brackets. As discussed in the previous section, the fourth and fifth elements of the array would be initialized to a default value, 0.

```
int testScore[] = { 74, 87, 91 };
```

However, you must tell the compiler how much memory to allocate. Therefore, when declaring an array, you cannot have both empty brackets and no initialization, as in the following example:
int testScore[] = };

The compiler error message will be that the array is of unknown size. This course is a problem because the computer has no knowing of how much memory to allocate for the array.

# Initializing a Character Array

As showed the previous section, you can initialize a character array using the same syntax as you would initialize an array of any other data type as an integer or a float. As you will see in this chapter, there are some important differences between character arrays and arrays of numeric data. This section will show you your first difference.
The two initializations of a character array to my first name are different in syntax but identical in effect:

```
char name[] = { 'J', 'e', 'f', 'f', '\0' };
char name[] = "Jeff";
```