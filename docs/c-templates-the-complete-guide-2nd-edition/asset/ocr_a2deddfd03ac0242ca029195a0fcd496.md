```
required
};
```

We could extend this archetype further, using deleted functions³ to also poison the operators && and || to help find problems in other template definitions. Typically, a template implementer will want to develop an archetype for every concept identified in the template library and then use these archetypes to test each template definition against its stated requirements.

# 28.4 Tracers

So far, we have discussed bugs that arise when compiling or linking programs that contain templates. However, the most challenging task of ensuring that a program behaves correctly at run time often follows a successful build. Templates can sometimes make this task a little more difficult because the behavior of generic code represented by a template depends uniquely on the client of that template (certainly much more so than ordinary classes and functions). A tracer is a software device that can alleviate that aspect of debugging by detecting problems in template definitions early in the development cycle.

A tracer is a user-defined class that can be used as an argument for a template to be tested. Often, a tracer is also an archetype, written just to meet the requirements of the template. More important, however, a tracer should generate a trace of the operations that are invoked on it. This allows, for example, to verify experimentally the efficiency of algorithms as well as the sequence of operations.

Here is an example of a tracer that might be used to test a sorting algorithm.⁴

[Click here to view code image](#)

```
debugging/tracer.hpp

#include <iostream>

class SortTracer {
private:
  int value;  // integer value to be sorted
  int generation;  // generation of this tracer
  inline static long n_created = 0; // number of constructor calls
  inline static long n_destroyed = 0; // number of destructor calls
  inline static long n_assigned = 0; // number of assignments
  inline static long n_compared = 0; // number of comparisons
```