Q: Why does C++ have both structures and classes?
A: So that C++ retains backward compatibly with C.

Q: When should I use structures?
A: Some game programmers use structures to group only data together, without functions (because that's how C structures work). But it's probably best to avoid structures whenever possible and use classes instead.

# Discussion Questions

+   1. What are the advantages and disadvantages of procedural programming?
+   2. What are the advantages and disadvantages of object-oriented programming?
+   3. Are accessor member functions a sign of poor class design? Explain.
+   4. How are constant member functions helpful to a game programmer?
+   5. When is it a good idea to calculate an object's attribute on the fly rather than storing it as a data member?

# Exercises

+   1. Improve the Critter Caretaker program so that you can enter an unlisted menu choice that reveals the exact values of the critter's hunger and boredom levels.
+   2. Change the Critter Caretaker program so that the critter is more expressive about its needs by hinting at how hungry and bored it is.
+   3. What design problem does the following program have?

```
#include <iostream>
using namespace std;

class Critter
{
public:
    int GetHunger() const { return m_Hunger; }
```