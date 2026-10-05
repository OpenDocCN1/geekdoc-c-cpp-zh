# Object-Oriented Programming with C++

# 11.4 Limitation of Exception Handling

The limitation of exception handling is that if a resource has acquired (file has been opened, memory has been allocated dynamically in the heap area, etc.) and the statements to release the resource are after the throw statements, then the acquired resource may remain locked up. Listing 11.15 illustrates this.

Listing 11.15 Dynamically resources remain locked after the throw statement

```
#include<iostream>
class A {
    public:
    A()
    {
        cout<<"Constructor\n";
    }
    ~A()
    {
        cout<<"Destructor\n";
    }
};
void abc(int);
void main() {
    try {
        abc(-1);
    }
    catch(char * s)
    {
        cout<<s<<endl;
    }
    return 0;
}

void abc(int p) {
    A * Aptr = new A[2];
    if(p<0)
        throw "Invalid argument to abc(");
}
```

Output
Constructor
Constructor
Invalid argument to abc()

In Listing 11.15, the stack is unwound, memory occupied by the pointer Aptr in abc() function gets destroyed. However, the memory block at which the pointer points remains locked up. (This is evident from the fact that the destructor was not called for the objects created in the heap.)