```
```cpp
priority_queue<
    int,
    vector<int>,
    decltype( [](int a, int b)->bool{return a>b;})> PQ;

PQ.push(10);
PQ.push(5);
PQ.push(8);
PQ.push(1);
PQ.push(11);

while (!PQ.empty()) {
    cout << PQ.top() << endl;
    PQ.pop();
}
}
```
```

A priority_queue is a container adapter (something that modified the behavior of a standard container, such as a vector) that makes performing lookups in a consistent manner possible. It does so at the expense of insertion and extraction times. However, if you perform mostly lookups, using a priority_queue can substantially improve application execution times.

This example creates a priority_queue that accepts int values as input, modifies the behavior of a vector, and uses a lambda expression within a decltype() as a comparator. The lambda expression is simple in this case — it just compares two values and returns true when the first value is greater than the second. The purpose of this priority_queue is to create a vector where the entries remain in sorted order at all times, making lookups faster.

After creating the priority_queue, the example pushes values in a random order. However, the priority_queue automatically sorts them for you. The code then uses a while loop to show the order in which the values are stored, as shown here:

```
```text
1
5
8
10
11
```
```