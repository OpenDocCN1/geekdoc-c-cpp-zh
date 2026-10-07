
## Smart Pointer Template Classes

If Listing 16.5 represents the pinnacle of your programming aspirations, any of these three smart pointers will serve your purposes. But there is more to the story.

## Smart Pointer Considerations

Why three smart pointers? (Actually, there are four, but we won't discuss weak_ptr.) And why is auto_ptr deprecated?

Begin by considering assignment:

```
auto_ptr<string> ps (new string("I reigned lonely as a cloud."));
auto_ptr<string> vocation;
vocation = ps;
```

What would the assignment accomplish? If ps and vocation were ordinary pointers, the result would be two pointers pointing to the same string object. That is not acceptable because the program would wind up attempting to delete the same object twice—once when ps expires, and when vocation expires. There are ways to avoid this problem:

- Define the assignment operator so that it makes a deep copy. This results in two pointers pointing to two distinct objects, one of which is a copy of the other.
- Institute the concept of *ownership*, with only one smart pointer allowed to own a particular object. If only the smart pointer owns its destructor will delete the object. Then assignment transfer ownership. This is the strategy used by auto_ptr and for unique_ptr, although unique_ptr is somewhat more restrictive.
- Create an even smarter pointer that keeps track of how many smart pointers refer to a particular object. This is called *reference counting*. Assignment, for example, would increase the count by one, and the expiration of a pointer would decrease the count by one. When the final pointer expires delete be invoked. This is the shared_ptr strategy.

The strategies we've discussed for assignment, of course, would also apply to the copy constructors.
Each approach has its uses. Listing 16.6 shows an example for which auto_ptr is poorly suited.

### Listing 16.6 fowl.cpp

```
// fowl.cpp -- auto_ptr a poor choice
#include <iostream>
#include <string>
#include <memory>

int main()
{
    using namespace std;
    auto_ptr<string> films[5] =
```
```
{
auto_ptr<string> (new string("Fowl Balls")),
auto_ptr<string> (new string("Duck Walks")),
auto_ptr<string> (new string("Chicken Runs")),
auto_ptr<string> (new string("Turkey Errors")),
auto_ptr<string> (new string("Goose Eggs"))
}
auto_ptr<string> pwin;
pwin = films[2]; // films[2] loses ownership

cout << "The nominees for best avian baseball film film are\n";
for (int i = 0; i < 5; i++)
  cout << *films[i] << endl;
cout << "The winner is " << *pwin << "!\n";
cin.get();
return 0;
```

Here is some sample output:
The nominees for best avian baseball film are
Fowl Balls
Duck Walks
Segmentation fault (core dumped)

The "core dumped" message should help fix in your memory that a misused auto_ptr can be a problem. (The behavior for this sort of code is undefined, so you might encounter different behavior, depending on ownership from films[2]) Here is the problem that the following statement transfers:
pwin = films[2]; // films[2] loses ownership

That causes films[2] to no longer refer to the string. An auto_ptr gives up ownership of an object, it no longer access to the object. When the program goes to print the string pointed to by films[2], it finds the null pointer, which appears an unpleasant surprise.

Suppose you go back to Listing 16.6 but use shared_ptr instead of auto_ptr. (You'll need a compiler that supports the C++11 shared_ptr class.) Then the program runs fine and gives this output:
The nominees for best avian baseball film are
Fowl Balls
Duck Walks
Chicken Runs
Turkey Errors
Goose Eggs
The winner is Chicken Runs!

## Smart Pointer Template Classes

The difference occurs in this part of the program:
shared_ptr<string> pwin;
pwin = films[2];

This time pwin and films[2] point to the same object, and the reference count is upped from 1 to 2. At the end of the program, pwin, which was declared last, is the object to have its destructor called. The destructor decreases the count to 1. The members of shared_ptrs are freed. The destructor for films [2] decrements the count to 0 and the previously allocated space.

So with shared_ptr, Listing 16 runs fine. With auto_ptr it experienced a runtime crash. What happens if you use unique_ptr? Like auto_ptr, unique_ptr incorporates the ownership model. Instead of destructing, the unique_ptr version yields a compile-time error to this line:

```
pwin = films[2];
```

Clearly, it is to look further into the differences between these last two types.

## Why unique_ptr Is Better than auto_ptr

Consider the following statements:

```
auto_ptr<string> p1(new string("auto")); //#1
auto_ptr<string> p2; //#2
p2 = p1; //#3
```

When, in statement #3, p2 takes over ownership of the string object, p1 is stripped of ownership. This, recall, is good because it prevents the destructors for both p1 and p2 from trying to delete the same object. But it is also bad if the program subsequently tries to use p1 because no longer points to valid data.

Now consider the unique_ptr equivalent:

```
unique_ptr<string> p3(new string("auto")); //#4
unique_ptr<string> p4; //#5
p4 = p3; //#6
```

In this case, the compiler does not allow statement #6, so avoid the problem of p3 not pointing to valid data. Hence, unique_ptr is safer (compile-time error versus potential program crash).

But there are times when assigning one smart pointer to another doesn't leave a dangerous orphan behind. Suppose we have this function definition:

```
unique_ptr<string> demo(const char * s)
{
    unique_ptr<string> temp(new string(s));
    return temp;
}
```

And suppose we then have this code:

```
unique_ptr<string> ps;
s = demo("Uniquely special");
```

Here, demo() returns a temporary unique_ptr, and then ps takes over ownership of the object originally owned by the returned unique_ptr.Then the returned unique_ptr is destroyed.That's okay because ps now has ownership of the string object. But another good thing has happened. Because the temporary unique_ptr returned by demo() is soon destroyed, there's no possibility of being misused in an attempt to access invalid data. In other words, there is no reason to forbid assignment in this case. And, miraculously enough, the compiler allows it!

In short, if a program attempts to assign one unique_ptr to another, the compiler allows it if the source object is a temporary value and disallows it if the source object has some duration:

```
using namespace std;
unique_ptr<string> ps1(new string "Hi ho!");
unique_ptr<string> ps2;
ps2 = ps1; // #1 not allowed
unique_ptr<string> ps3;
ps3 = unique_ptr(new string "Yo!"); // #2 allowed
```

Assignment #1 would leave a dangling unique_ptr behind (that is, a possible source of mischief).Assignment #2 leaves no unique_ptr behind because it invokes the unique_ptr constructor, which constructs temporary object that is destroyed when ownership is transferred to ps3. This selective behavior is one indication that unique_ptr is superior to auto_ptr, which would allow both forms of assignment. Its also the reason that auto_ptr are banned (by recommendation, not by the compiler) from being used in container objects, whereas unique_ptrs are allowed. If a container tries to do something along the lines of assignment #1 to the contents of a container of unique_ptrs, you get a compile-error. If the algorithm tries to do something assignment #2, that's okay, and the program proceeds. With auto_ptrs, cases like #1 could lead to undefined behavior and mysterious crashes.

Of course, it could be possible that you really want to do something like statement #1. The assignment is unsafe unless you use the abandoned pointer in an smart manner, such as dereferencing it. But you could safely since C++ has a standard library function std::move() that lets you assign one unique_ptr to another. Here is an example using the previously defined demo() function, which returns a unique_ptr<string> object:

```
using namespace std;
unique_ptr<string> ps1, ps2;
ps1 = demo("Uniquely special");
ps2 = move(ps1); // enable assignment
ps1 = demo("and more");
cout << *ps2 << " " << *ps1 << endl;
```
