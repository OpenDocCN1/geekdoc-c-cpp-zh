For inserting and removing elements, you can use the member functions insert() and erase(). The insertion is a bit inconvenient. It is more convenient to use an array notation, as in the following example:

```
```cpp
int num_agents = 20; // number of agents
int sizex=10, sizey=10; // size of system
agentkey_t k1; // one key
agent_t a1; // one agent

for(int i=0; i<num_agents; i++) // distrib. agents
{ // random positions
k1.x = static_cast<int>(floor(sizex*drand48()));
k1.y = static_cast<int>(floor(sizey*drand48()));
a1.capacity = 100;
a1.range = 1 + static_cast<int>(floor(3*drand48()));
m1[k1] = a1;
}
```
```

Two variables k1 and a1 are used (lines 5-6) to store the keys and agents, respectively. The agent positions and range values are initialized randomly (lines 10-11). Note that a static cast is used. This is a C++ operator, which performs some checks to be performed by the compiler and prevents meaningless type conversions. The agents are actually stored in line 14, using the array notation. You can access the map elements in the same way for reading, but, unlike for an array, if you ask for an element with a key value, which does not exist, the element will be created with default values.

For this reason, we use the find() member function in the following example to test whether an element with a specific key exists. The code loops over all elements in the map. For this purpose, one needs a special object, an iterator, which is something like an internal pointer in the map. There are some predefined iterators accessible via public member functions: begin() and end(). The first one returns always an iterator to the currently first element of the map. The second one returns an iterator which points behind the last element.