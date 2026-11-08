```
```
        return
    endif

    queue[front] = item

else            [Insertion at Rear]
    if rear < maxsize
        then
            rear = rear + 1
        else
            return
    end if
    queue[rear] = item
end if
end
```
```

As shown in Listing 24.18, the parameters passed to the functionDequeInsert() function are a dequeue, the front and rear pointers, the item to be inserted, and a variable called pos. The pos variable identifies where the insertion will take place, that is, at the front or at the rear. If the insertion takes place at the front, then the front pointer is decremented by one. If the insertion takes place at the rear, then the rear pointer is incremented by one. The overflow condition in dequeue is same as that of a queue.

Listing 24.19 shows the algorithm for deletion operation in a deque:

# **Listing 24.19: Showing the Algorithm for Deletion in a Deque**

```
```
functionDequeDelete(queue[maxsize], front, rear, item,pos)
begin
    if front = 0 AND rear = 0
        then
            Output "Queue underflow"
            return
    end if
    if pos = 0 [Deletion at front end]
        then
            if front > 0
                then
                    item = queue[front]
            end if
            if front = rear
                then
                    front = rear = 0
            else
                    front = front + 1
            end if
    else
        if rear > 0
            then
                item = queue[rear]
        end if
        if front = rear
            then
                front = rear = 0
        else
                rear = rear -1
        end if
    end if
end
```
```