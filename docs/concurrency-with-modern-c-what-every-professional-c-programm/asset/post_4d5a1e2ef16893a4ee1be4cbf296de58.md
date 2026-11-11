
![](img/d61a6c83410484053b8892275d2fcc4f_508_0.png)

A Boss/Worker Workflow

#### 9.2.4.4 Further Information

- Concurrent Programming in Java: Design Principles and Patterns (Doug Lea)²⁹. The difference between C++ and Java programming languages should not be an issue because the essence of concurrent programming is much deeper than syntax of a particular language.

#### Distilled Information

- A necessary prerequisite for a data race is shared mutable state. Synchronization patterns boil down to two concerns: dealing with sharing and dealing with mutation.
- The three patterns copied value, thread-specific storage, and future prevent the sharing of data.
- Thanks to the patterns scoped locking, strategized locking, thread-safe interface, or guarded suspension, you can safely share mutable data between threads.

²⁹ http://gee.cs.oswego.edu/dl/cpj/

## 10. Concurrent Architecture

![](img/d61a6c83410484053b8892275d2fcc4f_509_0.png)

Cippi designs a building

The patterns presented in this chapter are classics. The presented patterns are very well explained in the invaluable book Pattern-Oriented Software Architecture: Patterns for Concurrent and Networked Objects¹. My goal for this chapter is to give a concise overview of the Active Object, the Monitor Object. Additionally, I write about the Half-Sync/Half-Async pattern and the two strongly related patterns: Reactor, and Proactor. As in the last chapter on Synchronization Patterns, I'm wearing C++ glasses. Before I dive into the patterns, here are the patterns from a bird's-eye perspective.

- The **Active Object** design pattern decouples member function execution from member function invocation for objects that each reside in their own thread of control. The goal is to introduce concurrency by using asynchronous member function invocation and a scheduler for handling requests. Wikipedia: Active object¹
- The **Monitor Object** design pattern synchronizes concurrent member function execution to ensure that only one member function at a time runs within an object. It also allows object's member functions to schedule their execution sequences cooperatively. Pattern-Oriented Software Architecture: Patterns for Concurrent and Networked Objects²

Both patterns synchronize and schedule member function invocation. The main difference is that the Active Object executes its member function in a different thread but the monitor in the same thread as the client. In contrast to the Active Object and the Monitor Object, which have a subsystem focus and are, therefore, typically called design patterns, the Half-Sync/Half-Async, the Reactor, and the Proactor pattern have system perspective and are consequently called architectural patterns.

- The **Half-Sync/Half-Async** architectural pattern decouples asynchronous and synchronous service processing in concurrent systems to simplify programming without unduly reducing performance. The pattern introduces two intercommunicating layers, one for asynchronous and one for synchronous service processing. *Pattern-Oriented Software Architecture: Patterns for Concurrent and Networked Objects*^4
- The **Reactor** pattern is an event-driven framework to demultiplex and dispatch service requests concurrently onto various service providers. *Pattern-Oriented Software Architecture: Patterns for Concurrent and Networked Objects*^5
- The **Proactor** pattern enables event-driven applications to demultiplex and dispatch service requests triggered by the completion of an asynchronous operation. *Pattern-Oriented Software Architecture: Patterns for Concurrent and Networked Objects*^6

### 10.1 Active Object

The Active Object design pattern decouples method invocation from method execution. The method invocation is performed on the client thread, but the method execution on the Active Object. The Active Object has its own thread and a list of method request objects (short request) to be executed. The client's method invocation enqueues the requests on the Active Object's list. The requests are dispatched on the servant. The Active Object pattern is also known as Concurrent Object.

#### 10.1.1 Challenges

When many threads access a shared object synchronized, the following challenges have to be solved.

1. A thread invoking a processing-intensive member function should not block the other threads invoking the same object for too long.
2. It should be easy to synchronize access to a shared object.
3. The concurrency characteristics of the executed requests should be adaptable to the concrete hardware and software.

