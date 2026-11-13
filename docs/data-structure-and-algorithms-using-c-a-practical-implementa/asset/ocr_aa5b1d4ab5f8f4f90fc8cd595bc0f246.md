```
```cpp
while (preced(str[top]) > preced(s))
{
    t=pop();
    pofx[px]=t;
    px++;
}
push(s);
break;
default : pofx[px++]=s;
break;
}
i=i+1;
}
while(top>-1)
{
    t=pop();
    pofx[px++]=t;
}
pofx[px++]='\0';
strrev(pofx);
puts(pofx);
return;
}
```
```

```
```cpp
int main(void)
{
    char ifx[50];
    printf("\n Enter the infix expression ::");
    gets(ifx);
    strrev(ifx);
    //scanf("%s",ifx);
    infx2prefix(ifx);
    return 0;
}
```
```

# 5.6 Questions

+   1. In which principle does STACK work?
+   2. Write some implementations of stack.
+   3. What is polish and reverse polish notation?
+   4. Write a recursive program to check the validity of an expression in terms of parenthesis (),{},[].