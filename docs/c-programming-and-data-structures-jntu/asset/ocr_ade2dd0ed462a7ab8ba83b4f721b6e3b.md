```
```c
void main()
{
	int x,i,n;
	float s=0,c;
	clrscr();
	printf("\n enter the value of x");
	scanf("%d",&x);
	/*perform the looping operation*/
	for(i=0,n=0;i<n;i=i+2,n++)
	s=s+(pow(-1,n)*pow(x,i)/fact(i));
	printf("\n the result is %f",s);
	getch();
}
/* calling sub program*/
long fact(int x)
{
	long int y=1;
	while(x!=0)
	{
		y=y*x;
		x--;
	}
	return y;
}
```
```

# 3. Write a program and explain the working of malloc() and calloc() functions.

Ans. Memory space is required by the variable in a program to calculate, and assign during execution. The process of allocating memory out runtime is known as dynamic memory allocation. There are some memory management functions in C that can be used for allocating and freeing memory during program execution.

+   Some memory allocation functions are
+   
+   - Malloc() Allocates required size of bytes and returns a pointer to the first byte of allocated space.
+   
+   - Calloc() Allocates space for an array of elements, initializes them to zero and then returns a pointer to the memory.
+   
+   - Free() Free previously allocated space.
+   
+   - Realloc() Modifies the size of previously allocated space.

Memory allocation using malloc() function:

Block of memory may be allocated using malloc() function. Malloc() function reserves a block of memory of specified size and returns a pointer of typed void.