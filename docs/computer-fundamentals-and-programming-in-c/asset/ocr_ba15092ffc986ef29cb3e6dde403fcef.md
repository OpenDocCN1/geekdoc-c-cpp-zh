```
```text
/1234.560 /
/ 1234.560/
/ 1.235e+03/
```
```

26. Print character strings.

# Solution

```
```c
#include <stdio.h>
#define BLURB "Outstanding Program!"
int main()
{
    printf("%/2s/n",BLURB);
    printf("%/22s/n",BLURB);
    printf("%/22.5s/n",BLURB);
    printf("%/-22.5s/n",BLURB);
    return 0;
}
```
```

# Output

```
```text
/Outstanding Program!/
/ Outstanding Program!/
/                      Outst/
/Outst                 /
```
```

27. Write a program that prints the next character for the corresponding three characters given to the program.

# Solution

```
```c
#include <stdio.h>
int main()
{
    char a,b,c;
    scanf("%c%c%c",&a,&b,&c);
    a++;
    b++;
    c++;
    printf("a=%c b=%c c=%c",a,b,c);
    return 0;
}
```
```

```
```text
Input PQR
Output a=Q b=R c=S
```
```

28. Determine how much money is in a piggy bank that contains several 50, 25, 20, 10, and 5 paise coins. Use the following values to test the program: five 50 paise coins, three 25 paise coins, two 20 paise coins, one 10 paise coin, and fifteen 5 paise coins.

# Solution

```
```c
/* To determine how much money there is in a piggy bank */
#include <stdio.h>
#include <string.h>
int main(void)
{
    float coin1=0.50,coin2=0.25,coin3=0.20,
          coin4=0.10, coin5=0.05,total=0.0;
    int ncoins;
    printf("How many 50 paise coins : ");
    scanf("%d",&ncoins);
```
```

```
```c
    total += (ncoins * coin1);
    printf("% .2f **",total);

    printf("\nHow many 25 paise coins : ");
    scanf("%d",&ncoins);
    total += (ncoins * coin2);
    printf("% .2f **",total);

    printf("\nHow many 20 paise coins : ");
    scanf("%d",&ncoins);
    total += (ncoins * coin3);
    printf("% .2f **",total);

    printf("\nHow many 10 paise coins : ");
    scanf("%d",&ncoins);
    total += (ncoins * coin4);
    printf("% .2f **",total);

    printf("\nHow many 5 paise coins : ");
    scanf("%d",&ncoins);
    total += (ncoins * coin5);
    printf("\n\nThe total amount is Rs.% .2f",total);
    return 0;
}
```
```

# Output

```
```text
How many 50 paise coins : 5
 ** 2.50 **
How many 25 paise coins : 3
 ** 3.25 **
How many 20 paise coins : 2
 ** 3.65 **
How many 10 paise coins : 1
 ** 3.75 **
How many 5 paise coins : 15
The total amount is Rs 4.50
```
```

29. Modify the program given in Example 28 to accept the total amount (in rupees) and convert them into paise (vice-versa of Example 28)

# Solution

```
```c
#include <stdio.h>
#include <string.h>
int main(void)
{
    int nc1,nc2,nc3,nc4,nc5,temp;
    float total;
    printf("Enter the amount : ");
    scanf("%f",&total);
    temp = total * 100;
    nc1 = temp / 50;
    temp = temp % 50;

    nc2 = temp / 25;
    temp = temp % 25;

    nc3 = temp / 20;
    temp = temp % 20;
```
```