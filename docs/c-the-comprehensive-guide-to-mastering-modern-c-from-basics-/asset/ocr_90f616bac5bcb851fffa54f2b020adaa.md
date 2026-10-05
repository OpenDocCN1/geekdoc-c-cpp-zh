+   - An undo history of limited length, where executed actions are inserted at the front, removed from when they need to be undone, and elements are dropped at the back to limit the depth of the history.

+   - Search with pattern matching using regular expressions or their implementation through the simulation of a nondeterministic finite automaton. The nondeterministic transitions are placed in the double-ended queue for processing.

I will cover all methods of deque as well as the most useful free functions and other tools. Much similar to vector, and I will be briefed in those cases. You will find a directly transferable detailed discussion of the corresponding feature of vector in Section 24.6.3.

deque does not provide an interface for its capacity like vector does. Therefore, the reserve and capacity methods are not available as they are in vector.

Because deque is very similar to vector, refer to the examples. To save you from flipping pages, I have included crucial operations of deque in Listing 24.40.

```
#include <iostream>
#include <iterator>
#include <algorithm> // copy
using namespace std;
stream& operator<<=(ostream& os, int val) { return os<<val<<\n'; }
int main() {
	deque d(4, 6); // Create deque with elements
	// Insertion
	d.push_front(); // at the front: efficient
	d.insert(d.begin()+2, 5); // in the middle: slow
	d.push_back(); // at the end: efficient
	// Access
	cout << d.front(); // from the front: efficient
	cout << d[2]; // in the middle: efficient
	cout << d.back(); // from the end: efficient
	// Size
	d.resize(4); // read size
	// resize (or extend)
	// Iterators
	copy(d.begin(), d.end(), iterator<int>(cout, ""));
	cout << '\n'; // Output: 3 4 5 6
	// Remove
	d.pop_front(); // at the front: efficient
	d.erase(d.begin()+1); // in the middle: slow
	d.pop_back(); // at the end: efficient
	d.clear(); // clear
}
```

**Listing 24.40** What the "deque" can do!

Note my comment on << in the box followed Listing 24.12.