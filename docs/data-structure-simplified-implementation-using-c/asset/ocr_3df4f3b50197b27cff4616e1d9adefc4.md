```
int a=0;
if (! empty ())
{
    if (front==rear)            //only one element in the queue
    {
        a=queue [front];
        front=rear=-1;
    }
    else
    {            // More than one element in the queue
        a=queue [front];
        front= (front+1) %size;
    }
}
else
{
    cout<<"Queue underflow: \n";
}
return a;
}
```

The other significant function is empty function. This function ascertains whether the queue is empty or not. If the queue is empty it returns ‘1’ otherwise it returns ‘0’.

```
// function to check if any item in the list or empty
int empty ()
    {
        if (front==-1)
        return 1;
        else
        return 0;
    }
```

Finally, it is worth discussing the display function. Although, it appears to be simple function similar to the one we have learned other display function. However, it is significantly different since value need to hover between ‘0’ and the ‘size-1’. Upon attending the maximum value, it further gets initialized with zero. In the discussed function, we have started from the front position and continued till we have not reached to the tail (last element). Once last element is reached, loop is terminated and the remaining items are displayed. Before, displaying the