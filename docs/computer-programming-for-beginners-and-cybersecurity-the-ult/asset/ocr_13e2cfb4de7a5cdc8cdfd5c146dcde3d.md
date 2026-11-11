```
std::cout << "The value in the address is " << *p << std::endl;

int hold = 1;

std::cin >> hold;

return 0;

}
```

The function sizeof returns the number of bytes allocated for the array. Since char data type occupies one byte, the number of bytes returned by the sizeof function equals to the number of elements of the char array.

The integer data type occupies 4 bytes in the memory, and an array of 10 integers is stored in 40 bytes. As a result, the sizeof the array function returns 40 bytes for the integer array of 10 elements.

To calculate how many elements are stored in an array we can divide the number of bytes allocated for the whole array by the number of bytes allocated to one element of the array;

```
length=sizeof(numbers) / sizeof(numbers[0]);
```

```
40 / 4 = 10
```

To access the value of a single element, we have to use the array index. The index of array in C++ starts from 0.

The index of the first element is 0, the index of the second element is 1, and so on.

To access all elements of an array, we have to use for loop.

```
for(i=0; i<length; i++)

cout<<char_array[i];
```

If we declare a pointer and assign the array to the pointer, the pointer will hold the address of the first element of the array: