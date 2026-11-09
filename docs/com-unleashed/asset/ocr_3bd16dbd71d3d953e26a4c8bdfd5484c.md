through the ISubscriberControl interface. This interface enables clients to discard or redirect particular events.

Take for instance an order entry system. During design it was decided that availability information could be sent once the order was received, but wasn’t essential to the real-time order entry. This decision could be the result of a traffic estimate. The loosely coupled architecture (where no real-time availability information is available) can more effectively amortize the use of the applications servers over time. After an order is placed, the subscriber can be notified of any availability problems.

> > **Note**
> >
> > LCE is yet another very powerful tool in the COM+ kit. Much like queued components, LCE services address a critical gap in previous COM implementations. Queued components offer COM level one way of decoupled method invocation, and LCE provides a native COM broadcast mechanism. The features presented through the queued component and LCE services of COM+ solve problems that have caused many a developer to invent extensive custom software.

# Accessing Data with COM+

Data access in COM+ is much the same as that presented in MTS. In particular, OLE DB and ADO are the access mechanisms of choice. OLE DB supplies a very powerful and extensible architecture supporting various types of underlying data stores, including any ODBC source. OLE DB is necessarily complex because of its flexibility and performance. ATL Consumer and producer templates can ease the burden of OLE DB development in C++. By far, the most popular mechanism for programming OLE DB is, of course, ActiveX Data Objects (ADO). ADO provides a dual interface COM component implementation operating on top of OLE DB that can easily be used by compiled applications and scripts alike. Of course, if you’re like many developers, you already have very large ODBC-based systems that are fully supported in this environment as well.

# Read Optimized Data Access

IMDB is a smart in-memory database caching system optimized for read operations. IMDB allows static data to be loaded once and queried against many times. The performance advantages achievable with this type of in-memory data support are enormous. Queries satisfied locally through IMDB require neither network nor disk access. IMDB also supports write operations. It backlogs updates until they are committed. At that point, changes are submitted to the underlying database. Obviously, the real performance advantages lie in the arena of caching static-read weighted data.