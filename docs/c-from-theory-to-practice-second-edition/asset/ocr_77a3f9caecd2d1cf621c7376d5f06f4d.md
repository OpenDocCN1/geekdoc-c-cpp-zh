When you use the << operator to store the shifting result into a variable, make sure the type of the variable is large enough to hold the value. For example, consider the following program:

```
```
#include <stdio.h>
int main(void)
{
    unsigned char a = 1;

    a <<= 8; /* Equivalent to a = a << 8; */
    printf("%d\n", a);
    return 0;
}
```
```

The statement a <<= 8; shifts the value of a eight places to the left and inserts eight zero bits at the right. Therefore, the shifting result is 100000000. However, since a is declared as unsigned char, it can hold only the value of the eight low-order bits. Therefore, the program displays 0 and not 256, as you might expect. If it were declared as int, the program would display 256.

Let's see another example. If we write:

```
```
char a = 8;
a <<= 4;
```
```

the value of a is shifted four places to the left and becomes 10000000. If the char type is signed, the leftmost bit is reserved for the sign of the number and a becomes -128. If a were declared as unsigned char, its value would be 128.

> > Remember, it is safer to perform bitwise operations on unsigned types.

# ## Exercises

C.47 The ^ operator is often used in data encryption. For example, write a program that reads an integer that corresponds to the cipher key and another integer that will be encrypted with that key. The encryption is performed by applying the ^ operator on them. Then, the program should use once more the ^ operator to decrypt the encrypted result.

```
```
#include <stdio.h>
int main(void)
{
    int num, key;

    printf("Enter key: ");
    scanf("%d", &key);

    printf("Enter number: ");
    scanf("%d", &num);
```
```