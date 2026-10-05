# 5.3. Introduction to Pthreads

Each of the four threads will probably run on a different processor core on a processor with 4 or more cores.

On line 3, the program defines variables of the type pthread_t. The Pthread library will access administrative information about the threads using these variables.

The library function pthread_create() is used to create threads on lines 8, 10, and 12. The first argument is of type pthread_t *. During the call on lines 8 and 9, the pthread library will create a thread and make the variable thread point to information about that thread. Later information about the created thread can be accessed using thread1.

The second argument to pthread_create() will always be NULL for all. The third argument to pthread_create() is print_message, which is a function pointer. The third argument is the function that the thread will start executing as soon as it is scheduled to run. The third argument must be a pointer to a function that takes an argument of type void * and returns an argument of type void *. In this program, all three threads are created will run the same function.

The fourth argument to pthread_create() must be of type void *. When the thread starts running, it will get this pointer as an argument. In this program, each of the threads gets a different character string as its argument.

The library function pthread_join() may be used to retrieve the pointer returned by a thread. In this program, the pointer returned by each thread is saved in result. The variable result is defined on line 14 to be of void *. The threads do not return anything meaningful here. If they, the pointer result could be used to access the data returned by the threads.

The Pthread library has a fairly transparent syntax. By going over the definition of call_pthreads(), it is easy to see where threads are being created and how. C/C++ programmers Pthread header files by themselves without any prompting. The Pthread library may be linked using the -lpthread option.

# Thread stacks

Each thread gets its own stack. This stack is used for storing the local variables defined by the functions thread executes. When a thread makes a function call, the return address is pushed onto its stack.

On line 14, the function print_message() prints the value of ss, which is a pointer to a location in the thread stack. The three threads print as follows: