
4, 8, 6, 15, 9, 5, 4, 13, 8, 5, 11, 9, 9, 13, 7, 10, 6. 11

The basic unit of access in such an array is usually an individual element. Groups of consecutive elements normally do not have any special meaning.

For the above reason, various string operations have been developed which are not normally used with other kinds of arrays. This section discusses these string-oriented operations. The next section shows how these operations are used in word processing. (Unless otherwise stated or implied, we assume our character-type variables are dynamic and have a variable length determined by the context in which the variable is used.)

### Substring

Accessing a substring from a given string requires three pieces of information: (1) the name of the string or the string itself, (2) the position of the first character of the substring in the given string and (3) the length of the substring or the position of the last character of the substring. We call this operation SUBSTRING. Specifically, we write

```
SUBSTRING(string, initial, length)
```

to denote the substring of a string S beginning in a position K and having a length L.

### Example 3.4

(a) Using the above function we have:

```
SUBSTRING('TO BE OR NOT TO BE', 4, 7) = 'BE OR N'
SUBSTRING('THE END' , 4, 4) = ' END'
```

### Program 3.1

```
/* Code showing the implementation of SUBSTRING function in C */
#include <stdio.h>
#include <conio.h>

void main()
{
char S[80]=("TO BE OR NOT TO BE");
char *SUBSTR(char*,int,int);
clrscr();

printf("STRING = %s",S);
printf("\n\nSUBSTRING(S,4,7) = %s",SUBSTR(S,4,7));
getch();
}

char *SUBSTR(char *STR,int i,int j)
{
int k,m=0;
char STRRES[80];
for(k=i-1;k<=i+j-1-1;k++)
{
    STRRES[m]=STR[k];
    m=m+1;
}
STRRES[m]='\0';
return(STRRES);
}
```

Output:
STRING = TO BE OR NOT TO BE
SUBSTRING(S, 4, 7) = BE OR N

### Indexing

Indexing, also called pattern matching, refers to finding the position where a string pattern P first appears in a given string text T. We call this operation INDEX and write

```
INDEX(text, pattern)
```

If the pattern P does not appear in the text T, then INDEX is assigned the value 0. The arguments “text” and “pattern” can be either string constants or string variables.

### Example 3.5

(a) Suppose T contains the text
'HIS FATHER IS THE PROFESSOR'
Then,
INDEX(T, 'THE'), INDEX(T, 'THEN') and INDEX(T, ' THE')
have the values 7, 0 and 14, respectively.

### Program 3.2

```
/* Code showing the implementation of INDEX function in C */
#include <stdio.h>
#include <conio.h>
#include <string.h>
void main()
{
char T[80]=("HIS FATHER IS THE PROFESSOR");
int INDEX(char*,char*);
clrscr();
printf("T = %s",T);
printf("\n\nINDEX(T,'THE') = %d",INDEX(T,"THE"));
printf("\n\nINDEX(T,'THEN') = %d",INDEX(T,"THEN"));
printf("\n\nINDEX(T,' THE ') = %d",INDEX(T," THE "));
getch();
}

int INDEX(char *STR1,char *STR2)
{
 int m,n;
 int index,flag;
 for(m=0;m<strlen(STR1);m++)
 {
 index=m;
 flag=1;
 for(n=0;n<strlen(STR2);n++)
 {
 if(STR1[m+n]==STR2[n])
 ;
 else
 {
 flag=0;
 break;
 }
 }
 if(flag==0)
 continue;
 else
 return(index);
 }
 if(m==strlen(STR1))
 return(-1);
}
```

**Output:**
T = HIS FATHER IS THE PROFESSOR

INDEX(T,'THE') = 6

INDEX(T,'THEN') = -1

INDEX(T,' THE ') = 13

Remark: Since 0 is a valid index location in C, we have used -1 to denote instances where pattern does not match the text.

### Concatenation

Let S1 and S2 be strings. Recall (Sec. 3.2) that the concatenation of S1 and S2, which we denote by S1//S2, is the string consisting of the characters of S1 followed by the characters of S2.

### Example 3.6

(a) Suppose S1 = 'MARK' and S2 = 'TWAIN'. Then:
S1//S2 = 'MARKTWAIN' but S1// ' ' //S2 = 'MARK TWAIN'

(b) Concatenation is performed in C language using the strcat function, as shown below:
strcat(S1,S2); //Concatenates strings S1 and S2 and stores
the result in S1
strcat() function is part of the string.h header file; hence it must be included at the time of
pre-processing.

### Program 3.3

```
/* Code showing string concatenation in C */
#include <stdio.h>
#include <conio.h>
#include <string.h>

void main()
{
char S1[80]=("MARK");
char S2[80]=("TWAIN");
clrscr();

printf("S1 = %s",S1);
printf("\nS2 = %s",S2);
printf("\nS1//S2 = %s",strcat(S1,S2));
strcpy(S1,"MARK");
printf("\nS1//' '//S2 = %s",strcat(strcat(S1," "),S2));

getch();
}
```

Output:
S1 = MARK
S2 = TWAIN
S1//S2 = MARKTWAIN
S1//' '//S2 = MARK TWAIN

### Length

The number of characters in a string is called its length. We will write

### LENGTH(string)

for the length of a given string.

### Example 3.7

(a) Suppose S = 'COMPUTER'. Then:

