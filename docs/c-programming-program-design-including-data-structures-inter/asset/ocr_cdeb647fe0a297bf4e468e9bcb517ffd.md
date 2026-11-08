8. What is stored in `list` after the following C++ code executes?

```
int list[10];

for (int i = 0; i < 5; i++)
{
    list[i] = i * i - 5;
    if (i % 3 == 0)
        list[i] = list[i] + i;
    else
        list[i] = list[i] - i;
}
```

9. What is stored in `list` after the following C++ code executes?

```
int list[10];

list[0] = 2;
list[1] = 3;
for (int i = 2; i < 10; i++)
{
    list[i] = list[i - 1] + list[i - 2];
    if (i > 7)
        list[i] = 2 * list[i] - list[i - 2];
}
```

10. What is stored in `myList` after the following C++ code executes?

```
double myList[5];

myList[0] = 3.0;
myList[1] = 4.0;

for (int i = 2; i < 5; i++)
{
    myList[i] = myList[i - 1] * myList[i - 2];
    if (i > 3)
        myList[i] = myList[i] / 4;
}
```

11. Correct the following code so that it correctly sets the value of each element of `myList` to the index of the element.

```
int myList[10];

for (int i = 1; i <= 10; i--)
    myList[i] = i;
```

12. Correct the following code so that it correctly initializes and outputs the elements of the array `myList`.

```
int myList[10];

for (int i = 1; i <= 10; i++)
    cin >> myList;
```