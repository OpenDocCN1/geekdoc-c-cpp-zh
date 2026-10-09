![](bbox=[0.35, 0.08, 0.65, 0.28])

**FIGURE 18.2:** A doubly linked list storing the numbers 1 to 5.

However, if you want to find the *i*-th element of the list, you have no choice but to run through each element in sequence. This takes *O(i)*.

![](bbox=[0.35, 0.39, 0.65, 0.58])

**FIGURE 18.3:** The changes needed to insert the number 3.5 into the list.

Here is a code example showing how to insert some items at the beginning and end of a list using **push_front** and **push_back**. We then print out the list.

```
```python
// use a list to store items in priority order
list<string> list;
list.push_back("Drinking");
list.push_back("Dancing");
list.push_front("Exam");
list.push_front("Revision");

std::cout << "Todo list\n";
for (auto item : list) {
    std::cout << "Item " << item << "\n";
}
```
```