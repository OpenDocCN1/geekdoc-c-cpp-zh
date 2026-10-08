
## Output 2

Enter string one: C programming
Enter string two: C Programming
Strings "C programming" and "C Programming" are not same.

## Output 3

Enter string one: C Programming
Enter string two: C Programming
Strings "C Programming " and "C Programming" are not same.

It can be observed in Program 3 that the function strcmp takes an input of two character pointers. The first pointer points to the starting character of the first string, while the second pointer points to the starting character of the second string. It returns back an integer value that can be zero, positive, or negative.

The function strcmp starts by comparing characters stored at index 0 of both strings. If the character at index 0 of both the string is not same, then the function returns difference in ASCII values of character in string two and string one. In case the character at index 0 of both strings is same, we increment the index value by 1 and repeat the process of comparison until a mismatch is found. If the difference returned is positive, then the string one is greater than the string two; if the difference returned is negative, then the string one is less than the string two. If there is no mismatch of ASCII values, then zero is returned and the strings are said to be equal. The strings of ASCII valued to be case sensitive in Program 3; hence, character *V* is not equal to *v*.

Figure 4 shows how the three outputs have come:

![](img/5d422ba7108ffdf64376be51eaf0c459_223_0.png)

It can be observed in the first case of Figure 4 that the function does not find a mismatch. This causes the function to return a value zero, indicating that string one and string two are same. In the second case, the function finds a mismatch at the third character. The character stored at index *Z* of string *s_str1* is lower case *p*, while in string *s_str2*, it is upper case *P*. The function hence returns the difference in ASCII value of lower case *p* (112) and upper case *P* (80). The resultant value, as it turns out to be greater than zero, indicates that string one will come after string two in the dictionary. Similarly, in case three, the mismatch occurs at the sixth character. The function returns a negative value, indicating that string one will come before string two in the dictionary. The next section discusses how to append string two at the end of string one.

## Append Two Strings

Many applications have a need to append one string at the end of another string. This operation is known as concatenation of strings. The concatenation operation of second string on first string when performed, modifies the first string, while the second string remains the same. Program 4 illustrates how to append two strings:

## Program 4

```c
/* Program to append strings */
#include<stdio.h>
#define MAX 25

/* Function to append two strings */
char *strcat(char *s_str1, char *s_str2)
{
	int i_ctr1,i_ctr2, i_len1,i_len2;

	/* Find length of both strings */
	i_len1 = strlen(s_str1);
	i_len2 = strlen(s_str2);

	/* Check that length of source is big enough to hold both strings */
	if (MAX >= i_len1 + i_len2 + 2)
	{
		s_str1[i_len1] = ',';
		/* Transfer characters from string 2 to 1 */
		for ( i_ctr1 = i_len1+1, i_ctr2=0; i_ctr2 < i_len2; i_ctr1++,
			i_ctr2++)
			s_str1[i_ctr1] = s_str2[i_ctr2];
		s_str1[i_ctr1]='\0';
		return s_str1;
	}
	else
		return NULL;
}
/* End of Function */

/* Beginning of main function */
main()
{
	/* Declare character array */
	char s_str1[MAX], s_str2[MAX];
	char *p_result, c_temp;
	int i_len;

	/* Read strings */
	printf("\nEnter a string one : ");
	scanf("%[^\n]",&s_str1);
	c_temp=getchar();

        printf("\nEnter a string two : ");
        scanf("%[^\n]", &s_str2);

        p_result = strcat(s_str1, s_str2);
        if (p_result == NULL)
        {
            printf("\nStrings cannot be concatenated ");
        }
        else
        {
            printf("\n\nThe modified strings are \"%s\" and \"%s\".", s_str1, s_str2);
        }
        return;
    } /* End of function main */
```

**Output 1:**
Enter a string one: Proud to
Enter a string two: be Indian
The modified strings are "Proud to be Indian" and "be Indian".

**Output 2:**
Enter a string one: Please see that
Enter a string two: you do not fall
Strings cannot be concatenated

It can be observed in Program 4 that the function strcat takes an input of two character pointers and returns back a character pointer of the first string. Figure 5 shows the memory representation of concatenation operation performed in Output 1 of Program 4:

![](img/5d422ba7108ffdf64376be51eaf0c459_225_0.png)

It can be observed in Figure 5 that after the concatenation operation, s_str1 gets modified, while s_str2 remains unmodified. The next section discusses how to reverse the contents of a string.

