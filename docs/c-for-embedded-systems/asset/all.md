![](cover.jpeg)

![](images/00001.jpeg)

Table of Contents

[Introduction.                            3](#part0000_split_002.html___RefHeading__2313_977618933)

[Acknowledgements.                            4](#part0000_split_003.html___RefHeading__18198_1974188664)

[C++ code style.                            5](#part0000_split_004.html___RefHeading__13919_1660174531)

[Software primitives.                            5](#part0000_split_005.html___RefHeading__2315_977618933)

[Mutual exclusion.                            5](#part0000_split_005.html___RefHeading__10716_42486590)

[Parallel execution.                            14](#part0000_split_014.html___RefHeading__14882_1513893511)

[Containers.                            19](#part0000_split_019.html___RefHeading__2317_977618933)

[C++ templates.                            41](#part0000_split_041.html___RefHeading__2646_977618933)

[Memory management.                            50](#part0000_split_050.html___RefHeading__2948_1515059145)

[Operator new.                            74](#part0000_split_074.html___RefHeading__12039_1005710029)

[I/O access.                            77](#part0000_split_077.html___RefHeading__12421_1005710029)

[I/O access in C.                            79](#part0000_split_079.html___RefHeading__8080_1329019087)

[I/O access in C++.                            87](#part0000_split_087.html___RefHeading__8082_1329019087)

[Indirect I/O access.                            99](#part0000_split_099.html___RefHeading__11237_696237465)

[Code ROM and data RAM.                            103](#part0000_split_103.html___RefHeading__7726_2007975351)

[C++ Initialized data.                            104](#part0000_split_104.html___RefHeading__7728_2007975351)

[ROM patching.                            106](#part0000_split_106.html___RefHeading__7954_2007975351)

[Composition.                            109](#part0000_split_109.html___RefHeading__12357_1195782936)

[Static (class) member.                            110](#part0000_split_110.html___RefHeading__13575_1195782936)

[Non static member.                            119](#part0000_split_119.html___RefHeading__13577_1195782936)

[Interprocess communication.                            122](#part0000_split_122.html___RefHeading__16996_386140696)

[Log.                            133](#part0000_split_133.html___RefHeading__14433_1195782936)

[Software Timers.                            154](#part0000_split_154.html___RefHeading__14278_363426044)

[Lambda.                            182](#part0000_split_181.html___RefHeading__18748_1024792740)

[Fixed point arithmetic.                            187](#part0000_split_186.html___RefHeading__17941_1564319060)

[Interview questions.                            191](#part0000_split_190.html___RefHeading__18647_840412327)

[General programming.                            191](#part0000_split_191.html___RefHeading__30871_840412327)

[Bit tricks.                            205](#part0000_split_203.html___RefHeading__30873_840412327)

[Popular online tests.                            208](#part0000_split_204.html___RefHeading__21930_636559633)

[Brain teasers.                            230](#part0000_split_226.html___RefHeading__30875_840412327)

[Conclusion.                            232](#part0000_split_227.html___RefHeading__18119_1290114)

[Bibliography.                            233](#part0000_split_228.html___RefHeading__22224_1055311978)

# Introduction.

I've come to the conclusion that any programmer that would prefer the project to be in C++ over C is likely a programmer that I really would prefer to piss off, so that he doesn't come and screw up any project I'm involved with.

Linus Torvalds

This book is intended for firmware developers who mainly use the C language. I assume that the reader is comfortable with ARM or Intel assembly language and has working knowledge of the C++ syntax. In this book, I have tried to give examples of C++ code in situations where, arguably, C is not the perfect tool for the task. Many C++ code examples come with snippets of the resulting assembly. The examples of code have been constructed in a way that allows immediate reuse in real-world applications. Examples cover topics such as memory and speed optimization, organizing arrays, FIFOs, thread safety, and direct access to the hardware. The book addresses issues such as code bloat and the hidden performance costs of C++.

In all examples I assume that the C++ compiler supports version 11 of the language. One example of such a compiler is GNUC 4.8\. The availability of a C++ compiler supporting version 11 for specific hardware is not required, and most code examples can be rewritten for older C++ compilers. Throughout the book, I have demonstrated some of the lesser known features of the C++11 standard, such as type traits, static assertion, constant expressions and OpenMP support.

Problem can be solved in numerous ways. Where it was possible and made sense, I provided an alternative implementation in C and compared the performance of the C and C++ solutions.

# Acknowledgements.

I would like to thank my cousin and friend Andre Bar'yudin. Without Andre's help and contributions this book would have been much poorer. I think that between two of us this is Andre who knows C++.

# C++ code style.

#define AND  &&

#define OR   ||

#define EQ   ==

I have done my best to follow consistent C/C++ code style in all source code examples. In this book I have not placed curly brackets on a separate line. Please, do not send me hate mail. The only reason is to make the code snippets shorter. Shorter code has a better chance of fitting in the smaller e-reader displays. There are no comments in the code itself for the same reason. Hopefully, the lack of comments has been compensated for by the interspersed explanations. I am using the camelcase name convention. Types and class names begin with uppercase and variables begin with lower case, while constants are all upper case with the underscore delimiter.

# Software primitives.

## Mutual exclusion.

The great thing about Object Oriented code is that it can make small, simple problems look like large, complex ones.

In the multi-task environment, threads and interrupts can concurrently read and write data objects. I can use different tools to synchronize access to the data between different contexts and create thread safe APIs. Among the available tools are semaphores and mutual exclusion APIs provided by operating systems, as well as disabling all interrupts, disabling some interrupts, disabling the operating system scheduler, and using spin locks. When I write a wrapper around an API provided by my real-time operating system or by the hardware, I want the wrapper to be as thin as possible. Usually, I measure the overhead of the wrapper using a number of assembly instructions. The number of instructions provides a good approximation of the CPU cycles or execution time.

I am starting with a code snippet that creates and calls a dummy lock object.

class LockDummy {

public:

    LockDummy() {

cout << "Locked context" << endl;

    }

    ~LockDummy() {

cout << "Lock is freed" << endl;

    }

};

In the following usage example the C++ specifier “auto” tells to the compiler to automatically supply the correct type – the C++11 compiler knows to deduct certain types of variables in some situations. For example, the C++ compiler can figure out the return type of the left side of an assignment or the return type of a function.

In the function main() compiler will call the output function two times and will not add any other code. The lock is released – the destructor ~LockDummy gets called – when the scope of the variable myDummyLock ends. The scope could be a while loop. I do not have to call “unlock” before each and every return from the function. The C++ compiler makes sure that the destructor is always called and called exactly once (see more about RAII in [1]). This convenient service comes without any performance overhead. The output of the following code is going to be

Locked context

Protected context

Lock is freed

int  testDummyLock() {

#if (__cplusplus >= 201103) // use "auto" if C++11 or better

 auto myDummyLock = LockDummySimple();

#else

    LockDummySimple myDummyLock = LockDummySimple();

#endif

cout << "Protected context" << endl;

 return 0;

}

I want to stress this idea using another example. In the following code, I set a scope around the declaration of the lock variable. The output of the code is going to be

Locked context

Protected context

Lock is freed

End of main

int main() {

    {

        LockDummy lock;

cout << "Protected context" << endl;

    }

cout << "End of main" << endl;

 return 0;

}

My second lock is a more realistic one, and it disables a hardware interrupt. I assume that there is an API that disables and enables an interrupt. I am refactoring the original lock code a little bit. First of all, I use a template, which is a feature of C++ that allows you to declare a class that operates with generic types. I am going to reuse the code in the template Lock for different synchronization objects. The code in the template Lock can manipulate any structure or class that implements two public methods: static methods get() and release(). I carefully avoid polymorphism here, I do not require synchronization objects to belong to the same hierarchy of classes. The wrapper around the disable/enable interrupts API, which likely writes to the hardware, is not going to be a child/friend/parent/relative/derivation of a wrapper for the operating system semaphore.

This is what the API that disables and enables interrupts looks like:

static  inline  void  interruptDisable(void) {

cout << "Disable" << endl;

}

static  inline  void  interruptEnable(void) {

cout << "Enable" << endl;

}

I am describing a synchronization object. The class implements two methods: “get” and “release”. Both methods are “inline”, which helps the optimizer to decide if calls to the methods should be substituted by the methods code. The end result is going to be similar to using a macro definition in C. The default constructor in the class SynchroObject is private, I do not want any objects of this type in the application. My C++ compiler so far has not added any object code to my executable file.

class  SynchroObject {

 SynchroObject() {};

public:

 static  inline  void  get() {

        interruptDisable();

    }

 static  inline  void  release() {

        interruptEnable();

    }

};

The template class Lock can manipulate any type of synchronization objects that provides a get/release API. All methods of the template class Lock are “inline”. The C++ compiler is not going to add any functions to the object code, but will rather replace the calls to the Lock methods with the code of the get/release from the synchronization object.

template<typename  Mutex> class  Lock {

public:

 inline  Lock() {

 Mutex::get();

    }

 inline  ~Lock() {

 Mutex::release();

    }

};

Declare a new type MyLock that uses my SynchroObject to disable/enable interrupts. There is still no additional data or code in my executable except for the calls to the interrupt enable and interrupt disable API.

typedef  Lock<SynchroObject> MyLock;

Output of the function main() is going to be two words: Disable, Enable

int  main() {

    {

 MyLock lock;

    }

 return 0;

}

Overhead of the wrapper around the functions that disable and enable interrupts is exactly zero. Indeed,  if I check the disassembly, I will see two calls to the print function in the main routine and nothing else. I have written some C++ code which gets optimized to nothing. What did I gain? What is an added value?

The code does not allow me to leave out enable interrupts after I called disable interrupt. No matter how many return points or breaks out of a loop my function has, the C++ compiler ensures that the function interruptEnable is called exactly once.

## Parallel execution.

Some people, when confronted with a problem, think, 'I know, I'll use threads' – and then two they hav erpoblems.

I have a quad core CPU in my system. Compiler GCC 4.8 is available for my hardware. If I compile the code below with the compilation flag -fopenmp I will get the output “4”:

void  testReduction(void) {

 int a = 0;

 #pragma omp parallel reduction (+:a)

    {

      a = 1;

    }

cout << a << endl;

}

Without the flag -fopenmp the output will be “1”. When the C++ compiler encounters pragma “omp parallel”, it adds a chunk of code which spawns a “team” of threads (in Linux POSIX pthreads) according to the number of cores in the system. The following section is executed by the group of threads in parallel.

Execution of the following function on my system requires ~0.179s with OpenMP and ~0.322s without OpenMP:

volatile  uint_fast8_t myArray[(size_t)512*1024*1024];

uint_fast32_t  testOpenMPLoop() {

 uint_fast32_t sum = 0;

 #pragma omp parallel for reduction(+:sum)

 for (uint64_t i=0; i < sizeof(myArray); i++)

    {

        sum += myArray[i];

    }

 return sum;

}

If the array size is under 10M entries the OpenMP overhead kicks in and the multi-thread version of the loop requires more time than the single thread version. OpenMP implementation in the GCC compiler, GOMP library, calls malloc() from the C standard library to allocate pthread threads.

My next synchronization object is based on the OpenMP lock.

I restrict the instantiation of the class to one object. There is going to be only one instance of the class SynchroObjectOmpLock. This design pattern is called “singleton” ([2]):

class  SynchroObjectOmpLock {

public:

 static  inline  void  get();

 static  inline  void  release();

 ~SynchroObjectOmpLock();

protected:

 omp_lock_t  lock;

 static  SynchroObjectOmpLock *instance;

 inline  SynchroObjectOmpLock();

};

SynchroObjectOmpLock *SynchroObjectOmpLock::instance

= new  SynchroObjectOmpLock();

The rest of the class methods:

void  SynchroObjectOmpLock::get() {

 omp_set_lock(&instance->lock);

}

void  SynchroObjectOmpLock::release() {

 omp_unset_lock(&instance->lock);

}

SynchroObjectOmpLock::SynchroObjectOmpLock() {

 omp_init_lock(&lock);

}

SynchroObjectOmpLock::~SynchroObjectOmpLock() {

 omp_destroy_lock(&instance->lock);

}

I have a new type – a lock which is based on the OpenMP synchronization object:

typedef  Lock<SynchroObjectOmpLock> LockOmp;

And usage example:

    {

 LockOmp lock;

    }

## Containers.

When your hammer is C++, everything begins to look like a thumb.

Standard template library (STL) contains a lot of smart and very convenient code dealing with vectors, stacks, queues, hash tables, trees, and many other types of dynamic and static data storage. Unfortunately, a firmware developer often needs something different. There are cases when high performance and small code/data footprint should coexist in one application. In this chapter I will demonstrate a container which makes sense in an embedded system with limited resources. The API should be reentrant and allow safe concurrent access. The performance of the container is going to be at least not worse than an alternative implementation in the C language. All memory allocations are going to be static and done at build time – I will deal with the dynamic allocations later in this book.

### Cyclic buffer.

Asking from C++ programmers more content, less bloat is unfair.

My first example is going to be a cyclic buffer, which is also known as a ring buffer. A “producer” adds objects to the “tail” of the cyclic buffer and a “consumer” pulls the objects from the “head” of the cyclic buffer. An example of producer can be an interrupt routine which gets characters from an UART device (RS232 port). A “consumer” is a function called from the application main loop which handles commands arriving from the UART. The CyclicBuffer class is a template class, which should help the optimizer to generate the most efficient code possible for the given integer type and the CPU architecture.

template<typename  ObjectType, typename  Lock, std::size_t  Size>

class  CyclicBufferSimple {

public:

 CyclicBufferSimple();

 ~CyclicBufferSimple() {}

 inline  bool  add(const  ObjectType object);

 inline  bool  remove(ObjectType &object);

 inline  bool  isEmpty();

 inline  bool  isFull();

private:

 inline  size_t  increment(size_t index);

 inline  void  errorOverflow() {}

 inline  void  errorUnderflow() {}

 ObjectType  data[Size + 1];

 size_t  head;

 size_t  tail;

};

The CyclicBufferSimple constructor will fail the build if the application attempts to store in the buffer anything but integer. Storage for the objects larger than the size of the integer on the given CPU architecture should probably have a different API.

template<typename  ObjectType, typename  Lock, std::size_t  Size>

CyclicBufferSimple<ObjectType, Lock, Size>::CyclicBufferSimple() {

#if (__cplusplus >= 201103)

 static_assert(std::numeric_limits<ObjectType>::is_integer, "CyclicBuffer is intended to work only with integer types");

#elif defined(__GNUC____)

 __attribute__((unused)) ObjectType val1 = 1;

#else

 volatile ObjectType val1;

    *(&val1) = 1;

#endif

 this->head = 0;

 this->tail = 0;

}

There are two methods returning the buffer state:

template<typename  ObjectType, typename  Lock, std::size_t  Size>

inline  bool  CyclicBufferSimple<ObjectType, Lock, Size>::isEmpty() {

 bool res = (this->head == this->tail);

 return res;

}

template<typename  ObjectType, typename  Lock, std::size_t  Size>

inline  bool  CyclicBufferSimple<ObjectType, Lock, Size>::isFull() {

 size_t tail = increment(this->tail);

 bool res = (this->head == tail);

 return res;

}

A method handling wrap around of the buffer index:

template<typename  ObjectType, typename  Lock, std::size_t  Size>

inline  size_t  CyclicBufferSimple<ObjectType, Lock, Size>::increment(size_t index) {

 if (index < Size) {

 return (index + 1);

} else {

 return 0;

    }

}

Add/remove API of the cyclic buffer:

template<typename  ObjectType, typename  Lock, std::size_t  Size>

inline  bool  CyclicBufferSimple<ObjectType, Lock, Size>::add(const  ObjectType object) {

 Lock lock;

 if (!isFull()) {

 data[this->tail] = object;

 this->tail = increment(this->tail);

 return  true;

} else {

        errorOverflow();

 return  false;

    }

}

template<typename  ObjectType, typename  Lock, std::size_t  Size>

inline  bool  CyclicBufferSimple<ObjectType, Lock, Size>::remove(ObjectType &object) {

 Lock lock;

 if (!isEmpty()) {

object = data[this->head];

 this->head = this->increment(this->head);

 return  true;

} else {

        errorUnderflow();

 return  false;

    }

}

Instantiate a new type – a lock which does nothing:

typedef  Lock<SynchroObjectDummy> LockDummy;

The following function returns a number of the elements in the cyclic buffer. Compiler will fail if the value can not be calculated at the build time:

constexpr  size_t  calculateCyclicBufferSize() {

 return 10;

}

I create an object of class CyclicBuffer dealing with unsigned 8 bits integers. I use uint_fast8_t, which is yet another C++11 marvel targeting portability. Type uint_fast8_t allows the C++ compiler to choose best performing integer that has at least 8 bits. Operations with 32 bits integers can be faster on some CPUs than 8 bits operations. If the performance is more important than memory allocated by the storage, it makes sense to choose 32 bits integer instead of 8 bits. The smallest possible 8 bits unsigned integer is uint_least8_t, and the maximum unsigned integer available on the platform is uintmax_t.

static  CyclicBufferSimple<uint_fast8_t, LockDummy, calculateCyclicBufferSize()> myCyclicBuffer;

In the usage example there is a range loop from the C++11 standard. The main function will print numbers 1, 3, 11

int  main() {

 for (int i : { 1, 3, 11 }) {

        myCyclicBuffer.add(i);

    }

 uint8_t val;

 while (myCyclicBuffer.remove(val)) {

        cout << (int) val << endl;

    }

 return 0;

}

Let's examine the assembly generated by the GNUC compiler for the Intel CPU for a single call to the method add().

xor %esi,%esi

 inline  void add(const ObjectType object) {

mov 0x2009c0(%rip),%rax

 return (index + 1);

mov %rsi,%r8

...............................................

 inline  void add(const ObjectType object) {

mov %rcx,%rdx

cmovbe %rdi,%r8

 if (!isFull()) {

cmp %r8,%rax

...............................................

          data[this->tail] = object;

movb $0x0,0x6011a0(%rcx)

 return (index + 1);

mov %r8,%rdx

 this->tail = increment(this->tail);

mov %r8,0x2009a0(%rip)

I see a couple of move instructions which update the tail, update of the data in the cyclic buffer, a comparison when the tail is incremented. There are 9 opcodes total. There is no unexpected overhead in this code.

I coded one cyclic buffer implementation, but I gained four different cyclic buffers optimized for four different integer types, equally efficient when working with 8, 16, 32, 64 bits integers on different CPUs. Class CyclicBuffer encapsulates the data in the private region. The private data is accessible only via the class methods and this is supposed to be a good thing.

I could pointers instead of the index in the array ([3]), like this:

template<typename  ObjectType, typename  Lock, std::size_t  Size> class  CyclicBufferFast {

…..............................

 ObjectType *head;

 ObjectType *tail;

};

For example, the class constructor could be:

template<typename  ObjectType, typename  Lock, std::size_t  Size>

inline  CyclicBufferFast<ObjectType, Lock, Size>::

CyclicBufferFast() {

 this->head = &data[0];

 this->tail = &data[0];

}

The increment method:

template<typename  ObjectType, typename  Lock, std::size_t  Size>

ObjectType *CyclicBufferFast<ObjectType, Lock, Size>::

increment(ObjectType *entry) {

 if (entry < &data[Size]) {

 return (entry + 1);

} else {

 return &data[0];

    }

}

On my Intel desktop both versions of the cyclic buffer have similar performance. It is rather possible that for some CPUs the C++ compiler generates better optimized code for the “fast” version. The STL iterator in the class “array” accesses the data via a pointer.

### Cyclic buffer – C alternative.

/**

* Returns true

*/

int compare(int C)

{

    return (C > C++);

}

The following C implementation of the cyclic buffer is type safe. The C implementation contains approximately the same number of source code lines: ~80 lines in C vs ~90 lines in C++.

#undef CYCLIC_BUFFRE_SIZE

#define CYCLIC_BUFFRE_SIZE 10

#undef CYCLIC_BUFFER_OBJECT_TYPE

#define CYCLIC_BUFFER_OBJECT_TYPE uint8_t

#define CYCLIC_BUFFRE_DECLARE(ObjectType, Size) \

 typedef  struct { \

        ObjectType data[Size+1]; \

        size_t head; \

        size_t tail; \

    } CyclicBuffer;\

CYCLIC_BUFFRE_DECLARE(CYCLIC_BUFFER_OBJECT_TYPE, CYCLIC_BUFFRE_SIZE);

CyclicBuffer myCyclicBuffer;

static  inline  size_t  CyclicBufferIncrement(size_t index, size_t size) {

 if (index < size) {

 return (index + 1);

    }

 else {

 return 0;

    }

}

static  inline  bool  CyclicBufferIsEmpty(CyclicBuffer* cyclicBuffer) {

 bool res = (cyclicBuffer->head == cyclicBuffer->tail);

 return res;

}

static  inline  bool  CyclicBufferIsFull(CyclicBuffer* cyclicBuffer) {

 size_t tail = CyclicBufferIncrement(cyclicBuffer->tail, CYCLIC_BUFFRE_SIZE);

 bool res = (cyclicBuffer->head == tail);

 return res;

}

static  inline  void  errorOverflow() {

}

static  inline  void  errorUnderflow() {

}

static  inline  bool  CyclicBufferAdd(CyclicBuffer* cyclicBuffer, const CYCLIC_BUFFER_OBJECT_TYPE object) {

 if (!CyclicBufferIsFull(cyclicBuffer)) {

        cyclicBuffer->data[cyclicBuffer->tail] = object;

        cyclicBuffer->tail = CyclicBufferIncrement(cyclicBuffer->tail, CYCLIC_BUFFRE_SIZE);

 return  true;

} else {

        errorOverflow();

 return  false;

    }

}

static  inline  bool  CyclicBufferRemove(CyclicBuffer* cyclicBuffer, CYCLIC_BUFFER_OBJECT_TYPE* object) {

 if (!CyclicBufferIsEmpty(cyclicBuffer)) {

        *object = cyclicBuffer->data[cyclicBuffer->head];

        cyclicBuffer->head = CyclicBufferIncrement(cyclicBuffer->head, CYCLIC_BUFFRE_SIZE);

 return  true;

} else {

        errorUnderflow();

 return  false;

    }

}

Function main prints digits 0,1,2,3

int  main() {

 for (int i = 0;i < 4;i++) {

        CyclicBufferAdd(&myCyclicBuffer, i);

    }

 uint8_t val;

 while (CyclicBufferRemove(&myCyclicBuffer, &val)) {

        cout << (int) val << endl;

    };

 return 0;

}

This code has some limitations. Only cyclic buffers manipulating the same integer type can be used in the same C source file. Add/remove functions can be defined only once in a C file.

Corresponding assembly contains 10 opcodes for a call to add() API:

 return (index + 1);

 xor %esi,%esi

static  inline  void CyclicBufferAdd(CyclicBuffer* cyclicBuffer, const CYCLIC_BUFFER_OBJECT_TYPE object) {

  mov 0x2009be(%rip),%rax        # 0x6011b0 <myCyclicBuffer+16>

 return (index + 1);

  mov %rsi,%r8

int main() {

  push %rbp

 return (index + 1);

  lea 0x1(%rcx),%rdi

...............................................

static  inline  void CyclicBufferAdd(CyclicBuffer* cyclicBuffer, const CYCLIC_BUFFER_OBJECT_TYPE object) {

  mov %rcx,%rdx

  push %rbx

 return (index + 1);

  cmovbe %rdi,%r8

...............................................

 if (!CyclicBufferIsFull(cyclicBuffer)) {

  cmp %r8,%rax

...............................................

        cyclicBuffer->data[cyclicBuffer->tail] = object;

  movb $0x0,0x6011a0(%rcx)

GNUC for ARM produces essentially the same assembly for the C and the C++ code

xor    %esi,%esi

mov    0x2009be(%rip),%rax

mov    %rsi,%r8

push   %rbp

lea    0x1(%rdx),%rdi

cmp    $0x9,%rdx

mov    %rdx,%rcx

push   %rbx

cmovbe %rdi,%r8

cmp    %r8,%rax

je 40081c <main+0x3c>

movb   $0x0,0x6011a0(%rdx)

mov    %r8,%rcx

mov    %r8,0x20099c(%rip)

xor    %r12d,%r12d

Performance of the C and the C++ versions measured on Intel is the same.

## C++ templates.

To understand what recursion is, you must first understand recursion.

At this point a patient reader would ask about “code bloat” caused by the C++ templates and object code duplication. Typically, an implementation in C should have a smaller memory footprint, should not it?

In the C++ implementation of the cyclic buffer, all methods are inline and there is no any specific “template code”. In the general case, for every pair ObjectType/Size used in the code, the C++ compiler is going to instantiate a class and add a full set of methods to the application code. A careful C++ programmer shall move the methods which do not require template arguments to a base class and derive the CyclicBuffer template from the new class. Moving type-invariant code into a base class sometimes is called “code hoisting”. Code hoisting does not necessary cause a performance hit. In the following example I call the base class CyclicBufferBase. Constructor of the base class is protected. An application can create only objects of the child class.

class  CyclicBufferBase {

public:

 bool  isEmpty() {

 bool res = (this->head == this->tail);

 return res;

    }

 bool  isFull() {

 size_t tail = increment(this->tail);

 bool res = (this->head == tail);

 return res;

    }

protected:

 CyclicBufferBase(size_t size) {

 this->size = size;

 this->head = 0;

 this->tail = 0;

    }

 void  errorOverflow() {

    }

 void  errorUnderflow() {

    }

 size_t  increment(size_t index) {

 if (index < this->size) {

 return (index + 1);

} else {

 return 0;

        }

    }

 size_t  head;

 size_t  tail;

 size_t  size;

};

The template class CyclicBuffer contains data which depends on the template argument Size and add/remove methods which depend on the size of the integer. Class CyclicBuffer is derived from the class CyclicBufferBase, inherits all methods of the class CyclicBufferBase, and exposes all methods of the class CyclicBufferBase.

template<typename  ObjectType, typename  Lock, std::size_t  Size>

class  CyclicBuffer:public  CyclicBufferBase {

public:

 CyclicBuffer() :

        CyclicBufferBase(Size) {

 static_assert(std::numeric_limits<ObjectType>::is_integer, "CyclicBuffer is intended to work only with integer types");

    }

 ~CyclicBuffer() {

    }

 bool  add(const  ObjectType object) {

 Lock  lock;

 if (!isFull()) {

 data[this->tail] = object;

 this->tail = increment(this->tail);

 return  true;

} else {

            errorOverflow();

 return  false;

        }

    }

 bool  remove(ObjectType &object) {

 Lock lock;

 if (!isEmpty()) {

object = data[this->head];

 this->head = this->increment(this->head);

 return  true;

} else {

            errorUnderflow();

 return  false;

        }

    }

private:

 ObjectType  data[Size + 1];

};

Where a C++ template causes object code duplication the C code can lead to the source code and object code duplication. Analyzing of the object code generated by the C/C++ compiler helps to locate parts of the code responsible for the object code duplication. For example, a post build utility can look for patterns in the object code which occur more than once, and use a map file to report the corresponding position in assembly.

There is one use case for C++ templates that is rather hard to replicate in the plain vanilla C. It is called template “metaprogramming”. Let's declare a template which recursively calculates a factorial:

template<const  uint32_t  N> struct  factorial

{

 static  constexpr  uint32_t  value = N * factorial<N - 1>::value;

};

I need to define factorial of zero explicitly:

template<>struct  factorial<0>

{

 static  constexpr  uint32_t  value = 1;

};

Now I can have the following statement in my C++ code:

constexpr  uint32_t factorial_3 = factorial<3>::value;

C++ compiler will replace the call to factorial<3> with 6 and the variable factorial_3 will be a constant known at the build time. I have never met firmware code which was required to calculate a factorial, but there were cases when I needed to force the compilation failure instead of getting a run-time error. Calculating a number of bits in the “int” variable and failing the compilation if the integer is not large enough could be a good example, if C++11 already had not std::numeric_limits<T>::max() which returns maximum value representable by type T. Yet another example is calculating non-trivial constants. In the following example the function testSum() will print 15\. The template function accepts variable number of arguments and is called a variadic template function.

int  sum()

{

 return 0;

}

template<typename ... Types>

int  sum (int first, Types ... rest)

{

 return first + sum(rest...);

}

const  int SUM = sum(1, 2, 3, 4, 5);

This function prints 15:

void  testSum()

{

cout << "SUM=" << SUM << endl;

}

## Memory management.

Programming is like sex, one mistake and you have to support it for the rest of your life.

I am going to discuss two frequently used types of memory allocation in the embedded software – static allocation at the build time and allocation from memory pools.

I will start the discussion of the dynamic memory allocation from memory pools by declaration of a new class Stack. Template class Stack is similar to the class CyclicBuffer used previously. Class Stack implements two methods: “push” and “pop”.

template<typename ObjectType, typename Lock, std::size_t Size>

class Stack: public StackBase {

public:

    Stack() :

    StackBase(Size) {

    }

    ~Stack() {

    }

 inline  bool push(ObjectType* object);

 inline  bool pop(ObjectType** object);

private:

    ObjectType* data[Size + 1];

};

Base class StackBase contains “top” and “size” fields and a couple of useful APIs

class  StackBase {

public:

 bool  isEmpty() {

 bool res = (this->top == 0);

 return res;

    }

 bool  isFull() {

 bool res = (this->top == size);

 return res;

    }

protected:

 StackBase(size_t size) {

 this->size = size;

 this->top = 0;

    }

 void  errorOverflow() {

    }

 void  errorUnderflow() {

    }

 size_t  top;

 size_t  size;

};

Example of implementation of the push and pop methods:

template<typename  ObjectType, typename Lock, std::size_t Size>

inline  bool Stack<ObjectType, Lock, Size>::

push(ObjectType* object) {

    Lock lock;

 if (!isFull()) {

        data[this->top] = object;

 this->top++;

 return  true;

} else {

        errorOverflow();

 return  false;

    }

}

template<typename ObjectType, typename Lock, std::size_t Size>

inline  bool Stack<ObjectType, Lock, Size>::

pop(ObjectType** object) {

    Lock lock;

 if (!isEmpty()) {

 this->top--;

        *object = (data[this->top]);

 return  true;

} else {

        errorUnderflow();

 return  false;

    }

}

My next step is to define a block of “raw” data memory. A block of memory is a correctly aligned array of bytes, which, optionally, can be placed at a specific memory address. One popular application for the memory blocks is DMA transfers. Data buffer can be placed in the regular RAM or in the dedicated address space.

I define a memory region. I use operator “new” – a placement new operator – to “place” the data at the specified address. My memory region has a name for debug purposes. A region address is of type uintptr_t which is an unsigned integer that is capable of storing a pointer.

class  MemoryRegion {

public:

 MemoryRegion(const  char *name, uintptr_t address, size_t size) :

 name(name), address(address), size(size) {

 data = new (reinterpret_cast<void*>(address)) uint8_t[size];

    }

 size_t  getSize() const {

 return  size;

    }

 const  char* getName() const {

 return  name;

    }

 uintptr_t  getAddress() const {

 return  address;

    }

protected:

 const  char *name;

 uintptr_t  address;

 size_t  size;

 uint8_t *data;

};

I create an object of MemoryRegion type and point to the area dmaMemoryData in the dynamic data:

static  uint8_t dmaMemoryDummy[512];

static  MemoryRegion dmaMemoryRegion("dmaMem", (uintptr_t)dmaMemoryDummy, sizeof(dmaMemoryDummy));

I need an allocator. This is a class dealing with allocation of memory blocks. The allocator handles the correct alignment. I am going to use the allocator code only once (or rarely). For example, I need an allocator when I fill my memory pool with the data blocks. The performance is not extremely important here. The method reset “frees” all allocated blocks back to the allocator.

class  MemoryAllocatorRaw {

public:

 MemoryAllocatorRaw(MemoryRegion memoryRegion,

 size_t blockSize,

 size_t count, unsigned  int alignment);

 uint8_t* getBlock();

 bool  blockBelongs(const  void* block) const;

 const  MemoryRegion& getRegion() const;

 void  reset();

 constexpr  static  size_t  predictMemorySize(

 size_t blockSize,

 size_t count, unsigned  int alignment);

protected:

 int  alignment;

 size_t  blockSize;

 const  MemoryRegion& memoryRegion;

 size_t  count;

 size_t  sizeTotalBytes;

 size_t  alignedBlockSize;

 uintptr_t  firstNotAllocatedAddress;

 static  constexpr  size_t  alignConst(size_t value,

 unsigned  int alignment);

 inline  static  uintptr_t  alignAddress(

 uintptr_t address, unsigned  int alignment);

};

Implementation of the allocator methods follows. The allocator constructor makes sure that there is enough space in the memory region. I initialize the fields in the first line of the constructor, right after the constructor name:

MemoryAllocatorRaw::MemoryAllocatorRaw(MemoryRegion memoryRegion, size_t blockSize, size_t count, unsigned  int alignment) :

 alignment(alignment), blockSize(blockSize), memoryRegion(memoryRegion), count(count)  {

 alignedBlockSize = alignAddress(blockSize, alignment);

 sizeTotalBytes = alignedBlockSize * count;

 if (sizeTotalBytes > memoryRegion.getSize()) {

 // handle error

    }

 firstNotAllocatedAddress = memoryRegion.getAddress();

    reset();

}

Allocator implements only the “get a block” API. Memory pool calls the “get block” API from the pool constructor.

uint8_t* MemoryAllocatorRaw::getBlock() {

 uintptr_t block;

block = alignAddress(firstNotAllocatedAddress, alignment);

 firstNotAllocatedAddress += alignedBlockSize;

 return (uint8_t*)block;

}

My pool needs sanity check to ensure that “free” is called only for the blocks that indeed “belong” to the pool.

bool  MemoryAllocatorRaw::blockBelongs(const  void* block) const {

 uintptr_t blockPtr = (uintptr_t)block;

 bool res = true;

res = res && blockPtr >= memoryRegion.getAddress();

 size_t maxAddress = memoryRegion.getAddress()+sizeTotalBytes;

    res = res && (blockPtr <= maxAddress);

 uintptr_t alignedAddress = alignAddress(blockPtr, alignment);

    res = res && (blockPtr == alignedAddress);

 return res;

}

The rest of the methods:

constexpr  size_t  MemoryAllocatorRaw::alignConst(

 size_t value, unsigned  int alignment) {

 return (value + ((size_t)alignment-1)) &

      (~((size_t)alignment-1));

}

uintptr_t  MemoryAllocatorRaw::alignAddress(uintptr_t address, unsigned  int alignment) {

 uintptr_t res =

      (address+((uintptr_t)alignment-1)) & (~((uintptr_t)alignment-1));

 return res;

}

const  MemoryRegion& MemoryAllocatorRaw::getRegion() const {

 return  memoryRegion;

}

void  MemoryAllocatorRaw::reset() {

 firstNotAllocatedAddress =

 memoryRegion.getAddress();

}

Before I declare an object of the allocator, I check that the memory region is large enough. I want the compilation to fail if the memory region is too small:

static_assert((sizeof(dmaMemoryDummy) >= MemoryAllocatorRaw::predictMemorySize(63, 3, 2)), "DmaMemoryDummy region is not large enough");

static  MemoryAllocatorRaw dmaAllocator(dmaMemoryRegion, 63, 3, 2);

My memory pool is a stack of data blocks. The class contains allocate/free API, some debug statistics. Every memory pool has a name. Providing a name for the objects is useful for logging and printing debug statistics. The stack in the memory pool is intentionally protected by a LockDummy and is not thread safe. I am going to use a real synchronizer in the memory pool methods.

Class methods with “const” keyword in the signature, for example resetMaxInUse(), can not alter any member of the class. How comes that resetMaxInUse() changes the statistics field anyway?. Field “statistics” is mutable and this allows the “const” methods to modify it. Debug counters is a book example of using of the keyword “mutable”. Method resetMaxInUse() does not affect (not in a meaningfull way) the visible state of the object.

template<typename  Lock, size_t  Size>

class  MemoryPoolRaw {

public:

 MemoryPoolRaw(const  char* name,

 MemoryAllocatorRaw* memoryAllocator);

 ~MemoryPoolRaw() {

 memoryAllocator->reset();

    }

 inline  void  resetMaxInUse() const {

 statistics.maxInUse = 0;

    }

 typedef  struct {

 uint32_t  inUse;

 uint32_t  maxInUse;

 uint32_t  errBadBlock;

} Statistics;

 inline  bool  allocate(uint8_t** block);

 inline  bool  free(uint8_t* block);

 inline  const  Statistics &getStatistics(void) const {return  statistics;}

protected:

 mutable  Statistics  statistics;

 const  char* name;

 Stack<uint8_t, LockDummy, Size> pool;

 MemoryAllocatorRaw* memoryAllocator;

};

Memory pool constructor calls the allocator to fill the stack of free blocks. Constructor can, for example, register the newly created memory pool in the data base of the memory pools. Application can provide meanings for the run-time inspection of the memory pools. Destructor would remove the pool from the data base:

template<typename  Lock, size_t  Size>

MemoryPoolRaw<Lock, Size>::

MemoryPoolRaw(const  char* name,

MemoryAllocatorRaw* memoryAllocator) :

 name(name), memoryAllocator(memoryAllocator) {

 memset(&this->statistics, 0, sizeof(this->statistics));

 for (size_t i = 0;i < Size;i++) {

 uint8_t *block = memoryAllocator->getBlock();

 pool.push(block);

    }

}

If the Lock class is not a dummy lock, memory pool allocate/free API is reentrant and thread safe. All activity which can modify the state of the stack is protected by the lock. If an application uses the pool only in one context the application can provide LockDummy template argument for the memory pool. LockDummy adds no code to the executable. Statistics counters are relatively low cost, but are immensely helpful for debugging errors such as allocation failure.

template<typename  Lock, size_t  Size>

inline  bool  MemoryPoolRaw<Lock, Size>::

allocate(uint8_t** block) {

 bool res;

 Lock lock;

res = pool.pop(block);

 if (res) {

 statistics.inUse++;

 if (statistics.inUse > statistics.maxInUse)

 statistics.maxInUse = statistics.inUse;

    }

 return res;

}

Memory pool “free” makes sure that the pointer belongs to the pool. The memory allocator knows to recognize it's own blocks.

template<typename  Lock, size_t  Size>

inline  bool  MemoryPoolRaw<Lock, Size>::

free(uint8_t* block) {

 bool res;

 Lock lock;

res = memoryAllocator->blockBelongs(block);

 if (res) {

res = pool.push(block);

 statistics.inUse--;

    }

 else {

 statistics.errBadBlock++;

    }

 return res;

}

It is going to be fairly easy to prevent release of the same block more than once. If the data blocks are part of the continuous memory, the allocator can provide a method generating a unique index based on the address of the block. Memory pool can contain an array where blocks are marked as allocated or free, and method free() can check the block against this array. If the memory region is not continuous, the allocator can implement a hash function translating the address of a data block to a unique data block index.

## Operator new.

Algorithm (noun)
Word used by programmers when they do not want to explain what they did.

Many small microcontrollers have a relatively small heap for dynamic memory allocation. The design choice not to use the dynamic memory allocation at all is very popular. Often it does not make sense in the firmware to use standard implementations of operators “new” and “delete” from the C/C++ library. Operator new can throw an exception – a dynamically allocated object by itself – if the system runs out of free memory. Calls to new and delete for different objects in run-time will eventually cause memory fragmentation. Software timers from the later chapter and STL containers can take advantage of the user-defined memory allocation that employs custom allocators. Customized operator new can be based on a “placement new”. Constructor in the CyclicBufferDynamic class can be redefined like this:

template<typename  ObjectType, typename  Lock>

inline  CyclicBufferDynamic

<ObjectType, Lock>::

CyclicBufferDynamic(size_t size, void *address) {

 this->head = 0;

 this->tail = 0;

 this->size = size;

 if (address != nullptr) {

 this->data = new (address) ObjectType[size];

    }

 else {

 this->data = new  ObjectType[size];

    }

 static_assert(sizeof(ObjectType) <= sizeof(uintptr_t), "CyclicBuffer is intended to work only with integer types or pointers");

}

In the following example I make the compiler to allocate the required memory statically and use the address of the allocated data in the call to the constructor:

static  uint32_t myDynamicCyclicBufferData[calculateCyclicBufferSize()];

CyclicBufferDynamic<uint32_t, LockDummy> myDynamicCyclicBuffer(calculateCyclicBufferSize(), &myDynamicCyclicBufferData);

# I/O access.

How many programmers does it take to change a light bulb? None – it's a hardware problem.

Embedded software accesses the hardware via hardware registers. I will assume that there are three groups of registers: read and write registers, read only registers and write only registers. All registers are memory mapped and there is an address for every register. The software can access a register in the same way as it reads or writes a variable given the variable's address. In case of write only registers it is a custom to keep a cached value. Cache is a variable sitting in the data memory that contains the latest value written to the write only register.

The following example is based on the user interface of the Parallel Input/Output controller (PIO) in the Atmel SAMA5d3 microcontroller. I have simplified the interface to save lines of code and text.

| 0x0000 | PIO Enable Register | PIO_PER | Write-only |
| 0x0004 | PIO Disable Register | PIO_PDR | Write-only |
| 0x0008 | PIO Status Register | PIO_PSR | Read-only |
| 0x000C | Reserved |  |  |
| 0x0010 | Output Enable Register | PIO_OER | Write-only |
| 0x0014 | Output Disable Register | PIO_ODR | Write-only |
| 0x0018 | Output Status Register | PIO_OSR | Read-only |
| 0x001C | Reserved |  |  |
| 0x0020 | Not used |  |  |
| 0x0024 | Not used |  |  |
| 0x0028 | Not used |  |  |
| 0x002C | Reserved |  |  |
| 0x0030 | Set Output Data Register | PIO_SODR | Write-only |
| 0x0034 | Clear Output Data Register | PIO_CODR | Write-only |
| 0x0038 | Output Status Register | PIO_ODSR | Read-only |

There are five blocks such as this one called A, B, C, D, E, F in the microcontroller. The registers are mapped starting at the address 0xFFFFF200\. A user wishing to modify a write only register shall write 1 to the relevant bits. For example, user shall write 0x04 to PIO_SODR, PIO_PER, PIO_OER to drive pin 2 (zero based) of the PIO high. Write to the PIO registers is an atomic operation. The hardware interface allows to change the configuration of a single bit in a thread safe manner. The hardware provides convenient read only status registers which keep the current value of the write only registers.

## I/O access in C.

"Writing in C or C++ is like running a chain saw with all the safety guards removed" – Bob Gray.

I am providing quick and dirty C implementation. Macro RESERVED demonstrates a neat trick to generate a unique identifier name.

#define TOKEN_CAT(x, y) x ## y

#define TOKEN_CAT2(x, y) TOKEN_CAT(x, y)

#define RESERVED TOKEN_CAT2(reserved, __COUNTER__)

Declaration of the PIO structure, a group of32 bits registers, follows. I want to ensure that the compiler does not do any padding and I mark the structure “packed”. Pragma “pack” is potentially not safe. Some architectures, such as ARM or MIPS, do not support non-aligned access.

#pragma pack(push)

#pragma pack(1)

struct  PIO {

 volatile  uint32_t  PIO_PER  ;

 volatile  uint32_t  PIO_PDR  ;

 volatile  uint32_t  PIO_PSR  ;

 volatile  uint32_t RESERVED ;

 volatile  uint32_t  PIO_OER  ;

 volatile  uint32_t  PIO_ODR  ;

 volatile  uint32_t  PIO_OSR  ;

 volatile  uint32_t RESERVED ;

 volatile  uint32_t RESERVED ;

 volatile  uint32_t RESERVED ;

 volatile  uint32_t RESERVED ;

 volatile  uint32_t RESERVED ;

 volatile  uint32_t  PIO_SODR ;

 volatile  uint32_t  PIO_CODR ;

};

#pragma pack(pop)

Declaration of the pointer to the memory area:

#ifdef REAL_HARDWARE

static PIO *pios = (PIO*)0xFFFFF200;

#else

static  PIO pioDummy[5];

static  PIO *pios = pioDummy;

#endif

Five PIO blocks:

typedef  enum {

 PIO_A,

 PIO_B,

 PIO_C,

 PIO_D,

 PIO_E,

 PIO_F,

} PIO_NAME;

Function which configures a pin as output:

static  void  enableOutput(PIO_NAME name, int pin, int value) {

 PIO *pio = &pios[name];

 uint32_t mask = 1 << pin;

 if (value) {

        pio->PIO_SODR = mask;

    }

 else {

        pio->PIO_CODR = mask;

    }

    pio->PIO_PER = mask;

    pio->PIO_OER = mask;

}

Function which drives PIO A, pin 2 high can look like this:

static  void  main() {

    enableOutput(PIO_A, 2, 1);

}

This is how the relevant assembly for Intel looks like – as expected there are three 32-bits moves

  PIO *pio = &pios[name];

  uint32_t mask = 1 << pin;

  if (value) {

      pio->PIO_SODR = mask;

4007e0:              c7 05 e6 19 20 00 04               movl   $0x4,0x2019e6(%rip)

4007e7:              00 00 00

4007ea:31 c0                              xor %eax,%eax

      pio->PIO_SODR = mask;

  }

  else {

      pio->PIO_CODR = mask;

  }

  pio->PIO_PER = mask;

4007ec:              c7 05 aa 19 20 00 04               movl   $0x4,0x2019aa(%rip)

4007f3:              00 00 00

  pio->PIO_OER = mask;

4007f6:              c7 05 b0 19 20 00 04               movl   $0x4,0x2019b0(%rip)

4007fd:              00 00 00

Assembly generated for ARM is slightly longer. In ARM an address should be loaded to a register before a value can be stored.

PIO *pio = &pios[name];

uint32_t mask = 1 << pin;

if (value) {

    pio->PIO_SODR = mask;

8650:              e59f3014               ldr              r3, [pc, #20]

8654:              e3a02004               mov              r2, #4

8658:              e5832090               str              r2, [r3, #144]

865c:              e3a00000               mov              r0, #0

    pio->PIO_SODR = mask;

}

else {

    pio->PIO_CODR = mask;

}

pio->PIO_PER = mask;

8660:              e5832060               str              r2, [r3, #96]

pio->PIO_OER = mask;

8664:              e5832070               str              r2, [r3, #112]

## I/O access in C++.

"C(++) is a write-only, high-level assembler language." Stefan Van Baelen.

This is not easy to compete with the C implementation when accessing the I/O. The C compiler for i386 translated every line of the C code into a single machine opcode. There is no need to manually specify an address for every register. It is enough to create a pointer which references the physical address of the first register in the block. I want a C++ implementation with the same perfect performance score, similar convenience of usage AND some added value, for example type safety.

First class is an abstraction of a hardware module. The class constructor is protected. Application can create only objects of the derived classes.

class  HardwareModule {

protected:

 HardwareModule(const  uintptr_t address): address(address) {}

 ~HardwareModule() {}

 const  uintptr_t  address;

};

I declare a template for all hardware registers. Static assert will fail compilation if the argument IntegerType specified in the type instantiation is not an integer type. API “std::atomic” ensures an atomic read/write operation on any architecture, such as reading of 32 bis value on 8 bits CPU

template<typename  IntegerType> class  HardwareRegister {

protected:

 HardwareRegister() {}

 inline  IntegerType  get() const {

 return atomic_load(&value);

    }

 inline  void  set(IntegerType value) {

        atomic_store(&this->value, value);

    }

 volatile  atomic<IntegerType> value;

 static_assert(numeric_limits<IntegerType>::is_integer,

 "HardwareRegister works only with integer types");

};

Next class is a 32 bits register. Static assertion will fail the build if the object consumes more than 32 bits. Correct size of the data is absolutely vital for the access to the hardware and comes instead of the “packed” attribute in the C version.

class  HardwareRegister32: public  HardwareRegister<uint32_t> {

protected:

 HardwareRegister32() {}

};

static_assert((sizeof(HardwareRegister32) == sizeof(uint32_t)), "HardwareRegister32 is not 32 bits");

Read only and write only registers follow. The read only register class overloads the type cast operator and allows to use an assignment to read the register value. The write only register class overloads the assignment operator and allows to use an assignment to write the register value. Read/write registers would implement both the assignment operator and the type cast operator.

Read only register:

class  HardwareRegister32RO : public  HardwareRegister32{

public:

 operator uint32_t() const {

 return get();

    }

};

static_assert((sizeof(HardwareRegister32RO) == sizeof(uint32_t)), "HardwareRegister32RO is not 32 bits");

Write only register:

class  HardwareRegister32WO : public  HardwareRegister32{

public:

 uint32_t  operator=(uint32_t value) {

        set(value);

 return value;

    }

};

static_assert((sizeof(HardwareRegister32WO) == sizeof(uint32_t)), "HardwareRegister32WO is not 32 bits");

For the clarity I add a register “reserved” – I call it “not used”:

class  HardwareRegister32NotUsed : HardwareRegister32 {

public:

 HardwareRegister32NotUsed() {}

 ~HardwareRegister32NotUsed() {}

};

static_assert((sizeof(HardwareRegister32NotUsed) == sizeof(uint32_t)),

 "HardwareRegister32NotUsed is not 32 bits");

The framework is in place and can serve any 32 bits register. Declare the PIO hardware module. There is nothing unexpected, but just a repetition of all the same tricks including build time check of the size of the structure. An object of the type HardwarePIO requires about the same amount data as the competing C version. Depending on the optimization level and complexity of the class there is going to be one additional pointer in the RAM, a pointer “this”. In the specific implementation below all methods of the class are “inline” and the object data gets optimized out completely.

class  HardwarePIO : HardwareModule {

public:

 HardwarePIO(const  uintptr_t address) {

 interface = (struct  Interface*)address;

    }

 ~HardwarePIO() {}

 struct  Interface {

 HardwareRegister32WO  PIO_PER  ;

 HardwareRegister32WO  PIO_PDR  ;

 HardwareRegister32RO  PIO_PSR  ;

 HardwareRegister32NotUsed RESERVED ;

 HardwareRegister32WO  PIO_OER  ;

 HardwareRegister32WO  PIO_ODR  ;

 HardwareRegister32RO  PIO_OSR  ;

 HardwareRegister32NotUsed RESERVED ;

 HardwareRegister32NotUsed RESERVED ;

 HardwareRegister32NotUsed RESERVED ;

 HardwareRegister32NotUsed RESERVED ;

 HardwareRegister32NotUsed RESERVED ;

 HardwareRegister32WO  PIO_SODR ;

 HardwareRegister32WO  PIO_CODR ;

    };

 static_assert((sizeof(struct  Interface) == (14*sizeof(uint32_t))), "struct interface is of wrong size, broken alignment?");

 enum Name {A, B, C, D, E, F, LAST};

 inline  Interface &getInterface(Name name) const {return  interface[name];};

 inline  void  enableOutput(Name name, int pin, int value);

protected:

 struct  Interface *interface;

};

Implementation of the method enableOutput is similar to the C version:

inline  void  HardwarePIO::enableOutput(Name name, int pin, int value)

{

 struct  Interface &interface = getInterface(name);

 uint32_t mask = 1 << pin;

 if (value) {

        interface.PIO_SODR = mask;

    }

 else {

        interface.PIO_CODR = mask;

    }

    interface.PIO_PER = mask;

    interface.PIO_OER = mask;

}

Usage example:

static  HardwarePIO hardwarePIO(reinterpret_cast<uintptr_t>(pioDummy));

void  main() {

    hardwarePIO.enableOutput(HardwarePIO::A, 2, 1);

}

This C++ implementation produces the same assembly as the old trusty C one. There is no more “code bloat” than in the C implementation. C++ framework comes with some worthy benefits. If a user attempts to read a write only register the build will fail. The following statement will break the compilation:

uint32_t per = hardwarePIO.getInterface(HardwarePIO::A).PIO_PER;

Access to the PIO registers is encapsulated in the class methods of the hardware module. The methods in the HardwarePIO class are the only way to modify a register. C++ implementation allows to catch other wrong doings at compilation time, for example reading or writing reserved registers.

It is easy to cache all written values in the hardware module. One way to cache or log the read and write transactions is to add a “shadow” interface field to the hardware module class.

## Indirect I/O access.

In some case the hardware is accessible via a serial interface. One example of such interface is SPI. I am using a direct access API for the sake of brevity. A real access interface for a real SPI device can contain system calls or calls to the serial interface driver:

template<typename  IntegerType>

class  HardwareDirectAccessAPI {

public:

 inline  uint32_t  get() const {

 return atomic_load(&value);

    }

 inline  void  set(uint32_t value) {

        atomic_store(&this->value, value);

    }

protected:

 volatile  atomic<IntegerType> value;

 static_assert(numeric_limits<IntegerType>::is_integer,

 "HardwareDirectAccessAPI works only with integer types");

};

I am adding an argument to the template class HardwareRegister:

template<typename  IntegerType, typename  AccessAPI>

class  HardwareRegister {

protected:

 HardwareRegister() {}

 inline  IntegerType  get() const {

 return  api.get();

    }

 inline  void  set(IntegerType value) {

 api.set(value);

    }

 AccessAPI  api;

};

Instance of the HardwareRegister for 32 bits registers, direct access will look like this:

class  HardwareRegister32:

public  HardwareRegister<uint32_t, HardwareDirectAccessAPI<uint32_t> > {

protected:

 HardwareRegister32() {}

};

The rest of the classes remains the same.

# Code ROM and data RAM.

If at first you don't succeed; call it version 1.0\.

There are very popular hardware platforms, where ROM and RAM distinction is very important. One example of such device is rather popular 8 bits microcontrollers Atmega. In the Atmega MCUs code can not be placed in the data memory and CPU can not execute code sitting in the RAM. Any access to the data in the code memory requires special instructions. Another example is Application Specific Integration Circuits or ASICs. An ASIC often contains integrated ROM and RAM. Integrated, also called on die or on chip, ROM storage is relatively cheap, because it requires relatively small amount of space on the silicone wafer. RAM is relatively expensive because it requires more logic per bit of memory and square inches on the integrated circuit (die) come at premium. RAM consumes significantly more power. I think that the vast majority of the electronic device around us have integrated ROM and RAM (frequently SRAM) inside. Typically the on chip RAM is much smaller than the ROM.

There are two types of ROM: erasable and not erasable. In the Atmega MCUs different areas of the ROM can be programmed by the firmware, assuming that the firmware runs from another area. In case of ASICs the ROM is often not erasable. Programming of the ROM is a part of the ASIC production process. The ROM can not be modified after the chip leaves the factory (the FAB).

If there is not enough RAM to load the firmware, then parts of the firmware code should be located in the chip ROM. In case of an ASIC it means that the ROM based parts of the firmware can be changed only in the future versions of the chip. High complexity of the modern ASIC firmware makes it very hard to reach 100% code coverage in the ASIC verification process. Even if the ROM based firmware is verified and tested completely, still there is a chance that this or that protocol has been misunderstood by the development team, or product requirements has changed. The development team prepares the firmware and the hardware for the not unlikely event that a need to patch the ROM will arise.

This chapter covers some of the ROM related problems.

## C++ Initialized data.

At least one code section, a boot, constants and initialized data are parts of the ROM. Initialized, non-zero data is going to consume memory two times. Initialization values of the initialized data are part of the ROM. Usually boot process copies the values from the ROM to the RAM. If I inspect an object file generated by a compiler, I can easily find initialization data for the strings. There are utilities which help to inspect the object files, dump different section into separate files, and prepare the images for the ROM programming. One example of such utility is GNU objdump. Let's see some C++ initialized data in action. Following code produces two lines of output: “Hello, world!”, followed by “Hello from main()!”

class  HelloWorld {

public:

 HelloWorld() {

cout << "Hello, world!" << endl;

    }

};

static  HelloWorld helloWorld;

int  main()

{

cout << "Hello from main()!" << endl;

 return 0;

}

The function main() contains only one output. The entity responsible for initializing of the C++ object helloWorld and printing the first line is an object loader running in my operating system. In case of the embedded systems this code is usually part of the boot process. The constructor of the HelloWorld class is “text” and appears only once in the ROM. Arguments of the cout, the strings, can exist in two places in the memory: original or “master copy” is in the ROM, a second copy, created by the loader, is in the RAM. Pointer “this” which contains address of the statically allocated object helloWorld has two copies too. There is an initialization value for “this” pointer in the ROM and “this” pointer in the RAM.  Size allocated by helloWorld object in the ROM of 32 bits CPU is at least 4 bytes of “this” and 14 bytes of the zero terminated string. The linker script is responsible for correct placement of different sections of the code and the data. If the CPU can not access data stored in the code memory, the linker script should contain relevant allocation instructions. Specifically place for the constant data section will be allocated two times: in the code ROM address space and in the RAM. 

In a typical case, a linker script will add global variables that reference the start and the end address of the not initialized data section(s) “bss”, initialized data, and a table of “ctor” functions. Usually the ctor section is a table or tables of functions that the boot code calls to initialize static C++ objects. See your linker documentation for details.

## ROM patching.

Programming is a lot like sex. One mistake and you're providing support for a lifetime.

I want to prepare the constructor code for a patch in the future. I will check some location in the RAM. If there is a non-zero entry, then I will use the string from there. If not, I will print the default value – the ROMed one.

static  const  char *helloWorldStr = 0;

class  HelloWorld {

public:

 HelloWorld() {

 if (helloWorldStr == 0)

cout << "Hello, world!" << endl;

 else

cout << helloWorldStr << endl;

    }

};

Loading of an ASIC which can be patched contains two stages. In the first phase external CPU (also called a host processor) loads some firmware to the ASIC RAM. There is a dedicated hardware/boot firmware supporting load of the application firmware to the RAM. An alternative can be that the boot code in the ASIC loads the application firmware from some external programmable memory chip, for example, EEPROM or SPI FLASH. The second phase is when the boot jumps to the application code in the RAM. If the code loaded by the host processor contains non-zero at the address helloWorldStr the ROM based application code will print a new string. I am calling this type of patch a patch type A. In the patch type A I fix a part of the function.

For the patch type B I need the hardware support. If the CPU fetches an instruction from a specific address or a range of addresses – in case of the code below this is an address of the function printHello() – I want to “interrupt” the execution and switch control to the interrupt handler located in the RAM. Default interrupt handler does nothing. The handler is empty and simply returns allowing the function printHello() to complete it's useful work. The patched interrupt handler can modify the string “Hello, world” in the RAM before letting the function printHello() to print it The interrupt handler can execute some arbitrary code and return the control to the caller of the printHello(), skipping the original print code completely.

class  HelloWorld {

public:

 HelloWorld() {

        printHello();

    }

protected:

 void  printHello() {

cout << "Hello, world!" << endl;

    }

};

For the patch type C I need support in the linker script. I want to place the constructor of the HelloWorld in the ROM, but method printHello() I want to execute in the RAM. If the HelloWorld constructor calls a function in the RAM I can easily patch the function code.

# Composition.

Have you ever noticed the difference between a 'C' project plan, and a C++ project plan? The planning stage for a C++ project is three times as long. Precisely to make sure that everything which should be inherited is, and what shouldn't isn't. Then, they still get it wrong.

Remember the length of the average-sized 'C' project? About 6 months. Not nearly long enough for a guy with a wife and kids to earn enough to have a decent standard of living. Take the same project, design it in C++ and what do you get? I'll tell you. One to two years. Isn't that great?

I will attempt to write a wrapper for the “create task” API. A typical wrapper for APIs similar to the pthread_create or FreeRTOS xTaskCreate is based on a static method in a class called, for example, MyThread. Indeed this is the only way I know to write a portable C++ wrapper that will work for most operating systems. I will duly present a basic example of this approach not because it is fascinating, but because it is expected of a reasonable “C++ for embedded” book. Feel free to jump right to the next paragraph where I present non-portable code of C++ create task wrapper.

## Static (class) member.

C allows you to shoot yourself in the foot. C++ allows you to re-use the bullet.

I am going to allocate my job thread objects from a pool. For example an implementation of the Remote Procedure Call could use a pool of job threads to execute procedures locally. Allocation of a thread object from the memory pool is faster than calling the operating system API to create a new thread. MemoryPool is a generic pool of objects which allocates the objects statically. This is a reuse of the memory pool class from the previous chapters. I am skipping the details here, such as name for the pool, debug statistics.

template<typename  Lock, typename  ObjectType, size_t  Size>

class  MemoryPool {

public:

 MemoryPool();

 ~MemoryPool() {}

 inline  bool  allocate(ObjectType **obj);

 inline  bool  free(ObjectType *obj);

protected:

 Stack<ObjectType, LockDummy, Size> pool;

 ObjectType  objects[Size];

};

The stack keeps reference to the free (not allocated) objects. The pool constructor fills the stack of objects:

template<typename  Lock, typename  ObjectType, size_t  Size>

MemoryPool<Lock, ObjectType, Size>::MemoryPool() {

 for (int i = 0;i < Size;i++) {

 pool.push(&objects[i]);

    }

}

Allocate and free methods call the stack pop and push API:

template<typename  Lock, typename  ObjectType, size_t  Size>

bool  MemoryPool<Lock, ObjectType, Size>::allocate(ObjectType **obj) {

 bool res;

 Lock lock;

res = pool.pop(obj);

 return res;

}

template<typename  Lock, typename  ObjectType, size_t  Size>

bool  MemoryPool<Lock, ObjectType, Size>::free(ObjectType *obj) {

 bool res;

 Lock lock;

res = pool.push(obj);

 return res;

}

A JobThread implements a “start” API and a static method with loop forever. More realistic implementations would add “wait for completion”, some mechanism for asynchronous notifications of the calling context that the job is done, support for arguments for the job function.

template <typename  JobType> class  JobThread {

public:

 JobThread();

 void  start(JobType *job);

protected:

 JobType *job;

 xTaskHandle  pxCreatedTask;

 xQueueHandle  signal;

 static  void  mainLoop(JobThread *jobThread);

};

JobThread constructor creates a binary semaphore and spawns (this specific choice of verb is based on “taskSpawn” which is a create task API in vxWorks) a new thread. I am assuming FreeRTOS API in this example, but any other API would work here:

template<typename  JobType>

JobThread<JobType>::JobThread() : job(nullptr) {

 static  const  char *name = "a job";

    vSemaphoreCreateBinary(this->signal);

    portBASE_TYPE res = xTaskCreate((pdTASK_CODE)mainLoop, (const  signed  char *)name, 300, this, 1, &this->pxCreatedTask);

 if (res != pdPASS) {

cout << "Failed to create a task" << endl;

    }

}

The thread entry, the mainLoop method, enters the while loop and waits for the binary semaphore. In the real code I would probably test an object variable “bool exitFlag” instead of the condition which is always true:

template<typename  JobType>

void  JobThread<JobType>::mainLoop(JobThread *jobThread) {

 while (true) {

        xSemaphoreTake(jobThread->signal, portMAX_DELAY);

 if (jobThread->job != nullptr) {

            jobThread->job->run();

        }

        jobThread->job = nullptr;

    }

}

Method “start” sets the job pointer and wakes up the mainLoop:

template<typename  JobType>

void  JobThread<JobType>::start(JobType *job) {

 this->job = job;

    xSemaphoreGive(this->signal);

}

In the example below the code prints “Print job is running”:

struct  PrintJob {

 void  run(void) {

cout << "Print job is running" << endl;

    }

};

MemoryPool<LockDummy, JobThread<PrintJob>, 3> jobThreads;

PrintJob printJob;

int  main( void )

{

 JobThread<PrintJob> *jobThread;

    jobThreads.allocate(&jobThread);

    jobThread->start(&printJob);

    vTaskStartScheduler();

 return 1;

}

## Non static member.

"C makes it easy to shoot yourself in the foot; C++ makes it harder, but when you do it blows your whole leg.

I am modifying only two lines in the code above. The call to xTaskCreate gets a pointer to a member function. The C++ compiler warns about converting of the address of the method to a generic pointer:

void *pMainLoop = (void*)&JobThread<JobType>::mainLoop;

portBASE_TYPE res = xTaskCreate((pdTASK_CODE)pMainLoop, (const  signed  char *)name, 300, this, 1, &this->pxCreatedTask);

Main loop method is not a static method anymore and does not need any argument:

template<typename  JobType>

void  JobThread<JobType>::mainLoop() {

 while (true) {

        xSemaphoreTake(signal, portMAX_DELAY);

 if (job != nullptr) {

 job->run();

        }

 job = nullptr;

    }

}

The trick works because most (all?) C++ compilers push “this”, a pointer to the object, first to the arguments stack. The trick can fail if C and C++ code use stack frames differently. Pointers to virtual methods can fail too. This is always possible to use brute force – disassembly, and figure out how to call the member function correctly. The implementation of the calls to virtual functions differ widely between compilers. Most C++ compilers replace the call to a virtual member with a small chunk of assembly code which calculates the method address.

A reader of this text could ask what is the point behind this pointer-to-member exercise. When I run the application under a debugger, sometimes I want to set a break point using an absolute address. I can print an absolute address of a member and see in run-time how many instances of the same method my generic class creates. Taking a pointer of a function insures that the function is not an “inline” function.

## Interprocess communication.

I hate threading anyway. Multiprocessing is the way to go, and message-passing, not shared memory. That just doesn't scale. I use multithreading so I can use all of my 16 cores, or whatever is the average number of cores in a machine these days. Big furry deal. I've got a few thousand servers waiting for me in the data center and how do I use those with threading? – Alex Martelli.

The classical Interprocess Communication (IPC) design pattern is a mailbox or a message queue. The mailbox design pattern has gained popularity when Windows 3.11 and the first real-time operating systems, such as RT Kernel and vxWorks, were a bleeding edge of the technology. Some operating systems support the message queue API. I am going to demonstrate a message queue that based on two primitives: a semaphore and a FIFO. The Mailbox class is an example of “object composition” ([4],[5]). I use “a mailbox HAS a FIFO” relationship. Alternatively, I could use “a mailbox is a FIFO” formula and subclass – inheritance – the mailbox from the class FIFO. It is considered a good practice not to overuse inheritance.

The mailbox API has two methods: send a message and wait for a message ([6]):

template<typename  ObjectType, typename  Lock>

class  Mailbox {

public:

 Mailbox(const  char *name, size_t size);

 const  char *getName() {return  name;}

 inline  bool  send(ObjectType msg);

 enum TIMEOUT {NORMAL, NONE, FOREVER};

 bool  wait(ObjectType *msg,

TIMEOUT waitType, size_t timeout);

protected:

 const  char *name;

 xQueueHandle  semaphore;

 CyclicBufferDynamic<ObjectType, Lock> fifo;

};

The mailbox constructor employs the FreeRTOS counting semaphore:

template<typename  ObjectType, typename  Lock>

Mailbox<ObjectType, Lock>::Mailbox(const  char *name, size_t size) :

 fifo(size),

 name(name) {

 semaphore = xSemaphoreCreateCounting(size+1, 0);

}

The send method adds a message to the FIFO and bumps the semaphore:

template<typename  ObjectType, typename  Lock>

bool  Mailbox<ObjectType, Lock>::send(ObjectType msg) {

 bool res;

res = fifo.add(msg);

    xSemaphoreGive(semaphore);

 return res;

}

Receive message handles different types of the timeout:

template<typename  ObjectType, typename  Lock>

bool  Mailbox<ObjectType, Lock>::wait(ObjectType *msg,

TIMEOUT waitType, size_t timeout) {

 bool res = false;

    portBASE_TYPE semaphoreRes = pdFALSE;

 while (semaphoreRes == pdFALSE) {

 if (waitType == TIMEOUT::FOREVER) {

            semaphoreRes = xSemaphoreTake(semaphore, portMAX_DELAY);

        }

 else  if (waitType == TIMEOUT::NORMAL) {

            semaphoreRes = xSemaphoreTake(semaphore, timeout);

 break;

        }

 else {

            semaphoreRes = xSemaphoreTake(semaphore, 0);

 break;

        }

    }

 if ((semaphoreRes == pdTRUE) && !fifo.isEmpty()) {

res = fifo.remove(msg);

    }

 return res;

}

In the example application an interrupt (a producer) reads data from the UART devices, and sends the collected data to the processing task (a consumer). My message object contains two things: a message event and some data. The consumer task is expected to switch by the message event:

enum EVENT {UART0, UART1};

typedef  struct {

 enum EVENT event;

 size_t  data[32];

 int  dataSize;

} Message;

In the example below I reuse the memory pool from the previous chapter:

MemoryPool<LockDummy, Message, 3> pool;

Mailbox<Message*, LockDummy> myMailbox("mbx", 3);

void  rxTask( void ) {

    myMailbox.wait(&message,

      myMailbox.TIMEOUT::FOREVER, 0);

cout << "data=" <<

       message->data << ", event=" <<

       message->event << endl;

    pool.free(message);

}

int  main( void ) {

    Message *message;

    pool.allocate(&message);

    message->data[0] = 0x30;

    message->dataSize = 1;

    message->event = EVENT::UART0;

    myMailbox.send(message);

}

In many cases a modern firmware developer will use a “pipeline”. A “pipeline is a set of data processing elements connected in series, where the output of one element is the input of the next one” (Wikipedia). A processing element, for example a thread, wakes up and checks the mailbox – the job queue. If the queue is not empty, the thread executes one stage of processing and forwards the processed data to the next thread in the pipeline.

The pipeline task has two methods: add a new job and process the data. A pipeline task – a stage – has a name and keeps a reference to the next stage:

template<typename  ObjectType, typename  Lock, std::size_t  Size>

class  PipelineTask {

public:

 PipelineTask(const  char *name,

 PipelineTask *nextStage = nullptr) :

 name(name),

 nextStage(nextStage){}

 void  doJob();

 void  addJob(ObjectType &data);

protected:

 const  char *name;

 PipelineTask *nextStage;

 CyclicBuffer<ObjectType, Lock, Size> fifo;

};

The add job API adds data to the FIFO:

template<typename  ObjectType, typename  Lock, std::size_t  Size>

void  PipelineTask<ObjectType, Lock, Size>::addJob(ObjectType &data) {

 fifo.add(data);

}

The method doJob() fetches data from the FIFO, increments it – I assume that the data type supports operator++(), pushes the data to the next stage:

template<typename  ObjectType, typename  Lock, std::size_t  Size>

void  PipelineTask<ObjectType, Lock, Size>::doJob() {

 while (!fifo.isEmpty()) {

 ObjectType data;

 fifo.remove(data);

        data++;

cout << "Stage:" << name << ", data=" << data << endl;

 nextStage->addJob(data);

    }

}

A new type MyPipelineTask:

typedef  PipelineTask<int, LockDummy, 3> MyPipelineTask;

Three stages of the pipeline – the third last stage does not have a “next”:

MyPipelineTask pipelineTask3("3");

MyPipelineTask pipelineTask2("2", &pipelineTask3);

MyPipelineTask pipelineTask1("1", &pipelineTask2);

I can invoke stages of the pipeline from interrupts or from a main loop, for example, like this:

void  testPipeline() {

 int data = 0;

    pipelineTask1.addJob(data);

    pipelineTask1.doJob();

    pipelineTask2.doJob();

    pipelineTask3.doJob();

}

The code above generates the output:

Stage:1, data=1

Stage:2, data=2

Stage:3, data=3

The pipeline paradigm can improve utilization of the CPU, pipelines make it easier to leverage multi-core systems.

## Log.

Perfection is achieved, not when there is nothing left to add, but when there is nothing left to take away – Antoine de St. Exupery

In one C project I have seen following code for generating log entries:

enum {

 LOG_LEVEL_INFO,

 LOG_LEVEL_ERROR,

 LOG_LEVEL_LAST,

};

static  const  char *LOG_LEVEL_NAME[] = {"INFO", "ERROR", “UKNOWN”};

#define LOG_INFO(fmt, ...) log_print(__LINE__, LOG_LEVEL_INFO, fmt, ##__VA_ARGS__ )

#define LOG_ERROR(fmt, ...) log_print(__LINE__, LOG_LEVEL_ERROR, fmt, ##__VA_ARGS__ )

static  void  log_print(int line, int level, const  char *fmt, ...)

{

 va_list ap;

 printf("%s: line=%d, msg=", LOG_LEVEL_NAME[level], line);

    va_start(ap, fmt);

 vprintf(fmt, ap);

    va_end(ap);

}

void  testLog(void) {

    LOG_INFO("This is info %d", 1);

    LOG_ERROR("This is error %d", 2);

}

On my machine the code above generates output:

INFO: line=402, msg=This is info 1

ERROR: line=403, msg=This is error 2

There are many calls to the log API and size of the image is important. Calls to log_print() push at least three arguments into the stack. I think that I can save one push – a log level. In the C implementation I would add functions log_print_info(...) and log_print_error(...) which in turn call log_print(), and fix the macros accordingly. In C++ I have a template. The constructor is an exact copy of the original log_print function minus log level:

template <int  Level> class  Log {

public:

 Log(int line, const  char *fmt, ...) {

 va_list ap;

 printf("%s: line=%d, msg=", LOG_LEVEL_NAME[Level], line);

        va_start(ap, fmt);

 vprintf(fmt, ap);

        va_end(ap);

    }

};

The log macros call the constructor:

#define LOG_INFO(fmt, ...) Log<LOG_LEVEL_INFO>(__LINE__, fmt, ##__VA_ARGS__ )

#define LOG_ERROR(fmt, ...) Log<LOG_LEVEL_ERROR>(__LINE__, fmt, ##__VA_ARGS__ )

C++ compiler has duplicated two print log functions for me and saved a push to the stack for every call to the log API. Class log is a “functoid – it is a function on steroids. I can use a functoid based on a regular class instead of a template like this:

class  Log {

public:

 Log(const  char *level) : level(level) {}

 void  print(int line, const  char *fmt, ...) const {

 va_list ap;

 printf("%s: line=%d, msg=", level, line);

        va_start(ap, fmt);

 vprintf(fmt, ap);

        va_end(ap);

    }

protected:

 const  char *level;

};

const  Log LogInfo("INFO");

const  Log LogError("ERROR");

#define LOG_INFO(fmt, ...) LogInfo.print(__LINE__, fmt, ##__VA_ARGS__ )

#define LOG_ERROR(fmt, ...) LogError.print(__LINE__, fmt, ##__VA_ARGS__ )

I have dropped array LOG_LEVEL_NAME and now it is easier to expand an enumeration of log levels. There is only one instance of the print function in the object code. The cost is a couple of words in the data RAM or two objects of the type Log. The code and the data can be placed in the ROM.

Call to vprintf() is not something firmware developers do often. Indeed the code calls vprintf() again and again for the same set of format strings. I can send to the console only the arguments to the vprintf() and the exact location in the source code or the offset in the object file.

Class BinaryLog below handles only arguments of type “int”. A location in the source code is defined by a “unique” file identifier and a source line number:

class  BinaryLog {

public:

 BinaryLog(int fileId, int line, int count, ...);

};

I assume that there is “sendData” API which can send arbitrary number of integers to the console:

BinaryLog::BinaryLog(int fileId, int line, int count, ...) {

 const  int HEADER_SIZE = 3;

 int header[HEADER_SIZE];

    header[0] = fileId;

    header[1] = line;

    header[2] = count;

    sendDataStart();

    sendData(header, HEADER_SIZE);

 va_list ap;

    va_start(ap, count);

 for (int j=0; j < count; j++) {

 int arg = va_arg(ap, int);

        sendData(arg);

    }

    va_end(ap);

    sendDataEnd();

}

API “send data” in my simulation looks like this:

inline void  sendData(const  int data) {

cout << dec << data << " ";

}

inline void  sendDataStart() {cout << endl;}

inline void  sendDataEnd() {cout << endl;}

void  sendData(const  int *data, int count) {

 for (int i = 0;i < count;i++) {

cout << hex << data[i] << " ";

    }

}

Two macro definitions call constructor BinaryLog. Macro ARGUMENTS_COUNT is fairly portable and shall return number of arguments in a variadic macro:

#define ARGUMENTS_COUNT(...) (sizeof((int[]){__VA_ARGS__})/sizeof(int))

#define LOG_INFO(fmt, ...) BinaryLog(FILE_ID, __LINE__, ARGUMENTS_COUNT(__VA_ARGS__), __VA_ARGS__ )

#define LOG_ERROR(fmt, ...) BinaryLog(FILE_ID, __LINE__, ARGUMENTS_COUNT(__VA_ARGS__), __VA_ARGS__ )

The file identifier is generated by the compiler from the file name during the build. I use a simple hash function. A real thing, an MD5 hash, can be found in [7].

constexpr  int  hashData(const  char* s, int accumulator) {

 return *s ? hashData(s + 1, (accumulator << 1) | *s) : accumulator;

}

constexpr  int  hashMetafunction(const  char* s) {

 return hashData(s, 0);

}

constexpr  int FILE_ID = hashMetafunction(__FILE__);

Usage example:

void  testBinaryLog(void) {

    LOG_INFO("This is info %d %d", 1, 2);

    LOG_ERROR("This is error %d %d %d", 0, 1, 2);

}

In my system the test function produces output:

262140 511 2 1 2 262140 512 3 0 1 2

All I need now is a short script ([8]) that calculates file identifiers for all my source files, finds the right file according to the file identifier 262140, parses lines 511 and 512 in the C++ file and produces two readable output lines:

This is info 1 2

This is error 0 1 2

Yet another post build script can ensure that format strings correctly represent arguments in calls to the macros.

By removing an expensive call to vprintf() I saved lot of CPU cycles, lot of ROM and some bandwidth. The binary log API does not use any static data and the API is thread safe. My system generates logs which require additional processing before they can be read by a human, but there are situations when this is a small price to pay.

In the next example I assume that the application is statically linked and all addresses are getting resolved at build time. I can get rid of the line number and file identifier and, instead, use value of the program counter. Code below will work only for GCC. GCC compiler allows to get the address of a label.

The BinaryLog constructor accepts an address of the log entry:

BinaryLog::BinaryLog(void *address, int count, ...) {

 const  int HEADER_SIZE = 2;

 int header[HEADER_SIZE];

    header[0] = ((uintptr_t)address) & INTMAX_MAX;

    header[1] = count;

    sendDataStart();

    sendData(header, HEADER_SIZE);

 va_list ap;

    va_start(ap, count);

 for (int j=0; j < count; j++) {

 int arg = va_arg(ap, int);

        sendData(arg);

    }

    va_end(ap);

    sendDataEnd();

}

The magic macros generate unique labels and forward the labels address to the BinaryLog constructor:

#define TOKEN_CAT(x, y) x ## y

#define TOKEN_CAT2(x, y) TOKEN_CAT(x, y)

#define LABEL TOKEN_CAT2 (logLabel_, __LINE__)

#define LOG_INFO(fmt, ...) {  \

        LABEL:\

        BinaryLog(&&LABEL, ARGUMENTS_COUNT(__VA_ARGS__), __VA_ARGS__ ); \

}

A post build script shall read a map file generated by the linker, collect list of labels according to the pattern logLabel_XX and process format strings in the source code.

It is not done yet. I can save one more argument – an address of the label. GCC allows to find out a return address of the function. The functoid can look like this:

class  FastLog {

public:

 FastLog(int count, ...);

};

The FastLog constructor calls __builtin_return_address() to get the return address:

FastLog::FastLog(int count, ...) {

 const  int HEADER_SIZE = 2;

 int header[HEADER_SIZE];

 void *retAddress =

       __builtin_extract_return_addr(

       __builtin_return_address(0));

    header[0] = ((uintptr_t)retAddress) & INTMAX_MAX;

    header[1] = count;

    sendDataStart();

    sendData(header, 2);

 va_list ap;

    va_start(ap, count);

 for (int j=0; j < count; j++) {

 int arg = va_arg(ap, int);

        sendData(arg);

    }

    va_end(ap);

    sendDataEnd();

}

And the macros do not forward an address anymore:

#define LOG_INFO(fmt, ...)\

  FastLog(ARGUMENTS_COUNT(__VA_ARGS__), __VA_ARGS__ );

If I need to support two or more configurable destinations – log sinks – I need only to add to the functoid FastLoad a method which switches the destination. The logic of the code remains encapsulated in the class. They say in the academic world that the encapsulation is a good thing. I could convert the FastLog class into a template and provide Lock interface:

template <typename  Lock> class  SystemLog {

public:

 SystemLog(int count, ...);

};

When I call the system log from interrupts I need to disable the interrupts. For the task level system log a mutex is probably adequate. The C alternative with the similar performance would require a macro.

## Software Timers.

C++: Hard to learn and built to stay that way.

So far I have demonstrated fairly simple software components, such as a mutex or a cyclic buffer. In this chapter I am going to implement a software timer.

Modern operating systems provide timers API. Typically an application can start a timer with arbitrary expiration time. When the timer expires the operating system calls the application hook from a dedicated timer thread or a system interrupt. Performance of such API can degrade quickly if an application starts a lot of different timers. There is usually no control over the priority of the process which handles the timers. The API presented here allows an application to handle all timer related code in a single context or in multiple contexts running with different priorities.

The software timers API will have O(1) complexity. The API is going to be thread safe. The source code for the software timer can be found in [9].

You already know the object-oriented design routine. Let's declare a timer object first. A timer object keeps a unique timer identifier.

A unique timer identifier can be used to solve possible race conditions between stopTimer and timerExpired. Consider following scenario: timer “a” is started by context A. Timer “a” is stopped by context A, but too late - timer “a” has just expired and the application code handling the expiration is running. Depending on the implementation of the application callback, the processing of the event can be done asynchronously. Meanwhile the same timer object can be allocated and modified by context B, a different thread. If context A keeps identities of all started timers, the application callback can check if the timer identifier is on the list of running timers. If the timer was stopped, the callback can ignore the timer expiration. Using the reference to the timer object itself for such bookkeeping is not good because the pool of timer objects is probably a shared resource.

When starting a timer the user can supply optional pointer to the application data, a cookie. The timer class could be a template like this:

template<typename  CookieType> class  Timer {

protected:

 CookieType  cookie;

};

I want to simplify the interface and avoid using of virtual methods – more on virtual methods in a moment – in the timer objects. Instead of objects of an arbitrary type a timer object will keep a pointer to the application data.

A user can access the timer's data only via the public methods: getters and setters. This approach helps to maintain the code in the future.

The class Timer implements a constructor without arguments. I want to be able to create a static array of timers without too much of trouble. The TimerList class, which is not declared yet, is a friend class of the class Timer and can call protected methods of the Timer. Method start() is protected, because application shall start timers using the TimerList methods.

class  Timer {

public:

 Timer();

 inline  void  stop();

 bool  isRunning() const;

 TimerID  getId() const;

 inline  uintptr_t  getApplicationData() const;

 SystemTime  getStartTime() const;

protected:

 friend  class  TimerList;

 TimerID  id;

 uintptr_t  applicationData;

 bool  running;

 SystemTime  startTime;

 inline  void  start();

 inline  void  setApplicationData(uintptr_t applicationData);

 inline  void  setId(TimerID id);

 inline  void  setStartTime(SystemTime systemTime);

};

The implementation of the methods is straightforward:

Timer::Timer() {

    stop();

}

TimerID  Timer::getId() const {

 return  id;

}

SystemTime  Timer::getStartTime() const {

 return  startTime;

}

bool  Timer::isRunning() const {

 return  running;

}

void  Timer::stop() {

 running = false;

}

void Timer::start() {

 running = true;

}

void  Timer::setApplicationData(uintptr_t applicationData) {

 this->applicationData = applicationData;

}

uintptr_t  Timer::getApplicationData() const {

 return  applicationData;

}

void  Timer::setId(TimerID id) {

 this->id = id;

}

void  Timer::setStartTime(SystemTime systemTime) {

 this->startTime = systemTime;

}

The system time is often a tick incremented by an interrupt or read from the hardware. In this example I use size_t type. In a more advanced design the System Time type and the Timeout type could be two classes. The timer API only needs a function with the signature “bool isTimerExpired(SystemTime, Timeout, SystemTime)”. In the following implementation I handle SystemTime wrap around, assuming that timers timeouts are small relatively to the SystemTime maximum value.

typedef  size_t  SystemTime;

typedef  size_t  Timeout;

static  inline  bool  isTimerExpired(SystemTime startTime, Timeout timeout,

 SystemTime currentTime) {

 bool timerExpired = false;

 SystemTime timerExpiartionTime = startTime + timeout;

    timerExpired = timerExpired

            || ((timerExpiartionTime >= currentTime)

                    && (startTime < currentTime));

    timerExpired = timerExpired

            || ((timerExpiartionTime >= currentTime)

                    && (startTime > currentTime));

    timerExpired = timerExpired

            || ((timerExpiartionTime <= currentTime)

                    && (startTime > currentTime)

                    && (timerExpiartionTime < startTime));

 return timerExpired;

}

My API has an enumeration of possible return codes of the C+11 kind. C++11 “enum class” is not an integer and can not be converted to an integer. A member of one enumeration can not be assigned to a member of another enumeration.

enum  class TimerError {

 Ok, Expired, Stopped, Illegal, NoFreeTimer, NoRunningTimers

};

I need an application callback which handles timer expiration. The callback could be a template function in a more advanced design:

typedef  void (*TimerExpirationHandler)(const  Timer& timer);

I am going to provide a synchronization API via an argument to the constructor. In the base class TimerLock I set the get/release interface to zero. The lock API is going to be implemented by the derivative. Typical performance overhead of a virtual function is 1 or 2 opcodes.

class  TimerLock {

public:

 virtual  void  get() = 0;

 virtual  void  release() = 0;

protected:

 virtual  ~TimerLock() {}

};

class  TimerLockDummy : public  TimerLock {

public:

 virtual  void  get() {}

 virtual  void  release() {}

protected:

};

I need a cyclic buffer that uses the dynamic allocation from the heap via operator new[]. In the previous chapters I have discussed the operator new[] and situations when an allocation from the memory heap is not possible.

template<typename  ObjectType, typename  Lock>

class  CyclicBufferDynamic {

public:

 inline  CyclicBufferDynamic(size_t size);

 ~CyclicBufferDynamic() {

    }

 inline  bool  isEmpty();

 inline  bool  isFull();

 inline  bool  add(ObjectType object);

 inline  bool  remove(ObjectType *object);

 inline  bool  getHead(ObjectType *object);

private:

 void  errorOverflow() {

    }

 void  errorUnderflow() {

    }

 size_t  increment(size_t index);

 ObjectType *data;

 size_t  head;

 size_t  tail;

 size_t  size;

};

Constructor calls the operator new[] to allocate array of pointers. There is a static assert which insures that the template class is used only for pointers:

template<typename  ObjectType, typename  Lock>

inline  CyclicBufferDynamic<ObjectType, Lock>::

CyclicBufferDynamic(size_t size) {

 this->head = 0;

 this->tail = 0;

 this->size = size;

 this->data = new  ObjectType[size];

 static_assert(sizeof(ObjectType) <= sizeof(uintptr_t), "CyclicBuffer is intended to work only with integer types or pointers");

}

The rest of the code is similar to the previous implementation:

template<typename  ObjectType, typename  Lock>

inline  bool  CyclicBufferDynamic<ObjectType, Lock>::

isEmpty() {

 bool res = (this->head == this->tail);

 return res;

}

template<typename  ObjectType, typename  Lock>

inline  bool  CyclicBufferDynamic<ObjectType, Lock>::

isFull() {

 size_t tail = increment(this->tail);

 bool res = (this->head == tail);

 return res;

}

template<typename  ObjectType, typename  Lock>

inline  bool  CyclicBufferDynamic<ObjectType, Lock>::

add(ObjectType object) {

 Lock  lock;

 if (!isFull()) {

 data[this->tail] = object;

 this->tail = increment(this->tail);

 return  true;

} else {

        errorOverflow();

 return  false;

    }

}

template<typename  ObjectType, typename  Lock>

inline  bool  CyclicBufferDynamic<ObjectType, Lock>::

remove(ObjectType *object) {

 Lock  lock;

 if (!isEmpty()) {

*object = data[this->head];

 this->head = this->increment(this->head);

 return  true;

} else {

        errorUnderflow();

 return  false;

    }

}

template<typename  ObjectType, typename  Lock>

inline  bool  CyclicBufferDynamic<ObjectType, Lock>::

getHead(ObjectType *object) {

 Lock lock;

 if (!isEmpty()) {

*object = data[this->head];

 return  true;

} else {

        errorUnderflow();

 return  false;

    }

}

template<typename  ObjectType, typename  Lock>

size_t  CyclicBufferDynamic<ObjectType, Lock>::

increment(size_t index) {

 if (index < this->size) {

 return (index + 1);

} else {

 return 0;

    }

}

Use of LockDummy is deliberate here. I do not need the ring buffers storing pointers to objects of the class Timer to be reentrant:

typedef  CyclicBufferDynamic<Timer*, LockDummy> TimerCyclicBuffer;

A list of timers keeps timers with the same timeout. The timers expiration time depends on the start time. The timer API assumes that there are finite and relatively small number of different timers, timers with different timeout, in the system. Often I know what timers I need in the system before I start to write the code. The TimerList is an example of “object composition” – I compose simple objects, such as FIFOs, into a more complex one. Instead of a ring buffer I could use a memory pool for the list of free timers freeTimers.

class  TimerList {

public:

 TimerList(size_t size, Timeout timeout,

 TimerExpirationHandler expirationHandler,

 TimerLock &timerLock,

 bool callExpiredForStoppedTimers=false) :

 timeout(timeout),

 expirationHandler(expirationHandler),

 callExpiredForStoppedTimers(

       callExpiredForStoppedTimers),

 freeTimers(size),

 runningTimers(size),

 timerLock(timerLock) {

 Timer *timers = new  Timer[size];

 for (size_t i = 0;i < size;i++) {

 freeTimers.add(&timers[i]);

       }

    }

TimerError processExpiredTimers(SystemTime);

 enum TimerError startTimer(

 SystemTime currentTime,

 SystemTime &nearestExpirationTime,

 uintptr_t applicationData = 0,

 const  Timer **timer = nullptr);

 inline  enum TimerError stopTimer(Timer &timer) {

        timer.stop();

 return TimerError::Ok;

    }

 SystemTime  getNearestExpirationTime() {

 return  nearestExpirationTime;

    }

protected:

 inline  static  TimerID  getNextId();

 enum TimerError _startTimer(

 SystemTime currentTime,

 SystemTime &nearestExpirationTime,

 uintptr_t applicationData = 0,

 const  Timer **timer = nullptr);

TimerError _processExpiredTimers(SystemTime);

 Timeout  timeout;

 TimerExpirationHandler  expirationHandler;

 bool  callExpiredForStoppedTimers;

 SystemTime  nearestExpirationTime;

 CyclicBufferDynamic<Timer*, LockDummy> freeTimers;

 CyclicBufferDynamic<Timer*, LockDummy> runningTimers;

 TimerLock &timerLock;

};

Protected methods of the TimerList class are not necessary thread safe. For example getNextId() implementation is not thread safe. Only a child class or a public method can access protected class members and shall take care of the synchronization:

TimerID  TimerList::getNextId() {

 static  TimerID id = 0;

    id++;

 return id;

}

enum TimerError TimerList::startTimer(SystemTime currentTime,

 SystemTime &nearestExpirationTime, uintptr_t applicationData,

 const  Timer **timer) {

 timerLock.get();

TimerError res = TimerList::_startTimer(

        currentTime,

        nearestExpirationTime,

        applicationData,

        timer);

 timerLock.release();

 return res;

}

The protected method _startTimer() moves a timer from the list of the free timers to the list of the running timers

enum TimerError TimerList::_startTimer(

 SystemTime currentTime,

 SystemTime &nearestExpirationTime,

 uintptr_t applicationData,

 const  Timer **timer) {

 Timer* newTimer;

 if (freeTimers.isEmpty())

 return TimerError::NoFreeTimer;

 freeTimers.remove(&newTimer);

    newTimer->setStartTime(currentTime);

    newTimer->setApplicationData(applicationData);

    newTimer->setId(getNextId());

    newTimer->start();

 runningTimers.add(newTimer);

 Timer* headTimer;

 runningTimers.getHead(&headTimer);

nearestExpirationTime = headTimer->getStartTime() + timeout;

 this->nearestExpirationTime = nearestExpirationTime;

 if (timer != nullptr)

        *timer = newTimer;

 return TimerError::Ok;

}

The method _processExpiredTimers() moves stopped and expired timers from the head of the list of the running timers to the list of the free timers. A user of the timer list shall call processExpiredTimers() which will call the application callback for expired timers. The user shall call getNearestExpirationTime() to get expiration time for the next timer, time when processExpiredTimers() shall be called again. Difference between the nearestExpirationTime and currentTime can be used, for example, in the system call to sleep(). Timers on the runningTimers list is ordered by expiration time. I always add timers to the tail and timeout is the same for all timers on the list. The protected method is not reentrant:

TimerError TimerList::_processExpiredTimers(

 SystemTime currentTime) {

 Timer* timer;

 while (!runningTimers.isEmpty()) {

 if (!runningTimers.getHead(&timer))

 break;

 bool timerExpired = isTimerExpired(timer->getStartTime(), timeout,

                currentTime);

 bool timerIsRunning = timer->isRunning();

 bool callExpirationHandler = timerExpired;

        callExpirationHandler = callExpirationHandler

|| (!timerIsRunning && callExpiredForStoppedTimers);

 if (callExpirationHandler) {

            (expirationHandler)(*timer);

        }

 if (timerExpired || !timerIsRunning) {

 runningTimers.remove(&timer);

 freeTimers.add(timer);

        }

 if (!timerExpired && timerIsRunning) {

 nearestExpirationTime = timer->getStartTime() + timeout;

 break;

        }

    }

 if (!runningTimers.isEmpty())

 return TimerError::Ok;

 else

 return TimerError::NoRunningTimers;

}

Public method is reentrant:

TimerError TimerList::processExpiredTimers(

 SystemTime currentTime) {

 timerLock.get();

TimerError res = TimerList::_processExpiredTimers(currentTime);

 timerLock.release();

 return res;

}

I group timer lists in “sets”. For example, a set of relatively long, low priority timers with timeouts 5s, 20s, 60s and a set of high priority timers. Different sets can be served by threads running in different priorities. I know what timers types belong to a set at the compilation time.

The TimerSet class is an example of “object acquaintance” ([4], [5]). There is a “knows of” relationship between the TimerSet class and the TimerList class. The component objects, lists of timers, may be accessed through other objects without going through the aggregate object, TimerSet. The components objects may survive the aggregate object.

class  TimerSet {

public:

 TimerSet(const  char* name, int size) :

 name(name), listCount(size) {

 this->size = size;

 timerLists = new  TimerList*[size];

    }

 const  char *getName() {

 return  name;

    }

TimerError processExpiredTimers(SystemTime currentTime,

 SystemTime& expirationTime);

 bool  addList(TimerList* list);

protected:

 const  char *name;

 TimerList **timerLists;

 size_t  listCount;

 size_t  size;

};

The addList API fills the array timerLists:

bool  TimerSet::addList(TimerList* list) {

 if (listCount < size) {

 timerLists[listCount] = list;

 listCount++;

 return  true;

} else {

 return  false;

    }

}

Method processExpiredTimers() calls the corresponding API in all timer lists and conveniently returns next time the method should be called. Complexity of the method is O(number of timer lists):

TimerError TimerSet::processExpiredTimers(

 SystemTime currentTime, SystemTime &expirationTime) {

 TimerList* timerList;

 size_t i;

 SystemTime nearestExpirationTime;

 bool res = false;

 for (i = 0; i < listCount; i++) {

timerList = timerLists[i];

        TimerError timerRes = timerList->processExpiredTimers(currentTime);

 if (timerRes == TimerError::Ok) {

 SystemTime listExpirationTime =

                    timerList->getNearestExpirationTime();

 if (res) {

 if (nearestExpirationTime > listExpirationTime) {

                    nearestExpirationTime = listExpirationTime;

                }

            }

 else {

                nearestExpirationTime = listExpirationTime;

            }

res = true;

        }

    }

 if (res)

 return TimerError::Ok;

 else

 return TimerError::NoRunningTimers;

}

Finally a usage example:

static  void  mainExpirationHandler(const  Timer& timer) {

 TimerID timerId = timer.getId();

 uintptr_t data = timer.getApplicationData();

cout << "Expired id=" << timerId << ",appdata=" << data << endl;

}

TimerLockDummy timerLock;

static  TimerList timerList(3, 3, mainExpirationHandler, timerLock);

int  main()

{

 SystemTime currentTime = 0;

 for (int i = 0;i < 3;i++) {

 SystemTime nearestExpirationTime;

        TimerError err =

          timerList.startTimer(currentTime,

          nearestExpirationTime, i);

 if (err == TimerError::Ok) {

cout << "nearestExpirationTime=" <<

nearestExpirationTime << endl;

        }

 else {

cout << "timer start failed for timer "

<< i << endl;

        }

    }

    timerList.processExpiredTimers(3);

 return 0;

}

Suppose, that I need two different Timer types – one with the timer identifier and another without. I subclass a larger timer class from a new base class, where the timer identifier setter is an empty method. The conversion will involve no changes in the TimerList class. The TimerList class can work with any “interface” ([10]) implementing the Timer class API – the Timer class “contract”.

In a different system the system time is a structure containing the following fields: hours, minutes, seconds and milliseconds. The TimerList class can handle this system time if there are two operators defined: compare and add.

Yet in another system I can not work with dynamically allocated cyclic buffers. I convert the TimerList class into a template class with a size of the list argument. The TimerSet class can work with any list of timers implementing processExpiredTimers() API. I subclass the TimerList class – now a template – from an abstract base class with a pure virtual method processExpiredTimers(). The code modification will not affect the logic in the TimerList or TimerSet methods.

In some application I start timers, stop timers and handle the expiration in the same thread. I do not need reentrant API. I can save CPU cycles by using the dummy lock for the timer list.

Once written and debugged, the TimerList and TimerSet classes serve me in many different situations. I could do the same thing in C using void* here and there and some type castings. C++ fans would argue that the C++ alternative is more elegant and type safe.

## Lambda.

Analog-to-digital converter (ADC) is a device that converts a continuous physical quantity, for example  voltage, to a digital number that represents the quantity's amplitude ([11]). In my application I want to read ADC devices, collect samples in a ring buffer, run a simple low path filter ([12]). The ADC class looks like this:

template<typename  ObjectType, std::size_t  Size> class  ADC {

public:

 inline  ADC(ObjectType initialValue=0);

 typedef  ObjectType (*Filter)(ObjectType current,

 ObjectType sample);

 inline  void  add(ObjectType sample, Filter filter);

 inline  ObjectType  get();

protected:

 CyclicBuffer<ObjectType, LockDummy, Size> data;

 ObjectType  value;

};

The ADC constructor sets an initial value for the calculated result:

template<typename  ObjectType, std::size_t  Size>

ADC<ObjectType, Size>::

ADC(ObjectType initialValue) {

 value = initialValue;

}

Method “get” returns the calculated value:

template<typename  ObjectType, std::size_t  Size>

ObjectType  ADC<ObjectType, Size>::

get() {

 return  value;

}

Method “add” updates the cyclic buffer and calls the “filter” to calculate a new ADC value:

template<typename  ObjectType, std::size_t  Size>

void  ADC<ObjectType, Size>::

add(ObjectType sample, Filter filter) {

 data.add(sample);

 value = filter(value, sample);

}

The function pointer Filter is a template function. Instantiation of a template function would require quite a few C++ lines. In the following usage example I employ an anonymous function – a lambda function:

static  void  testADC()

{

 static  ADC<double, 4> myAdc(3.0);

cout << "ADC=" << myAdc.get() << endl;

 for (int i = 0;i < 10;i++) {

        myAdc.add(4.0,

                [](double current, double sample) {

 return current+0.5*(sample-current);

                }

        );

    }

cout << "ADC=" << myAdc.get() << endl;

}

On my desktop this code produces output:

ADC=3

ADC=3.99902

Lambda functions save the code lines. Inline lambda functions help the C++ compiler to optimize the code. In the assembler code for my Intel based machine the call to the method “add” is replaced by update of the CyclicBuffer data and the filter code.

A composition of JobThread, HardwareModule and ADC classes creates a fully functional ADC API. I am skipping details in the example below:

class  HardwareModuleADC : HardwareModule {

public:

 double  read();

protected:

};

class  ReadADC {

public:

 ReadADC() : myAdc(3.0) {}

 void  run(void) {

 double sample = hardwareModuleADC.read();

 myAdc.add(sample,

            [](double current, double sample) {

 return current+0.5*(sample-current);

            });

    }

protected:

 ADC<double, 4> myAdc;

 HardwareModuleADC  hardwareModuleADC;

};

JobThread<ReadADC> jobThreadReadADC;

## Fixed point arithmetic.

Three out of two people have trouble with fractions.

Often in the application which requires analog-to-digital converters I need fixed-point arithmetic ([13]). Fixed-point arithmetic is significantly faster – from 2x to 3x times – than the scalar floating-point code. Unfortunately, fixed-point arithmetic is not a part of the C++ standard. There is support in the GCC compiler ([14]). For a great example of fixed-point arithmetic API see Kurt Guntheroth implementation ([15]). The following example is a simple implementation of four arithmetic operations. In the code snippet below “lhs” and “rhs” stand for left-hand side and right-hand side – two arguments on the sides of an arithmetic operator. The unnamed enumeration with a single member “scale” is a trick which helps to create a constant member of the template.

template<typename  IntType, const  int  FRACTION_BITS>

class  FixedPoint

{

public:

 typedef  FixedPoint<IntType, FRACTION_BITS> T;

 FixedPoint(){}

 FixedPoint(double d) {v = (IntType)(d*scale);}

 FixedPoint(const  T &rhs) : v(rhs.v) { }

 T& operator=(const  T &rhs) {v = rhs.v;return *this;}

 double  toDouble() const {return  double(v)/scale;}

 friend  T  operator+(T lhs, const  T &rhs) {T r;r.v = lhs.v + rhs.v;return r;}

 friend  T  operator-(T lhs, const  T &rhs) {T r;r.v = lhs.v - rhs.v;return r;}

 friend  T  operator*(T lhs, const  T &rhs) {

 T r;

       r.v = (lhs.v * rhs.v) / scale;

 return r;

    }

 friend  T  operator/(T lhs, const  T &rhs) {

 T r;

       r.v = (lhs.v * scale)/rhs.v;

 return r;

    }

 friend  bool  operator==(const  T &lhs, const  T &rhs) {return lhs.v == rhs.v;}

protected:

 int  v;

 enum{scale  = 1<<FRACTION_BITS};

};

A usage example:

static  void  FixedPointTest() {

 typedef  FixedPoint<int_fast16_t, 3> FixedPoint_3;

 FixedPoint_3 value(3.43188);

    value = (2*(value+FixedPoint_3(1.4)-FixedPoint_3(1.4)))/2;

cout << value.toDouble() << endl;

}

The usage example output:

3.375

I could extend the composition ReadADC from the previous chapter by an instance of the fixed-point arithmetic template. The lambda function could look like this:

class  ReadADC {

public:

 ReadADC() : myAdc(3.0) {}

 typedef  FixedPoint<int_fast16_t, 3> FPADC;

 void  run(void) {

 FPADC sample = FPADC(hardwareModuleADC.read());

 myAdc.add(sample,

            [](FPADC current, FPADC sample) {

 return current+(sample-current)/2;

            });

    }

protected:

 ADC<FPADC, 4> myAdc;

 HardwareModuleADC  hardwareModuleADC;

};

# Interview questions.

The clever shall inherit the earth. - Economist, Jan 20th, 2011

I know that for you and me programming is not about money. Still, some of my dear readers have to think about the families. A programmer is one of the top paying professions in the world.

“As technology advances, the rewards to cleverness increase. Computers have hugely increased the availability of information, raising the demand for those sharp enough to make sense of it. In 1991 the average wage for a male American worker with a bachelor's degree was 2.5 times that of a high-school drop-out; now the ratio is 3“([16]).

A skilled software developer can get a job paying 6 figures or an equivalent in the US, UK, Canada, Australia and other countries. Between you and your dream job lies a professional interview.

No worries if you often fail to answer brain teasers. In many companies this specific class of interview questions is forbidden. There is a very small group of people who is capable to find a solution for a hard question in real time. Be sure, that these people are already hired by Googles and Apples of the world and they are not competing with you for the job. Your interviewer most likely does not expect the correct answer, but mainly wants to see how you approach tough problems.

In this chapter I have attempted to gather a small set of questions which you can encounter when applying for a job of a real-time, embedded, firmware developer. I skip graphs, binary trees, jars of water because these type of problems rarely appear in technical interviews of embedded system developers.

## General programming.

Q. What are limitations of the code below? Are there any potential problems?

#define LOG_CAT(fmt, ...) print_log("%s %d" fmt, __FUNCTION__, __LINE__, ##__VA_ARGS__ )

static  inline  void  print_log(const  char *fmt, ...)

{

 va_list ap;

    va_start(ap, fmt);

 vprintf(fmt, ap);

    va_end(ap);

}

A. Macro LOG_CAT assumes that “fmt” is a const string. For example, the following code will not compile:

void  testLogCat()

{

 char *f = "Test %d";

    LOG_CAT(f, 1);

}

Call to function vprintf() is not reentrant on some platforms. On other platforms vprintf() uses a large buffer on the stack which can create problems if called from interrupts.

Q. What is wrong with the following interrupt routine? Try to point as many potential problems as possible:

uint32_t Tick = 0;

int  MyTickIsr()

{

    Tick++;

 printf("%s", __FUNCTION__);

 return 0;

}

A.

1.  Usually interrupt handlers should not return a value. The result of returning a value depends on the operating system.
2.  Incrementing of the global variable is a read-modify-write operation. Another thread can be in the middle of modifying the value of the tick when the interrupt handle is getting called.
3.  In many systems printf() is not a reentrant API. Call to printf() can cause interrupt stack overflow if printf() uses the stack to allocate the string. Depending on the implementation call to printf() can require significant time.

Q. List most popular ways to implement a FIFO between “producer” and “consumer”. Assume that producer generates data blocks of different size between 1 and 256 bytes.

A.

1.  Ring buffer of pointers where every pointer is a linked list of, for example, 16 bytes data blocks . Data blocks are allocated by the producer from the linked list of free blocks.
2.  Ring buffer of pointers referencing data blocks 256 bytes each. Data blocks are allocated by the producer from the linked list of free blocks.
3.  Ring buffer of data where each chunk of data is prepended by the data block size.

Be prepared to discuss pros and cons of every approach in terms of memory and performance, “skb” buffers in the Linux kernel, DMA descriptors, zero copy data processing.

Q. Write a program to find whether a machine is big endian or little endian.

A. In run-time this function can be used:

int  isLittleEndian() {

 short  int data = 0x0001;

 char *byte = (char *) &data;

 return (byte[0] ? 1 : 0);

}

In compilation time this macro:

#define IS_LITTLE_ENDIAN (*(uint16_t *)"\0\xff" >= 0x100)

In Linux we have a macro BYTE_ORDER. In GCC we have macros __LITTLE_ENDIAN__, __BIG_ENDIAN__, __BYTE_ORDER__.

Q. Write a class such that no other class can be inherited from it.

A. The solution is based on Singleton design pattern – a class with a private constructor:

class  YouCanNotInheritMe;

class  Singleton {

private:

 Singleton() {}

 friend  YouCanNotInheritMe;

};

class  YouCanNotInheritMe : virtual  public  Singleton {

public:

 YouCanNotInheritMe(){}

};

I can create an object of type YouCanNotInheritMe:

YouCanNotInheritMe youCanNotInheritMeObject;

An attempt to inherit the class YouCanNotInheritMe will fail with error “Singleton::Singleton() is private ”:

class  TryToInheritAnyway : YouCanNotInheritMe {

public:

 TryToInheritAnyway() {}

};

In C++11 you can use the word final:

class  FinalClass  final {

public:

 FinalClass() {}

};

Q. Is there a bug in the following code?

class  A {

public:

 A() : isDone(false) {}

 virtual  void  m1() = 0;

 void  m2() {

        m1();

 MutexAB m;

 isDone = true;

    }

 virtual  ~A() {

 MutexAB m;

 while (!isDone) {}

    }

protected:

 bool  isDone;

};

class  B : public  A {

public:

 void  m1() {}

 virtual  ~B() {}

};

void  testAB() {

 B *b = new  B;

    std::thread t1{ [=] {

        b->m1();

        b->m2();

    }};

    std::thread t2{ [=] {

 delete b;

    }};

}

A. Thread t2 can destroy the class object b and destroy virtual table as well while thread t1 is calling the virtual method m1\. C++ compiler can modify the virtual table pointer the moment code enters class A, the base class, destructor. When thread t1 kicks in it can discover that pointer b->m1 is not initialized.

Q. Is there a bug in the following code?

typedef  struct {

 int  f1 : 8;

 int  f2 : 8;

} myDataT;

static  myDataT myData;

void  testMyData() {

    std::thread t1{ [=] {

        myData.f1 = 0;

    }};

    std::thread t2{ [=] {

        myData.f2 = 1;

    }};

}

A. On 32 bits architecture C++ compiler will place bit fields f1 and f2 in the same 32 bits location. Write to the bit fields f1 and f2 is implemented as read-modify-write operation. There is a race between threads t1 and t2. For example, t1 reads myData, t2 interrupts t1, t2 continues to the completion and modifies f2, t1 resumes and completes write to the field f1 using old value for the field f2, field f2 remains unchanged.

Q. In the code below one of the functions consistently outperforms another. Why?

static  struct {

 int  a[128];

 int  b[128];

 int  c[128];

} dataArray;

void  initDataArrayB() {

 memset(dataArray.a, 0, sizeof(dataArray.a));

 memset(dataArray.b, 0, sizeof(dataArray.b));

}

void  initDataArrayC() {

 memset(dataArray.a, 0, sizeof(dataArray.a));

 memset(dataArray.c, 0, sizeof(dataArray.c));

}

A. In some architectures the CPU can try to predict data usage and load the data cash lines accordingly. Usually a single line in the cash memory is 64 or 128 bytes. In the function initDataArrayC when the second memset is called the data cache will likely contain the field “a” and all or part of the field “b” – CPU predicts sequential writes. The function initDataArrayC writes to the filed “c” which causes data cache line flush and slows down the execution of the second memset().

Q. What single modification of the code below could improve performance of the function testFastSum?

class  FastSum {

public:

 FastSum(int delta) : delta(delta) {}

 virtual  int  sum(int a) { return  delta+a;}

 virtual  ~FastSum() {}

 protected:

 int  delta;

};

void  testFastSum(int delta, int *result, int count) {

 FastSum fastSum(delta);

 for (int i = 0;i < count;i++) {

        result[i] = fastSum.sum(i);

    }

}

A. Devirtualization – replacing of the virtual method sum() by a non-virtual one – can help. Replacing a virtual call by a non-virtual one can save 2-3 instructions per iteration. If the C++ compiler does a decent job of devirtualization (GCC 4.8 does not) next option would be to ensure that the compiler inlines the constructor FastSum and the method sum.

Q. There is a race condition in the code below. What is it?

class  LazyInitialization {

 static  LazyInitialization *getInstance() {

 if (instance == nullptr) {

 MutexAB m;

 if (instance == nullptr) {

 instance = new  LazyInitialization();

            }

        }

 return  instance;

    }

private:

 LazyInitialization();

 static  LazyInitialization *instance;

};

LazyInitialization *LazyInitialization::instance = nullptr;

A. Thread A enters synchronized section and initializes the static variable “instance”. The constructor of the class LazyInitialization is probably not called yet, but the variable “instance” is probably already set. The exact order of the operations depends on the compiler. At this moment thread B enters the method getInstance() and returns an invalid pointer – a pointer to the object which is not completely initialized. Another problem is that the assignment of the address, a 32 or 64 bits or something else variable, is not necessary an atomic operation and can involve two write transactions to the memory. The code can be fixed by declaring the variable “instance” an atomic variable:

atomic<LazyInitialization*> LazyInitialization::instance(nullptr);

Q. Explain rvalue and lvalue. What is the difference between ++x and x++?

A. Rvalues are temporaries that evaporate at the end of the full-expression in which they live ("at the semicolon").  For example, 1729 , x + y , std::string("meow") , and x++ are all rvalues. Lvalues name objects that persist beyond a single expression.  For example, obj , *ptr , ptr[index] , and ++x are all lvalues. The expression x++ is an rvalue.  It copies the original value of the persistent object, modifies the persistent object, and then returns the copy. This copy is a temporary. Both ++x and x++ increment x, but ++x returns the persistent object itself, while x++ returns a temporary copy.

Q. Explain what happens in every line of the following function:

const char *dataTest()

{

 // 1.

 char *a = "123";

 // 2.

 char b[] = "123";

 // 3.

 const  char *c = "123";

 // 4.

 static  char d[] = "123";

 // 5.

a[0] = '0';

 // .................

 // 6.

 return a;

 // .................

 // 7.

 return c;

 // ................

 // 8.

 return b;

}

A.

1.  Assign local variable 'a' address of the constant data ['1','2','3',0]. Some compilers will generate a warning – assignment const pointe to non-const pointer.
2.  Run-time copy of the data ['1','2','3',0] to local (on the stack) array. The initialization of the array 'b' will be done every time the function is being called.
3.  Same as 1, but compilation warning is fixed.
4.  Run-time copy of the array ['1','2','3',0] to the static variable 'd'. The copy is done only once by the code loader.
5.  Attempt to modify the constant data. On some architectures constant data is read only and this line can cause an exception.
6.  Return pointer to the constant data. The pointer is global and exists in the program address space.
7.  Same as 6
8.  Return address of the local (stack) variable. Data at the address 'b' depends on the architecture.

Q. What does the following x86 assembly code do:

              call next

next:              pop eax

A. Operator 'call' pushes the current program counter (PC) to the stack. The following 'pop' sets register eax with the PC value. This code is a way to get the current value of the PC.

Q. Implement an efficient memory pool for allocation of 4 bytes blocks.

A. Organize a linked list of free blocks using the data in the blocks themselves. Initially write in the first (offset zero) block “1” - offset of the next free block. In the second block (offset 1) write “2” and so on. Example of code is below:

static  const  int POOL_SIZE = 7;

static  uint32_t fastPoolData[POOL_SIZE];

static  uint32_t fastPoolHead;

static  const  int ALLOCATED_ENTRY = (POOL_SIZE+1);

static  inline  uint32_t  fastPoolGetNext(uint32_t node)

{

 return fastPoolData[node];

}

static  inline  void  fastPoolSetNext(uint32_t node, uint32_t next)

{

    fastPoolData[node] = next;

}

void  fastPoolInitialize()

{

    fastPoolHead = 0;

 for (int i = 0;i < (POOL_SIZE-1);i++)

    {

        fastPoolSetNext(i, i+1);

    }

    fastPoolSetNext(POOL_SIZE-1, ALLOCATED_ENTRY);

}

uint32_t *fastPoolAllocate()

{

 uint32_t blockOffset = fastPoolHead;

 if (blockOffset != ALLOCATED_ENTRY)

    {

        fastPoolHead = fastPoolGetNext(blockOffset);

        fastPoolSetNext(blockOffset, ALLOCATED_ENTRY);

 return &fastPoolData[blockOffset];

    }

 return  nullptr;

}

void  fastPoolFree(uint32_t *block)

{

 uint32_t blockOffset = block-&fastPoolData[0];

    fastPoolSetNext(blockOffset, fastPoolGetNext(fastPoolHead));

    fastPoolSetNext(fastPoolHead, blockOffset);

}

Q. Implement itoa() - a function which converts an integer to string. Consider only positive integers.

A.

int  itoa(int value, char *s, int size)

{

 int i = 0;

 int chars = size - 1;

 int digits = 0;

 int v = value;

 while (v)

    {

        v = v / 10;

        digits++;

    }

 while (value)

    {

 if (i >= chars)

 break;

s[digits-1-i] = '0' + (value%10);

        i++;

        value = value / 10;

    }

 if ((digits-1-i) < 0)

    {

        s[digits-1] = 0;

 return size;

    }

 else

    {

        s[chars] = 0;

 return 0;

    }

}

## Bit tricks.

Q. You have two numbers, M and N, and two bit positions, i and j. Write a method to set all bits in M between i and j equal to N. Assume that i < j. For example, if input M=0x00, N=0x10, i=0, j=5, then output is 0x10.

A. You need to clear bits from i to j in N, and use bitwise OR between M and N. Using uint32_t or similar is probably a good idea – discuss it with the interviewer.

int mask = ((i<< 1)-1) | ((1 << j)-1);

M = M & mask;

M = M | (N << i);

Q.What does the following code ((n & (n-1)) == 0)?

A. This condition is true if n is zero or if n is a power of 2\.

Q. How to find the highest set bit?

A. GCC has a built-in function __builtin_clz() which returns the number of leading zeros in the argument. Alternative solution:

unsigned  int v;

unsigned r = 0;

while (v >>= 1) {

    r++;

}

Q. How to set or cleat bits without branching? Why would you need it?

A. You can use, for example, the following code:

bool f;

unsigned  int mask;

unsigned  int w;

w ^= (-f ^ w) & mask;

Lack of branching can improve performance by 5-10% depending on the context and the CPU. See also  [17].

Q. Find first set bit in an integer number.

A. In GCC we have a built in function __builtin_ffs(). Alternatively you can use software implementation like one below. Discuss possible return code which covers the case of x equal to zero.

int  findFirst(int x)

{

 if (x == 0)

 return 0;

 int t = 1;

 int r = 1;

 while ((x & t) == 0) {

        t = t << 1;

        r = r + 1;

    }

 return r;

}

Q. How to clear all but the least significant bit in an integer number? For example for 0x60 (2 bits are set) the result is 0x20 (one bit is set).

A. In a single C line it is (see [18])

x &= -x;

or, which is the same thing:

x &= (~x+1)

Q. How to check if the integer is even.

A. In the even integer the least significant bits is zero:

((x & 1) == 0)

Q. How to clear the rightmost set bit?

A. Reduce the integer by 1 and use bitwise AND with itself:

x & (x-1)

Q. How to set the rightmost zero bit?

A. Add 1 to the integer and use bitwise OR with itself:

x | (x+1)

Q. Count non-zero bits in an integer. Is there a solution with one branch?

A. Clear rightmost bit and check if the result is zero (see [19]):

int  countBits(int n)

{

 int count=0;

 while(n)

    {

        count++;

        n = n&(n-1);

    }

 return count;

}

## Popular online tests.

In the following tests every question is followed by five possible answers. Up to three answers can be correct. I do not provide the correct answers .

Which of the following statements describe the condition that can be used for conditional compilation in C?

*   the condition must evaluate to 0 or 1
*   the condition can depend on the values of any “const” variables
*   the condition can use the sizeof to make decisions about compiler-dependent operations based on the size of standard data types
*   the condition can depend on the value of environment variables

If an ANSI C operator is used with operand of differing types ,which of the following correctly describes type conversion of operands or result?

*   no automatic conversion of the operands occurs at all
*   such an operation will be flagged as an error by the compiler
*   “narrow” operands are converted to the type of the “wider’ operands to avoid losing information
*   the values of operands are changed to prevent possible overflow in “barrow” types
*   assignment of th result to “narrow” type may lose information, but are not illegal

Which of the following peripheral devices allow an embedded system to communicate with other devices using a two wire or three wire serial interface?

*   a bidirectional three-state buffer
*   an address decoder
*   a universal synchronous receiver transmitter
*   a digital-to-analogue converted
*   a non-volatile memory

What of the following statements correctly describe funcitons in the ANSI C programmign language when used in an embedded system?

*   the name of global functions in two different files which are linked together do need to be unique
*   function can be called by a value or pointer
*   functions cannot return more than one value
*   the maximum number of arguments that a function can take is 12
*   every function must returns a value

What of the following statements correctly describe the ANSI C code below?

typedef  char *pchar;

pchar  funcpchar();

typedef  pchar (*pfuncpchar)();

pfuncpchar  fpfuncpchar();

*   pfuncpchar is a name for a pointer to a function returning a pointer to a char
*   fpfuncpchar is a pointer to char that returns a pointer to a function
*   fpfuncpchar is a pointer that returns a pointer to function that returns a pointer char
*   fpfuncpchar is a function returning a pointer to a function that returns a pointer to a char
*   funcpchar is a function that returns a pointer to a char

What of the following statements correctly describe the bitwise right-shift operator >> in ANSI C?

*   the right-side operator must be one or greater,
*   it shifts every bit of its left-size operand to the right by the number of bit positions specified by the right-side operand
*   it can be used to reverse the sign of a number
*   for unsigned integer it fills in vacated bits on the left with zero
*   it can be be used to divide an integer by powers of 2

What of the following statements are correct assuming 2s complement implementation of ANSI C

*   a negative value expressed as a signed integer will be expressed as a positive value greater than the maximum value of the signed integer if expressed as an unsigned integer of the same size
*   the range of he signed and unsigned variations of the same integer type are equivalent in size and numeric maximum and minimum
*   The range of the unsigned variation of an integer type is twice that of the signed variation
*   the representation of a signed integer has one additional bit for the sign

How call to the print function can look like in the following code

void  process (int (*p)(int, int, char*))

{

 int a = 5, b  = 47;

 char *c = "aggregate";

 /* Call print for b,a, c */

 /***************/

 return ;

}

int  main(void)

{

    process(report);

 return 0;

}

*   p->report(b,a,c);
*   (*p)(b,a,c);
*   p(b,a,c);
*   (*p)(report, b, a, c)
*   p.report(b,a,c)

What is the right fix of the compilation failure in the code below:

/* File A */

struct  pair a[10];

void  initialize(int x, int m, int b)

{

 int i;

    a[0].y = (a[0].x = x) * m + b;

 for (i = 1;i < 10;++i)

        a[i].y = (a[i].x = a[i-1].x + 1)*m + b;

}

/*File B:*/

struct  pair {int  x, y;};

struct  pair *op(int x)

{

 int i;

    for (i = 10;i > 0;--i)

 if (a[i].x == x)

 break;

    return a+ 1;

}

extern  struct  pair a[];

*   the declaration of array a must occur before the definition of op().
*   the returned pointer is invalid unless the array is declared as extern in all files with functions that call op()
*   the definition of the array a is missing the extern keyword in file A
*   the size of the array must be specified in file b
*   the definition of struct pair is missing the extern keyword in both files

Which of the following are properly formed #define directives in ANSI C ?

#define DIF(X,Y) (X-Y)

#define sqr(x) ((x)*(x))

#define mm_per_meter 1000;

#define SUM(X,Y) ((X)+(Y));

#define INCHES PER FEET 12

What is the output of executing the ANSI code below:

void f(void **p);

int k =2;

int *pk=&k;

int  main()

{

 int *p;

 f(&p);

 printf(“%d\n”, *p);

 return 0;

}

void  f(void **pp)

{

    (*pk)++;

    *pp = pk;

}

*   syntax error
*   address of pk
*   garbage
*   3
*   2

What is the contents of the array output after the completoonm of the for loop?

int encode (char, char);

int  main(void)

{

 char input [7] = {'M', 'E',':','G','O',':'}, output [7];

 int i;

 for (i = 0;i < 7;++i)

    {

output[i] = encode(input[i], ':');

    }

 return 0;

}

int  encode(char c , char t)

{

 switch(c) {

 case  'E': c = 'A';break;

 case  'O': c = 'X'; break;

 case  'A': c = 'T'; break;

 case  'U': c = 'M'; break;

}

 if  (c >= 'A' && c <= 'Z' || c >= 'a' && c <= 'z' && (c=t))

c = '\0';

 return c;

}

*   \0’,\0’,\0’,\0’,\0’,\0’,\0’
*   ‘M’,’A’,’\0’,’G’,’O’,\0’,\0’
*   ‘M’,’A’,’\0’,’G’,’X’,\0’,\0’
*   ‘\0’,’\0’,’:’,’\0’,’\0’,’:’,’\0’
*   ‘:’,‘:’,‘:’,‘:’,‘:’,‘:’,‘\0’

What function dump_port() shall output:

/* Number of registers in the I/O */

#define PORT_SIZE 7

typedef  unsigned  int  word;

union  IO_port {

 word  reglist[PORT_SIZE];

 struct {

 word  ENABLE ;

 word  DIRECTION;

 word  OPEN_COLLECTOR;

 word  DATA;

} reg;

};

static  union  IO_port *GPIO = 0xE0004000; /* address of the port */

#include  <stdio.h>

void  dump_port(union  IO_port *p)

{

 int i;

 for (i = 0;i < PORT_SIZE;++i)

    {

 printf("%X ", p->reglist[i]);

    }

}

int  main(void)

{

    GPIO->reg.DATA            = 0x000000D0;

    GPIO->reg.OPEN_COLLECTOR  = 0x000000F0;

    GPIO->reg.DIRECTION       = 0xFFFFFF0F;

    GPIO->reg.ENABLE          = 0x000030F0;

    dump_port(GPIO);

 return 0;

}

*   D0 F0 FFFFFF0F 30F0
*   undefined
*   D000000 F000000 FFFFFF0F F0300000
*   FFFFFFF F0300000  20000000 D0000000
*   FFFFFF0F 30F0 2 D0

What is returned by the following function

unsigned  int process(unsigned int x, int p, int n)

{

 return x ^ (~(~0 << n) << p + 1 -n);

}

*   p bits of x beginning at position n
*   x multiplied by 2^(p-n)
*   x with the n bits beginning at position p set to 1
*   the nth bit of x at position p
*   x with the n bits that begin at position p inverted

A program must produce a pulse-width modulated signal on a digital output. Value 0 is represented by digital output HIGH and value 0xFFFF is represented by digital level LOW. What pulse signal represents a value 0x7000?

*   30ms period, 13.3ms pulse width
*   2000Hz, 563us pulse width
*   100KHz, 5.63us pulse width
*   100KHz, 4.38us pulse width
*   20ms, 11.25ms pulse width

Which of the following statements correctly describe the C++ code snippet below?

void  foo(long l);

int i =12;

foo(i);

*   i is promoted to a long to invoke the function foo.
*   the function foo is invoked with a long that has a value of “12”
*   the compiler instantiates a new function that accept an int instead of long
*   the function foo is invoked with an int that has a value of “12”
*   the function foo is invoked with a long that has an undefined value

The following code tries to categorize the incoming mails by groups - complains, complements, other. What is the code to use in the for loop?

enum  class LetterType {complement, complaint, unknown};

LetterType getMailType(string letter)

{

 pair<string, int> happy = make_pair(happyString, 0);

 pair<string, int> sad = make_pair(sadString, 0);

 string word;

 string fstream ss(letter);

 vector<string> letterWords;

 while (ss >> word) letterWords.push_back(word);

 vector<string>::iterator words;

 for (words=letterWords.begin();words<letterWords.end();words++)

    {

        word = *words;

 //...

    }

 if (happy.second > sad.second) return complement;

 else  if (happy.second < sad.second) return complaint;

 else  return unknown;

}

*   if (happy.find(word)) happy.second++;if (sad.find(word)) sad.second++;
*   if (happy.find(word) != string::npos) happy.second++;if (sad.find(word) != string::npos) sad.second++;
*   if (happy.first.find(word)) happy.second++;if (sad.first.find(word)) sad.second++;
*   if (happy.first.find(word) != string::npos) happy++;if (sad.first::find(word) != string::npos) sad++;
*   if (happy.first.find(word) != string::npos) happy.second++;if (sad.first::find(word) != string::npos) sad.second++;

Which of the following are C+ declare pointers that can not be changed as opposed to declaring a pointer to something that can not be changed?

*   extern double *float;
*   extern const int *const reference_only;
*   extern const std::vector<int> *global_vector;
*   extern const void *anything;
*   extern float *const some_scalar;

Which of the following actions are performed by the C++ catch(...) statement?

*   catch default exceptions.
*   ignore exceptions.
*   catch an exception, then pass it to the next level of program control.
*   disable the throwing of further exceptions.
*   catch exception types that do not have a corresponding catch block.

Which of the following statements correctly describe compiler generate copy constructor?

*   the compiler-generated copy constructor creates a reference to the original object.
*   the compiler-generated copy constructor invokes the assignment operator of the class.
*   the compiler-generated copy constructor does nothing by default.
*   the compiler-generated copy constructor tags the object as having being copy-constructed by the compiler.
*   the compiler-generated copy constructor performs a member-wise copy of the original object.

When overloading C++ unary operators, which of the following statements are correct?

*   no parameters when the operator function is a class member.
*   one parameter when the operator function is not a class member.
*   any number of parameters when the operator function is not a class member.
*   one dummy parameter when the operator is a particular type of increment/decrement and a class member.
*   no parameters when the operator function is not a class member.

In the C++ code segment below which of the following correctly describe the behavior of the line containing assert()?

int val = 5;

while (true)

{

 int res = testVal(val);

   assert(res);

 //...

}

*   It logs the value of val to a file
*   In debug mode it makes sure that val is within user-defined bounds and terminates the program if not. When not in the debug mode it logs the val to a file
*   If the program is not compiled in debug mode it does nothing
*   If val is negative it terminates the program
*   If the program is compiled in debug mode it causes the program to terminate if val is zero.

## Brain teasers.

Q. The submarine is located on a line and has an integer position (can be negative). It moves at a constant integer speed each second in the same direction. Is there a way to ensure that you can hit the submarine in a finite amount of time if you allowed to fire once every second?

A. After T seconds the submarine is going to be in the position (v*T) or ((-v)*T), where v is the absolute value of the velocity of the submarine. If v=1 two bombs should be enough in the positions 1 and (-2). If there is a hit we have solved the problem. If not we have wasted 2 seconds. Let's assume that the speed is 2 and drop the bombs in the positions 2*3=6 and (-2)*4=(-8). After T seconds we shall bomb positions T*(T+1)/2 and (-T)*(T/2).

Q. There is a building of 100 floors. If an egg drops from the Nth floor or above it will break. If it’s dropped from any floor below, it will not break. You’re given 2 eggs. Find N, while minimizing the number of drops for the worst case.

A. Regardless of how we drop the first egg, we must do a linear search with the second egg. A perfect system would be one in which drops of the first egg + drops of the second egg is always the same. For example, if the first egg is dropped on floor 20 and then floor 30 (where it breaks), second egg is potentially required to take 9 steps. When we drop the first egg again, we must reduce potential steps for the second egg to only 8. Which means that we must drop first egg at floor 39\. Therefore, the first egg must start at floor X, then go up by X-1 floors, then X-2, ...,

X+(X-1)+(X-2)+...+1 = 100

X(X+1)/2 = 100

X = 14

We go to floor 14, then 27, then 39, ... for maximum 14 steps (see [20]).

Q. How to negate a number using only operator “+”.

A. If the number is positive you can add -1 to the number and count how many loops you did:

int negate(int x) {

 int result = 0;

 int sign = x < 0 ? 1 : -1;

 while (x != 0) {

        result += sign;

        x += sign;

    }

 return result;

}

Q. Find mistakes, if any, in the following function:

void  mistake()

{

 unsigned  int i;

 for (i = 100; i <= 0; --i) {

 printf("%d\n", i);

    }

}

A. Print will never get executed. The “for” loop is an infinite loop.

Q. An application crashes when it is run. It never crashes in the same place. The application is single threaded, and uses only the C standard library. What programming errors could be causing this crash?

A. Crashes can be caused by the input: user input or a specific hardware state, stack overflow, attempts to use not allocated (already freed) memory. It is possible to log the system inputs. There are tools (valgrind) which help to discover memory leaks and access to not initialize memory.

Q. Given a random numbers generator r5 which generates integer number between 0 and 4 implement a random numbers generator r7.

A. A sum of two random numbers is not a uniformly distributed random number. Any solution which involves a sum of randomly generated numbers will be wrong. In the following code the first assignment generates a two digits number base 5 – a random number between 0 and 24\. The next line removes from the series of random numbers 21, 22, 23, 24\. The result of the operation is a series of uniformly distributed numbers between 0 and 20. Modulus 7 completes the task.

int  random_7() {

 while (true) {

 int ret = 5 * random_5() + random_5();

 if (ret < 21)

 return (ret % 7);

    }

}

# Conclusion.

You have delighted us long enough. Let the other young ladies have time to exhibit – Jane Austen, Pride and Prejudice.

I hope you have found this book interesting and worth the time and money spent. This book gets updates often. You can always get the updated version by turning on “Automatic Update” in the “Manage Your Content and Devices” part of the Amazon WEB site.

Please, let me know what do you think or ask questions by leaving a review on the Amazon WEB site or sending an e-mail to [arkady.miasnikov@gmail.com](mailto:arkady.miasnikov@gmail.com)

Thank you, Arkady.

Bibliography.

[1]              RAII [http://en.wikipedia.org/wiki/Resource_Acquisition_Is_Initialization]

[2]              Singleton [http://en.wikipedia.org/wiki/Singleton_pattern]

[3]              Cyclic Buffer [https://github.com/larytet/emcpp/blob/master/src/CyclicBuffer.h]

[4]              Object composition [http://en.wikipedia.org/wiki/Object_composition]

[5]              "Design Patterns: Elements of Reusable Object-Oriented Software",1994, Erich Gamma, Richard Helm, Ralph Johnson, John Vlissides

[6]              Mailbox [https://github.com/larytet/emcpp/blob/master/src/Mailbox.h]

[7]              Constexpr hashes [https://github.com/mfontanini/Programs-Scripts/tree/master/constexpr_hashes]

[8]              Open TI [https://www.assembla.com/code/OpenTI/subversion/nodes/641/scripts]

[9]              Timers [https://github.com/larytet/emcpp/blob/master/src/Timers.h]

[10]              Interface Class [http://en.wikibooks.org/wiki/More_C%2B%2B_Idioms/Interface_Class]

[11]              ADC [http://en.wikipedia.org/wiki/Analog-to-digital_converter]

[12]              Low path filter [http://en.wikipedia.org/wiki/Low-pass_filter]

[13]              Fixed-point arithmetic [https://en.wikipedia.org/wiki/Fixed-point_arithmetic]

[14]              Fixed-Point Types in GCC [https://gcc.gnu.org/onlinedocs/gcc-4.9.0/gcc/Fixed-Point.html]

[15]              Fixed-Point library from Kurt Guntheroth [http://www.guntheroth.com/]

[16]              The rise and rise of the cognitive elite [http://www.economist.com/node/17929013]

[17]              Bit Twiddling Hacks [http://graphics.stanford.edu/~seander/bithacks.html]

[18]              Low Level Bit Hacks You Absolutely Must Know [http://www.catonmat.net/blog/low-level-bit-hacks-you-absolutely-must-know/]

[19]              Puddle of Riddles! [http://puddleofriddles.blogspot.co.il/]

[20]              Career cup [http://www.careercup.com/]