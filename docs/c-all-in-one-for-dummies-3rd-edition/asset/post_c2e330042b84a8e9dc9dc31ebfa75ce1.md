
## Book IV: Chapter 6 — Programming with the Standard Library

When you compile and run this application, you see the following output:

```text
ten 10
thirty 30
twenty 20
hello
there
ladies
and
aliens
```

![](img/6ba99460b0feb3585671a4612ff5fabb_594_0.png)

When you create a `vector`, it allocates some space for the data you put in it. But after all that space gets filled up and `vector` is stuffed to the brim, `vector` will resize itself, adding more space. But in doing so, it uses the old memory-shuffle trick where it first allocates a bigger chunk of memory; then it copies the existing data into the beginning of that bigger chunk of memory, and finally it frees the original chunk of memory. Now, if you use the various iterator functions to home in on a certain item in `vector` (giving you a pointer to the item) — and you save that pointer — then, after `vector` reallocates itself, that pointer will no longer be valid! It will point to somewhere in the original memory block that's no longer being used. So be careful.

For example, suppose you have the following code to set up a `vector`:

```cpp
vector<int> test;
test.push_back(1);
test.push_back(2);
test.push_back(3);
```

and then you use an iterator to get to the beginning: from there you go to the second item in `vector`; then you print the address of the second item:

```cpp
vector<int>::iterator i1 = test.begin();
i1++;
cout << i1 << endl;
```

Then you decide to add a whole bunch of items:

```cpp
for (int loop = 0; loop < 5000; loop++)
{
    test.push_back(loop);
}
```

Now, if you once again use an iterator to get to the second item, and then print the address like so:

```cpp
vector<int>::iterator i2 = test.begin();
i2++;
cout << i2 << endl;
```

you will likely see a different number from the one you saw previously. If so, it means `vector` reallocated itself — which means, in turn, that the original pointer is no longer valid.

### A map of pairs in your hand

When you iterate through `map`, you get back not just the value of each item nor do you get just the key of each item. Instead, you get back a pair of things — the key and the value together. These live inside an instance of a class called `Pair`. (Although, really, it’s a template.) This pair instance has two member variables, `first` and `second`. The `first` member refers to the key in the pair, and the `second` member refers to the value in the pair. When you iterate through `map`, the iterator points to an instance of `Pair`, so you can grab the key by looking at `first` and the value by looking at `second`. But be careful, because `Pair` is the internal storage bin inside `map`. You’re not looking at copies; you’re looking at the actual data in `map`. If you change the data as in this code:

```cpp
while (loopy != NumberWords.end())
{
    loopy->second = loopy->second * 2;
    loopy++;
}
```

you will be changing the value stored in `map` — not a copy of it. So use caution!

### The Great Container Showdown

In the sections that follow, we give a rundown of the containers available in the Standard Library. Different containers have different places in life. Some are tall, some are short — wait a minute, that’s not right. They each have a different purpose; in the following sections, we show you where you can use each of them.

### Associating and storing with a set

First things first. `set` is not a set. If you have any background in mathematics, you’ll feel more at home with the notion of a set. And in math, a set doesn’t have an order to it. It’s a group of items stored in, well, a set.

In the Standard Library, `set` has an order to it. However, like a math set, `set` doesn’t allow duplicates. If you try to put an item in `set` that’s already there, `set` will ignore your attempt to do so.

The `Sets` example shown in Listing 6-7 demonstrates how to use `set`.

The reason we get back an iterator is because the iterator type is really a typedef for a pointer to an item inside `set`. Oh, okay; that makes sense, then: When we call `find()`, we get back a pointer to an item in `set`, even if its typename is `iterator`. And so, to access the item, we dereference the pointer.

In Listing 6-7, we did something handy: We created a function that lets us use our `Employee` instance with `cout`. We did this by overloading the insertion function. This function's header looks like this:

```cpp
ostream& operator << (ostream &out, const Employee &emp) {
```

The first parameter represents `cout`, and the second is the item we're couting. And so, inside this function, we write to `cout` the individual members of the `Employee`. Not a problem.

### Unionizing and intersecting sets

Everybody has an opinion on unionizing, but fortunately, we're not talking about workers' unions in this section. Instead, we're talking about sets and how you can a) combine two sets to get the union, or b) find the common elements to get the intersection.

