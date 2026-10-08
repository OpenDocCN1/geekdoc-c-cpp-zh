+   4. Why is a constructor used for the Date type instead of an init_day() function?
5. What is an invariant? Give examples.
6. When should functions be put in the class definition, and when should they be defined outside the class? Why?
7. When should operator overloading be used in a program? Give a list of operators that you might want to overload (each with a reason).
8. Why should the public interface to a class be as small as possible?
9. What does adding const to a member function do?
10. Why are “helper functions” best placed outside the class definition?

# Terms

+   built-in types
class
const
constructor
destructor
enum
enumeration

+   enumerator
helper function
implementation
in-class initializer
inlining
interface
invariant

+   representation
struct
structure
user-defined types
valid state

# Exercises

+   1. List sets of plausible operations for the examples of real-world objects in §9.1 (such as toaster).
2. Design and implement a Name_pairs class holding (name,age) pairs where name is a string and age is a double. Represent that as a vector<string> (called name) and a vector<double> (called age) member. Provide an input operation read_names() that reads a series of names. Provide a read_ages() operation that prompts the user for an age for each name. Provide a print() operation that prints out the (name[i],age[i]) pairs (one per line) in the order determined by the name vector. Provide a sort() operation that sorts the name vector in alphabetical order and reorganizes the age vector to match. Implement all “operations” as member functions. Test the class (of course: test early and often).
3. Replace Name_pair::print() with a (global) operator << and define == and != for Name_pairs.
4. Look at the headache-inducing last example of §8.4. Indent it properly and explain the meaning of each construct. Note that the example doesn’t do anything meaningful; it is pure obfuscation.
5. This exercise and the next few require you to design and implement a Book class, such as you can imagine as part of software for a library. Class