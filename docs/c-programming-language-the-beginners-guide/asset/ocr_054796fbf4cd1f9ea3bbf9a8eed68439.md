question in a moment. But for now, remember that a pointer is a variable that holds a memory location. Here, that memory location is of the variable.

Now, duplicate the *printf* statement. This time, replace *&pokey* with pointer variable

```
```c
1  #include 2
3  int main()
4  {

•  int pokey;
•  int *p;

7

•  p = &pokey;
•  printf("The address of ‘pokey’ is %p\\n",&pokey);

   •  printf("The address of ‘pokey’ is %p\\n",p);
12 return(0);
13 }
14
15
```
```

Save these changes and then build and run the code. As you can see, both lines output the same address. One is the address of variable *pokey* obtained with the ampersand. The other is the value saved in pointer variable *p*, which is that