Here are some plausible macros:

```
#define CASE break;case
```

```
#define FOREVER for(;;)
```

Here are some completely unnecessary macros:

```
#define PI 3.141593
```

```
#define BEGIN {
```

```
#define END }
```

Here are some dangerous macros:

```
#define SQUARE(a) a*a
```

```
#define INCR_xx (xx)++
```

To see why they are dangerous, try expanding this:

```
int xx = 0; // global counter
```

```
void f(int xx)
{
int y = SQUARE(xx+2); // y=xx+2*xx+2; that is,y=xx+(2*xx)+2 INCR_xx; // increments argument xx (not the global xx)
```

If you must use a macro, use the scope resolution operator, ::, when referring to global names (§6.3.4) and enclose occurrences of a macro argument name in parentheses whenever possible. For example:

```
#define MIN(a,b) (((a)<(b))?(a):(b))
```

This handles the simpler syntax problems (which are often caught by compilers), but not the problems with side effects. For example:

```
int x = 1;
int y = 10;
int z = MIN(x++,y++); // x becomes 3; y becomes 11
```

If you must write macros complicated enough to require comments, it is wise to use /* */ comments because old C preprocessors that do not know about // comments are sometimes used as part of C++ tools. For example:

```
#define M2(a) something(a) /* thoughtful comment*/
```

Using macros, you can design your own private language. Even if you prefer this “enhanced language” to plain C++, it will be incomprehensible to most C++ programmers. Furthermore, the preprocessor is a very simple-minded macro processor. When you try to do something nontrivial, you are likely to find it either impossible or unnecessarily hard to do. The auto, constexpr, const, decltype, enum, inline, lambda expressions, namespace, and template mechanisms can be used as better-behaved alternatives to many traditional uses of preprocessor constructs. For example:

```
const int answer = 42;
```

```
template<class T>
inline const T& min(const T& a, const T& b) {
return (a<b)?a:b;
}
```