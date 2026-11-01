encapsulating and data hiding: it allows us to create levels of complexity and expose only the bare minimum required to interact with an object.

In Chapter 2.2 we looked at how arguments increase in number, and observed that this could be down to a missing abstraction. The complexity of comprehending many parameters is hidden behind the abstraction that describes the role those parameters play.

> *Abstraction localizes and minimizes complexity.*

In Chapter 4.1 we carried out a similar transformation and collected together a messy bunch of data into a single abstraction, returning that rather than taking multiple out parameters.

The Core Guidelines are explicitly motivated by abstraction in some cases. In C.8: “Use class rather than struct if any member is non-public,” the reason for so doing is to make it clear that something is being abstracted. Since class members are private by default, a class signals to you that there are things that you do not need to see.

In Core Guideline ES.1: “Prefer the standard library to other libraries and to ‘handcrafted code,’” it is observed that library code tends to be of a higher level of abstraction. As I remarked earlier, I have participated in code reviews where the engineer simply rewrote std::rotate or std::mismatch without realizing it, and did a worse job.

In Core Guideline ES.2: “Prefer suitable abstractions to direct use of language features,” the use of abstraction is explicit in the title. This guideline demonstrates that application concepts are further from the bare language than they are from appropriate combinations of library features.

Even the term “abstract base class” describes an entity that hides complexity by only exposing a public API, insulating the client from the implementation details. Abstraction is fundamental to developing software in C++.

When a guideline violation seems unavoidable, facilities exist to minimize and hide the violation. One of the driving principles of C++ is zero-cost abstraction, so make use of that to maximize the clarity and comprehensibility of your code.