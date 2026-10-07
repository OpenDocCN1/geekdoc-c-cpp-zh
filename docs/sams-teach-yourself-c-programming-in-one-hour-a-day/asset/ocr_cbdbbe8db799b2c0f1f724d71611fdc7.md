#  Answers for Lesson 8

# Quiz

+   1. All of them, but one at a time. Given array can contain only a single data type.
2. Regardless of the size of an array, all C arrays start with subscript 0. (Obviously an array of size 0 would not start with subscript 0, as it has no elements at all.)
3. n-1
4. The program compiles and runs, but it produces unpredictable results.
5. In the declaration statement, follow the array name with one set of brackets for each dimension. Each set of brackets contains the number of elements in the corresponding dimension.
6. 240. This is obtained by multiplying 2x3x5x8.

# Exercises

+   1. int one[1000], two[1000], three[1000];
2. int array[10] = { 1, 1, 1, 1, 1, 1, 1, 1,  };
3. This exercise can be solved in numerous ways. The first way is to initialize the array when it's declared:
int inteight[88] = {88,88,88,88,88,88,88,...,88};
However, this approach requires you to place 88's between the braces (instead of using ..., as I did). I do not recommend this method for initializing such a large array. The following is a better method:
int inteight[88];\int x;
for ( x = 0; x < 88; x++ )
inteight[x] = 88;
4. The code is as follows:
int stuff[12][10];\int sub1, sub2;

```
for( sub1 = 0; sub1 < 12; sub1++ )
for( sub2 = 0; sub2 < 10; sub2++ )
stuff[sub1][sub2] = 0;
```