```
    if (myQueue.empty()) throw std::out_of_range("The queue is empty!");
    auto val = myQueue.front();
    myQueue.pop();
    return val;
    }
    ConcurrentQueue() = default;
    ConcurrentQueue(const ConcurrentQueue&) = delete;
    ConcurrentQueue& operator=(const ConcurrentQueue&) = delete;
      private:
    mutable std::mutex mutexFrontQueue;
    mutable std::mutex mutexBackQueue;
    std::queue<T, Cont<T, std::allocator<T>>> myQueue;
};
```

There is an obvious issue that makes the implementation incorrect. When the queue is empty, push and pop operate on the same element, which is a data race. Adding an element to separate the push from the pop operations solves this issue.

I could not achieve the fine-grained concurrent queue, based on the abstraction std::queue provides. Now, I have to do it by myself. First of all, how could a queue be implemented?

# ### 13.1.3.2 A Simple Queue

The straightforward way to implement a queue is it by using a singly-linked list. Singly-linked means that one node points to the next node but not the other way around. Additionally, a head pointer points to the head and a tail pointer to the tail of the data structure. Items can be removed (pop) from and added (push) to the queue. Elements are removed from the queue by putting the head pointer one position further. The remove operation will also return the old head node. Elements are added to the queue by pointing the previous tail node to the new node. The remove and the add operation adjust the head and the tail pointer.

![](bbox=[0.25, 0.7, 0.75, 0.835])

Here is the implementation of the simple queue.