#### 10.1.2 Solution

The client's method invocation goes to a proxy, which represents the interface of the Active Object. The servant implements these member functions and runs in the Active Object's thread. At run time, the proxy transforms the invocation into a method invocation on the servant. This request is enqueued in an activation list by the scheduler. A scheduler's event loop runs in the same thread as the servant, dequeues the requests from the activation list, removes them, and dispatches them on the servant. The client obtains the result of the method invocation via a future from the proxy.

1. https://www.dre.vanderbilt.edu/~schmidt/POSA/POSA2/
2. https://www.dre.vanderbilt.edu/~schmidt/POSA/POSA2/
3. https://www.dre.vanderbilt.edu/~schmidt/POSA/POSA2/

#### 10.1.3 Components

The Active Object pattern consists of six components:

1. **The proxy** provides an interface for the accessible member functions on the Active Object. The proxy triggers the construction of a request which goes into the activation list. The proxy runs in the client thread.
2. **The method request class** defines the interface for the method executing on an Active Object. This interface also contains guarded methods, indicating if the job is ready to run. The request includes all context information to be executed later.
3. **The activation list** maintains the pending requests. The activation list decouples the client’s thread from the Active Object thread. The proxy inserts the request object, and the scheduler removes them. Consequently, the access onto the activation list must be serialized.
4. **The scheduler** runs in the thread of the Active Object and decides which request from the activation list is executed next. The scheduler evaluates the guards of the request to determine if the request could run.
5. **The servant** implements the Active Object and runs in the active object’s thread. The servant implements the interface of the method request, and the scheduler invokes its member functions.
6. **The future** is created by the proxy and is only necessary if the request returns a result. Therefore, the client receives the future and can obtain the result of the method invocation on the Active Object. The client can wait for the outcome or poll for it.

#### 10.1.4 Dynamic Behavior

The dynamic behavior of the Active Object consists of three phases:

1. **Request construction and scheduling:** The client invokes a method on the proxy. The proxy creates a request and passes it to the scheduler. The scheduler enqueues the request on the activation list. Additionally, the proxy returns a future to the client if the request returns a result.
2. **Member function execution:** The scheduler determines which request becomes runnable by evaluating the guard method of the request. It removes the request from the activation list and dispatches it to the servant.
3. **Completion:** When the request returns something, it is stored in the future. The client can ask for the result. When the client has the result, the request and the future can be deleted.

The following picture shows the sequence of messages.

![](img/d61a6c83410484053b8892275d2fcc4f_512_0.png)

Active Object

### Proxy

The proxy design pattern is one of the classics from the book Design Patterns: Elements of Reusable Object-Oriented Software³. A proxy is an object which stands for something else. A typical proxy could be a remote proxy CORBA⁴, a security proxy, a virtual proxy which is created on-demand, or a smart pointer such as std::shared_ptr⁵. Each proxy adds additional functionality to the object it represents. A remote proxy stands for a remote object and gives the client the illusion of a local object. A security proxy turns an insecure connection into a secure connection by encrypting and decrypting data. A virtual proxy encapsulates the creation of a heavy-weight object in a lazy fashion, and a smart pointer manages the lifetime of the underlying memory.

![](img/d61a6c83410484053b8892275d2fcc4f_513_0.png)

Proxy

- The Proxy has the same interface, such as the RealSubject, manages the reference, and often the subject's lifetime.
- The Subject has the same interface such as the proxy and the RealSubject.
- The RealSubject provides the functionality.

The Wikipedia article about the proxy pattern¹⁰ gives you more details.

- ³https://en.wikipedia.org/wiki/Design_Patterns
- ⁴https://en.wikipedia.org/wiki/Common_Object_Request_Broker_Architecture
- ⁵https://en.cppreference.com/w/cpp/memory/shared_ptr
- ¹⁰https://en.wikipedia.org/wiki/Proxy_pattern
