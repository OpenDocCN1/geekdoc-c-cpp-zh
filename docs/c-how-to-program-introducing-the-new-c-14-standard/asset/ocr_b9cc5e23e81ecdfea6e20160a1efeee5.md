# 9.8.2 Constructors and Destructors
for Non-`static` Local Objects

The constructor for a non-`static` local object is called when execution reaches the point where that object is defined—the corresponding destructor is called when execution leaves the object’s scope (i.e., the block in which that object is defined has finished executing).

Constructors and destructors for non-`static` local objects are called each time execution enters and leaves the scope of the object. Destructors are not called for local objects if the program terminates with a call to function `exit` or function `abort`.