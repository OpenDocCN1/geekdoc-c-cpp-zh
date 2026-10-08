implementation of concurrent programming by modern operating systems. The use of threads increases the efficiency of an application and saves the wastage of CPU cycle.

To make a program execute more than one task at a time, it can be divided into smaller threads.

# Thread life cycle

The life cycle of a thread starts when an object of the System.Threading. The thread class is created and ends when the thread completes execution or is terminated. The various states in the lifecycle of a thread are –

+   a) Unstarted state- this is the situation when the instance of the thread is created but the Start method is not called.

+   b) Ready state – this is the situation when the thread is ready to run and waiting CPU cycle.

+   c) Not Runable State – the thread is not executable when –

+   Wait method has been called

+   Sleep method has been called

+   Blocked by I/O operations

+   a) Dead state – this is a situation when the thread completes execution or is aborted.

# Main Thread

The System.Threading.Thread class is used for working with threads in C#. It allows accessing and creating individual threads in a multithreaded application. The first thread to be executed in a process is called the main thread. The main thread is automatically created when a C# program starts executing. The threads using the Thread class are called as child threads of the main thread. A thread can be accessed using the CurrentThread property of thread class.

Creating threads – Threads are created by extending the thread class. Extended thread class then calls Start() method to begin the child thread execution. For example –