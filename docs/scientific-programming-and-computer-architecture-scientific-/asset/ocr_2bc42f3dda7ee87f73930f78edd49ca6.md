# 318
Chapter 5. Threads and Shared Memory

The argument to this function is a message or character string. On line 2, this message is recovered by casting it back to type char *.

The statements that extend from line 3 through line 9 define another ss, and copy the characters in ss into its even positions. The odd positions are filled with the underscore character except when the preceding even position has a blank character. Line 9 ensures that the string is properly terminated with '\0' following C convention.

The program prints the s, the string ss, and the pointer ss on lines 10, 12, and 14, respectively.

Presently, we will introduce Threads. For the ensuing discussion, the key items are the definition of ss on line 3 and the address that is printed on line 14 of print_message().

Pthreads are created inside call_pthreads() whose definition follows.

```
1 #include <thread.h>
2 void call_pthreads(){
3 pthread_t thread1, thread2, thread3;
4 char s[600];
5 sprintf(s, "Message for thread 1");
6 sprintf(s+200, "Message for thread 2");
7 sprintf(s+400, "Message for thread 3");
8 pthread_create(&thread1, NULL, print_message,
9 (void *)s);
10 pthread_create(&thread2, NULL, print_message,
11 (void *)(s+200));
12 pthread_create(&thread3, NULL, print_message,
13 (void *)(s+400));
14 void *result;
15 pthread_join(thread1, &result);
16 pthread_join(thread2, &result);
17 pthread_join(thread3, &result);
18 }
```

The function call_pthreads() creates three threads and sends a character string as the argument to each of them. The three threads print the message in the character string and return. There are four threads in this program, including the master thread.