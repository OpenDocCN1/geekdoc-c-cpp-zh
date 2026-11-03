```
puts("\nType character:\n");asc.k=getchar();asc.i=asc.k;
    printf("%6d %c Number: %6d\n", asc.k, asc.k, asc.i);}
```

# unsigned (rem.: with math.h)

```
main() {unsigned int n;n=fabs(floor(log10(.005)));
    printf("\n abs(log(x))=%d\n",n);}
```

# void

```
void Answer(){printf("\nDisobedient!");}
main(){char j;puts("\nType anything, except '*',");
    j=getchar();if(j!='*') printf("\nAsc %d",j); else Answer();}
```

# volatile

```
main(){volatile float u,x=0; puts("\n Type positive value");
    scanf("\n %f",&x);
    for(u=1;u<=x;u++) printf("\n %.1f",u/2);}
```

# while

```
main(){char c;puts("\nType character:");
    do{scanf("\n %c",&c);    printf("\nCode: %d\n('!' finish)\n\n",c);}
    while(c!='!');}
```