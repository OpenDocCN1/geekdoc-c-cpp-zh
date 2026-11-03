**Output: y.**
Because when we print s[4] then it print the 5th character of string here we use string “matrix” in the place of s and similarly of s it will print the 5th character of string that is r.

```
char a[] = {'M','A','T','R','T','X'};
int i;
for(i = 0;i<=5;i++)
printf("%c",a[i]);
```

Each time the i th of array gets printed till condition is true because the counter is start from 0 so the printing will start from 0th element and gets printed till 5 so each character of string “MATRIX” gets printed and separated by the line.

```
main()
{
char s[7]="Strings";
printf("%s",s);
}
```

Unpredictable. Here s[] has been declared as a 7 character array and into it a 8 character string has been stored. This would result into overwriting of the bytes beyond the seventh byte reserved for the array with a “0”.there is always a possibility that ...

```
{
char string[] = "Author Harry";
int a=5;
printf("a>0?%20s":"%s",string);
}
```

**Output: Author Harry**

```
main()
{
printf(5+"Computers");
}
```

**Output: ters**

```
main()
{
char s1="Matrix";
char s2="Computers";
if(s1 == s2)
printf("Equal");
else
printf("Unequal");
}
```

**Output: Unequal**

```
main()
{
printf("%c", "Matrix"[4]);
}
```

**Output: i**
15. Which is more appropriate for reading in a multi-word string?
gets()
scanf()
puts()