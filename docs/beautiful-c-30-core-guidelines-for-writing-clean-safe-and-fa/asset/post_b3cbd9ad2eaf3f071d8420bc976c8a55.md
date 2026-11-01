
easily visible to the client engineer. The danger of making them at file scope is less than that of making a using-directive at file scope, but risks still remain.

The fourth is for making using-directives. These are of very limited use: perhaps you are writing a slide for a presentation and you want to signal to the audience that you are using a particular namespace in some example code. For example:

Click here to view code image

```
#include <iostream>
using namespace std;

int main() {
    cout << "Hello, world!";
    return 0;
}
```

Rather than type std::cout, you are relying on the introduction of all symbols from the std namespace so far declared in the <iostream> header. It is very convenient.

Very, very convenient.

This is a very simple use of a using-directive, suitable for trivial code. In more complicated code surprising things happen, because a using-directive does not only introduce the new symbols into the current scope.

We’ll just say that again: a using-directive does not only introduce new symbols into the current scope. It does something rather more surprising, and we need to cover a little graph theory to work out what’s going on.

## Where do the symbols go?

First, we need to look at the idea of a directed acyclic graph, or DAG, a term coined by Bjarne Stroustrup’s office mate, Al Aho. A graph is a set of nodes with relationships between them. A directed graph is a set of nodes with relationships between them that only operate in one direction. For example, a class hierarchy is a graph with is-child-of and is-parent-of relationships between classes, which are the nodes. These relationships follow different directions. If we take out the is-child-of relationships, we have a directed graph because the relationships work in one direction only. An acyclic graph has an entry and an exit; there is no way to end up back where you started by following the relationships. A class hierarchy of parent relationships is not only directed, but also acyclic.

The same thing can be said of namespaces and containment relationships. A namespace can nest another namespace, but the graph of nesting is a DAG. For example:

Click here to view code image

```
namespace World {
    namespace Buildings {
        namespace Municipal {}
        namespace Business {}
    }
}
```

We can go from World to Municipal by examining nested namespaces, but we can’t go from Municipal to World in the same way.

Second, we need to look at the lowest common ancestor (LCA). The LCA of a pair of nodes is the deepest node common to both. In the above namespace example, both namespace World and namespace World::Buildings are common ancestors of namespace World::Buildings::Municipal and namespace World::Buildings::Business, but namespace World::Buildings is the LCA.

You should now be comfortable with the idea of a DAG and an LCA, so let’s examine exactly what a using-directive does. This is covered over three pages of the standard at [namespace.udir.]² To summarize, a using-directive introduces its new meanings into the scope which is the LCA of the current scope and the target namespace’s own scope. This can be quite surprising and becomes more surprising as a codebase grows and acquires more namespaces. Let’s try out a real-world example using the above namespace hierarchy.

First of all, using namespace Municipal injects int signal_result (Result::DecisiveVictory) into the LCA of Municipal and Business. Remember that this hides previous meanings of signal_result. Can you identify what this has hidden?

It has hidden gdg::signal_result and World::signal_result. Keep that in mind.

The next using-directive introduces gdg::signal_result into the global namespace. This is the LCA of namespace gdg and namespace Business. However, that itself has been hidden by World::signal_result, which has itself been hidden by Municipal::signal_result. So which signal_result is invoked at the end of the test function?

Municipal::signal_result is the only available choice. Even though it takes a DecisiveVictory rather than a CrushingVictory, it is the best fit, being the only fit.

Did you follow that, answer the questions correctly and deduce the correct function?

Now, I appreciate that this might seem contrived and overly complicated. However, this is not too dissimilar from a real-world example that utterly defeated me for the best part of a week. I have taken out all the extraneous furniture that was nothing to do with the bug to aid exposition. Imagine this code spread over a few thousand lines through a handful of source files. Imagine this code manifesting by silently recording the wrong kind of victory that was not too far from the right kind of victory. Imagine thinking that this bug is unrelated to the quality of the victory, but to the way that the details of the victory are passed to the rest of the system. Why on earth would you think that CrushingVictory would not be recorded? There it is, right there in the code. The solution only came to me when I was stepping through the code and suddenly realized that I had gone to the wrong place. I blamed the debugger and spent far too long arguing about optimizers with anyone who would listen. Perhaps a COMDAT had been incorrectly folded. But no, the error was that I didn’t understand how using-directives worked.

## An altogether more insidious problem

Perhaps you remain unconvinced. Perhaps you work on small projects and you do not nest your namespaces. There is yet another trap you can fall into. Consider this snippet of code from 2005:

Click here to view code image

```
// numerical_maths.h
namespace maths {
    float clamp(float v, float max, float min);
}
using namespace maths;
```

```
// results.cpp
#include "numerical_maths.h"
#include <algorithm>
using namespace std;
```

results.cpp contained quite a lot of calls like this:

```
int x = clamp(12, 6, 4);
```

Even though there was no overload that took int rather than float, the existing function was a suitable candidate since int can convert to float, albeit with loss of precision at higher magnitudes. Technically, this was a bug, but it failed to manifest in any code since the values were always reasonably small.

Something important happened in 2017: the function clamp was added to the std namespace. As a result, results.cpp contained an additional overload for clamp. Unfortunately, being a function template, it was a superior choice to maths::clamp() if the parameters were all of type int, since it required no parameter conversions. Fortunately, it did the same thing as maths::clamp(). Unfortunately, it took the max and min parameters in the reverse order. Fortunately, the implementation would warn you if the max parameter was less than the min parameter. Unfortunately, we disabled all the furniture that emitted this warning because it made debugging awfully slow.

As a result, weird and subtle bugs started appearing. Incorrect clamping results would propagate to unexpected parts of the code that were not necessarily catastrophic but did not properly match with the intention. Nor was this limited to results.cpp: clamp was a widely used function. Fortunately, there was plenty of time to fix all the bugs and a huge sigh of relief was heaved by all at the end of that debacle.

Actually, that last sentence is not true.

It was not a happy time, and it wasn’t until someone was browsing through cppreference.com that they learned of the introduction of std::clamp, noticed that the order of parameters was different, and felt a terrible realization swamping their attention. With several thousand uses of clamp scattered through the codebase, a frustrating, detailed search through the codebase was required to ensure that the intended clamp was being called, and that the engineer had got their parameters the right way round.

Simply moving the using-directive out of the header file and into each source file where it was included would not have been enough: the same problem would have arisen, although at least the presence of a namespace would have advertised another source of symbols. Nor would making a using-declaration at the top of each source file have been sufficient either, since there were some places where the engineer had written code subsequent to the C++17 upgrade, inadvertently inverted the parameters, but invoked the std::clamp function rather than the maths::clamp function. Each of those uses would have been invalidated.

The only defenses against this horror in the first instance were to make a using-declaration, not a using-directive, in the source file, ideally at the narrowest scope, or to fully qualify uses of clamp. When you put a using-directive in your source, you are exposing yourself to the risk of the silent introduction of new meanings to your symbols in other namespaces at inopportune moments. If you are lucky, you will get an “ambiguous symbol” compiler error. At worst, a superior overload will appear with subtle differences to the choice you were expecting.

We invite you to review the first part of this chapter.
