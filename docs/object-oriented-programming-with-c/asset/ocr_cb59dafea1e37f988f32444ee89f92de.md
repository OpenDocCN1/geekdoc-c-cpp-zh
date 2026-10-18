```
```cpp
void Add(int i, int j)
{
cout << i << " + " << j << " = " << i + j;
}
void Subtract(int i, int j)
{
cout << i << " - " << j << " = " << i - j;
}
void main()
{
FunPtr ptr;
ptr = &Add;
ptr(1,2);
cout << endl;
ptr = &Subtract;
ptr(3,2);
}
```
```

The output of Program 9.7 would be:

1 + 2 = 3
3 - 2 = 1

# 9.3  Pointers to Objects

We have already seen how to use pointers to access the class members. As stated earlier, a pointer can point to an object created by a class. Consider the following statement:

```
```cpp
item x;
```
```

where **item** is a class and x is an object defined to be of type item. Similarly we can define a pointer **it_ptr** of type **item** as follows:

```
```cpp
item *it_ptr;
```
```