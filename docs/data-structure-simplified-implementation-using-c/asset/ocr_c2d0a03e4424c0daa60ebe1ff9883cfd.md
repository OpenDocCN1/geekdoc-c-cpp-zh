```
{
for (int i=0; i<second; i++)
cout<<first<<"\t";
}
int main ()
{
clrscr ();
one<char*, int> o1 ("jitendra", 2);
one<int, int> o2 (30, 4);
o1.display ();
cout<<endl;
o2.display ();
getch ();
return 0;
}
Output
Jitendra          jitendra
30    30    30    30
}
```

In the above example, we have used the class template that has accepted the two arguments. In first object i.e. o1, we have passed two arguments of different type, the first argument was string and the second was integer type. Argument passed first i.e. string is repeated number of times the value of second argument.

In the second object, again we have passed two arguments, however, this time types are same. It means that the argument of same types can also we passed even though we have defined two arguments. Precisely, speaking, number of template arguments governs the number of arguments that can be passed instead of number of data types. In our case, the first argument is the number to be printed and the second argument is the number of times the first argument is to be printed.

# Function template

Function template is used to create the generic function. Consequently, same function can be used for wide variety of data types. To declare that the function is template type, we define the function with the keyword template similar to that of class type. Syntax for declaring the generic function can be written as follows:

```
template<class t>
return-type function_name (class t);
```