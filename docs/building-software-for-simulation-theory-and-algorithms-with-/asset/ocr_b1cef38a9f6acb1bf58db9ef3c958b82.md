```
```cpp
26        void removeMinimum();
27        // Remove the imminent models from the queue.
28        void removeImminent();
29        // Add, remove, or move a model as required by its priority.
30        void schedule(Atomic<X>* model, double priority);
31        // Returns true if the queue is empty, and false otherwise.
32        bool empty() const { return size == 0; }
33        // Get the number of elements in the heap.
34        unsigned int getSize() const { return size; }
35        // Destructor.
36        ~Schedule() { delete [] heap; }
37    private:
38        // Definition of an element in the heap.
39        struct heap_element
40        {
41            Atomic<X>* item;
42            double priority;
43            // Constructor initializes the item and priority
44            heap_element():item(NULL),priority(DBL_MAX){}
45        };
46        unsigned int capacity, size;
47        heap_element* heap;
48        // Double the schedule capacity
49        void enlarge();
50        // Move the item at index down and return its new position
51        unsigned int percolate_down(unsigned int index, double priority);
52        // Move the item at index up and return its new position
53        unsigned int percolate_up(unsigned int index, double priority);
54        // Construct the imminent set recursively
55        void getImminent(Bag<Atomic<X>*>& imm, unsigned int root) const;
56    };
58    template <class X>
59    void Schedule<X>::getImminent(Bag<Atomic<X>*>& imm, unsigned int root) const
60    {
61        // Stop at the bottom or where the next priority is not the minimum
62        if (root > size || heap[1].priority < heap[root].priority) return;
63        heap[root].item->active = true; // Put the model into the imminent set
64        imm.insert(heap[root].item);
65        getImminent(imm,root*2); // Look for immients in the left subtree
66        getImminent(imm,root*2+1); // Look in the right subtree
67    }
69    template <class X>
70    void Schedule<X>::removeMinimum()
71    {
72        if (size == 0) return; // Don't do anything if the heap is empty
73        size--; // Otherwise reduce the size of the schedule
74        // Set index to 0 to show that this model is not in the schedule
```
```