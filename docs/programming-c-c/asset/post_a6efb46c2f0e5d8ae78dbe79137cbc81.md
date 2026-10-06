
arr[0]=arr[i];
}

printf("Largest element = %d",arr[0]);

return 0;
}

Output
Enter the number of elements (1 to 100): 5
Enter number1: 5
Enter number2: 56
Enter number3: 43
Enter number4: 27
Enter number5: 78
Largest element = 78

# 33. Write a C Program to add two matrices using multi-dimensional arrays.

```c
#include <stdio.h>
int main(){
    int r, c, a[100][100], b[100][100], sum[100][100], i, j;
    printf("Enter the number of rows (between 1 and 100): ");
    scanf("%d",&r);
    printf("Enter the number of columns (between 1 and 100): ");
    scanf("%d",&c);
    printf("\nEnter elements of 1st matrix:\n");

printf("\nEnter elements of 2nd matrix:\n");

// adding two matrices
for(i=0; i<r;i++)
for(j=0; j<c;j++){
sum[i][j] = a[i][j] + b[i][j];
}

return 0;
}
```

Output
Enter the number of rows (between 1 and 100): 2
Enter the number of columns (between 1 and 100): 3
Enter elements of 1st matrix:
Enter element a11: 2
Enter element a12: 3
Enter element a13: 4
Enter element a21: 5
Enter element a22: 2
Enter element a23: 3
Enter elements of 2nd matrix:
Enter element b11: -4
Enter element b12: 5
Enter element b13: 3
Enter element b21: 5
Enter element b22: 6
Enter element b23: 3
Sum of two matrices:
-2 8 7
10 8 6

# 34. Write a C Program to find the length of a string.

```c
#include<stdio.h>
int main(){
    char s[]="Programming is fun";
int i;

for(i=0; s[i]!='\0';++i);

printf("Length of the string: %d", i);
return 0;
}
```

# Output

Length of the string: 18

# 35. Write a C Program to concatenate two strings.

```c
#include<stdio.h>
int main(){
  char s1[100]="programming ", s2[]="awesome";
  int i, j;

// length of s1 is stored in i
for(i=0; s1[i]!='\0';++i)
  printf("%i = %d\n", i);

// concatenating each character of s2 to s1
for(j=0; s2[j]!='\0';++j,i){
  s1[i]=s2[j];
}

// terminating s1 string
s1[i]='\0';

printf("After concatenation: ");
puts(s1);
return 0;
}
```

# Output

After concatenation: programming is awesome

# 36. Write a C Program to copy string without using strcpy().

```c
#include<stdio.h>
int main(){
  char s1[100], s2[100], i;
  printf("Enter string s1: ");

fgets(s1,sizeof(s1),stdin);

for(i=0; s1[i]!='\0'; ++i) {
  s2[i] = s1[i];
}

s2[i]='\0';
printf("String %s", s2);
return(0);
}
```

Output
Enter string s1: Indrakantishar.
String s2: Indrakantishar

# 37. Write a C Program to count the number of vowels, consonants and on.

```c
#include<stdio.h>
int main(){
  char line[100];
  int vowels, consonant, digit, space, i;

  vowels = 0; consonant = 0; digit = 0; space = 0;

  printf("Enter a line of string: ");
  fgets(line,sizeof(line),stdin);

  for(i=0; line[i]!='\n'; i) {
    if(line[i]=='a' || line[i]=='e' || line[i]=='i' || line[i]=='o' || line[i]=='u') {
      vowels++;
    } else if(line[i]>='a' && line[i]<='z') {
      consonant++;
    } else if(line[i]>='0' && line[i]<='9') {
      digit++;
    } else if(line[i]==' ') {
      space++;
    }
  }

  printf("Vowels: %d", vowels);
  printf("Consonants: %d", consonant);
  printf("Digits: %d", digit);
  printf("Spaces: %d", space);
  return 0;
}
```

