
Let us start with a simple priority queue of strings using the STL. Note that the STL contains also a class string for strings. To use the string class and the template class for priority queues, you have to write in your program

```
#include <queue>
#include <string>
```

The following simple part of a program shows how a priority queue of strings is defined and used:

```
priority_queue<string> q2;
q2.push("hello"); // fill priority queue
q2.push("you");
q2.push("are");
q2.push("welcome");

while(!q2.empty()) // get events from queue
{
string s;
s = q2.top(); // get "smallest" string
q2.pop(); // remove it
cout << s << endl;
}
```

| GET SOURCE CODE |
|---|
| DIR: libraries |
| FILE(S): pqueue0.cpp |

In line 1, the priority queue q2 is defined, and initialized automatically as empty queue. Behind the class name priority_queue, the template arguments are given in angular brackets < >, here the type string of the queue elements. In this way, for all templates the types and further arguments (see below) are specified. In line 2, an auxiliary string variable is declared. Some strings are put into the queue using the member function push(), which receives as argument the object to be put into the queue (technically it receives a reference to the object). In lines 8–13, the priority queue is read out. Here, the following three other member functions are used: empty() tests, whether the queue is empty. The function top() returns a reference to the currently first element in the queue. Using pop(), the currently first element is removed. For completeness, we note that the member function size() returns the number of elements being currently stored in the queue.

When running this program, the output will read:

```
you
welcome
hello
are
```

Hence, the strings are returned by the queue in decreasing lexicographic order. For simple predefined data types, one can specify other sorting criteria as template parameters for the queue. We only consider here the most general case: The sorting criterion is completely self-defined, which will usually be the case for priority queues of more complex objects.

Let us assume that you want to create a priority queue for events. Each event describes a collision of two atoms in a simulation of a gas. Within an event-driven simulation (see Sec. 6.7.1), one event will be treated after the other, in the order of increasing event times. Thus, each event can be described by the IDs of the two participating atoms and a time, where the collision takes place. The following data structure is used here:

| GET SOURCE CODE |
|---|
| DIR: libraries |
| FILE(S): pqueue.cpp |

```
struct event_t
{
    int part1, part2;    // IDs of particles colliding
    double time;         // time of collision
};
```

A structure is used, which is a class where by default all members are public. Everything shown in the following would work also if we defined a class for events with data encapsulation, member functions for access etc.

For the priority queue, we have to provide a function to compare two events. For this purpose, no standard comparison operator can be used; therefore, we have to provide one. To achieve maximum flexibility, this comparison function must be a function object (also called functor). This is an object obj of a class which provides the operator () as member function. Consequently, applying this operator to the object, i.e. writing obj(), implements exactly a call to the function. The advantage over defining an ordinary function is that object functions are C++ objects as well. Thus, they can have all class properties like member data etc. In this way, one can have different function objects of the same class, which behave in a different way, because their internal data looks different. The following example, which provides a comparison for events, should make it clear how classes providing function objects are defined:

```
class EventSortCriterion
{
public:
    bool operator() (const event_t &e1, const event_t &e2)
    {
        return(e1.time > e2.time);
    }
};
```

This looks like a standard class definition, without member data here, and one member function is the () operator. The operator receives two arguments and returns a variable of type bool, which is a special C++ type. The type bool has the possible values true and false, being equivalent to 0 and non-zero, compatible with standard C. In front of the arguments const is written, which prohibits that the values are modified by the operator.

Next, it is shown how a priority queue of events is defined and used:

```
priority_queue<event_t, vector<event_t>, EventSortCriterion> q;
event_t e; // one event
int i; // loop counter
int num_events = 20;

srand48(1000);
for(i=0; i<num_events; i++) // put events into queue
{
    e.part1 = i;
    e.part2 = i+10;
    e.time = 1000*srand48();
    q.push(e);
}

while(!q.empty()) // get events from queue
{
    e = q.top(); // get smallest event
    q.pop(); // remove it
    cout << "(" << e.part1 << "," << e.part2 << ") at t="
         << e.time << endl;
}
```

The most important line is the first line. Here, the priority queue is defined. In comparison to the queue of strings example above, here two additional template arguments are given. The second is the data type, which is used to implement the queue. Here, a vector is used, which stores elements of type event_t. Note that this is also a template, as visible from the

Here, a basic example is considered. The simulation consists of some "agents" which are distributed in the x-y plane. Each agent has a position, serving as key. Furthermore, the data associated with each agent consists of some "capacity" and of some "interaction range", the exact meaning is not important here. This is implemented via the following two type definitions for agent_t and agentkey_t:

| GET SOURCE CODE |
|---|
| DIR: libraries |
| FILE(S): maps.cpp |

```
struct agent_t
{
    int capacity;    // how much an agent can process
    int range;       // interaction range
};
```

```
struct agentkey_t
{
    int x,y;         // position of agent
};
```

Since the implementation is based on search trees, one has to supply a comparison criterion. Here, we assume that the x coordinates determine the order at first. If the x coordinates of two agents are the same, the y coordinates are compared next. The comparison is implemented as corresponding function object class, similar to the priority queue shown above:

```
class AgentkeySortCriterion
{
public:
    bool operator() (const agentkey_t &k1, const agentkey_t &k2) const
    {
        return( (k1.x < k2.x) || ( (k1.x == k2.x) &&(k1.y < k2.y) ) );
    }
};
```

In the main() function, a map m1 is defined via

```
typedef map<agentkey_t, agent_t, AgentkeySortCriterion> agentmap_t;
agentmap_t m1;                                           // stores all agents
```

The first template argument signifies the type of the keys, the second refers to the type of the value objects to be stored, while the third is the sorting criterion. The third argument is optional, if the operator < is defined for the keys, as for example for integer keys.

For inserting and removing elements, you can use the member functions insert() and erase(). The insertion is a bit inconvenient. It is more convenient to use an array notation, as in the following example:

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

Two variables k1 and a1 are used (lines 5-6) to store the keys and agents, respectively. The agent positions and range values are initialized randomly (lines 10-11). Note that a static cast is used. This is a C++ operator, which performs some checks to be performed by the compiler and prevents meaningless type conversions. The agents are actually stored in line 14, using the array notation. You can access the map elements in the same way for reading, but, unlike for an array, if you ask for an element with a key value, which does not exist, the element will be created with default values.

For this reason, we use the find() member function in the following example to test whether an element with a specific key exists. The code loops over all elements in the map. For this purpose, one needs a special object, an iterator, which is something like an internal pointer in the map. There are some predefined iterators accessible via public member functions: begin() and end(). The first one returns always an iterator to the currently first element of the map. The second one returns an iterator which points behind the last element.
