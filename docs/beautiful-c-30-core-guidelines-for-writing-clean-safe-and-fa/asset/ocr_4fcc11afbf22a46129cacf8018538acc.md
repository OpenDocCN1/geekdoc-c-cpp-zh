and have the compiler call the appropriate mem_vector depending on the nature of the template parameter rather than the specific type of the template parameter. One day I heard about SFINAE (Substitution Failure Is Not An Error) and suddenly it dawned on me: I could embed an empty struct called trivial in all the appropriate types. Then I could redeclare the second resize function:

Click here to view code image

```
```cpp
template <class T>
void mem_vector<T>::resize(size_type count,
T::trivial* = 0);
```
```

If the trivial member struct did not exist, then the function would not be considered. But all I had done was move the problem around. There was still no way of enforcing the trivial member struct would be removed if the class were no longer trivial. This was especially obvious when structs were inherited from other trivial structs and the parent struct became nontrivial. I despaired.

It wasn’t all bad: we were able to fudge something together using compiler-specific intrinsics, and then C++11 arrived. Suddenly everything was fixed by the awesome power of std::enable_if and the type_traits header. Oh, frabjous day!

There was one teensy little problem, though. The code was nearly illegible. Types like this:

Click here to view code image

```
```cpp
std::enable_if<std::is_trivially_constructible<T>::value>::type
```
```

(yes, that’s a type) became scattered throughout the codebase, introducing further cognitive load.

Again, the problem with this TMP technique is that it obfuscates the code and puts the brakes on rapid apprehension of what is going on. Frankly, it looks like transmission noise to me. Yes, with practice, we became able to read it with some ease, but there was a big learning phase for new programmers.