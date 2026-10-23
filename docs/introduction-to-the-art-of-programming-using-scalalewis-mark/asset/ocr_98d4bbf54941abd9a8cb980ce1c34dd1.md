# **26.3.2 Exercises**

+   1. Code the search-based priority queue and do speed tests to compare it to the version that maintains a sorted linkedlist. For the speed tests, insert elements with random times and dequeue them. Vary the number of elements used across an exponential range to measure how that impacts performance.

+   2. Code **Array**-based implementations of a priority queue using both a sorted **Array** and an unsorted **Array** that you search. Do speed tests to compare them to each other and to the linked list-based implementations. For the search-based method with an **Array**, do both shifting elements down and and swapping the last element into the hole left by the one that is removed.

+   3. Implement priority queues using **ArrayBuffer** and **ListBuffer** to see how efficient they are relative to our “custom” implementations.

+   4. Implement some extra wall types for the collision simulation. Consider trying walls that are not lines or writing a method that creates wall segments.

+   5. Look up some different distributions for random variables and try the cell splitting simulation using those.

# **26.3.3 Projects**

+   1. There are a few ways that you could use a priority queue in your MUD to good effect. All of them involve having a single priority queue that actions can be added to so that they will run at a later time. This will allow things like spells to have delayed effects or to wear off. It can also be used by computer controlled characters and to implement random spawning of characters. The advantage of a priority queue is that you do not have to have checks in every single character/room/item for whether something should happen. Instead, all those things could place events on the priority queue with a delay, and the main thread only pulls off places as needed.
+   
+   The idea here uses a sorted list or **Array** for the priority queue so that the **peek** operation is fast. The idea is that in most “ticks” there will not be any events on the priority queue to process. In that case, the code only does a **peek**, sees that the time of the first element is after the current time, then goes on to whatever else needs to be done.

+   2. If you are working on the web spider project, you might have noticed that many websites are extremely large. Even if you limit your spider to a single domain, say only pages coming from domains ending with cnn.com, espn.go.com, or google.com, there can still be an extremely large number of pages. If you let the processing proceed in the order that links are found, you are likely to never get to a lot of the data that you are interested in because of resource limitations. One way to deal with this is to make the queue of pages to be read work as a priority queue.
+   
+   If you know the types of pages you are looking for and have an idea of what paths they are at on the site you are running through, you can give those pages a higher priority. That way you will visit those pages first. As long as the program keeps finding pages that have a structure you have coded to be interesting, it will work on those pages and not go to other pages that are less likely to have interesting information.