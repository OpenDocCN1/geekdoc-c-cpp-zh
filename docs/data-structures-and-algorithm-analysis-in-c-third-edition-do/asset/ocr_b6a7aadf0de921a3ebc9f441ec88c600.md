# 1.3 Design Patterns

that tradeoffs are possible. Therefore, a given design pattern might have variations
on on its application to match the various tradeoffs inherent in a given situation.

The rest of this section introduces a few simple design patterns that are used
later in the book.

# 1.3.1 Flyweight

The Flyweight design pattern is meant to solve the following problem. You have an
application with many objects. Some of these objects are identical in the informa-
t they contain, and the role that they play. They must be reached from
various places, and conceptually they really are distinct objects. Because there is
so much duplication of the same information, we would like to take advantage of
the opportunity to reduce memory cost by sharing that space. An example comes
from representing the layout for a document. The letter "C" might reasonably be
represented by an object that describes character's strokes and bounding box.
However, we do not want to create a separate "C" object everywhere in the doc-
ment a "C" appears. The solution is to allocate a single copy of the shared
representation for "C" objects. Then, every place in the document that needs a
"C" in a font size, and typeface will reference this single copy. The various
instances of references to a specific form of "C" are called flyweights.

We could describe the layout of a page by using a tree structure. The
row of the root represents the entire page. The page has multiple nodes, for
each column. The column nodes have child nodes for each row. The rows
have child nodes for each character. These representations for characters are the fly-
weight. The flyweight includes the reference to the shared shape information, and
might contain additional information to that instance. For example, each
instance for "C" will contain a reference to the shared information about
strokes and it might also contain the location for that instance of
character on the page.

Flyweights are used in the implementation for the PR quadtree structure
storing collections of point objects, described in Section 13.3. In a PR quadtree,
we have a tree with leaf nodes. Many of these leaf nodes represent empty
areas, and so the information that they store is the fact that they are empty.
These identical nodes can be implemented using a reference to a single instance of
tflyweight for better memory efficiency.

# 1.3.2 Visitor

Given a tree to describe a page layout, we might wish to perform some
activity on every node in the tree. Section 5.2 discusses tree traversal, which is the
process of visiting every node in the tree in a defined order. A simple example for
tour text composition application might be to count the number of nodes in the tree