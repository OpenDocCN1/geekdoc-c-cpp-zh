```
```cpp
q->print();                         //Line 5
cout << endl;                       //Line 6
r->print();                         //Line 7

cout << "*** Calling the function callPrint ***"  //Line 8
cout << endl;                       //Line 9
callPrint(q);                       //Line 10
cout << endl;                       //Line 11
callPrint(r);

return 0;
}
```
```

```
```cpp
void callPrint(petType *p)
{
    p->print();
}
```
```

# Sample Run:

```
```text
Name: Lucky
Name: Tommy, Breed: German Shepherd
*** Calling the function callPrint ***
Name: Lucky
Name: Tommy, Breed: German Shepherd
```
```

The preceding examples show that if a formal parameter, say p of a class type, is either a reference parameter or a pointer and p uses a virtual function of the base class, we can effectively pass a derived class object as an actual parameter to p.

However, if p is a value parameter, then this mechanism of passing a derived class object as an actual parameter to p does not work, even if p uses a virtual function. Recall that, if a formal parameter is a value parameter, the value of the actual parameter is copied into the formal parameter. Therefore, if a formal parameter is of a class type, the member variables of the actual object are copied into the corresponding member variables of the formal parameter.

Suppose that we have the above classes—that is, petType and dogType. Consider the following function definition:

```
```cpp
void callPrint(petType p)   //p is a value parameter
{
    p.print();
}
```
```

Further suppose that we have the following declaration:

```
```cpp
dogType dog;
```
```

The object dog has two member variables, name and breed. The member variable name is inherited from the base class. Consider the following function call:

```
```cpp
callPrint(dog);
```
```

![](bbox=[0.944, 0.705, 1.0, 0.823])