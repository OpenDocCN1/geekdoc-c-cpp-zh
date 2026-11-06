functions. However, for complex initialization, this approach may require significant additional work and time.

![](bbox=[0.122, 0.181, 0.196, 0.232])

# Performance Tip 9.4

*Initialize member objects explicitly through member initializers.* This eliminates the overhead of “doubly initializing” member objects—once when the member object’s default constructor is called and again when set functions are called in the constructor body (or later) to initialize the member object.

![](bbox=[0.12, 0.49, 0.194, 0.544])

# Common Programming Error 9.5

*A compilation error occurs if a member object is not initialized with a member initializer and the member object’s class does not provide a default constructor (i.e., the member object’s class defines one or more constructors, but none is a default constructor).*

![](bbox=[0.12, 0.776, 0.194, 0.833])

# Software Engineering Observation 9.9