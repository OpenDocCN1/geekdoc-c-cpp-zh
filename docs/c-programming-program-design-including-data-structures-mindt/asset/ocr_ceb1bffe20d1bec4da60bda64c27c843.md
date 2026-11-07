```
```cpp
intQueue.push(50);                                      //Line 9
intQueue.push(33);                                      //Line 10

cout << "Line 11: The front element of intQueue: "
     << intQueue.front() << endl;                       //Line 11

cout << "Line 12: The last element of intQueue: "
     << intQueue.back() << endl;                        //Line 12

intQueue.pop();                                         //Line 13

cout << "Line 14: After the pop operation, "
     << "the front element of intQueue: "
     << intQueue.front() << endl;                       //Line 14

cout << "Line 15: intQueue elements: ";                 //Line 15

while (!intQueue.empty())                                //Line 16
{
    cout << intQueue.front() << " ";                    //Line 18
    intQueue.pop();                                     //Line 19
}                                                       //Line 20

cout << endl;                                           //Line 21

return 0;                                               //Line 22
}                                                       //Line 23
```
```

# Sample Run:

```
Line 11: The front element of intQueue: 26
Line 12: The last element of intQueue: 33
Line 14: After the pop operation, the front element of intQueue: 18
Line 15: intQueue elements: 18 50 33
```

The preceding output is self-explanatory. The details are left as an exercise for you.

# Containers, Associated Header Files, and Iterator Support

The previous sections discussed various types of containers. Recall that every container is a class. The definition of the class implementing a specific container is contained in the header file. Table 21-21 describes the container, its associated header file, and the type of iterator supported by the container.