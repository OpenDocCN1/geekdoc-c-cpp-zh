
```
{
    if(str[i] == ' ' || str[i] == '\t')
    {
        /* Since more than one space character may be included between words, we check if the next character, that is str[i+1], is also a space character. If it isn't, it means that a new word begins, so the value of words is increased. */
        if(str[i+1] != ' ' && str[i+1] != '\t' && str[i+1] != '\0')
        {
            words++;
            printf("\n");
        }
    }
    else
        printf("%c", str[i]);
    i++;
}
printf("\nThe text contains %d words\n", words);
return 0;
}
```

### C.10.34
A simple algorithm to encrypt data is the algorithm of the single transformation. Let’s see how it works. In one line, we write the letters of the used alphabet. In a second line, we write the same letters in a different order. This second line constitutes the cryptography key. For example, see Figure 10.2.

Each letter of the original text is substituted with the respective key letter. For example, the word test is encrypted as binb.

Write a program that reads a string of less than 100 characters, the key string consisting of 26 characters, and encrypts the lowercase letters of the input string. Then, the program should decrypt the encrypted string and display it (should be the same with the original string). The program should check that the key characters are 26 and appear only once.

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define LETTERS 26

int read_text(char str[], int size, int flag);

int main(void)
{
    char str[100], key[LETTERS+1];
    int i, j, len, error;
```

![](img/b8da5dcf9ba7f1fad5213c453d095246_310_0.png)

### FIGURE 10.2
Single transformation algorithm.

```
~~~c
printf("Enter text: ");
len = read_text(str, sizeof(str), 1);
do
{
    error = 0;
    printf("Enter key (%d different characters): ", LETTERS);
    read_text(key, sizeof(key), 1);
    if(strlen(key) != LETTERS)
    {
        printf("Error: Key must be of %d characters\n", LETTERS);
        error = 1;
    }
    else
    {
        for(i = 0; i < LETTERS; i++)
        {
            for(j=i+1; j < LETTERS; j++)
            {
                if(key[i] == key[j])
                {
                    error = 1;
                    printf("Key characters must be different\n");
                    getchar();
                    break;
                }
            }
            if(error == 1)
                break;
        }
    }
}while(error != 0);

for(i = 0; i < len; i++)
{
    if(str[i] >= 'a' && str[i] <= 'z')
        str[i] = key[str[i]-'a'];
}
printf("Encrypted text: %s\n", str);
for(i = 0; i < len; i++)
{
    for(j = 0; j < LETTERS; j++)
    {
        if(str[i] == key[j])
        {
            str[i] = 'a'+j;
            break;
        }
    }
}
printf("Original text: %s\n", str);
return 0;
}
~~~
```

## Exercises

### C.10.35
What is the output of the following program?

```
```c
#include <stdio.h>
int main(void)
{
    char arr[7][10] = {"Monday", "Tuesday", "Wednesday", "Thursday",
"Friday", "Saturday", "Sunday"};
    int i;

    for(i = 0; i < 7; i++)
        if(arr[i][2] == 'n' && *(arr[i]+3) == 'd' && *(*(arr+i)+4)
== 'a')
            printf("%s is No.%d week day\n", arr[i], i+1);

    return 0;
}
```
```

Answer: The characters of "Monday" are stored in the first row of arr, the characters of "Tuesday" in the second row, and so on. Remember that *(arr[i]+3) is equivalent to arr[i][3] and *(*(arr+i)+4) is equivalent to *(arr[i]+4), that is, arr[i][4]. Therefore, the loop checks each row of arr and displays the strings whose third, fourth, and fifth characters are 'n', 'd' and 'a', respectively. Therefore, the program displays:

```
```
Monday is No.1 week day
Sunday is No.7 week day
```
```

### C.10.36
Write a program that reads 10 strings (less than 40 characters each) and stores in an array those that begin with an 'a' and end with 's'. Then, the program should read a character and display in which column it occurs most. If there is more than one column with the same most occurrences, the program should display the one found first.

```
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define NUM 10

int read_text(char str[], int size, int flag);

