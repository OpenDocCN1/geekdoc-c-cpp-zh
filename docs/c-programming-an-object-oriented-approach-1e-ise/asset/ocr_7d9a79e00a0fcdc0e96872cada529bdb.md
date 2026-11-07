![](bbox=[0.29, 0.09, 0.96, 0.26])

+   Notes:
+   1. An object is created and pushed in the stack when the constructor is called.
+   2. Initialization allocates memory in the heap and the value is stored in it during the execution of the constructor body.
+   3. The constructor is terminated and an object is available to the main function.
+   4. The main function uses the object.
+   5. When the object goes out of scope, the destructor is called.
+   6. The destructor deletes the integer in the heap.
+   7. The object goes out of scope after the destructor returns and the object is popped.

Figure 14.13  Construction and destruction when no exception is thrown

constructed, the destructor is not called, which means the memory allocated in the heap is never deleted. We may have memory leak. Although the Integer object is popped up from the stack during unwinding, the destructor is never called and the memory in the heap is never released (Figure 14.14).

The problem here is that we separated the two related tasks of allocating memory and releasing memory by another task (storing data in the allocated memory). Because this third task failed (an exception is thrown), the constructor has allocated memory, but its work is not finished. This means that the destructor is not called to release the memory. The two related tasks of allocating and releasing memory are partially done. Memory is allocated, but not released. We may have memory leak.

![](bbox=[0.29, 0.64, 0.96, 0.8])

+   Notes:
+   1. An object is created and pushed into the stack when the constructor is called.
+   2. Allocation of the location in the heap memory is done, but an exception occurs when the constructor needs to store values in the object allocated in the heap.
+   3. An exception is thrown that terminates the main function. Stack unwinding pops the Integer object from the stack, but the memory in the heap is not released because the destructor is not called.

Figure 14.14  Construction and destruction when an exception is thrown