LENGTH (S) = 8

Similarly,

LENGTH ('MARC TWAIN') = 10

(b) String length is determined in C language using the strlen function, as shown below:

```
x = strlen("Sunrise"); //strlen function returns an integer value
7 and assigns it to the variable X
```

Similar to strcat, strlen is also a part of string.h, hence the header file must be included at the time
of pre-processing.

### Program 3.4

```
/* Code showing the use of strlen () in C */
#include <stdio.h>
#include <conio.h>
#include <string.h>

void main()
{
char S1[80]={"COMPUTER"};
char S2[80]={"MARC"};
clrscr();

printf("Length(%s) = %d",S1,strlen(S1));
printf("\nLength(%s) = %d",S2,strlen(S2));

getch();
}
```

Output:
Length(COMPUTER) = 8
Length(MARC) = 4

## 3.7 WORD/TEXT PROCESSING

In earlier times, character data processed by the computer consisted mainly of data items, such as
names and addresses. Today the computer also processes printed matter, such as letters, articles
and reports. It is in this latter context that we use the term “word processing.”

Given some printed text, the operations usually associated with word processing are the following:

- (a) Replacement. Replacing one string in the text by another.
- (b) Insertion. Inserting a string in the middle of the text.
- (c) Deletion. Deleting a string from the text.

The above operations can be executed by using the string operations discussed in the preceding section. This we show below when we discuss each operation separately. Many of these operations are built into or can easily be defined in most of the programming languages.

### Insertion

Suppose in a given text T we want to insert a string S so that S begins in position K. We denote this operation by

```
INSERT(text, position, string)
```

For example,

```
INSERT ('ABCDEFG', 3, 'XYZ') = 'ABXYZCDEFG'
INSERT ('ABCDEFG', 6, 'XYZ') = 'ABCDEXYZFG'
```

This INSERT function can be implemented by using the string operation defined in the previous section as follows:

```
INSERT(T, K, S) = SUBSTRING(T, 1, K – 1) /// SUBSTRING(T, K, LENGTH(T) – K + 1)
```

That is, the initial substring of T before the position K, which has length K – 1, is concatenated with the string S, and the result is concatenated with the remaining part of T, which begins in position K and has length LENGTH(T) – (K – 1) = Length (T) – K + 1. (We are assuming implicitly that T is a dynamic variable and that the size of T will not become too large.)

### Deletion

Suppose in a given text T we want to delete the substring which begins at position K and has length L. We denote this operation by

```
DELETE(text, position, length)
```

For example,

```
DELETE( ' ABCDEFG ', 4, 2) = ' ABCFG '
DELETE( ' ABCDEFG ', 2, 4) = ' AFG '
```

We assume that nothing is deleted if position K = 0. Thus

```
DELETE( ' ABCDEFG ', 0, 2) = ' ABCDEFG '
```

The importance of this “zero case” is seen later.

The DELETE function can be implemented using the string operations given in the preceding section as follows:

```
DELETE(T, K, L) =
SUBSTRING(T, 1, K – 1)//SUBSTRING(T, K + L, LENGTH(T) – K – L + 1)
```

That is, the initial substring of T before position K is concatenated with the terminal substring of T beginning at position K + L. The length of the initial substring is K – 1, and the length of the terminal substring is:

LENGTH(T) - (K + L - 1) = LENGTH(T) - K - L + 1

We also assume that DELETE(T, K, L) = T when K = 0.

Now suppose text T and pattern P are given and we want to delete from T the first occurrence of the pattern P. This can be accomplished by using the above DELETE function as follows:

DELETE(T, INDEX(T, P), LENGTH(P))

That is, in the text T, we first compute INDEX(T, P), the position where P first occurs in T, and then we compute LENGTH(P), the number of characters in P. Recall that when INDEX(T, P) = 0 (i.e., when P does not occur in T) the text T is not changed.

- **Example 3.8**

  (a) Suppose T = 'ABCDEFG' and P = 'CD'. Then INDEX(T, P) = 3 and LENGTH(P) = 2. Hence
  
  DELETE ('ABCDEFG', 3, 2) = 'ABEFG'
  
  (b) Suppose T = 'ABCDEFG' and P = 'DC'. Then INDEX(T, P) = 0 and LENGTH(P) = 2. Hence, by the "zero case,"
  
  DELETE('ABCDEFG ', 0, 2) = ' ABCDEFG '
  
  as expected.

Suppose after reading into the computer a text T and a pattern P, we want to delete every occurrence of the pattern P in the text T. This can be accomplished by repeatedly applying

DELETE(T, INDEX(T, P), LENGTH(P))

until INDEX(T, P) = 0 (i.e., until P does not appear in T). An algorithm which accomplishes this follows.

- **Algorithm 3.1:** A text T and a pattern P are in memory. This algorithm deletes every occurrence of P in T.

  1. [Find index of P.] Set K := INDEX(T, P).
  2. Repeat while K ≠ 0:
     (a) [Delete P from T.]
         Set T := DELETE(T, INDEX(T, P), LENGTH(P))
     (b) [Update index.] Set K := INDEX(T, P).
     [End of loop.]
  3. Write : T.
  4. Exit.

We emphasize that after each deletion, the length of T decreases and hence the algorithm must stop. However, the number of times the loop is executed may exceed the number of times P appears in the original text T, as illustrated in the following example.
