Most C language programmers will combine the statements at line 10 and 11 into a single line. It looks like this:

```
~~~c
1 #include 2
3 int main()
4 {
5 int array[] = { 11, 13, 17, 19 };
~~~
```

+   - int x;
+   - int *aptr;

```
~~~c
8
9 apr = array;
10 *(aptr+2) = 0;
11
12 for(x=0;x<4;x++)
13 {
14 printf("Element %d: %d\n",x+1,array[x]);
%d\n",x+1,array[x]);
%d\n",x+1,array[x]);
~~~
```

You need to use parenthesis because the pointer location must happen before the asterisk references the value. Save the changes, and then build and run the code. As you can see, the output is the same. You’ll see this type of shorthand notation is used a lot. The main reason is that it doesn’t affect the value of the *aptr* pointer variable, which still references the base address of the array.

Perhaps the best way to demonstrate pointer and array manipulation is to use strings, instead of numeric arrays. Take a look at the code below: