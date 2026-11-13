```
```cpp
B.Str[i] = Str[i];
B.Str[i] = '\0'; // Append the termination character
return B;
}

String String :: Copy_Reverse()
{
int i, 1, Len_A;
for(i = 0; Str[i] != '\0'; i++);
// loop terminates after reaching end of A
Len_A = 1--;
for(i = 1, j = 0; i >= 0; i--, j++)
B.Str[j] = Str[i];
B.Str[j] = '\0'; //Append termination character
return B;
}

void String :: Rev_String()
{
int i, len = 0;
//exchange i^th and j^th characters till middle position
char t;
for(len = 0; Str[len] != '\0', len++);
for(i = 0, j = len - 1; i != j; i++, j--)
{
t = Str[i]; Str[i] = Str[j]; Str[j] = t;
}
}

int String :: Str_cmp(String A, String B)
{
int i = 0;
if (A.Length() != B.Length())
return(0);
while
(A.Str[i] == B.Str[i] && A.Str[i] != '\0' &&
B.Str[i] != '\0')
++ i;
if(A.Str[i] == '\0' && B.Str[i] == '\0')
return(1);
else
return(0);
}
```
```