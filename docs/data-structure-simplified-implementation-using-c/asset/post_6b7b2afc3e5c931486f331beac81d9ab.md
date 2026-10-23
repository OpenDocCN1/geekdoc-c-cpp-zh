
## Data Structure Simplified

the array usage.

```cpp
Program: To accept and display five marks using array
int main ()
{

//Creation of an array to store five elements
int marks [5];
int i;
// input of five elements
cout<<"enter marks for five students";
for (i=0; i<=4; i++)
cin>>marks[i];
cout<<"marks entered for five students are :"<<endl;
//Display of marks for five students
for (i=0; i<=4; i++)
cout<<marks[i] <<endl;
return 0;
}
```

Similarly, we can determine an element having the maximum value from the given set of elements. We would use an array to store the elements.

```cpp
// Program: To input 5 random numbers and to find out the maximum element.

(Hint: Assume first element as maximum element)

int maximum (int a [])
{
int i=0;
int m=a [0];
while (a[i])     // examine all the elements of an array
{
if (a[i]>max)     // if array element is more than the max
max=a[i];    // Make this element as maximum
i++;  // increment the index
}
return max; //return the max
}
```

## 2.2.2　Initialization of an Array

Other than assigning the value using input technique, arrays can be initialized at the time of creation. Once array is initialized at the time of creation, there is no need to declare the size of an array.

```cpp
int A[5] = {45, 6, 7, 8, 12};      (1)

int A[] = {45, 6, 7, 8, 12};        (2)
```

The above (1) is redundant, since the array is initialized at the time of creation. Therefore, it is suggested to use the syntax depicted in (2), since compiler automatically allocates the array size based on the number of elements initialized.

```
Program: Initializing of an array during creation

Solution:

void array1 ()
{
int arr [] = {12, 5, 67, 98, 54};
int i=0;
while(arr[i])
{
cout<<arr[i]<<endl;
i++;
} //end of while statement
} //end of function
```

In the above program, the array is initialized at the time of creation. Here the size of an array will be five, if user is attempting to initialize the size of an array say arr [3] then also it will be overruled by the compiler and the new size will be 05. This feature is extremely helpful in cases where we are aware the number of values to be enumerated.

```
Program: Write down the program that demonstrate the initializing of an array at the time of creation.

void array1 ()
{
int arr [] = {12, 5, 67, 98, 54};
int i=0;
while(arr[i])
{
cout<<arr[i]<<endl;
i++;

```
```
} //end of while statement
} //end of function
```

### A. Special cases of initialization

Beyond, the above methods of initialization, there is one more method of initialization that is worth discussing at this point in time. In this method, instead of initializing all the index individually, we are initializing only one and the remaining indexes are initialized by the compiler. Syntax for the program is shown in (3).

```
int arr [8] = {0};
(3)
```

In the above statement, all the array index will be initialized with 0 (i.e. arr[0] to arr[7])

But consider another example:

```
int arr [7] = {4};
(4)
```

In the above case (4), all the indexes are not initialized with data 4; instead seventh index will have the value 4, whereas others will have the value of 0 only. Method (3) is significantly helpful in cases where we need to initialize all the index of an array to 0 or any other value.

### B. Problems based on integer array and their solutions

In this section, we will discuss some of the interesting problems related to the integer array and their solutions.

```
Program: Searching the element in an array.
void array1 (int arr [], int element) // element to be searched from arr array
{
int i=0;
int found=0;                //initially, item is not found
while (arr[i])    // Run till item exist in the array
{
if (arr[i] ==element)    //Element found
{
found=1;
break;            // terminate the further searching
}
i++;
}      //end of while statement
return found; // Now we need to return the status of found
} //end of function
```

Explanation: In this program, user is intending to search an element from an array. To accomplish this objective, array is to be scanned from the first index till the last index is reached. During the search, there are two probabilities, i) element exist in the array. ii) It does not exist in an array, in the second case, found should return false value. In case element is found in an array, instead of continue to go upto the end, loop should terminate at the point where element is traced. Value of found to be changed to 1 that signifies success. Eventually, the value of false is returned to the caller.

```
Problem: Program to count the number of elements which are more than the given number
//Function to count the number of elements with values more than the given number 'n'.
int countNumbers(int array [], int number)
{
int count=0;
int i=0;
while(array[i])
{
if (array[i]> number) // test if array element is more than number
count++;   //increment the count
i++;  //increment the index of array
}
return count;     // return the count
}
```

Explanation: In this program, we intend to count the number of elements in the array which are more than the given number (n), in this case we have to scan the array from the first element and continued upto the last element. On each run, array element need to be compared with the given number, if it is more than the given number then the variable count is incremented each time. Eventually, variable holding the count is returned to the caller.

```
Program: Program to modify the array element to some specific multiple. For instance, if multiple is 5, then it should modify each element by multiplying them by 5.
void increase (int array1 [], int mul)
{
int i=0;
while(array1 [i])
{
//multiply the element with the given multiple
```

```
```c
while(name[len++]!='\0');  // From beginning to end
return len;                 //return length.
}
```
```

In the above program, array is started from the first index and we increment the index till end of an array is reached. Once the end of an array is reached the length of the array is returned to the calling function.

These functions help enormously in other functions of string. Correspondingly, we can determine whether a given string is palindrome or not. A string is known as palindrome if reading from left or right returns the same result. For instance, madam, Malayalam, nitin, pop etc. is widely used string palindrome.

To determine whether the string is palindrome or not first element is compared with the last element, second element with the penultimate element, so on and so forth, till we don’t reach to the mid element. If all these elements are same then the given string is known as palindrome otherwise it is not a palindrome. Function to determine the palindrome has been given below.

```c
// Program to determine the string is palindrome, (// creating
function palindrome and accepting one argument of string type)

int palindrome(char str[])
{
int l=length(str);       // finding out length of the string

int i=0, flag=1;

while(i<=l) // executing the loop upto center element
{

if(str[i]!=str[l])
{
flag=0;                 // setting the flag value to false and breaking
the loop
break
}
i--;
l--;
}

return flag;            // returning the value of flag to the calling
function
}
```

## 2.2.3.1　String Programs

In the above function, we have considered that the given string is palindrome, correspondingly flag has been set to true. In the while loop, we compare the first element with the last element, if both are same, we compare the second element with the penultimate element. If these two are also same then remainder elements are tested for the equality. This will continue till the string is not exhausted. At any point of time, if the characters that are matched are not same, then the flag is set to false and further test of the element is terminated. Eventually, flag is returned to the caller function where the status of flag is evaluated to flash the appropriate message (true or false).

In addition to the above discussed string program, there are many other interesting array program. Several of them have been discussed in detail.

### A.　Program to concatenate two strings

In our daily usage, we require that second string should be concatenated with the first. For instance, in a database that is storing the first name and the last name, here the need is to concatenate the second name with first and eventually, concatenated string is then displayed.

```c
// Program to concatenate second string with first
// function to concatenate the string2 with string1
void concate(char s1[],char s2[])
{
    int i=0,j=0;
    // Running upto the end of the first string
    while(s1[i]!='\0')
        i++;
    // concatenate the second into first from the end
    while(s2[j])
    {
        s1[i]=s2[j];
        i++;
        j++;
    }
    s1[i]=s2[j];    // copying the null character into the first string
}
int main()
{
    clrscr();
```
