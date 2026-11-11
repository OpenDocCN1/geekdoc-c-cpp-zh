
a Shape (i.e., any object of a class derived from Shape) without recompilation.

We can easily generalize this to any container that meets the C++ standard library requirements:

```cpp
template<class C>
void draw_all(const C& c)
{
    typedef typename C::const_iterator CI;
    for (CI p = c.begin(); p != c.end(); ++p)
        (*p)->draw();
}
```

Using iterators allows us to apply this draw_all() to containers that do not support subscripts, such as a standard library list:

```cpp
vector<Shape*> vs;
list<Shape*> ls;
// ...
draw_all(vs);
draw_all(ls);
```

We can even generalize this further to handle any sequence of elements defined by a pair of iterators:

```cpp
template<class Iterator> void
draw_all(Iterator b, Iterator e)
{
    for_each(b, e, mem_fun(&Shape::draw));
}
```

To simplify the implementation, I used the standard library algorithm for_each.

We might call this last version of draw_all() for a standard library list and an array:

```cpp
list<Shape*> ls;
Shape* as[100];
// ...
draw_all(ls.begin(), ls.end());
draw_all(as, as + 100);
```

## SELECTING THE "RIGHT" LANGUAGE FOR THE JOB

How useful is it to have this background in numerous paradigms? Or would it be better to invest time in becoming even more familiar with OO languages rather than learning these other paradigms? It is essential for anyone who wants to become a professional in the areas of software to know several languages and several programming paradigms. Currently, C++ is the best language for multiparadigm programming and a good language for learning various forms of programming. However, it's not a good idea to know just C++, let alone to know just a single-paradigm language. That would be a bit like being colorblind or monoglot. You would hardly know what you were missing. Much of the inspiration to good programming comes from having learned and appreciated several programming styles and seen how they can be used in different languages.

Furthermore, I consider programming of any non-trivial program a job for professionals with a solid and broad education, rather than for people with a hurried and narrow "training."

the base class constructor, it is given in the call to the derived object constructor. In general, this is done with the following construct:

```cpp
subclass (subclass parameters) : base_class (superclass parameters) {
    . . .
}
```

If no constructor is included by the developer in a class definition, the compiler includes a trivial constructor. This default constructor calls the constructor of the base class, if there is a base class.

Class members can be `private`, `protected`, or `public`. Private members are accessible only by member functions and friends of the class. Standalone functions, member functions, and classes can be declared to be friends of a class and thereby be given access to its private members. Public members are visible everywhere. Protected members are like private members, except in derived classes, whose access is described next. Derived classes can modify accessibility for their inherited members. The complete syntactic form of a derived class is as follows:

```cpp
class derived_class_name : derivation_mode base_class_name
    {data member and member function declarations};
```

The `derivation_mode` can be either `public` or `private`.⁹ (Do not confuse public and private derivation with public and private members.) The public and protected members of a base class are also public and protected, respectively, in a public-derived class. In a private-derived class, both the public and protected members of the base class are private. So, in a class hierarchy, a private-derived class cuts off access to all members of all ancestor classes to all successor classes. Private members of a base class are inherited by a derived class, but they are not visible to the members of that derived class and are therefore of no use there.

Private derivations provide the possibility that a subclass can have members with different access than the same members in the parent class. Consider the following example:

```cpp
class base_class {
private:
    int a;
    float x;
protected:
    int b;
    float y;
public:
    int c;
    float z;
};

class subclass_1 : public base_class {. . .};
class subclass_2 : private base_class {. . .};
```

9. It can also be `protected`, but that option is not discussed here.

which hides it from all other classes. Its members are public, however, so they are visible to the nesting class, single_linked_list. If they were private, node would need to declare the nesting class to be a friend to make them visible in the nesting class. Note that nested classes have no special access to members of the nesting class. Only static data members of the nesting class are visible to methods of the nested class.^10

10. A class can also be defined in a method of a nesting class. The scope rules of such classes are the same as those for classes nested directly in other classes, even for local variables declared in the method in which they are defined.

The enclosing class, single_linked_list, has just a single data member, a pointer to act as the list's header. It contains a constructor function, which sets head to the null pointer value. The four member functions allow nodes to be inserted at either end of a list object, nodes to be removed from one end of a list, and lists to be tested for empty.

The following definitions provide stack and queue classes, both based on the single_linked_list class:

```cpp
class stack : public single_linked_list {
public:
    stack() {}
    void push(int value) {
        insert_at_head(value);
    }
    int pop() {
        return remove_at_head();
    }
};
class queue : public single_linked_list {
public:
    queue() {}
    void enqueue(int value) {
        insert_at_tail(value);
    }
    int dequeue() {
        return remove_at_head();
    }
};
```

Note that objects of both the stack and queue subclasses can access the empty function defined in the base class, single_linked_list (because it is a public derivation). Both subclasses define constructor functions that do nothing. When an object of a subclass is created, the proper constructor in the subclass is implicitly called. Then, any applicable constructor in the base class is called. So, in our example, when an object of type stack is created, the constructor in single_linked_list is called, which does the necessary initialization. Then the stack constructor is called, which does nothing.

The classes stack and queue both suffer from the same serious problem: Clients of both can access all of the public members of the parent class, single_linked_list. A client of a stack object could call insert_at_tail, thereby destroying the integrity of its stack. Likewise, a client of a queue object could call insert_at_head. These unwanted accesses are allowed because both stack and queue are subtypes of single_linked_list. Public derivation is used when one wants the subclass to inherit the entire interface of the base class. The alternative is to use a derivation in which the subclass inherits only the implementation of the base class. Our two example derived classes can be written to make them not subtypes of their parent class by using private, rather than public, derivation.^11 Then, both will also need to reexport empty, because it will become hidden to their instances. This situation illustrates the motivation for the private-derivation option. The new definitions of the stack and queue types, named stack_2 and queue_2, are shown in the following:

```cpp
class stack_2 : private single_linked_list {
public:
    stack_2() {}
    void push(int value) {
        single_linked_list::insert_at_head(value);
    }
    int pop() {
        return single_linked_list::remove_at_head();
    }
    single_linked_list::empty;
};
class queue_2 : private single_linked_list {
public:
    queue_2() {}
    void enqueue(int value) {
        single_linked_list::insert_at_tail(value);
    }
    int dequeue() {
        return single_linked_list::remove_at_head();
    }
    single_linked_list::empty;
};
```

These two classes use reexportation to allow access to base class methods for clients. This was not necessary when public derivation was used.

The two versions of stack and queue illustrate the difference between subtypes and derived types that are not subtypes. The linked list is a generalization of both stacks and queues, because both can be implemented as linked lists. So, it is natural to inherit from a linked-list class to define stack and queue classes. However, neither is a subtype of the linked-list class, because both make the public members of the parent class private, which makes them inaccessible to clients.

One of the reasons friends are necessary is that sometimes a subprogram must be written that can access the members of two different classes. For

11. They would not be subtypes because the public members of the parent class can be seen in a client, but not in a client of the subclass, where those members are private.
