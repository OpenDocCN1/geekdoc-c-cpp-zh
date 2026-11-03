# Operators and Expressions

```
(11)main()
{
	int a;
	float b;
	b=15/2;
	printf("%f\t%c\n",b);
	b=(float)15/2+(15/2);
	printf("%f\n",b);
}
```

```
(12)main()
{
	int a=9;
	char ch='A';
	a=a+ch+24;
	printf("%d\t%c\t%d\t%c\n",ch,ch,a,a);
}
```

```
(13)main()
{
	int a,b,c,d;
	a=b=c=d=4;
	a*=b+1;
	c+=d*3;
	printf("a = %d,c = %d\n",a, c);
}
```

```
(14)main()
{
	int a=5,b=10,temp;
	temp=a,b=a,b=temp;
	printf("a = %d,b = %d\n",a,b);
}
```

```
(15)main()
{
	int a=10,b=3,max;
	a?b:max=a=b;
	printf("%d",max);
}
```

```
(16)#include<stdio.h>
main()
{
	int a=5,b=6;
	printf("%d\t",a=b);
	printf("%d\t",a==b);
	printf("%d",a,b);
}
```

```
(17)main()
```