## Reverse a String

The string reverse operation swaps the contents of the first index elements with the last index element, the second index element with the second last index element, and so on till the mid index is reached. Program 5 illustrates how to reverse a string:

## Program 5

```c
/* Program to reverse a string */
#include<stdio.h>
#include<string.h>

/* Function to reverse a string */
char *strrev(char *s_str)
{
/* Declare front counter, back counter and length */
int i_fctr, i_bctr, i_len;
char c_temp;

i_len= strlen(s_str);

/* Reverse the string */
for ( i_fctr=0, i_bctr= i_len-1;  i_fctr< i_len/2; i_fctr++,  i_bctr--)
{
c_temp= s_str[i_fctr];
s_str[i_fctr]= s_str[i_bctr];
s_str[i_bctr]= c_temp;
}
s_str[i_len]='\0';
return s_str;
}
/* End of function */

/* Beginning of main function */
main()
{
/* Declare character array */
char s_str[25];

/* Read data in array */
printf("\nEnter a string : ");
scanf("%[^\n]" , &s_str );

strrev(s_str);

/* Print reversed string */
printf("\nThe reversed string: %s\n",s_str);
return;
}
/* End of function main */
```

**Output:**

Enter a string : Good Morning
The reversed string: gniMrooM dooG

It can be observed in Program 5 that the function strrev takes an input of one character pointer and returns back a character pointer of the same string. Figure 6 shows the memory representation of the string before and after the operations are performed:

![](img/5d422ba7108ffdf64376be51eaf0c459_227_0.png)

**Figure 6: Example of Reverse Operation**

It can be observed in Figure 6 that except for NULL character, the contents of all the indexes have changed. If the string has odd length, then the content of middle index will also remain the same. The next section discusses how to convert a given string into lower case string.

## Converting String to Lower Case

Case conversion is a normal operation performed on strings while editing a text. We may convert an upper case string to lower case string, and vice versa. It is also possible to convert a string to title case (proper case) also. We make use of the ASCII values to perform the case-conversion operation. Program 6 illustrates how to convert a string given in any case to lower case string:

## Program 6

```c
/* Program to illustrate case conversion of string */

#include<stdio.h>

/*  Function to convert case */
char   *strlower(char *s_str)
{

    int i_ctr,i_len;
    i_len = strlen(s_str);

    for ( i_ctr=0; i_ctr < i_len; i_ctr++)
    {
        if ( s_str[i_ctr] >= 'A' && s_str[i_ctr] <= 'Z')
            s_str[i_ctr] = s_str[i_ctr] + 32;
    }
    s_str[i_ctr]='\0';
    return s_str;
}
/*  End of Function */

/*  Beginning of main function */
main()
{
    /*  Declare character array */
    char s_str[25];

    /*  Read data in array */
    printf("\nEnter a string : ");
    scanf("%[^\n]",&s_str);

    strlower(s_str);
    /* Print string */
    printf("\nThe lower case string: %s\n",s_str);
    return;
}
/* End of function main */
```

**Output:**

Enter a string : PROUD TO BE INDIAN
The lower case string: proud to be indian

It can be observed in Program 6 that the function strlower takes an input of one character pointer and returns back a character pointer of the same string. Figure 7 shows the memory representation of the string before and after the operations are performed:

![](img/5d422ba7108ffdf64376be51eaf0c459_228_0.png)

It can be observed in Figure 7 that except for the NULL character, all the characters have changed to lower case characters. Note that the ASCII value of the character will be modified only if the character is an upper case alphabet. In all other cases, the characters within the string will not be modified.

The character arrays discussed so far were single dimensional. We can store only one name in such arrays. Practical scenarios need us to store many names at a time. For example, the application that is used for student mark sheet generation may need us to store names of all students in a class. To implement such a feature, we need multidimensional character arrays. The next section discusses the concept of multidimensional character arrays.

## 10.6 Array of Strings

An array of strings refers to a multidimensional character array. We have already learned in Chapter 9 that multidimensional array uses two indexes. The syntax to define the array of string is as follows:

```c
char s_student_name[3][15];
```

The preceding definition helps to store three students name, each having a maximum length of 14 characters. The multidimensional character array can also be initialized at compile time. The syntax for initializing multidimensional character array at run time is as follows:

```c
char s_student_name[3][15]={ "Jain Harshit","Aroklar Vidita","Jain Navya"};
```
