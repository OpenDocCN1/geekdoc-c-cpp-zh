data of any other object of that class (using a handle that indicates
which object to access).

![](bbox=[0.124, 0.181, 0.194, 0.239])

# Software Engineering Observation 10.3

*The argument to a copy constructor should be a* `const` *reference to
allow a* `const` *object to be copied.*

![](bbox=[0.12, 0.418, 0.194, 0.474])

# Common Programming Error 10.3

*If the copy constructor simply copied the pointer in the source object
to the target object’s pointer, then both would point to the same
dynamically allocated memory. The first destructor to execute would
delete the dynamically allocated memory, and the other object’s ptr
would point to memory that’s no longer allocated, a situation called a
**dangling pointer**—this would likely result in a serious runtime error
(such as early program termination) when the pointer was used.*