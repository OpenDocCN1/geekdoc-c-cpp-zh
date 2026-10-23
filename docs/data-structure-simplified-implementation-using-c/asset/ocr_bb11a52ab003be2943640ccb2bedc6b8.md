# Data Structure simplified

```
else
{
    l3.first=current=two;  // initialize with the first node of second list
    two=two->next;
}
while((one!=NULL) && (two!=NULL))
{
    if(one->data < two->data)
    {
        current->next=one;  // connect current to the one
        current=one;        // move one to the current
        one=one->next;      // move to the next node
    }
    else
    {
        current->next=two;  // connect current to the two
        current=two;         // move two to the current
        two=two->next;      // move to the next node
    }
}// end of while
if(one)           // if list one is not exhausted
{
    current->next=one;
}
else if(two)      // if list two is not exhausted
{
    current->next=two;
}
return l3;
}
```

# 3.8  USE OF OPERATOR OVERLOADING IN A LINK LIST

Operator overloading allows the programmer to define the operators to function as per programmer’s way, instead of the way defined for the primitive data type. However, use of the overloading is restricted at the place and scope of definition, beyond which it can be used