
int read_text(char str[], int size, int flag);
int main(void)
{
    char str1[100], str2[100];
    int i;
    printf("Enter first string: ");
    read_text(str1, sizeof(str1), 1);
    printf("Enter second string: ");
    read_text(str2, sizeof(str2), 1);
    i = str_cmp(str1, str2);
    if(i == 0)
        printf("%s = %s\n", str1, str2);
    else if(i < 0)
        printf("%s < %s\n", str1, str2);
    else
        printf("%s > %s\n", str1, str2);
    return 0;
}
int str_cmp(const char *s1, const char *s2)
{
    while(*s1 == *s2)
    {
        if(*s1 == '\0')
            return 0;
        s1++;
        s2++;
    }
    return *s1-*s2;
}

Comments: If two different characters are found, the loop terminates and the function returns their difference. The str_cmp() function is an implementation example of the strcmp() library function.

## C.11.26 What is the output of the following program?

```
#include <stdio.h>
void test(int *ptr1, int *ptr2, int a);
int main(void)
{
    int i = 1, j = 2, k = 3;
    test(&i, &j, k);
    printf("%d %d %d\n", i, j, k);
    return 0;
}
```

```c
void test(int *ptr1, int *ptr2, int a)
{
    ptr1 = ptr2;

    *ptr1 = 100;
    *ptr2 = 200;
    a = *ptr1 + *ptr2;
    printf("%d\n", a);
}
```

**Answer:** When test() is called, we have ptr1 = &i, ptr2 = &j and a = k. The statement ptr1 = ptr2; makes ptr1 point to the address of j. Therefore, the statement *ptr1 = 100; makes j equal to 100. Since ptr2 points to the address of j, the statement *ptr2 = 200; changes the value of j to 200. Since the statement a = *ptr1 + *ptr2; is equivalent to a = j+j = 200+200 = 400, test() displays 400. Since any change in the value of a does not affect k, k remains the same. As a result, the program displays:

```
400
1 200 3
```

## C.11.27 Write a function that takes as parameters a character, an integer, and a string and uses it as a pointer to check whether the character exists in the string or not. If not, it should return NULL. Otherwise, if the integer is 0, it should return a pointer to its first occurrence, otherwise to the last one. Write a program that reads a string of less than 100 characters, a character, and an integer, calls the function, and displays the part of the string. For example, if the user enters "booststrap", 't' and 0, the program should display tstrap. If it is "booststrap", 't' and 3, the program should display trap.

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int read_text(char str[], int size, int flag);
char *find(char str[], char ch, int f);

