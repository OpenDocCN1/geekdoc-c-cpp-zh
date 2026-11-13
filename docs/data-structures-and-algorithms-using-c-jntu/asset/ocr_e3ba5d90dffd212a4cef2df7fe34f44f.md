```
} z=c;
}
void show()
{
	cout<<x<<"i"<<y<<"j"<<z<<"k"<<""
}
vector operator++(int i)
{
	i=i;
	x+=i;
	y+=i;
	z+=i;
	return*this;
}
}
void main()
{
	vector a(10,20,30);
	clrscr();
	cout<<"\n Vector A:";
	a.show();
	a++;
	cout<<"\nAfter Increment A:";
	a.show();
}
```

# Output

```
Vector A:10i+20j+30k
After Increment A:11i+21j+31k
```

In Program 2.9, the operator ++ is overloaded to perform a post increment on the vector class objects. In the postfix form ++ operator, an integer argument is required, and the method is called when ++ operator follows the operand.

# 2.3.5 Prefix Form of Overloading the Unary Operator --

The general form of the prefix form of a unary -- operator is as follows:

```
return-type operator--();
```

In Program 2.10, operator -- is overloaded to perform a predecrement on the vector class object. The method operator--() is called when -- operator follows the operand.

# Program 2.10

```
/*Program to overload--operator as prefix form*/
#include<iostream.h>
#include<conio.h>
class vector
```