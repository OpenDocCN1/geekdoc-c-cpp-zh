In a circular queue, items are still inserted from the rear. Insertion operation remains continue till front is not encountered. In a circular queue, value of rear moves between '0' to the 'size - 1'. When rear attends the maximum value, its next value is reinitialized with zero. This is accomplished with the usage of mod operator. We are aware of that the mod is widely used in calculating the remainder and this remainder will not go beyond the value of its right side number. For instance, if the size of the queue is 4 then due to the usage of remainder method, the potential values will lie in the range of 0 to 3 only.

To insert the element in the queue, we have created the 'insert' function. This function accepts one argument as integer type and does not return a value. To insert the values, we have increment the rear. Once rear is incremented, it is always examined with the front; so that it should not overlap the front (does not insert the value more than the capacity of the queue). Complete function has been enumerated in the following example.

```
// Program to insert the item in a circular queue.
void insert (int &n)
{
    if ((rear+1) %size!=front)
    {
        rear= (rear+1) %size;
        queue [rear] =n;
        if (front<0)
            front=0;
    }
    else
    {
        cout<<"Queue overflow, element not inserted: \n";
    }
}
```

After the elements are inserted, then the other major task is to remove the items from the queue. Before removing the item from the queue, it is examined that queue is not empty. During removal of the item, it is removed from the front of the queue. Correspondingly, front moves towards the rear index. Here, we have considered the two significant cases of queue:

+   - Queue has only one element (front and rear at the same position).
+   - There is more than one element in the queue.

Both these cases have been considered in the remove () function discussed herein:

```
// Program to remove the items from the queue
int remove ()
{
```