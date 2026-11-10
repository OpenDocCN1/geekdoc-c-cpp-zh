
```sage
sage: map(copy, L)
```

whereas the deepcopy function recursively duplicates Python objects at all levels:

```sage
sage: La = [1, 2, 3]; L1 = [1, La]; L2 = deepcopy(L1)
sage: L1[1][0] = 5; [L1 == L2, L1 is L2, L1[1] is L2[1]]
[False, False, False]
```

The inverse lexicographic order is defined from the lexicographic order on *n*-tuples by reversing the order on each element:

$$P = (p_0, p_1, \ldots, p_{n-1}) <_{\mathrm{lex\,inv}} Q = (q_0, q_1, \ldots, q_{n-1})$$
$$\Longleftrightarrow \exists r \in \{0, \ldots, n-1\},\quad (p_{r+1}, \ldots, p_{n-1}) = (q_{r+1}, \ldots, q_{n-1}) \text{ and } p_r > q_r.$$

Programming this inverse lexicographic order might be done using the above-defined alpha function, which implements the lexicographic order. We have to copy the lists $P$ and $Q$ to perform the inversion without modifying the lists. More precisely the lexInverse function reverts the *n*-tuples by reverse, and returns the opposite of the Python integer corresponding to the wanted comparison: −(P₁ <ₗₑₓ Q₁):

```sage
sage: def lexInverse(P, Q):
....:     P1 = copy(P); P1.reverse()
....:     Q1 = copy(Q); Q1.reverse()
....:     return -alpha(P1, Q1)
```

The changes made on a list given as argument of a function are performed on the original list, since the functions do not copy arguments which are lists. Thus a function that would perform P.reverse(), in place of P1 = copy(P) and P1.reverse(), would modify definitively the list $P$; this side effect is usually not wanted.

The variable $P$ is a local variable of the function, independent from any other global variable also called $P$, but this has nothing to do with modifications made to a list given as argument of the function.

The lists in Python and Sage are implemented as dynamic tables, contrary to Lisp and OCaml where lists are defined by a head $t$ and a tail list $Q$. The Lisp command cons(t,Q) returns a list with head $t$ without modifying the list $Q$, whereas in Python, adding an element $e$ to a dynamic table $T$ via T.append(e) modifies the table $T$. Both representations have advantages and drawbacks, and switching from one to the other is possible, however the efficiency of a given algorithm might greatly vary from one representation to the other.

#### 3.3.7 Mutable and Immutable Data Structures

Lists enable us to construct and manipulate elements that can be modified: they are called *mutable* data structures.

Python also allows to define immutable objects. The immutable data structure corresponding to lists is called sequence or tuple, and is denoted with parentheses (...), instead of square brackets [...]. A tuple with only one element is defined by adding a comma after this element, to distinguish it from mathematical parentheses.

```sage
sage: S0 = (); S1 = (1,); S2 = (1, 2)
sage: [1 in S1, 1 == (1)]
[True, True]
```

The operations on tuples are essentially the same as those on lists, for example map constructs the image of a tuple by a function, filter extracts a sub-sequence. In all cases the result is a list, and the for comprehension transforms a tuple into a list:

```sage
sage: S1 = (1, 4, 9, 16, 25); [k for k in S1]
[1, 4, 9, 16, 25]
```

The zip command groups several lists or tuples term-by-term, and is equivalent to the following map command:

```sage
sage: L1 = [0..4]; L2 = [5..9]
sage: zip(L1, L2)
[(0, 5), (1, 6), (2, 7), (3, 8), (4, 9)]
sage: map(lambda x, y: (x, y), L1, L2)
[(0, 5), (1, 6), (2, 7), (3, 8), (4, 9)]
```

#### 3.3.8 Finite Sets

Contrary to lists, the set data structure only keeps track of whether an element is present or absent, without considering its position or number of repetitions. Sage constructs finite sets via the Set function, applied to the list of its elements. The result is output with curly brackets:

```sage
sage: E = Set([1, 2, 4, 8, 2, 2, 2]); F = Set([7, 5, 3, 1]); E, F
({8, 1, 2, 4}, {1, 3, 5, 7})
```

The operator in checks whether a set contains a given element, and Sage allows the union of sets by + or |, the intersection by &, the set difference by -, and the symmetric difference using ^:

