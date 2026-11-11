# **Launching each promise in a separate thread**

```
~~~cpp
auto fut = std::async(std::launch::async, [&conStack]{ conStack.push(2011); });
auto fut1 = std::async(std::launch::async, [&conStack]{ conStack.push(2014); });
auto fut2 = std::async(std::launch::async, [&conStack]{ conStack.push(2017); });
~~~
```

Finally, the output of the program:

![](bbox=[0.25, 0.21, 0.75, 0.39])

A concurrent stack

# ## 13.1 Concurrent Queue

Accordingly to the chapter to the Concurrent Stack I want to answer the question: What is a queue?

# ### 13.1.1 A Queue

![](bbox=[0.3, 0.63, 0.7, 0.72])

A Queue

A `std::queue` follows the FIFO principle (First In First Out). A queue `que`, which needs the header `<queue>`, has four member functions.

With `que.push(e)` you can insert an element `e` at the end of the queue and remove the first element from the queue with `que.pop()`. `que.back()` enables you to refer to the last element in the `que`, `que.front()` to the first element in the `que`. `std::queue` has similar characteristics as `std::stack`. So you can compare `std::queue` instances and get their sizes. The operations of the queue have constant complexity.