Now data members or functions can be accessed as ptr -> num or (*ptr).Num

```
ptr -> input (x), ptr->show() etc.
```

The -> operator is known as pointer to member operator. On the left of this there will always be a pointer.

Just like we create pointer to data member we can also create pointer to member functions of the class. But before telling you how to do it. We see how to create pointer to normal functions which are not member functions of the class. We take two examples:

```
void show ();
int disp(int, float);
```

For creating a pointer to a function we have to note the prototype of the function. In the program the return type of the function is void and function takes no argument. To create the pointer to this type of function we write in this manner.

```
void (*pf) ();
```

Here pf is pointer to function takes no argument. Parenthesis around *pf is must otherwise it will become void *pf(void); which means pf is function which takes no argument and which return an address of type void.

For second function return type is int and function takes two arguments of type int and float. To create a pointer to function of this type we write.

```
int (*pdisp)(int, float);
```

The above declaration tells the compiler that pointer pdisp is a pointer to function which can store address of a function whose return type is int and takes two arguments of type int and float.

Both the pointer to function pointers can be used as :

```
pf = &show (); // assigning address of function show
(*pf) (); // calls function show using pointer
pdisp =&disp; // assigning address of function disp
int ans=(*pdisp)(20,34.5f);//callfunction disp using pointer.
```

The ampersand (&) is not necessary as name of the function alone represent its address.

Now, assume both the above mentioned functions show and disp are public members of class demo. We now see how to create pointer to these functions of demo class.

We first write for function show. The return type is void and function does not take any argument. Follow the same ways as we did earlier but simply insert the demo :: as.

```
void (demo :: *pf) ( ) = &demo :: show;
```

Similarly for the disp function we write as :

```
int (demo :: &pdisp)(int, float) = &demo :: disp;
```

Now, for an object d of demo class, function can be called as :

```
(d.*pf) (); and int ans = (d.*pdisp)(20, 34.56f);
```