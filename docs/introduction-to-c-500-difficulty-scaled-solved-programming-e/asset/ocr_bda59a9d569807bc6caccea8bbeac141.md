# 312 Introduction to C++

```
for(i = 1; i < size; i++)
{
    if(v[i] > *max)
        *max = v[i];
    if(v[i] < *min)
        *min = v[i];
    sum += v[i];
}
*avg = sum/size;
```

# C.11.19 What is the output of the following program?

```
#include <iostream>

void swap(const char *s1, const char *s2)

int main()
{
    const char *p[] = { "Shadow", "Play" };

    swap(p[0], p[1]);
    std::cout << p[0] << ' ' << p[1] << '\
';
    return 0;
n
```

```
void swap(const char *s1, const char *s2)
{
    const char *p;

    p = s1;
    s1 = s2;
    s2 = p;
}
```

Answer: What kind of play is that, did you answer Play Shadow? Read the answer of the example C.11.8. It is the only song to change; Shadow Play from the great Rory Gallagher.
As (test) in example C.11.8, swap() takes as arguments the values of the pointers, not their addresses. Therefore, the swapping has no effect and the program displays Shadow Play. What you want to do is to modify the program in order to output Play Shadow. Let's see, can you do that? To give you a hint, change the type of the parameters to... find it, no more to say.

# C.11.20 Write a function that takes as parameter array and checks if it contains duplicated values. If so, the function returns a pointer to the element which appears the most times, otherwise nullptr. Write a program that reads 100 integers, stores them in an array and uses the function to display the element with the most occurrences. Note: if more than one element appears the same most times, the function should return the first found.

```
#include <iostream>

const int *find(const int arr[])
const int SIZE = 100;
```