When you `#include <set>`, you automatically get a couple of handy functions for finding the union and intersection of some sets.

| **Showdown: maps versus sets** |
| --- |
| And for the first showdown, we'd like to offer you a philosophical (yet practical!) discussion on the difference between `map` and `set`. `map` lets you store information based on a key, through which you can retrieve a value. Elsewhere in this chapter, we use an example where the key is an `Employee` instance and the value is a `Salary` instance. But with `set`, you can achieve something similar: In Listing 6-7, we could have had a single class containing both `Employee` and `Salary` information. And you can see in Listing 6-7 that we were able to look up the `Employee` instance based on nothing but a social security number. So in this sense, we created a `map` where the key is a social security number and the value is the rest of the employee information. Tricky, no? The fact is, you can often accomplish associations with `set`, as you can with `map`. But the advantage to `set` is that you need to store only one instance for each item, whereas with `map`, you must have two instances, both a key and a value. But the advantage to `map` is that you can use the nice bracket notation. The choice is yours. |

![](img/6ba99460b0feb3585671a4612ff5fabb_599_0.png)

`set` does not allow duplicates. A union of two sets is a set that consists of all the elements of the two sets combined, but without any duplicates. The intersection is also itself a set, and therefore it also has no duplicates.

The `Sets2` example in Listing 6-8 demonstrates how you can find the intersection and union of two sets.

### Listing 6-8: Finding an Intersection and a Union Is Easy!

```cpp
#include <iostream>
#include <set>
#include <algorithm>

using namespace std;

void DumpClass(set<string> *myset)
{
    set<string>::iterator iter = myset->begin();

    while (iter != myset->end())
    {
        cout << *iter << endl;
        iter++;
    }
}

int main()
{
    set<string> EnglishClass;
    set<string> HistoryClass;

    EnglishClass.insert("Zeus");
    EnglishClass.insert("Magellan");
    EnglishClass.insert("Vulcan");
    EnglishClass.insert("Ulysses");
    EnglishClass.insert("Columbus");

    HistoryClass.insert("Vulcan");
    HistoryClass.insert("Ulysses");
    HistoryClass.insert("Ra");
    HistoryClass.insert("Odin");

    set<string> Union;
    set<string> Intersection;

    insert_iterator<set<string> >
        IntersectIterate(Intersection, Intersection.begin());

    insert_iterator<set<string> >
        UnionIterate(Union, Union.begin());

    set_intersection(EnglishClass.begin(),
        EnglishClass.end(),
        HistoryClass.begin(), HistoryClass.end(),
        IntersectIterate);
    cout << "==Intersection==" << endl;
    DumpClass(&Intersection);

    set_union(EnglishClass.begin(),
              EnglishClass.end(),
              HistoryClass.begin(), HistoryClass.end(),
              UnionIterate);
    cout << "==Union==" << endl;
    DumpClass(&Union);

    return 0;
}
```

When you run the code in Listing 6-8, you see this output:

```text
==Intersection==
Ulysses
Vulcan

==Union==
Columbus
Magellan
Odin
Ra
Ulysses
Vulcan
Zeus
```

But as you can see, something a little bizarre is in the code. Specifically, this part isn't exactly simple:

```cpp
insert_iterator<set<string> >
    IntersectIterate(Intersection, Intersection.begin());
```

This is used in the call to `set_intersection`. First, recognize that this crazy code is a variable declaration. The first line is the type of the variable, a template called `insert_iterator`. The template parameter is the type of `set`, in this case `set<string>`.

The next line is the instance name, `IntersectIterate`, and the constructor requires two things: the set that will hold the intersection (called `Intersection`) and an iterator pointing to the beginning of the `Intersection` set (even though the set is empty).

The variable that these two lines create is an iterator, and it is basically a helper object that some function can use to insert multiple items into a list. In this case, the function is `set_intersection()`. Now the `set_intersection()` function doesn't take as parameters the sets directly; instead, it takes the beginning and ending iterators of the two sets, along with the `IntersectIterate` thingamabob declared earlier. And you can see in Listing 6-8 that those are the five items we passed to the `set_intersection()` function.

Then, after calling the `set_intersection()` function, the `Intersection` object will contain the intersection of the two sets.
