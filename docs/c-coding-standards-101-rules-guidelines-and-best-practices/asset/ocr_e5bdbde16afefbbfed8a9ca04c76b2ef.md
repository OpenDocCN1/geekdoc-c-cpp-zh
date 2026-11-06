# 79. Store only values and smart pointers in containers.

# Summary

Store objects of value in containers: Containers assume they contain value-like types, including value types (held directly), smart pointers, and iterators.

# Discussion

The most common use of containers is to store values held directly (e.g., `vector<int>`, `set<string>`). For containers of pointers: If the container owns the pointed-to objects, prefer a container of reference-counted smart pointers (e.g., `list<shared_ptr<Widget> >`); otherwise, a container of raw pointers (e.g., `list<Widget*>`) or of other pointer-like values such as iterators (e.g., `list< vector<Widget>::iterator >`) is fine.

# Examples

*Example 1: auto_ptr.* Objects of **auto_ptr<T>** are not value-like because of their transfer-of-ownership copy semantics. Using a container of **auto_ptrs** (e.g., a **vector< auto_ptr<int> >**) should fail to compile. Even if it does compile, *never* write that; if you want to write it, you almost certainly want a container of **shared_ptrs** instead.

*Example 2: Heterogeneous containers.* To have a container store and own objects of different but related types, such as types derived from a common **Base** class, prefer **container< shared_ptr<Base> >**. An alternative is to store proxy objects whose non-virtual functions pass through to corresponding virtual functions of the actual object.

*Example 3: Containers of non-value types.* To contain objects even though they are not copyable or otherwise not value-like (e.g., **DatabaseLocks** and **TcpConnections**), prefer containing them indirectly via smart pointers (e.g., **container< shared_ptr<DatabaseLock> >** and **container< shared_ptr<TcpConnection> >**).

*Example 4: Optional values.* When you want a **map<Thing, Widget>**, but some Things have no associated **Widget**, prefer **map<Thing, shared_ptr<Widget> >**.

*Example 5: Index containers.* To have a main container hold the objects and access them using different sort orders without resorting the main container, you can set up secondary containers that “point into” the main one and sort the secondary containers in different ways using dereferenced compare predicates. But prefer a container of **MainContainer::iterators** (which are value-like) instead of a container of pointers.

# References

*[Allison98] §14 • [Austern99] §6 • [Dewhurst03] §68 • [Josuttis99] §5.10.2 • [Koenig97] §5 • [Meyers01] §3, §7-8 • [SuttHys04b]*