int main(void)
{
    char *ptr, ch, str[100];
    int flag;

    printf("Enter text: ");
    read_text(str, sizeof(str), 1);

    printf("Enter character to search: ");
    scanf("%c", &ch);

    printf("Enter choice (0-first, other-last): ");
    scanf("%d", &flag);

    ptr = find(str, ch, flag);
    if(ptr == NULL)
        printf("'%c' is not included in the text\n", ch);
    else
```

then the MCD is r; otherwise, this procedure is repeated. Write a program that reads two positive integers and uses the function to calculate their MCD.

```c
#include <stdio.h>

int mcd(int a, int b);

int main(void)
{
    int num1, num2;
    do
    {
        printf("Enter the first number: ");
        scanf("%d", &num1);
        printf("Enter the second number (equal or less than the first one): ");
        scanf("%d", &num2);
    } while(num2 > num1 || (num1 <= 0) || (num2 <= 0));
    printf("MCD of %d and %d is %d\n", num1, num2, mcd(num1, num2));
    return 0;
}

int mcd(int a, int b)
{
    int r;

    while(1)
    {
        r = a%b;
        if(r == 0)
            return b;
        else /* According to the algorithm, we divide b by r, so we change the values of a and b. */
        {
            a = b;
            b = r;
        }
    }
}
```

## C.11.30 What is the output of the following program?

```c
#include <stdio.h>

void test(int *arg);

int var = 100;

int main(void)
{
    int *ptr, i = 30;

    ptr = &i;
    test(ptr);
    printf("%d\n", *ptr);
    return 0;
}

void test(int *arg)
{
    arg = &var;
}
```

Answer: You answered 100, didn't you? Basket Case from Green Day, play it loud. Let's see the trap.

Since the value of ptr and not its address is passed to test(), any change in the value of arg does not affect ptr. Therefore, the program displays 30.

## C.11.31 Write a function that returns the value of the polynomial a₀ + a₁x + a₂x² +...+ aₙxⁿ for a given x. The function prototype is double poly(double a[], double x, int n); where the coefficients of the polynomial are stored into a and n represents its degree. Write a program that reads the degree of a polynomial, its coefficients, and a value (e.g., x) and uses the function to calculate the value of the polynomial. Assume that the maximum degree is 100. To calculate the power of the coefficients, use the function pow(), as shown in Appendix C.

#include <stdio.h>
#include <math.h>

#define MAX_DGR 100

double poly(double a[], double x, int n);

int main(void)
{
    int i, dgr;
    double num, arr[MAX_DGR+1];

    do
    {
        printf("Enter degree (<= %d): ", MAX_DGR);
        scanf("%d", &dgr);
    } while(dgr < 0 || dgr > MAX_DGR);

    for(i = 0; i <= dgr; i++)
    {
        printf("Enter coefficient arr[%d]: ", i);
        scanf("%lf", &arr[i]);
    }
    printf("Enter number: ");
    scanf("%lf", &num);
    printf("Poly(%f) = %f\n", num, poly(arr, num, dgr));
    return 0;
}

double poly(double a[], double x, int n)
{
    int i;
    double sum;

    sum = 0;
    for(i = 0; i <= n; i++)
        sum += a[i]*pow(x, i);
    return sum;
}

## C.11.32 What is the output of the following program?

#include <stdio.h>

float *test(float *ptr1, float *ptr2);

int main(void)
{
    float a = 1.2, b = 3.4;
    *test(&a, &b) = 5.6;
    printf("val1 = %.1f val2 = %.1f\n", a, b);
    *test(&a, &b) = 7.8;
    printf("val1 = %.1f val2 = %.1f\n", a, b);
    return 0;
}

float *test(float *ptr1, float *ptr2)
{
    if(*ptr1 < *ptr2)
        return ptr1;
    else
        return ptr2;
}

Answer: test() returns a pointer to the parameter with the smaller value. In the first call, we have ptr1 = &a, so *ptr1 = a = 1.2. Similarly, we have ptr2 = &b, so *ptr2 = b = 3.4. Therefore, test() returns the ptr1 pointer. Since test() returns a pointer to a, the statement *test(&a, &b) = 5.6; makes a equal to 5.6. Therefore, the program displays val1 = 5.6 val2 = 3.4.

The second call of test() returns the ptr2 pointer because *ptr1 = a = 5.6 and *ptr2 = b = 3.4. Like before, since test() returns a pointer to b, b becomes 7.8 and the program displays: val1 = 5.6 val2 = 7.8

## C.11.33 Write a void function that takes as parameters an array that contains the prices of some products in a shop and their number and uses proper variables to return the lowest, the highest, and the average of the prices. Write a program that reads the prices of less than 100 products and stores them in an array. If the user enters -1, the insertion of prices should terminate. The program should use the function to display the lowest, the highest, and the average of the prices.

#include <stdio.h>

void stat_arr(float arr[], int size, float *min, float *max, float *avg);

int main(void)
{
    int i;
    float min, max, avg, arr[100];

for(i = 0; i < 100; i++)
{
    printf("Enter price: ");
    scanf("%f", &arr[i]);
    if(arr[i] == -1)
        break;
}
if(i == 0)
    return 0;
/* The variable i indicates how many prices were stored into the array. For example, if the user does not enter the value -1, i would be equal to 100. */
stat_arr(arr, i, &min, &max, &avg);
printf("Max=%.2f Min=%.2f Avg=%.2f\n", max, min, avg);
return 0;
}

void stat_arr(float arr[], int size, float *min, float *max, float *avg)
{
    int i;
    float sum;
    sum = *min = *max = arr[0];
    for(i = 1; i < size; i++)
    {
        if(arr[i] > *max)
            *max = arr[i];
        if(arr[i] < *min)
            *min = arr[i];
        sum += arr[i];
    }
    *avg = sum/size;
}

## C.11.34 What is the output of the following program?

#include <stdio.h>

int *test(int *ptr1, int *ptr2);

int main(void)
{
    int arr[] = {1, 2, 3, 4};
    *test(arr, arr+3) = 30;
    printf("%d %d %d %d\n", arr[0], arr[1], arr[2], arr[3]);
    return 0;
}

int *test(int *ptr1, int *ptr2)
{
    *(ptr1+1) = 10;
    *(ptr2-1) = 20;
