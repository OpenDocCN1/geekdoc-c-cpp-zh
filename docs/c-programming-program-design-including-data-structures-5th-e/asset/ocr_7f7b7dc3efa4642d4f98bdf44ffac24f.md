The destructor automatically executes when the class object goes out of scope. The use of destructors is discussed in subsequent chapters.

# Data Abstraction, Classes, and Abstract
Data Types

For the car that we drive, most of us want to know how to start the car and drive it. Most people are not concerned with the complexity of how the engine works. By separating the design details of a car’s engine from its use, the manufacturer helps the driver focus on how to drive the car. Our daily life has other similar examples. For the most part, we are concerned only with how to use certain items, rather than with how they work.

Separating the design details (that is, how the car’s engine works) from its use is called **abstraction**. In other words, abstraction focuses on what the engine does and not on how it works. Thus, abstraction is the process of separating the logical properties from the implementation details. Driving the car is a logical property; the construction of the engine constitutes the implementation details. We have an abstract view of what the engine does but are not interested in the engine’s actual implementation.

Abstraction can also be applied to data. Earlier sections of this chapter defined a data type clockType. The data type clockType has three member variables and the following basic operations:

+   1. Set the time.
+   2. Return the time.
+   3. Print the time.
+   4. Increment the time by one second.
+   5. Increment the time by one minute.
+   6. Increment the time by one hour.
+   7. Compare two times to see whether they are equal.

The actual implementation of the operations, that is, the definitions of the member functions of the class clockType, was postponed.

Data abstraction is defined as a process of separating the logical properties of the data from its implementation. The definition of clockType and its basic operations are the logical properties; the storing of clockType objects in the computer and the algorithms to perform these operations are the implementation details of clockType.

**Abstract data type (ADT):** A data type that separates the logical properties from the implementation details.