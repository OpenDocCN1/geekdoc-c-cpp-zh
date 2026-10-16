define and use base classes with both state and pure virtual functions. However, such mixtures of approaches can be confusing and require extra care.

With the introduction of abstract classes, we have the basic facilities for writing a complete program in a modular fashion using classes as building blocks.

# 20.5 Access Control

A member of a class can be private, protected, or public:

+   - If it is private, its name can be used only by member functions and friends of the class in which it is declared.
+   - If it is protected, its name can be used only by member functions and friends of the class in which it is declared and by member functions and friends of classes derived from this class (see §19.4).
+   - If it is public, its name can be used by any function.

This reflects the view that there are three kinds of functions accessing a class: functions implementing the class (its friends and members), functions implementing a derived class (the derived class’s friends and members), and other functions. This can be presented graphically:

general users derived class’s member functions and friends
own member functions and friends

public:
protected:
private:

The access control is applied uniformly to names. What a name refers to does not affect the control of its use. This means that we can have private member functions, types, constants, etc., as well as private data members. For example, an efficient nonintrusive list class often requires data structures to keep track of elements. A list is nonintrusive if it does not require modification to its elements (e.g., by requiring element types to have link fields). The information and data structures used to organize the list can be kept private:

```
template<class T>
class List {
public:
void insert(T);
T get();
// ...
private:
struct Link { T val; Link* next; };
struct Chunk {
enum { chunk_size = 15 }; Link v[chunk_size];
Chunk* next;
Chunk* allocated; Link* free;
Link* get_free(); Link* head;
```