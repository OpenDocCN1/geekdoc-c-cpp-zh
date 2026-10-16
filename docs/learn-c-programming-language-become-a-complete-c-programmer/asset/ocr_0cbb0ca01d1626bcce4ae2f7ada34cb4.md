us to remove the error-handling code from the main algorithm. The resulting code is simpler and less errorprone than its traditional counterpart.

This technique for managing resources using local objects is usually referred to as “Resource Acquisition Is Initialization” (RAII; §5.2). This is a general technique that relies on the properties of constructors and destructors and their interaction with exception handling.

It is often suggested that writing a “handle class” (a RAII class) is tedious so that providing a nicer syntax for the catch(...) action would provide a better solution. The problem with that approach is that you need to remember to “catch and correct” the problem wherever a resource is acquired in an undisciplined way (typically dozens or hundreds of places in a large program), whereas the handler class need be written only once.

An object is not considered constructed until its constructor has completed. Then and only then will stack unwinding (§13.5.1) call the destructor for the object. An object composed of subobjects is constructed to the extent that its subobjects have been constructed. An array is constructed to the extent that its elements have been constructed (and only fully constructed elements are destroyed during unwinding).

A constructor tries to ensure that its object is completely and correctly constructed. When that cannot be achieved, a well-written constructor restores – as far as possible – the state of the system to what it was before creation. Ideally, a well-designed constructor always achieves one of these alternatives and doesn’t leave its object in some “half-constructed” state. This can be simply achieved by applying the RAII technique to the members.

Consider a class X for which a constructor needs to acquire two resources: a file x and a mutex y (§5.3.4). This acquisition might fail and throw an exception. Class X’s constructor must never complete having acquired the file but not the mutex (or the mutex and not the file, or neither). Furthermore, this should be achieved without imposing a burden of complexity on the programmer. We use objects of two classes, File_ptr and std::unique_lock (§5.3.4), to represent the acquired resources. The acquisition of a resource is represented by the initialization of the local object that represents the resource:

```
class Locked_file_handle {
File_ptr p;
unique_lock<mutex> lck;

public:
X(const char* file, mutex& m)

:p{ file ,"rw"}, // acquire “file”
lck{m} // acquire “m”
{}
//...
};
```

Now, as in the local object case, the implementation takes care of all of the bookkeeping. The user doesn’t have to keep track at all. For example, if an exception occurs after p has been constructed but before lck has been, then the destructor for p but not for lck will be