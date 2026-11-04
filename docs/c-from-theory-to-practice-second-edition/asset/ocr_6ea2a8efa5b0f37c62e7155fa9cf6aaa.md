```
num = num ^ key;
printf("Encrypted : %d\n", num);

num = num ^ key;
printf("Original: %d\n", num);
return 0;
}
```

Comments: Since (a ^ b) ^ b = a, the result of the decryption is the input number.

# C.4.8 What is the output of the following program?

```
#include <stdio.h>
int main(void)
{
    printf("%d\n", ~(-0 << 4));
    return 0;
}
```

Answer: According to the precedence table in Appendix A, the ~ operator has higher precedence than the << operator; therefore, the expression ~0 is evaluated first, and then the result is shifted four places to the left. In a 32-bit system, the result of ~0 is the number with all 32 bits set to 1s. Therefore, the value of (~0 << 4) is the number:

11111111 11111111 11111111 11110000

Since the ~ operator reverses its bits, the value of the entire expression is:

00000000 00000000 00000000 00001111 and the program displays 15.

# C.4.9 What is the output of the following program?

```
#include <stdio.h>
int main(void)
{
    unsigned int i = 10;
    if((i >> 4) != 0)
        printf("One\n");
    else
        printf("Two\n");
    printf("%d\n", i);
    i = i;
    if((i << 3) == 8)
        printf("One\n");
    else
        printf("Two\n");
    printf("%d\n", i);
    return 0;
}
```