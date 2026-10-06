# # 4
# Message Passing

In this chapter, we will cover the following topics:

+   - Explaining Message Passing Interface
- Understanding a message queue
- Using the thread message queue
- Communicating through the pipe object

# Introduction

To explain the Message Passing Interface (MPI), we need to understand the operating system well. As we mentioned in Chapter 1, Introduction to C++ Concepts and Features, modern Windows operating systems are designed as event-driven systems.

An event-driven system is the one where some action occurs as a response to some signal sent to the operating system. For example, when you move a mouse, cursor X-coordinate change and cursor Y-coordinate change are raised (we say an event is raised, not occurred). When you press any keyboard, another event is raised–pressed and so on.

At the operating system level, a large number of events are raised every few milliseconds, hidden from the user. Programming without events would be very difficult, especially for synchronization tasks.

One form of an event is the message at the operating system level. When you press your mouse button, the operating system calls the window procedure (event handler) for the window in which region (area) the click occurred. Parameters that define a message, along event-specific details, such as click coordinates, are passed to the window procedure that's being called.