
## Chapter 25 GUI Components: Part 2

25.12 (Creating a Color Chooser: Modification) Modify the MyColorChooser class of Exercise 25.11 to allow the user to enter an integer value into a JTextField to set the red, green or blue value. When the user presses Enter in the JTextField, the corresponding JSlider should be set to the appropriate value.

25.13 (Creating a Color Chooser: Modification) Modify the application in Exercise 25.12 to draw the current color as a rectangle on an instance of a subclass of JPanel which provides its own paintComponent method to draw the rectangle and provides set methods to set the red, green and blue values for the current color. When any set method is invoked, the drawing panel should automatically repaint itself.

25.14 (Drawing Application) Modify the application in Exercise 25.13 to allow the user to drag the mouse across the drawing panel (a subclass of JPanel) to draw a shape in the current color. Enable the user to choose what shape to draw.

25.15 (Drawing Application Modification) Modify the application in Exercise 25.14 to provide the user with the ability to terminate the application by clicking the close box on the window that is displayed and by selecting Exit from a File menu. Use the techniques shown in Fig. 25.5.

25.16 (Complete Drawing Application) Using the techniques developed in this chapter and Chapter 14, create a complete drawing application. The program should use the GUI components from Chapter 14 and Chapter 25 to enable the user to select the shape, color and fill characteristics. Each shape should be stored in an array of MyShape objects, where MyShape is the superclass in your hierarchy of shape classes. Use a JDesktopPane and JInternalFrames to allow the user to create multiple separate drawings in separate child windows. Create the user interface as a separate child window containing all the GUI components that allow the user to determine the characteristics of the shape to be drawn. The user can then click in any JInternalFrame to draw the shape.

## 26.1 Introduction

It would be nice if we could focus our attention on performing only one action at a time and performing it well, but that’s usually difficult to do. The human body performs a great variety of operations in parallel—or, as we’ll say throughout this chapter, concurrently. Respiration, blood circulation, digestion, thinking and walking, for example, can occur concurrently, as can all the senses—sight, touch, smell, taste and hearing.

Computers, too, can perform operations concurrently. It’s common for personal computers to compile a program, send a file to a printer and receive electronic mail messages over a network concurrently. Only computers that have multiple processors can truly execute multiple instructions concurrently. Operating systems on single-processor computers create the illusion of concurrent execution by rapidly switching between activities, but on such computers only a single instruction can execute at once. Today’s multicore computers have multiple processors that enable computers to perform tasks truly concurrently. Multicore smartphones are starting to appear.

Historically, concurrency has been implemented with operating system primitives available only to experienced systems programmers. The Ada programming language—developed by the United States Department of Defense—made concurrency primitives widely available to defense contractors building military command-and-control systems. However, Ada has not been widely used in academia and industry.

## Java Concurrency

Java makes concurrency available to you through the language and APIs. Java programs can have multiple threads of execution, where each thread has its own method-call stack and program counter, allowing it to execute concurrently with other threads while sharing with them application-wide resources such as memory. This capability is called multithreading.

- 26.1 Introduction
- 26.2 Thread States: Life Cycle of a Thread
- 26.3 Creating and Executing Threads with Executor Framework
- 26.4 Thread Synchronization
  - 26.4.1 Unsynchronized Data Sharing
  - 26.4.2 Synchronized Data Sharing—Making Operations Atomic
- 26.5 Producer/Consumer Relationship without Synchronization
- 26.6 Producer/Consumer Relationship: ArrayBlockingQueue
- 26.7 Producer/Consumer Relationship with Synchronization
- 26.8 Producer/Consumer Relationship: Bounded Buffers
- 26.9 Producer/Consumer Relationship: The Lock and Condition Interfaces
- 26.10 Concurrent Collections Overview
- 26.11 Multithreading with GUI
  - 26.11.1 Performing Computations in a Worker Thread
  - 26.11.2 Processing Intermediate Results with SwingWorker
- 26.12 Interfaces Callable and Future
- 26.13 Java SE 7: Fork/Join Framework
- 26.14 Wrap-Up

Summary | Self-Review Exercises | Answers to Self-Review Exercises | Exercises

## Performance Tip 26.1

A problem with single-threaded applications that can lead to poor responsiveness is that lengthy activities must complete before others can begin. In a multithreaded application, threads can be distributed across multiple processors (if available) so that multiple tasks execute truly concurrently and the application can operate more efficiently. Multithreading can also increase performance on single-processor systems that simulate concurrency—when one thread cannot proceed (because, for example, it’s waiting for the result of an I/O operation), another can use the processor.

## Concurrent Programming Uses

We’ll discuss many applications of concurrent programming. For example, when downloading a large file (e.g., an image, an audio clip or a video clip) over the Internet, the user may not want to wait until the entire clip downloads before starting the playback. To solve this problem, multiple threads can be used—one to download the clip, and another to play it. These activities proceed concurrently. To avoid choppy playback, the threads are synchronized (that is, their actions are coordinated) so that the player thread doesn’t begin until there’s a sufficient amount of the clip in memory to keep the player thread busy. The Java Virtual Machine (JVM) creates threads to run programs and threads to perform housekeeping tasks such as garbage collection.

## Concurrent Programming Is Difficult

Writing multithreaded programs can be tricky. Although the human mind can perform functions concurrently, people find it difficult to jump between parallel trains of thought. To see why multithreaded programs can be difficult to write and understand, try the following experiment: Open three books to page 1, and try reading the books concurrently. Read a few words from the first book, then a few from the second, then a few from the third, then loop back and read the next few words from the first book, and so on. After this experiment, you’ll appreciate many of the challenges of multithreading—switching between the books, reading briefly, remembering your place in each book, moving the book you’re reading closer so that you can see it and pushing the books you’re not reading aside—and, amid all this chaos, trying to comprehend the content of the books!

## Use the Prebuilt Classes of the Concurrency APIs Whenever Possible

Programming concurrent applications is difficult and error prone. If you must use synchronization in a program, you should follow some simple guidelines. Use existing classes from the Concurrency APIs (such as the ArrayBlockingQueue class we discuss in Section 26.6) that manage synchronization for you. These classes are written by experts, have been thoroughly tested and debugged, operate efficiently and help you avoid common traps and pitfalls.

If you need even more complex capabilities, use interfaces Lock and Condition that we introduce in Section 26.9. These interfaces should be used only by advanced programmers who are familiar with concurrent programming’s common traps and pitfalls. We explain these topics in this chapter for several reasons:

- They provide a solid basis for understanding how concurrent applications synchronize access to shared memory.
- The concepts are important to understand, even if an application does not use these tools explicitly.
