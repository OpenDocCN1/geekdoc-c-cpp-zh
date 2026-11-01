example, a class hierarchy is a graph with is-child-of and is-parent-of relationships between classes, which are the nodes. These relationships follow different directions. If we take out the is-child-of relation-ships, we have a directed graph because the relationships work in one direction only. An acyclic graph has an entry and an exit; there is no way to end up back where you started by following the relationships. A class hierarchy of parent relationships is not only directed, but also acyclic.

The same thing can be said of namespaces and containment relationships. A namespace can nest another namespace, but the graph of nesting is a DAG. For example:

Click here to view code image

```
namespace World {
    namespace Buildings {
        namespace Municipal {}
        namespace Business {}
    }
}
```

We can go from World to Municipal by examining nested namespaces, but we can’t go from Municipal to World in the same way.

Second, we need to look at the lowest common ancestor (LCA). The LCA of a pair of nodes is the deepest node common to both. In the above namespace example, both namespace World and namespace World::Buildings are common ancestors of namespace World::Buildings::Municipal and namespace World::Buildings::Business, but namespace World::Buildings is the LCA.

You should now be comfortable with the idea of a DAG and an LCA, so let’s examine exactly what a using-directive does. This is covered over three pages of the standard at [namespace.udir.]² To summarize, a using-directive introduces its new meanings into the scope which is the LCA of the current scope and the target namespace’s own scope. This can be quite surprising and becomes more surprising as a codebase grows and acquires more namespaces. Let’s try out a real-world exam-ple using the above namespace hierarchy.