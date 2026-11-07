+   19.  
+      a. 4  
+      b. 21  
+      c. `!queue.isEmptyQueue()`  
+      d. `queue.addQueue("programming")`

After the insertion operation the index of the last element is 5.

```
21.  cin >> num;
    while (cin)
    {
        switch (num % 2)
        {
            case 0:
                stack.push(num);
                break;
            case 1: case -1:
                if (num % 3 == 0)
                    queue.addQueue(num);
                else
                {
                    if (!stack.isEmptyStack())
                        stack.pop();
                    stack.push(num * num);
                }
        } //end switch

        cin >> num;
    } //end while
```

After processing these numbers, stack and queue are as follows:

```
stack: 14 289 10 121 28
queue: 15 -9 21 -3 33
```

+   23.  
+      a. 26  
+      b. `queueFront = 35; queueRear = 61.`  
+      c. `queueFront = 36; queueRear = 60.`

+   25.  
+      a. 31  
+      b. `queueFront = 25; queueRear = 56.`  
+      c. `queueFront = 26; queueRear = 55.`

+   27. 51

+   29. 5 -4 5 -7 1 2 1 4 1 -2 2 -7 7 -6

```
31.  template<class Type>
     void reverseStack(stackType<Type> &s)
     {
         linkedQueueType<Type> q;
         Type elem;
```