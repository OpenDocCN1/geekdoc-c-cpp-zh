Overall, we find the trait design necessary in practice for efficiency and modularity, but we regret the modularity lost in Value classes. We regard traits as a necessary evil in practice.

# ## 37.3 Characterizing Data Structures

◇ Classic ordered structures contain a set of elements. Each element has **value** and a single integer or real number **key**. For example, the values might be student records and the keys the students' grades. We say that the data structures are **ordered** because there is a total ordering on the keys.

Regardless of their original denotation, one can interpret the key as a position on the real number line. This leads to our later generalization of multidimensional keys representing points in space.

There are many ways to analyze data structures. In this chapter, you'll see two kinds of analysis intermitted. It is impossible to give a one-size-fits-all characterization of these structures and advice on which is "best"—it depends on the kind of data you expect to encounter in the scene. We therefore sketch asymptotic analyses and offer practical considerations of how they apply to real use. The conclusions of each section aren't really the goal. Instead, the issues raised in the course of reaching them are what we want you to think about and apply to problems.

We do recognize two usage patterns and prescribe the following high-level advice in selecting data structures.

+   - **When using data structures in a generic way**, trust asymptotic bounds ("big-O"). Generic use means for a minor aspect of an algorithm, for fairly large problems, and where you know little about the distribution of keys and queries. Trusting bounds means, for example, that operations on trees are often faster than on lists at comparable storage cost. Parameterize the bound on the factor that you really expect to dominate, which is often the number of elements.
+   - **When considering a specific problem** for which you have some domain knowledge and really care about performance, use all of your engineering skill. Consider the actual kinds of scenes/distributions and computer architecture involved, and perform some experiments. Perhaps for the size of problem at hand the scattered memory access for a tree is inferior to that of an array, or perhaps the keys fall into clusters that can be exploited.

To make the analysis tools concrete and set up an analogy to spatial data structures, we show an example on two familiar classic data structures in the following subsections. Consider two alternatives for storing *n* values that are student records in a course database at a college, where each record is associated with a real-number key that is the student's grade in the course.

The first structure to consider is a **linked list**. Although we say that a list is an "ordered" data structure, recall that the description applies to the fact that any two *keys* have a mathematical ordering: less than, greater than, or equal to. The order of elements within the list itself will be arbitrary. More sophisticated data structures exploit the ordering of the keys to improve performance.

The second data structure is a **balanced binary tree**. The elements within the tree are arranged so that every element in the right subtree of a node contains elements whose *keys* are larger than or equal to the key at the node. The left subtree of a node contains elements whose *keys* are less than or equal to the key at the node.