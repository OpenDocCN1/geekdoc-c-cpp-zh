```
```cpp
{
        // Interchange both the elements
        int t = child->num;
        child->num =parent->num;
        parent->num = t;
        r=c;
        // Assign c to r this make child now parent
        c= 2*r;
        // and c = 2 * r this calculate child of new parent
}
else
// If the child element is less then parent then make done =1
done =1 ;
}
}
void dllist :: heapify()   // To create heap of the elements of the node
{
        for(int i = n/2; i>=1;i--)
                swapdown(i,n);          // Call swapdown function
}
void dllist :: hsort()  // For sorting the elements
{
        heapify();          // First create a heap of the elements
        for(int i = n;i>=2;)  // From last node to the second last node
        {
                dnode * ptr = head1;  // Assign ptr to head1
                int q = 1;
                while((q<i) && (ptr->link != NULL) )
                // For taking ptr to the ith node
                {
                        ++q;
                        ptr=ptr->link;
                }

                int t = ptr->num;
                // Change the first and the last element in the heap
                ptr->num= head1->num;
                head1->num=t;

                swapdown(1,--i);
                //Call swapdown without the last element in the heap
        }
}
```
```