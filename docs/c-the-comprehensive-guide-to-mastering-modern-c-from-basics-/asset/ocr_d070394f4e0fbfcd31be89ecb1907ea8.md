```
template<typename T>
auto func(T e) { return e<10; }
```

In both notations, you don't have to worry about the
type of what is in the container, and you don't have to
adjust it if the type changes.

The next step, to actually write your own template
function if appropriate, is then not far off.

The reasons for creating your own template class are
someewhat different than for a function, but here too you\make your code more general and avoid code
duplication. Templates are also very fast; the compiler
often chooses to inline them.

And don't forget that machine code only actually ends
u in the compiled output if the template function or the
element of the template class is actually used
somewhere in the program. This is different from
nontemplate functions, which can indeed end up in the
compiled program (but do not have to), even if they are
not used.

# Use Templates for Containers

If you write a function that sorts a specific vector in a
specific way, you should not pass the vector as a
concrete type. Either make it a template parameter
yourself or use iterators, which is best done via
template parameters.

Do not do it like this: