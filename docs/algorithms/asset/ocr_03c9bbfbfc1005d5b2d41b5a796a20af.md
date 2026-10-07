# Crawling fast

All this assumes that the graph is given to us, with vertices numbered 1 to n and edges tucked in adjacency lists. The realities of the World Web are very different. The nodes of the graph are not known in advance, and they have to be discovered by one during the process of search. And, of course, recursion is out of the question.

Still, crawling the Web is done by algorithms similar to depth-first search. An explicit stack is maintained, containing all nodes that have been discovered (as endpoints of hyperlinks) not not explored. In fact, this “stack” is not a last-in, first-out list. It gives highest priority to the nodes that were inserted most recently (not the ones that were inserted early, that would be a breadth-first search, see Chapter 2), but to the ones that look most “interesting”—a heuristic criterion whose purpose is to keep the stack from overflowing, and to the extent, to leave unexplored nodes that are unlikely to lead to vast expenses.

In fact, crawling is typically done by many computers running simultaneously; each takes the next node to be explored from the top of the stack, downloads the http file (the kind of Web files that point to other), and scans it for hyperlinks. But when a new document is found at the end of a hyperlink, recursive calls are made; the new vertex is inserted in the central stack.

But one question: When we see a “new” document, how do we know that it is indeed new, that we have not seen before in our crawl? And how do we give it a name, so it can be inserted in the stack and recorded as “already seen?” The answer is by hashing. Incrementally, researchers have run the strongly connected components algorithm on the Web and discovered some very interesting structure.

the highest post number among those remaining will belong to a sink connected component of what remains of G. Therefore we can keep the post numbering from our initial depth-first search on GR to successively output the second strongly connected component, the third strongly connected component, and so on. The resulting algorithm is this:

+   1. Run depth-first search on GR
2. Run the undirected connected components algorithm (from Section 3.2.3) on G, and during the depth-first search, process the vertices in decreasing order of their post numbers from 1 to.

This algorithm is linear-time, the only constant in the linear term is twice that of depth-first search. (Question: How do one construct an adjacency list representation of GR in linear time? And how, in linear time, does one order the vertices of G by decreasing post values?)

Let’s run this algorithm on the graph of Figure 3.9. If step 1 considers vertices in lexicographic order, then the ordering it sets up for the second step (namely),