```sage
sage: E = Set([1, 2, 4, 8, 2, 2, 2]); F = Set([7, 5, 3, 1])
sage: 5 in E, 5 in F, E + F == F | E
(False, True, True)
sage: E & F, E - F, E ^ F
({1}, {8, 2, 4}, {2, 3, 4, 5, 7, 8})
```

The len(E) command gives the cardinality of such a finite set. The operations map, filter and for..if... apply to sets as well as tuples, and yield lists as results. Accessing a given element is done via E[k]. The commands below construct in two different ways the list of elements of a set:

```sage
sage: E = Set([1, 2, 4, 8, 2, 2, 2])
sage: [E[k] for k in [0..len(E)-1]], [t for t in E]
([8, 1, 2, 4], [8, 1, 2, 4])
```

The following function checks whether E is a subset of F, using the union operator:

```sage
sage: def included(E, F): return E + F == F
```

Contrary to lists, sets are immutable, and thus cannot be modified; their elements must also be immutable. Sets of tuples or sets of sets are thus possible, but not sets of lists:

```sage
sage: Set([Set([]), Set([1]), Set([2]), Set([1, 2])])
{{}, {1}, {2}, {1, 2}}
sage: Set([(), (1,), (2,), (1, 2)])
{(1, 2), (2,), (), (1,)}
```

The following function scans all subsets of a set recursively:

```sage
sage: def Parts(EE):
....:     if EE == Set([]): return Set([EE])
....:     else:
....:         return withOrWithout(EE[0], Parts(Set(EE[1:])))
```

```sage
sage: def withOrWithout(a, E):
....:     return Set(map(lambda F: Set([a]) + F, E)) + E
```

```sage
sage: Parts(Set([1, 2, 3]))
{{}, {1}, {2}, {3}, {1, 2}, {1, 3}, {2, 3}, {1, 2, 3}}
```

The withOrWithout(a, E) function call takes a set E of subsets, and constructs the set twice as large made from those subsets, and those subsets added (in the set union sense) with a. The recursive construction starts with a set with one element E = {{}}.

#### 3.3.9 Dictionaries

Last but not least, Python, and thus Sage, provides the notion of dictionary. Like a phone book, a dictionary associates a value to a given key.

The keys of a dictionary might be of any immutable type: numbers, character strings, tuples, etc. The syntax is like lists, using assignments from the empty dictionary dict() which can be written {} too:

```sage
sage: D = {}; D['one'] = 1; D['two'] = 2; D['three'] = 3; D['ten'] = 10
sage: D['two'] + D['three']
5
```

The above example shows how to add an entry (key, value) to a dictionary, and how to access the value associated to a given key via D[...].

The operator in checks whether a key is in a dictionary, and the commands del D[x] or D.pop(x) erase the entry of key x in this dictionary.

The following example demonstrates how a dictionary can be used to represent a function on a finite set:

E = {a0, a1, a2, a3, a4, a5}, f(a0) = b0, f(a1) = b1, f(a2) = b2, f(a3) = b0, f(a4) = b3, f(a5) = b3.

## 4 Graphics

Drawing a function of one or two variables, or a series of data, makes it easier to grasp a mathematical or physical phenomenon, and helps us make conjectures. In this chapter, we illustrate the graphical capabilities of Sage using several examples.

### 4.1 2D Graphics

Several definitions of a plane curve are possible: as the graph of a function, from a parametric system, using polar coordinates, or by an implicit equation. We detail these four cases, and give some examples of data visualisation.

#### 4.1.1 Graphical Representation of a Function

To draw the graph of a symbolic or Python function on an interval $[a,b]$, we use `plot(f(x), a, b)` or the alternative syntax `plot(f(x), x, a, b)`.

```sage
sage: plot(x * sin(1/x), x, -2, 2, plot_points=500)
```

Among the numerous options of the `plot` command, we mention the following:

- `plot_points` (default value 200): minimal number of computed points;
- `xmin` and `xmax`: interval bounds over which the function is displayed;
- `color`: colour of the graph, either a RGB triple, a character string such as `'blue'`, or an HTML colour like `'#aaff0b'`;
- `detect_poles` (default value False): enables to draw a vertical asymptote at poles of the function;
