references or constants in the class (see Chapter 16). You need to define the default constructor yourself as you have Number(int) as a custom constructor; the compiler would not generate Number() automatically.

A small note: if you are clever and restrict yourself regarding the operations you perform on the containers, you can even forgo some requirements for the element type. For example, you can forgo the default constructor if you do not use numbers.resize() or the like. Normally, however, it is a good idea to equip types in containers with a default constructor, copy constructor, assignment operator, and move operations.

Under these conditions, you can create the vector<Number>. The same applies to array, deque, list, and forward_list.

Collectively, these are called sequence containers. You determine the order of the elements by the explicit insertion position (see Chapter 20).

In contrast, the ordered associative containers are always in an order defined by the elements themselves. For map and set as well as their relatives multi_map and multi_set, the order depends on the order in which you inserted the elements. When you check, the elements are in a consistent position.

map and set achieve this by keeping the elements in the container in a sorted order at all times. The sorting is determined by the operator< free function. For example, because operator< is already defined for int and string, set<int> and set<string> work directly.