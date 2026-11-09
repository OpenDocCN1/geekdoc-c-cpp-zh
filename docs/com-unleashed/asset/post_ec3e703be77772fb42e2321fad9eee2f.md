
is that you will either have to develop sophisticated transaction services and scalability features yourself or do without. COM+ makes MTS and COM inseparable and entices you by adding even more performance advantages.

A good MTS component is a good COM+ component. If a developer has taken the time to reason through the issues related to enterprise applications when designing an MTS component, chances are that these will carry through to a COM+ component. There are several specific areas in which COM+ stands apart from MTS. COM+ improves the scalability features introduced by MTS through the implementation of object pooling and dynamic load balancing. (Dynamic load balancing is not here at this moment, but it will be very soon.) Well-written MTS components can immediately take advantage of these services. COM+ also simplifies the creation of constituent objects within an MTS activity. Because COM+ unifies MTS and COM, object construction need no longer be an MTS-specific behavior. COM+ introduces additional object construction hooks (such as parameterized object creation), presenting developers with extended performance facilities.

## Creating COM+ Objects

COM+ creates all object instances of COM+ classes in much the same way as MTS would create an MTS-configured, server-based object. Standard COM objects operate in much the same way as they always have, the unification of COM and MTS in COM+ has cleared the way for several enhancements to the MTS interception mechanism. Most notable is the fact that context objects and interception functionality have been merged into the standard COM proxy/stub mechanism. This means that you can create a new object using CoCreateInstanceEx() without losing context. MTS developers must use the IObjectContext::CreateInstance() method in order to construct new objects within the current context. The CreateInstance() approach works in COM+ as well, however, providing complete compatibility with existing MTS components.

Context and interception are discussed in Chapter 15, “MTS.”

### Parameterized Object Construction

COM+ also introduces a parameterized object construction mechanism. The standard COM and MTS object-creation facilities do not supply a way to differentiate creation requests targeting the same class. A COM+ class can choose to support the IObjectConstructor interface that supports parameterized construction. The Component Services Manager (equivalent to the MTS Explorer) shown in Figure 3.1 can be used to configure a string parameter for object construction of any given COM+ class. The IObjectConstructor interface can be used by the new object to retrieve the construction string configured by the COM+ administrator. This would enable an administrator to define a message queue path to be used by objects associated with a set of clients, for example. Currently, COM+ 1.0 allows classes to be associated with only one application at a time. This restricts administrators to one construction string per class. This is shown in Chapter 5, “Monikers.”

**FIGURE 3.1**  
*The Component Services Manager.*

![](img/112c2326f49d26b8d59aa054e14c5747_83_0.png)

## Monikers

*Monikers* are objects that are capable of reconstituting some other type of object through a simple string name (see Chapter 5). COM+ provides a “new moniker” that enables you to construct new objects from a simple string name, such as “new:OrderEntry.Ord1.1”. Of course, monikers are interface-based COM objects that anyone can create and are therefore much more flexible than strict API calls such as `CoCreateInstance()`. For example, using a moniker, the caller can pass initialization parameters to be used during object creation, something that can’t be done with the standard COM object creation functions.

## The Neutral-Threaded Apartment

COM+ introduces a new threading model known as the neutral-threaded apartment. This new apartment model is in direct response to the specific performance requirements of transaction-based application servers (such as MTS and COM+). The neutral apartment is also the preferred COM+ threading model.

Recall that COM threading models are designed to control concurrency within COM components. An apartment is a collection of objects and the definition of which process threads can execute the methods of those objects. Calls across apartment boundaries usually cause expensive marshaling services to be invoked. In this way, COM can control the concurrency within an apartment. The preferred MTS threading model is the single-threaded apartment (STA). The STA model collects created objects into the apartment of the single thread creating them. Any calls to STA objects from outside the apartment must be marshaled by the calling thread and dispatched by the target STA thread. The advantage of this system is that you can build STA-components quickly without worrying about the complexity of synchronization in a multithreaded application environment. The disadvantage is that COM serializes all method calls into the apartment, whether or not serialization is required. To further exacerbate the performance bottleneck, all external calls into the apartment must be marshaled. This can easily more than triple the method call overhead. COM threading is discussed in detail in Chapter 6.

So what’s the solution? Current COM supports one multithreaded apartment (MTA) per process. The MTA can be equipped with a free-threaded marshaler (FTM) that allows any thread in the process (even those from STAs) to call directly into MTA object methods without marshaling. Sounds like just the ticket, right? Well, not really. The MTA basically eliminates the concurrency controls supplied by MTS/COM+ and reintroduces all the complexity and overhead involved with managing synchronization and threads in multithreaded applications, not to mention the contention introduced between application-specific and MTS/COM+-style thread management. In general, MTA components should not be implemented within MTS or COM+. A new threading solution is required to improve performance in COM+.

![](img/112c2326f49d26b8d59aa054e14c5747_84_0.png)

The neutral-threaded apartment is the solution. Neutral-threaded components are always created in the neutral apartment. The neutral apartment contains objects but no threads. Otherwise, the neutral apartment is similar to the MTA in that it enables many threads to execute concurrently on its objects. The advantage is that COM+ still takes care of thread management and concurrency tasks, ensuring that no single object receives more than one method call at a time.

## Object Pooling

COM+ is the first application server to actually implement the object-pooling system provided for in MTS. Components adhering to the basic pooling guidelines of MTS can be pooled in COM+. Administrators use the Component Services Manager to configure capable components for object pooling. Pooling enables objects to be created once and then reused over several sequential transactions for various clients. Object pooling eliminates the overhead of constructing and destroying objects on a per-transaction basis. Objects must carefully reinitialize any state they require through user-supplied IObjectControl interface and must report support for pooling through IObjectControl as well.

Objects that supported pooling in MTS might break under COM+ if they aren’t well written. MTS never really pooled objects, but acted as if it did. Objects supporting pooling would receive all the appropriate IObjectControl calls, but MTS deleted the objects upon transaction completion instead of pooling them. This meant that initialization bugs that don't appear when constructors and destructors are called at transaction boundaries will show up in COM+, where the objects are not really destroyed but pooled instead. It's also important to note that pooled objects cannot be single threaded or apartment threaded. Objects created in an STA live in the same STA for their entire lifetime, and must always be called on the thread associated with the STA. This would have a serious impact on the performance of your application. COM+ lets you set many of the object-pooling parameters administratively, as shown in Figure 3.2.

![](img/112c2326f49d26b8d59aa054e14c5747_85_0.png)

### Object Pooling Administration

There is an administrative side of the pooling coin as well. Administrators who want to enable object pooling on a specific class must first ensure that the class is pool capable. Next, the Component Services Manager (the functional equivalent of the MTS Explorer) is used to enable pooling on the class in question. The Component Services Explorer also supplies minimum and maximum pool limits, as well as a client timeout setting used when no objects from the pool are available. The savvy administrator can carefully tune pool settings to improve overall server performance.

## Dynamic Load Balancing

MTS enables administrators to configure client applications to use a specific server within a set of servers. This is called static load balancing. It is a load-balancing solution
