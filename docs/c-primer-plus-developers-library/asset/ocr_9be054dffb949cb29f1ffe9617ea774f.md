```
class bad_1 {...};
class bad_2 : public bad_1 {...};
class bad_3 : public bad_2 {...};
...
void duper()
{
    ...
    if (oh_no)
        throw bad_1();
    if (rats)
        throw bad_2();
    if (drat)
        throw bad_3();
}
...
try {
    duper();
}
catch(bad_3 &be)
{ // statements }
catch(bad_2 &be)
{ // statements }
catch(bad_1 &be)
{ // statements }
```

If the bad_1 & handler were first, it would catch the bad_1, bad_2, and bad_3 exceptions. With the inverse order, a bad_3 exception would be caught by the bad_3 & handler.

> **Tip**
> 
> If you have an inheritance hierarchy of exception classes, you should arrange the order of the catch blocks so that the exception of the most-derived class (that is, the class furthest down the class hierarchy sequence) is caught first and the base-class exception is caught last.

Arranging catch blocks in the proper sequence allows you to be selective about how each type of exception is handled. But sometimes you might not know what type of exception to expect. For instance, say you write a function that calls another function, and you don’t know whether that other function throws exceptions. You can still catch the exception even if you don’t know the type. The trick to catching any exception is to use an ellipsis for the exception type:

```
catch (...) { // statements }  // catches any type exception
```