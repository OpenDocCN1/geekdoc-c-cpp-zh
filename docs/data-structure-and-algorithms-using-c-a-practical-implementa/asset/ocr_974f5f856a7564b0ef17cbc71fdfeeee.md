```
case '+' :
case '-' :
case '*' :
case '/' :
    while(prec(str[top])>prec(s))
    {
    t=pop();
    pofx[px++]=t;
    px++;
    }
    push(s);
    break;
default : pofx[px++]=s;
    break;
}
i=i+1;
}
```

```
while(top>-1)
{
t=pop();
pofx[px++]=t;
}
pofx[px++]='\0';
puts(pofx);
return;
}
```

```
//driver program
int main(void)
{
char ifx[50];
cout<<endl<<"Enter the infix expression";
//read the infix expression
gets(ifx);
infx2pofx(ifx); //call to the method
return 0;
}
```