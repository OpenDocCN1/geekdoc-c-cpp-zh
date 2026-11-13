```
Template<class T>
class MinHeap
{
    public:
    explicit MinHeap(int capacity=150);
    explicit MinHeap(const vector<T>&items);
    bool empty() const;
    bool full() const;
    void insertEle(const T&x);
    void deleteMinEle(T&minEle);
    private:
    int cSize; //Number of elements in heap
    vector<T>array; //The heap array
    void buildMinHeap();
    void moveDownHeap(int newnode);
};
```

(a) Class interface for min priority queue

```
Template<class T>
class MaxHeap
{
    public:
    explicit MaxHeap(int capacity=150);
    explicit MaxHeap(const vector<T>&items);
    bool empty() const;
    bool full() const;
    void insertEle(const T&x);
    void deleteMaxEle(T&maxEle);
    private:
    int cSize; //Number of elements in heap
    vector<T>array; //The heap array
    void buildMaxHeap();
    void moveDownHeap(int newnode);
};
```

(b) Class interface for max priority queue

Figure 11.10 Class interface

# 11.3.2 Min Heap-Insertion

To insert an element x into the min heap, a new node is created in the next available location to keep the tree complete (preserving the property of the complete binary tree). Bubble up the new node to maintain the min heap property. To insert the element 16, a new node is created in the next available heap location