# 24.1 Remoting

# Concept

1. Distributed computing is an integral part of almost every software development. Before .NET Remoting, DCOM (dynamic component object modeling) was widely used method for developing distributed application on Microsoft platform. Because of object oriented architecture, .NET remoting replaces DCOM as .NET framework replaces COM.

# Explanation

2. .NET Remoting is a architecture/mechanism which enables communicating between objects which are not in the same process. It is a generic system for different applications to communicate with one another. .NET objects are exposed to remote processes, by which it allows inter process communication. The applications can be located on the same computer, different computers on the same network, or on computers across separate networks.

3. Remoting enables communication between different application domains or processes using different transportation protocols, serialization formats, object lifetime schemes, and modes of object creation.

# 4. Advantages of Distributed Application Development

# Fault Tolerance

Fault tolerance means that a system should be resilient when failures within the system occur.

# Scalability

Scalability is the ability of a system to handle increased load with only an incremental change in performance.

# Administration

Managing the system from one place.

# 24.2 C# Remoting Architecture

# Concept

1. The .NET Remoting provides an inter-process communication between Application Domains by using Remoting Framework. The applications can be located on the same computer, different computers on the same network, or on computers across separate networks. The .NET Remoting supports distributed object communications over the TCP and HTTP channels by using Binary or SOAP formatters of the data stream.