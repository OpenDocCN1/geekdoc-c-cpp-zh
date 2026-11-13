this, the dynamic extension of KDEEB can be seen as a fully online visualization technique. As KDEEB can execute hundreds of bundling iterations per second, it means it can be used to generate real-time bundled animations of streaming graphs [Hurter et al. 13].

Visualizing large dynamic graphs is a challenging, and increasingly important, area in information visualization. However, even more so here than for static graphs, a gap exists between the effectiveness and efficiency of dynamic graph visualization methods and the size and complexity of the graph datasets. Several innovative visual metaphors to show change in hierarchies, association edges, and data attributes are presented by Burch et al. in a series of papers [Burch and Diehl 08, Burch et al. 10, Greilich et al. 09]. For a framework of dynamic layout techniques for graphs drawn using node-link metaphors, a good starting reference is [Frishman and Tal 08].

# 11.4.3 Diagram Visualization

Consider a set of elements _E_ = {_e<sub>i</sub>_}. Over this set, assume we have defined several subsets _S<sub>j</sub>_ = {_e<sub>i</sub>_<sup>j</sup>} ⊂ _E_. Furthermore, let us assume that the set _E_ already admits a visualization which maps its elements _e<sub>i</sub>_ to particular spatial locations and also associate particular drawing metaphors, such as shapes, colors, and sizes. How can we intuitively show the sets _S<sub>j</sub>_ atop of a given visualization of _E_? More precisely, how can we construct a visualization of all _S<sub>j</sub>_ so that

+   1. given a set _S<sub>j</sub>_, we can easily tell which are its elements _e<sub>i</sub>_<sup>j</sup> from all elements _e<sub>i</sub>_ of _E_;

+   2. given an element _e<sub>i</sub>_ of _E_, we can easily tell which are the sets _S<sub>j</sub>_ which include _e<sub>i</sub>_;

+   3. we achieve the above two tasks without modifying the underlying visualization proposed for _E_?

Essentially, the problem we face is that of drawing so-called Venn-Euler diagrams atop of a given visualization of the set _E_. A Venn-Euler diagram typically consists of a set of closed contours _C<sub>j</sub>_ so that all visual representations of elements in a subset _S<sub>j</sub>_ can be easily seen as being contained within _C<sub>j</sub>_. Furthermore, the drawing of the contours _C<sub>j</sub>_ should help spotting all sets _S<sub>j</sub>_ into which a given element _e<sub>i</sub>_ ∈ _E_ falls.

Several solutions exist to this problem. First and easiest, of the number of subsets is small, we can color elements _e<sub>i</sub>_ in each subset by a distinct color. This addresses task (1) mentioned above—all elements having the same color belong to