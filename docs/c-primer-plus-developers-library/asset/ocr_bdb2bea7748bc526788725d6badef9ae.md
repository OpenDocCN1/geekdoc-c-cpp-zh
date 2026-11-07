+   3. Place proper values into the node. In this case, the code copies an Item value into the data part of the node and sets the node’s next pointer to `NULL` (or 0, or in C++11, `nullptr`). This prepares the node to be the last item in the queue.

+   4. Increase the item count (`items`) by one.

+   5. Attach the node to the rear of the queue. There are two parts to this process. The first is linking the node to the other nodes in the list. This is done by having the next pointer of the currently rear node point to the new rear node. The second part is to set the Queue member pointer `rear` to point to the new node so that the queue can access the last node directly. If the queue is empty, you must also set the front pointer to point to the new node. (If there’s just one node, it’s both the front and the rear node.)

![](bbox=[0.17, 0.374, 0.854, 0.877])

Figure 12.10  Enqueuing an item.