int main(void)
{
    char tmp[40], str[NUM][40] = {0};
    int i, j, ch, num, len, max_len, cnt, max_cnt, col;

    num = max_len = 0;
    for(i = 0; i < NUM; i++)
    {
        printf("Enter text: ");
        len = read_text(tmp, sizeof(tmp), 1);
        if(tmp[0] == 'a' && tmp[len-1] == 's')
```
```
{
    strcpy(str[num], tmp);
    num++;
    if(len > max_len)
        max_len = len;
}
}
if(num == 0)
{
    printf("None string is stored\n");
    return 0;
}
printf("Enter character: ");
ch = getchar();
max_cnt = 0;
/* We use the length of the longest string and the number of the
stored strings, to search for the character only in those rows and
columns where characters are stored. */
for(j = 0; j < max_len; j++)
{
    cnt = 0;
    for(i = 0; i < num; i++)
    {
        if(str[i][j] == ch)
            cnt++;
    }
    if(cnt > max_cnt)
    {
        max_cnt = cnt;
        col = j;
    }
}
if(max_cnt == 0)
    printf("%c is not stored\n", ch);
else
    printf("Max appearances of %c is %d in col_%d\n", ch, max_cnt, col+1);
return 0;
}
```

### C.10.37
Write a program that reads 20 names (less than 100 characters each), stores them in an array, and uses an array of pointers to display them in alphabetical order.

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define SIZE 20

int read_text(char str[], int size, int flag);

int main(void)
```
```
{
    char *temp, *ptr[SIZE], str[SIZE][100];
    int i, j;

    for(i = 0; i < SIZE; i++)
    {
        printf("Enter name: ");
        read_text(str[i], sizeof(str[i]), 1);
        ptr[i] = str[i]; /* The elements of the array point to the input strings. */
    }
    for(i = 0; i < SIZE-1; i++)
    {
        for(j = i+1; j < SIZE; j++)
        {
            /* If the string pointed to by ptr[j] is less than the string pointed to by ptr[i], swap the respective pointers. */
            if(strcmp(ptr[j], ptr[i]) < 0)
            {
                temp = ptr[j];
                ptr[j] = ptr[i];
                ptr[i] = temp;
            }
        }
    }
    for(i = 0; i < SIZE; i++)
        printf("%s\n", ptr[i]);
    return 0;
}
```

### Comments
The main reason we added this exercise is to show you how useful an array of pointers might be. When two strings must be swapped, it is the respective pointers that are swapped, not the strings. As a result, we gain in performance. The sorting algorithm we used is called selection sort and it will be discussed in Chapter 12. The “negative” point in this solution is the potential waste of space. Each row of str allocates 100 characters, even if the string contains less. In Chapter 14 and the exercise C.14.8, you’ll see a more efficient way where the exact memory needed is dynamically allocated instead of using a fixed two-dimensional array.

## Unsolved Exercises

- **U10.1** Write a program that reads characters until the sum of their ASCII values exceeds 500 or the user enters ‘q’. The program should display how many characters were read.
- **U10.2** Write a program that reads characters and displays how many characters between the first two consecutive ‘*’ are: (a) letters, (b) digits, and (c) other than letters and digits. If no two ‘*’ occur, the program should display a related message. For example, if the user enters: `1abc*D2Efg #!*345Higkl*mn+op*qr` the program should display the following: `Between first two stars (letters:4, digits:1, other:3).`

U.10.3 Write a program that reads three strings of less than 100 characters and stores them in three arrays (e.g., str1, str2, and str3). Then, the program should copy their contents one place right, meaning that the content of str3 should be copied to str1, the content of str1 to str2, and that of str2 to str3.

U.10.4 Write a program that reads a string of less than 100 characters, and if it ends with aa, the program should display it in reverse order.

U.10.5 What is the output of the following program?

```
```c
#include <stdio.h>
#include <string.h>
int main(void)
{
    char str[] = "test", *p = str;
    *str = str[strlen(str)];
    while(*p)
        printf("%s", p++);
    return 0;
}
```
```

U.10.6 Write a program that reads a string of less than 100 characters and stores it in an array. Then, the program should reverse the stored string and display the new one. For example, if the string code is stored, the program should reverse it and store in the array edoc. Use just one array.

U.10.7 Write a program that reads a string of less than 100 characters, how many characters are going to be deleted, and the position of the first character to be deleted. After the deletion, the rest part of the string should be shifted to the left, a number of places equal to the number of deleted characters. The program should display the string before it ends. For example, if the input string is test case and the numbers are 4 and 2, the program should display tcase. The program should check the validity of the input numbers in order to ensure that the characters are contained in the string,

U.10.8 Write a program that reads two strings of less than 100 characters and displays how many times the second string is contained in the first one. The length of the second string should be less than or equal to the first one.

U.10.9 Write a program that reads a string of less than 100 characters and stores it in an array. Then, the program should delete from the array all the characters that are not letters, and the multiple repetitions of the same letter, and display the new string. For example, if the string ja*%&cr1*c is stored in the array, the program should change its content to ja cr. There is one restriction; don't use a second array to store the characters that are not deleted.

U.10.10 Modify C.10.33 in order to display the words in reverse order. For example, if the user enters imagine the case, the program should display case the imagine.
