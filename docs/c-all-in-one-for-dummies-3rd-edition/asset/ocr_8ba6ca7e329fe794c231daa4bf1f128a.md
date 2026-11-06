# **Listing 6-10 (continued)**

```
    MyQueue.pop();
}

int main()
{
    StackDemo();
    QueueDemo();
    return 0;
}
```

![](bbox=[0.15, 0.29, 0.23, 0.35])

When you specify a container to use inside the stack or queue, remember to put a space between the closing angle brackets. Otherwise the compiler reads it as a single insertion operator, >>, and gets confused. Here is the output from this example:

```
===Stack Demo===
20
15
40
===Queue Demo===
5
10
15
```

# ## Copying Containers

Structures are easy to copy when class libraries are well designed. The Standard Library is that well designed. Each container class contains both a copy constructor and an equal operator. To copy a container, you either set one equal to the other or pass the first container into the constructor of the second (which copies the first into the second). The CopyContainer example shown in Listing 6-11 demonstrates how to perform this task.

# **Listing 6-11: Copying Containers Couldn't Be Easier**

```
#include <iostream>
#include <map>

using namespace std;

class Scrumptious
{
public:
    string Dessert;
};

bool operator < (const Scrumptious & first,
const Scrumptious & second)
{
```