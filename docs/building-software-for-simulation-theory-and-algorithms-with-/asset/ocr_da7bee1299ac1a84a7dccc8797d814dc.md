```
```cpp
65     return *this;
66 }
67 // Count the instances of a stored in the bag
68 unsigned count(const T& a) const
69 {
70     unsigned result = 0;
71     for (unsigned i = 0; i < size_; i++)
72         if (b[i] == a) result++;
73     return result;
74 }
75 // Get the number of elements in the bag
76 unsigned size() const { return size_; }
77 // Same as size()==0
78 bool empty() const { return size_ == 0; }
79 // Get an iterator pointing to the first element in the bag
80 iterator begin() const { return iterator(0,b); }
81 // Get an iterator starting just after the last element
82 iterator end() const { return iterator(size_,b); }
83 // Erase the first instance of k
84 void erase(const T& k)
85 {
86     iterator p = find(k);
87     if (p != end()) erase(p);
88 }
89 // Erase the element pointed to by p
90 void erase(iterator p)
91 {
92     size_--;
93     b[p.i] = b[size_];
94 }
95 // Remove all of the elements from the bag
96 void clear() { size_ = 0; }
97 // Find the first instance of k, or end() if no instance is found.
98 // Uses == for comparing T.
99 iterator find(const T& k) const
100 {
101     for (unsigned i = 0; i < size_; i++)
102         if (b[i] == k) return iterator(i,b);
103     return end();
104 }
105 // Put t into the bag
106 void insert(const T& t)
107 {
108     if (cap_ == size_) enlarge(2*cap_);
109     b[size_] = t;
110     size_++;
111 }
112 ~Bag() { delete [] b; }
113 private:
```
```