```
String::String(){
    ptr = NULL;
}
```

# 19.2.3 The print member function

We next discuss the member function print. This is very simple.

```
void String::print(){
    if(ptr != NULL) cout << ptr << endl;
    else cout << "NULL" << endl;
}
```

Since ptr gives the address from where the string is stored, it suffices to write cout << ptr << endl;. However, if ptr is NULL, then we cannot print it, instead we must explicitly print out "NULL".

# 19.2.4 Assignments

We discussed in Chapter 15 that assignment is already defined for structure types, provided the right hand side of the assignment is also a structure of the same type as the left hand side. Such a statement executes by copying each data member of the right hand side to the corresponding member of the left hand side. We will see that this is not adequate for our purpose. In addition, our String data type allows the right hand side to be of type char*. This we will have to define afresh. This is what we consider first.

As discussed in Section 16.6, we can define a member function operator= to specify how assignment should work. Since the right hand side is to be of type char*, this member function must have a char* parameter. In the body of the function we describe what we want to happen to execute the assignment. We can define this as follows.

```
void String::operator=(char *rhs){
    delete [] ptr;
    ptr = new char[length(rhs) + 1];
    strcpy(ptr,rhs);
}
```

We give an example to see how this will work. Suppose z is of type String and say we have a statement

```
z = "mno";
```

This statement will cause the member function operator= to execute, with the variable z being the receiver, and the parameter rhs being the address of the text string "mno".

Note that the variable z may already contain some value before control arrives at the assignment statement, say the variable z contains the text "pqr". In this case, before our assignment statement, z.ptr will already be pointing to a heap region storing "pqr". When we set z.ptr to point to the area storing "mno", the area containing "pqr" will no longer be