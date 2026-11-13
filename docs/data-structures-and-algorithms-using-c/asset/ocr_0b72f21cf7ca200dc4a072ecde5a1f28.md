# Dequeue Operation

Accessing data from the queue is a process of two tasks – access the data where front is pointing and remove the data after access. The following steps are taken to perform dequeue operation –

+   Step 1 – Check if the queue is empty.
+   Step 2 – If the queue is empty, produce underflow error and exit.
+   Step 3 – If the queue is not empty, access the data where front is pointing.
+   Step 4 – Increment front pointer to point to the next available data element. Step 5 –

![](bbox=[0.21, 0.245, 0.88, 0.505])

Return success.

# Algorithm for dequeue Operation

```
procedure dequeue
if queue is empty
return underflow
end if
data = queue[front]
front <- front + 1
return true
end procedure
```

Implementation of dequeue() in C programming language –

```
int dequeue() {
if(isempty())
return 0;
int data = queue[front];
front = front + 1;
return data;
}
```

For a complete Queue program in C programming language, please click here.