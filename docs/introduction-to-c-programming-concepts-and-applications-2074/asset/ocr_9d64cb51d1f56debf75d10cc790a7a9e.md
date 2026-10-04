Suppose you're running a business where you're letting people buy on credit and want to keep track of their name, how many purchases they make, and how much they owe.

In this case, you'd want to create a tuple storing 3 types: string for the name, integer for the number of purchases, and a double that can hold decimal values for the amount owed.

The tuple can be named customer to make it more descriptive (8). Then, you can use this type, customer, to declare a variable, c.

You'll have a make_tuple command that you can use to make an instance of that tuple type. Here, the tuple says John made 3 purchases and owes you $100 (12).

You can then use a count to access the elements. For the first element, you get<0>(c) outputs John. Then, get<1>(c) gives you 3 purchases, and get<2>(c) gives you 100.0 (a).

The function can also assign values to the elements or manipulate them. Because it returns a value, you can do anything to the result of get that you would have done to the element. In this code, you are incrementing the second element, indicating one more purchase, and increasing the third element $50 (b).

```
// Program 21_4
// Tuple example - extended
#include <iostream>
#include <string>
#include <tuple>
using namespace std;
typef<string, int, double> customer;
int main() {
    customer c;
    c = make_tuple("John", 3, 100);
    cout << get<0>(c) << " "\nhas made " << get<1>(c) << " "\npurchases and owes $" << get<2>(c) << " "\n endl;
    cout << get<0>(c) << " "\nhas made " << get<1>(c) << " "\n endl;
}
```

# /* PRIORITY QUEUE */

The priority queue only takes one type in, so it's not associative, but it's often used with associative containers like pairs or tuples.

The idea of a priority queue is that you want to insert items into the container and then pull them out in order from greatest to smallest. The values of a priority queue are the priority, or how important that element is. So, each element at the front of the queue should be the one with the greatest

priority. Each time you pull an element out of the queue, it will be the highest-priority element in the container.

To create an instance of a priority queue, you give a single data type. For a priority queue to work, this data type must have a less-than comparator defined; and how elements are compared to find which is largest. If you want to have a priority queue of your own type, make sure it has defined.

When using priority_queue with a pair or a tuple, the comparison is based on comparing the first element, and if they are equal, the second. For a tuple, this continues with the remaining elements. Either way, the comparison is already defined so that you don't have to explain a less-than comparator.

23 | C++ Associative Containers and Algorithms