Output
Enter a line of string: Indrakantishar
Vowels: 5
Consonants: 9
Digits: 0
Spaces: 0

# 38. Write a C Program to find frequency of characters in a string.

```c
#include<stdio.h>
int main(){
  char str[100],ch;
  int count = 0, i;

  printf("Enter a string: ");
  gets(str,sizeof(str),stdin);

  printf("Enter a character to find frequency: ");
  scanf("%c", &ch);

  for(i=0;str[i]!='\0';++i){
    if(str[i]==ch)
      count++;
  }

  printf("Frequency of %c = %d",ch,count);
  return0;
}
```

Output
Enter a string: This is awesome.
Enter a character to find frequency: o
Frequency of o = 2

# 39. Write a C Program to access array elements using pointer.

```c
#include<stdio.h>
int main(){
    int commerce[5];

    printf("Enter elements: \n");
    for(i=0; i <5;++i)
        scanf("%d", &commerce+ i);

    printf("You entered: \n");
    for(i=0; i <5;++i)
        printf("%d\n",*(commerce+ i));
    return 0;
}
```

Output
1
2
3
5
4
You entered:
1
2
3
5
4

# 40. Write a C Program to create, initialize, assign and access a pointer variable.

```c
#include <stdio.h>

int main(){
    int num;/*declaration of integer variable*/
    int *pNum;/*declaration of integer pointer*/

    pNum=&num;/*assigning address of num*/
    num=100;/*assigning 100 to variable num*/

    //access value and address using variable num
    printf("Using variable num: %d\n", num);
    printf("value of num: %d address of num: %p\n", *pNum,pNum);
    //access value and address using pointer num
    printf("Using pointer variable: %d\n", *pNum);
    return 0;
}
```

Output
Using variable num: 100
value of num: 100 address of num: 0x276456484
Using pointer variable: 100

# 41. Write a C program to swap two numbers using pointers.

```c
#include <stdio.h>
// function : swap two numbers using pointers
void swap(int *a, int *b)
{
    int t;
    t = *a;
    *a = *b;
    *b = t;
}

int main()
{
    int num1,num2;

    printf("Enter value of num1: %d", &num1);
    scanf("%d", &num1);
    printf("Enter value of num2: %d", &num2);
    scanf("%d", &num2);

    // print values before swapping
    printf("Before Swapping: num1=%d,num2=%d\n", num1, num2);

    // call function by passing addresses of num1 and num2
    swap(&num1,&num2);

    // print values after swapping
    printf("After Swapping: num1=%d,num2=%d\n", num1,num2);
    return0;
}
```

Output
Enter value of num1: 10
Enter value of num2: 20
Before Swapping: num1=10,num2=20
After Swapping: num1=20,num2=10

# 44. Write a C Program to add two distances (in-feet) using structures.

```c
#include<stdio.h>
structDistance{
    int feet;
    float inch;
};

int d1, d2,sumOfDistances;
int main(){
    printf("Enter information for 1st distance\n");
    printf("Enter feet: %d\n");
    scanf("%d",&d1.feet);
    printf("Enter inch: %f\n");
    scanf("%f",&d1.inch);
    printf("nEnter information for 2nd distance\n");
    printf("Enter feet: %d\n");
    scanf("%d",&d2.feet);
    printf("Enter inch: %f\n");
    scanf("%f",&d2.inch);

    sumOfDistances.feet=d1.feet+d2.feet;
    sumOfDistances.inch=d1.inch+d2.inch;
    // If inch is greater than 12, changing it to feet
    if(sumOfDistances.inch>12.0){
        sumOfDistances.inch=sumOfDistances.inch-12.0;
        +sumOfDistances.feet;
    }
    printf("nSum of distances = %d-%.1f'\n",sumOfDistances.feet,sumOfDistances.inch);
    return 0;
}
```

Output
Enter information for 1st distance
Enter feet: 23
Enter inch: 8.6
Enter information for 2nd distance
Enter feet: 34
Enter inch: 2.4
Sum of distances = 57-11.0
