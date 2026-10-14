+   - Mixing up the units of values in calculations can have serious consequences; see “When NASA Lost a Spacecraft Due to a Metric Math Mistake” by Ajay Harish: https://www.simscale.com/blog/2017/12/nasa-mars-climate-orbiter-metric/.
+   - Kevlin Henney’s book 97 Things Every Programmer Should Know (O’Reilly, 2010) has lots of good advice on this general subject and many others. Representing domain concepts in the code is nicely captured by Dan North in Chapter 11, and by Einar Landre in Chapter 65.
+   - Henney also looks at Value Object, Whole Value, Class Factory Method, and other patterns for values in “Patterns in Java,” which applies equally well to C#: https://www.slideshare.net/Kevlin/value-added-43542768. Also see his paper “Factory and Disposal Methods: A Complementary and Symmetric Pair of Patterns,” from the 2003 VikingPLoP (Pattern Languages of Programs) conference, at https://www.researchgate.net/publication/238075361.
+   - It has long been recognized that keeping objects simple helps in creating programs that are understandable. The single responsibility principle—the S in SOLID—is perhaps the most well-known guidance on this: https://en.wikipedia.org/wiki/SOLID.
+   - However, the benefits of separate responsibilities were recognized in the 1970s, if not earlier, when Edsger Dijkstra wrote about separating concerns:
+     - “The Effective Arrangement of Logical Systems,” https://www.cs.utexas.edu/users/EWD/transcriptions/EWD05xx/EWD562.html
+     - “On the Role of Scientific Thought,” https://www.cs.utexas.edu/users/EWD/transcriptions/EWD04xx/EWD447.html

# Chapter 2

+   - The Common Type System is summarized in the following Microsoft documentation:
+     - https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/types/#the-common-type-system
+     - https://docs.microsoft.com/en-us/dotnet/standard/base-types/common-type-system
+   - The Microsoft documentation for the language rules around struct types is at https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/language-specification/structs.
+   - More information on the behavior of System.Threading.Monitor with respect to lock objects can be found at https://docs.microsoft.com/en-us/dotnet/api/system.threading.monitor?view=net-6.0#Lock.
+   - The specific overload resolution rules regarding optional parameters are explained at https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/named-and-optional-arguments#overload-resolution.