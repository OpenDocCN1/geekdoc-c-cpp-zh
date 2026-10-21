```
void main( )
{
	demo d[] ={
	demo("Prof.RR Sedamkar"),
	demo("Mr.Hari Mohan"),
	demo("Mr.Deshmukh"),
	demo("Mr.Bharat"),
	demo("Mr.Joshi"),
	};
	clscr( );
	const int x = sizeof(d)/sizeof(demo);
	for(int i=0;i<x;i++)
	d[i].show( );
	getch( );
}
```

EXPLANATION : The program is similar to previous one with the difference that we have used string instead of integer data.

# 7.4 COPY CONSTRUCTOR

A copy constructor is used to declare and initialized an object from another object when ever we have statement like demo d2 = d1 (assume demo is class name and d1 is an already declared object of demo class), they make call to copy constructor defined in the class. When we have two objects say d1 and d2 and if we write d2=d1 then this results in copying all members of d1 to d2 but does not call copy constructor. This is simply assignment of one object to another of same type, but when you want to do something more than merely copying one object to another you may use copy constructor. For a class demo, copy constructor is written as :

```
demo (demo &d)
{
	// copy constructor
}
```

For better understanding point of view we present few programs here.