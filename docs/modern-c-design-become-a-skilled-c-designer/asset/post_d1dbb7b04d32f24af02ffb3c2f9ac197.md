
module will consist of one class, an adapter for an underlying stack data structure, let’s design it. One of the first questions to be asked when designing a class is, “How will this class be used?” For example, are you designing an abstract base class to be inherited and thus be used polymorphically? Are you designing a class primarily as a plain old data (POD) repository? Will many different instances of this class exist at any given time? What is the lifetime of any given instance? Who will typically own instances of this class? Will instances be shared? Will this class be used concurrently? By asking these and other similar questions, we uncover the following list of functional requirements for our stack:

- Only one stack should exist in the system.
- The stack’s lifetime is the lifetime of the application.
- Both the UI and the command dispatcher need to access the stack; neither should own the stack.
- Stack access is not concurrent.

Anytime the first three criteria above are met, the class is an excellent candidate for the singleton pattern [6].

## The Singleton Pattern

The singleton pattern is used to create a class where only one instance should ever exist in the system. The singleton class is not owned by any of its consumers, but neither is the single instance of the class a global variable (however, some argue that the singleton pattern is global data in disguise). In order to not rely on the honor system, language mechanics are employed to ensure only a single instantiation can ever exist.

Additionally, in the singleton pattern, the lifetime of the instance is often from the time of first instantiation until program termination. Depending on the implementation, singletons can be created either to be thread safe or suitable for single threaded applications only. An excellent discussion concerning different C++ singleton implementations can be found in

```
class Singleton
{
public:

static Singleton& Instance {
static Singleton instance;
return instance;
}

void foo(){ /* does foo things */ }

private:
// prevent public instantiation, copying,
assignment, movement, // & destruction
Singleton() { /* constructor */ }
Singleton(const Singleton&) = delete;
Singleton& operator=(const Singleton&) =
delete;
Singleton(Singleton&&) = delete;
Singleton&& operator=(Singleton&&) =
delete;
~Singleton() { /* destructor */ }
};
```

The static instance of the Singleton class is

held at function scope instead of class scope to prevent uncontrollable instantiation order conflicts in the event that one singleton class’s constructor depends on another singleton. The details of C++’s instantiation ordering rules are beyond the scope of this book, but a detailed discussion in the context of singletons can be found in Alexandrescu [2].

Note that due to the lack of locking surrounding the access to the one instance, our model singleton is currently only suitable for a single threaded environment. In this age of multicore processors, is such a limitation wise? For pdCalc, absolutely! Our simple calculator has no need for multi-threading. Programming is hard. Multi-threaded programming is much harder. Never turn a simpler design problem into a harder one unless it’s absolutely necessary.

Now that we have the shell of a Singleton class, let’s see how to use it. In order to access the instance and call the foo() function, we simply use the following code:

```
Singleton::Instance().foo();
```

On the first function call to the Instance() function, the instance variable is statically instantiated and a reference to this object is returned. Because objects statically allocated at function scope remain in memory until program termination, the instance object is not destructed at the end of the Instance() function’s scope. On future calls to Instance(), instantiation of the instance variable is skipped (it’s already constructed and in memory from the previous function call), and a reference to the instance variable is simply returned. Note that while the underlying singleton instance is held statically, the foo() function itself is not static.

The inquisitive reader may now question, “Why bother holding an instance of the class at all? Why not instead simply make all data and all functions of the Singleton class static?” The reason is because the singleton pattern allows us to use the Singleton class where instance semantics are required. One particular important usage of these semantics

is in the implementation of callbacks. For example, take Qt’s signals and slots mechanism (you’ll encounter signals and slots in Chapter 6), which can be loosely interpreted as a powerful callback system. In order to connect a signal in one class to a slot in another, we must provide pointers to both class instances. If we had implemented our singleton without a private instantiation of the Singleton class (that is, utilizing only static data and static functions), using our Singleton class with Qt’s signals and slots would be impossible.

## The Stack Module as a Singleton Class

We now possess the basic design for our stack module. We have decided that the entire module will be encapsulated in one class, which essentially acts as an adapter for an STL container. We have decided that our one class fits the model criteria for a singleton, and this singleton class will have the public interface designed in Chapter 2. Combining

each of these design elements gives us the initial declaration for our class, shown in Listing 3-2.

### Listing 3-2. The Stack as a Singleton class

```
Stack
{
class StackImpl;
public:
static Stack& Instance();
void push(double);
double pop();
void getElements(int, vector<double>&) const;
void swapTop();

private:
Stack();
~Stack();
// appropriate blocking of copying, assigning, moving... unique_ptr<StackImpl> pimpl_;
};
```

Because the focus of this book is on design,

the implementation for each member function is not provided in the text unless the details are particularly instructive or highlight a key element of the design. As a reminder, the complete implementation for pdCalc can be downloaded from the GitHub repository. Occasionally, the repository source code will be a more sophisticated variant of the idealized interfaces appearing in the text. This will be the general format for the remainder of this book.

For those readers unfamiliar with the pimpl idiom (placing the implementation of one class in a separate private implementation class), the pimpl member variable will seem very mysterious. Don’t fret. You’ll review this principle in a section below.

Before temporarily departing the discussion of the Stack class’s design, let’s take a brief detour and discuss a relevant implementation detail. We spent a lot of time reviewing the importance of using the adapter pattern in the Stack’s design to hide the underlying data structure. One of the justifications for this

decision was that it offered the ability to seamlessly alter the underlying implementation without impacting classes dependent upon the Stack’s interface. The question is, “Why might the underlying implementation of the Stack change?”

In my first version of the Stack’s implementation, I selected the obvious choice for the underlying data structure, the STL stack. However, I quickly encountered an efficiency problem using the STL stack. Our Stack class’s interface provides a getElements() function that enables the user interface to view the contents of the calculator’s stack. Unfortunately, the STL stack’s interface provides no similar function. The only way to see an element other than the top element of an STL stack is to successively pop the stack until the element of interest is reached. Obviously, because we are only trying to see the elements of the stack and not alter the stack itself, we’ll need to immediately push all the entries back onto the stack. Interestingly enough, for our purposes, the STL stack turns out to be an
