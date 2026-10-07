class SingingWaiter : public Waiter, public Singer {...};

Note that you must qualify each base class with the keyword public. That's because the compiler assumes private derivation unless instructed otherwise:

class SingingWaiter : public Waiter, Singer {...}; // Singer is a private base

As discussed earlier in this chapter, private and protected MI can express a has-a relation; the student i implementation of the Student class is an example. We'll concentrate on public inheritance now.

MI can introduce new problems for programmers. The two chief problems are inheriting different methods with the same name from two base classes and inheriting multiple instances of a class via two or more related base classes. Solving these problems involves introducing a few new rules and syntax variations. Thus, MI can be more difficult and problem-prone than using single inheritance. For this reason, many in the C++ community object strongly to MI; some want it removed from the language. Others suggest MI and argue it's very useful, even necessary, for particular projects. Still others suggest MI cautiously and in moderation.

Let's explore a particular example and see what the problems and solutions are You need several classes to create an MI situation. For this example, we define an abstract Worker base class and derive a Waiter class and a Singer class from it. Then we can use MI to derive a SingingWaiter class from the Waiter and Singer classes (see Figure 14.3). This is a case in which a base class (Worker) is inherited via two separate derivations, which is the circumstance that causes the most difficulties with MI.We start with declarations for the Worker, Waiter, and Singer classes, as shown in Listing 14.7.

![](bbox=[0.268, 0.566, 0.732, 0.806])

Figure 14.3 MI with a shared ancestor.