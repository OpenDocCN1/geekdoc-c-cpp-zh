# 386 — 9 Collections and Their Organization

![](bbox=[0.181, 0.085, 0.903, 0.445])

Fig. 9.17: States of a queue.

![](bbox=[0.163, 0.511, 0.903, 0.658])

Fig. 9.18: States of a circular queue. <iostream>

```
#include <iostream>
#include <cstdlib>
using namespace std;
```

```
const int MaxQueueSize = 50; //Maximum elements in queue
```

```
//Definition of class
template <class T>
class Queue
```