# Initializing Classes

can see the order of execution. First the +load method is called, as soon as the class is loaded. When the run-time loader finishes, it calls the main() function. When you send a message to the class, the +initialize method is called, then the method you actually called, and then you can send an -init message to the returned instance.

+   - a.out[2690:903] +load called
- a.out[2690:903] main() entered
- a.out[2690:903] +initialize called
- a.out[2690:903] -init called
- a.out[2690:903] -init called

Output from: classInit

Note that the +initialize method is only called once. The second time you send a message to the class, it is delivered directly. The +initialize method call is also thread-safe. If you send two messages to the same class at the same time from different threads, one will block until the other finishes running the +initialize method, and then both will continue.