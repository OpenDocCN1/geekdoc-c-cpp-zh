# Chapter 4

In an application entry, we have created a queue whose elements are references to the PLOTDATA type or some specific structure that we have defined. After creating a window, we will associate the following queue address to the window section for user-specific data that belongs to the window:

```
SetWindowLongPtr(hwnd, GWLP_USERDATA, (LONG_PTR) &queue);
```

Using the GWLP_USERDATA macro as a parameter to set the SetWindowLongPtr API call, the function associates the address of the queue object in a manner that the window handle can handle(hwnd). After creating the necessary controls, we need to create four threads for calculation purposes and one thread to draw. Whenever we need the object address, we can obtain it using GetWindowLongPtr as follows:

```
CPLOTDATA* plotPtr = (CPLOTDATA*)
GetWindowLongPtr(hwnd, GWLP_USERDATA);
```

In order to avoid the complexity of drawing (which is not the thread here), we will set the working threads to sleep for 1 second, while the draw thread will sleep for 2.3 seconds, only to create an environment where the consumer is slower than the producer. All the threads have fixed number of calculations to perform as the draw thread to draw.

After each completion, the PLOTDATA object is created and put into the queue. The draw thread then calls the PostMessage API to send (post) a message to the window specified with the first parameter--the handle to the window. The second parameter specifies a message to send (post), the third and fourth parameters are message specific if it is a window message (less than WM_), then its meaning is known; if it is a user-defined message then both parameters are left to the user to use. We are using the lParam parameter to pass the address of a newly created PLOTDATA object so that the window procedure can display the MESSAGE ID or any value from the PLOTDATA object that the user needs.

After the producer creates a message, it places the message into the queue. The draw thread, on the other hand, takes the messages from the consumer to perform drawing. If a pointer to the PLOTDATA object is obtained (when empty), the consumer performs drawing. After a successful drawing, the PLOTDATA object is destroyed in order to avoid memory leaks. When all the points are drawn and all the messages are processed, the draw thread uses PostMessage to notify the window procedure about completion.

# There's more...

Even though we used the PostMessage API, we are using the term message is sent and not the term posted. Why not? Because both, routines send messages; the only difference is that PostMessage returns without waiting for the callee to process the message. SendMessage API does the same thing; it sends messages, except that it waits while the callee processes the message, leaving the caller blocked until then. The messages in a message queue are retrieved using GetMessage or PeekMessage API.

155