
## Basic Concepts

```
while (low<=upper)
{
mid= (low+upper)/2;             // find out the center
if (b [mid] ==n)
{
found=true;
break;
}
if (n < b [mid])
    {
    upper=mid-1;    // Select the left half
    }
        else
low=mid+1;          //Select the right half
}       end of while loops
return found;
}
```

Upon application of the aforecited algorithm, the number of items that would remain in the series will be the half of the previous step. Therefore, total number of items remaining can be computed as:

n + n/2+ n/4…………4+2+1.

When we apply the definition of logarithm, and subsequently simplify it, the algorithm will result in O log (n)

## EXERCISES

## A. Descriptive Answers

- 1. What is the significance of data type in a programming language?
- 2. ADT is complement to the data type and not its substitution, justify.
- 3. How ADT is related to object oriented language?
- 4. What is an algorithm? How it is different with the program?
- 5. Efficient algorithm is the prerequisite for efficient program, justify?
- 6. Write an algorithm for binary sort?

7. What is asymptotic notation? How it computes the efficiency of a program?

8. How to define big ‘O’?

9. How to define the upper and lower bound in complexity analysis?

10. Consider a case that in complexity computation, it has been computed in logarithm, what will be the effect on the value calculated, if the base of log is changed?

11. How complexity may differ in best case, average and worst case? Justify with help of suitable examples?

12. What will be the complexity of the following algorithms:

- - Insertion sort.
- - Linear search.
- - Binary search.

13. In the above question (12), how the efficiency will vary for each method? Which one among them is the best? Prove mathematically.

## B. Multiple Choice Questions

(Mark the most appropriate answer. In case(s), if more than one options are true, select the most appropriate one.)

B.1 Abstract data type, allows defining:

- i) New data type
- ii) Extend the feature of an existing type.
- iii) Both i and ii
- iv) None of these

B.2 Abstract data type is widely utilized in modern programming:

- i) True for all the language
- ii) False for all the language.
- iii) Both i) and ii)
- iv) None of these.

B.3 In asymptotic notation, we compute

- i) Time complexity.
- ii) Space complexity.
- iii) Running complexity.
- iv) None of these

## Basic Concepts

B.4 Big ‘O’ is the

- i) Upper bound of an algorithm.
- ii) Lower bound of an algorithm.
- iii) both i) and ii)
- iv) None of these.

B.5 Big ‘O’ of quicksort is

- i) log n.
- ii) n².
- iii) n log n
- iv) None of these.

B.6 In Big ‘O’, if the base is of log is changed

- i) It will change the resultant value.
- ii) It will not change the resultant value.
- iii) It will change the value, however that change is negligible, therefore can be neglected.
- iv) None of these.

## Arrays and Pointers

## Chapter Objective

- - Define array
- - To describe the types of array
- - Usage of single dimensional and two dimensional arrays
- - Defining pointers
- - Describing the single pointers and its usage
- - Describing the pointer to pointer and its usage.

### 2.1 INTRODUCTION

Arrays are widely used in any programming language. It is extremely useful in cases where we need to store the similar set of elements. It helps in reducing the program complexity at the same time increases the programmer's productivity. In C++, it is used in implementing the string with the help of array of characters. Depending upon the element organization, arrays can be categorized into the following:

- - Single Dimensional array.
- - Double Dimensional array.
- - Multidimensional array.

For this text book, multidimensional array is out of scope and here it has been discussed for the sake of completeness only. Remainder of the topics has been described in the upcoming sub-sections.

### 2.2 SINGLE DIMENSIONAL ARRAY

Consider a case that we need to store the marks of five students; in order to store the marks of these five students, we need to declare five different variables. Due to the involvement of homogeneous information that needs to be stored, variables declared should be of the same type. Program to store five elements has been depicted below:

```
Program: To accept marks of five subjects and display them (without an array)
Solution:
int main ()
```

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

- - Used to store, set of similar data types.
- - In an array, elements are stored in continuous memory locations.
- - Index, or subscript starts with 0.
- - Size of the array should be constant.
- - Character array terminates with the special symbols '\0', known as null.

Index is also known as subscript and starts from '0th' number. At index '0', first element is stored. Same has been illustrated in figure 2.2.

### 2.2.1 Declaration of an array

If we are intending to create an array that should be capable to store 10 elements. Consider that number to be stored is of integer type. To declare this array, following syntax can be used.

```
int number [10];
```

![](img/9b7c80a1312a664ae505ba138aa3306b_33_0.png)

In the above statement, number is acting as an array identifier. Here an array of integer type is created, that is capable to store 10 integer type numbers. If we assume that the size of integer is 2; also assume that first address of an array is 3000 then we can compute the address of subsequent elements. Address computation of various elements of an array has been illustrated in the figure 2.1.

In an array, elements are placed one after another; however, storage at any index/subscript is possible. For instance, if the order of arrival of elements is 15, 10, and 7 then it is not mandatory that they have to be stored in the index 0, 1, 2 respectively. We can store them at any index of an array based on the availability. For instance, the first element can be stored in the array index 2, 10 at index 1 and the element 7 at the index number 0. Initialization of these elements is as follows:

```
array [2] =15;

array [0] =10;

array [1] =7.
```

However, as a good practice, it is suggested to use the contiguous address for storage. Correspondingly, to access an array element stored at 4ᵗʰ index, syntax array [4] need to be used. It is worth mentioning that the element that is stored at 5ᵗʰ location of an array will be accessed (Since index starts from 0). For instance, if the array is given as **int array1 = {4, 9, 12, 67, 90, 45}**, in this case, array1 [4] will be 90. Since, the index 4 which is 5ᵗʰ element of an array has value of 90.

![](img/9b7c80a1312a664ae505ba138aa3306b_33_1.png)

Array offers number of advantages such as it eliminates the need of creating many variables. Consequently, complexity of the program is reduced to a great extent. The other advantage is array is fast relative to the dynamically allocated variables. Following program demonstrates
