Smart? Yes. Thread-safe? No.

What is the issue? The call `instance= new MySingleton()` in line 4 consists of at least three steps.

+   1. Allocate memory for MySingleton
+   2. Initialize the MySingleton object
+   3. Let instance refer to the fully initialized MySingleton object

The issue is that the C++ runtime provides no guarantee that the steps are performed in that sequence. For example, the processor may reorder the steps to the sequence 1, 3, and 2. So in the first step, the memory is allocated, and in the second step, instance refers to a non-initialized singleton. If just at that moment another thread t2 tries to access the singleton and makes the pointer comparison, the comparison succeeds. The consequence is that thread t2 refers to a non-initialized singleton, and the program behavior is undefined.

# ### 6.3.2 Performance Measurement

I want to measure how expensive it is to access a singleton object. For reference timing, I use a singleton which I access 40 million times sequentially. Of course, the first access initializes the singleton object. In contrast, the accesses from four threads is done concurrently. I am only interested in the performance numbers. Therefore I sum up the execution time of the four threads. I measure the performance using a static variable with block scope (Meyers Singleton), a lock `std::lock_guard`, the function `std::call_once` in combination with the `std::once_flag`, and atomics with sequential consistency and acquire release semantic.

The program runs on two PCs. My Linux PC with the GCC compiler has four cores, while my Windows PC with the cl.exe compiler has two. I compile the program with maximum optimization. Please refer to the beginning of this chapter for the details about my setup.

I want to answer two questions:

+   1. What are the performance numbers of the various singleton implementations?
+   2. Is there a significant difference between Linux (GCC) and Windows (cl.exe)?

Finally, I collect all numbers in a table.

Before I present the performance numbers of the various multithreading implementations, here is the sequential program. The getInstance member function is not thread-safe with the C++03 standard.