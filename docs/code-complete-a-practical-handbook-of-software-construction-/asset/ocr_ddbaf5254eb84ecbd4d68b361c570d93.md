# Member Functions and Data

> **Cross-Reference** For more discussion of routines in general, see Chapter 7, “High-Quality Routines.”

Here are a few guidelines for implementing member functions and member data effectively.

**Keep the number of routines in a class as small as possible** A study of C++ programs found that higher numbers of routines per class were associated with higher fault rates (Basili, Briand, and Melo 1996). However, other competing factors were found to be more significant, including deep inheritance trees, large number of routines called within a class, and strong coupling between classes. Evaluate the tradeoff between minimizing the number of routines and these other factors.

**Disallow implicitly generated member functions and operators you don’t want** Sometimes you’ll find that you want to disallow certain functions—perhaps you want to disallow assignment, or you don’t want to allow an object to be constructed. You might think that, since the compiler generates operators automatically, you’re stuck allowing access. But in such cases you can disallow those uses by declaring the constructor, assignment operator, or other function or operator *private*, which will prevent clients from accessing it. (Making the constructor private is a standard technique for defining a singleton class, which is discussed later in this chapter.)

**Minimize the number of different routines called by a class** One study found that the number of faults in a class was statistically correlated with the total number of routines that were called from within a class (Basili, Briand, and Melo 1996). The same study found that the more classes a class used, the higher its fault rate tended to be. These concepts are sometimes called “fan out.”

> **Further Reading** Good accounts of the Law of Demeter can be found in *Pragmatic Programmer* (Hunt and Thomas 2000), *Applying UML and Patterns* (Larman 2001), and *Fundamentals of Object-Oriented Design in UML* (Page-Jones 2000).

**Minimize indirect routine calls to other classes** Direct connections are hazardous enough. Indirect connections—such as *account.ContactPerson().DaytimeContact-Info().PhoneNumber()*—tend to be even more hazardous. Researchers have formulated a rule called the “Law of Demeter” (Lieberherr and Holland 1989), which essentially states that Object A can call any of its own routines. If Object A instantiates an Object B, it can call any of Object B’s routines. But it should avoid calling routines on objects provided by Object B. In the *account* example above, that means *account.ContactPerson()* is OK but *account.ContactPerson().DaytimeContactInfo()* is not.

This is a simplified explanation. See the additional resources at the end of this chapter for more details.

+   **In general, minimize the extent to which a class collaborates with other classes** Try to minimize all of the following:
+   
+   - Number of kinds of objects instantiated
+   - Number of different direct routine calls on instantiated objects
+   - Number of routine calls on objects returned by other instantiated objects