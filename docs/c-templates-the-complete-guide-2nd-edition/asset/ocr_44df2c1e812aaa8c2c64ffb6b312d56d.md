Section 21.4 on page 512 describes a technique that allows us to provide a nondefault template argument for a specific parameter without having to specify other template arguments for which a default value is available. Although it is an interesting technique, it is also clear that it results in a fair amount of work for a relatively simple effect. Hence, providing a language mechanism to name template arguments is a natural thought.

We should note at this point that a similar extension (sometimes called *keyword arguments*) was proposed earlier in the C++ standardization process by Roland Hartinger (see Section 6.5.1 of [*StroustrupDnE*]). Although technically sound, the proposal was ultimately not accepted into the language for various reasons. At this point there is no reason to believe named template arguments will ever make it into the language, but the topic arises regularly in committee discussions.

However, for the sake of completeness, we mention one syntactic idea that has been discussed: [Click here to view code image](#).

```
template<typename T,
typename Move = defaultMove<T>,
typename Copy = defaultCopy<T>,
typename Swap = defaultSwap<T>,
typename Init = defaultInit<T>,
typename Kill = defaultKill<T>>
class Mutator {
…
};

void test(MatrixList ml)
{
mySort (ml, Mutator <Matrix, .Swap = matrixSwap>);
}
```

Here, the period preceding the argument name is used to indicate that we’re referring to a template argument by name. This syntax is similar to the “designated initializer” syntax introduced in the 1999 C standard: [Click here to view code image](#).

```
struct Rectangle { int top, left, width, height; };
struct Rectangle r = { .width = 10, .height = 10, .top = 0, .left = 0 };
```

Of course, introducing named template arguments means that the template parameter names of a template are now part of the public interface to that template and cannot be freely changed. This could be addressed by a more explicit, opt-in syntax, such as the following: [Click here to view code image](#).

```
template<typename T,
Move: typename M = defaultMove<T>,
Copy: typename C = defaultCopy<T>,
```