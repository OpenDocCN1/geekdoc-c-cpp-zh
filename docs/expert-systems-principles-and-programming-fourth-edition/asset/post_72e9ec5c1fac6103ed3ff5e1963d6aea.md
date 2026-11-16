
if all of the subgoals are satisfied. The exception is when the special predicate for failure is used. A failure predicate is convenient because it's not easy to prove negation in classical logic, and PROLOG is based on classical logic. Negation is viewed as the failure to find a proof and this can be a very long and involved process if there are many potential matches. The **cut** and special failure predicate makes the negation process more efficient by reducing the searching for a proof.

The commas separating the subgoals represent a logical AND. The symbol :- is interpreted as an IF. If only the head exists and there is no right-hand side, as in:

p.

then the head is considered true. This is why predicates such as the following are considered facts and thus must be true:

```
color (red) .
has_a (john , father) .
```

Another way of to a query is negative. That is, for a query to produce a negative result, many or all of the links in a net may have to be searched. As shown in the Traveling Salesman problem in Chapter 1, the number of links is the factorial of the number of nodes minus one if they are all connected. Although not all representations will require this degree of connectivity, the possibility of a combinatorial explosion exists.

Semantic nets were originally proposed as a model of human associative memory in which one node has links to others and information retrieval occurs due to a spreading activation of nodes. However, other mechanisms must also be available to the human brain since it does not take a long time for a human to answer the query—Is there a football team on Pluto? There are about 10^11 neurons in the human brain and about 10^15 links. If all knowledge were represented by a semantic net, it would take a very, very long time to answer negative queries like the football question because of all the searching involved with 10^15 links.

Semantic nets are logically inadequate because they cannot define knowledge in the way that logic can. A logic representation can specify a certain chair, some chairs, all chairs, no chairs, and so forth, as will be discussed later in this chapter. Another problem is that semantic nets are heuristically inadequate because there is no way to embed heuristic information in the net on how to efficiently search the net. A **heuristic** is a rule of thumb that may help in finding a solution but is not guaranteed, in the way an algorithm is guaranteed, to find a solution. Heuristics are very important in AI because typical AI problems are so hard that an algorithmic solution does not exist or is too inefficient for practical use. The only standard control strategy built into a net that might help is inheritance but not all problems may have this structure.

A number of approaches have been tried to correct the inherent problems of semantic nets. Logic enhancements have been made and heuristic enhancements have been tried by attaching procedures to nodes. The procedures will be executed when the node becomes activated. However, the resulting systems gained little in capability at the expense of the natural expressiveness of semantic nets. The conclusion of all of this effort is that like any tool, semantic nets should be used for those things they do best, showing binary relationships, and not be distorted into a universal tool.
