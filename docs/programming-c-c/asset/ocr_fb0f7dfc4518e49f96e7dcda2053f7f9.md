Lab Programming 277

```
for(i=0; s[i]!='0';++i);
```

```
printf("Length of the string: %d", i);
return 0;
}
```

# Output

Length of the string: 18

# 35. Write a C Program to concatenate two strings.

```
#include<stdio.h>
int main(){
  char s1[100]="programming ", s2[]="awesome";
  int i, j;
```

```
// length of s1 is stored in i
for(i=0; s1[i]!='0';++i)
printf("%i = %d\n", i);
}
```

```
// concatenating each character of s2 to s1
for(j=0; s2[j]!='0';++j,i){
  s1[i]=s2[j];
}
```

```
// terminating s1 string
s1[i]='0';
```

```
printf("After concatenation: ");
puts(s1);
return 0;
}
```

# Output

After concatenation: programming is awesome

# 36. Write a C Program to copy string without using strcpy().

```
#include<stdio.h>
int main(){
  char s1[100], s2[100], i;
  printf("Enter string s1: ");
```