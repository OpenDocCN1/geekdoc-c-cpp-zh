```
void g(A& a)
{
    B& bref= static_cast<B&>(a);
    std::cout << "fb returns " << bref.fb() << "\\n";
}
```

The compiler verifies that B is a sub-class of A and accepts our implementation. When the argument a refers to an object that is not of type B (or a sub-type thereof), the program behavior is undefined—the most likely result being a crash.

In our diamond-shaped example, we can also down-cast pointers from B to D. To this end, we declare pointers of type B* that are allowed to refer to objects of sub-class D:

```
B *bbp= new B, *dbp= new D;
```

The compiler accepts a down-cast to D* for both pointers:

Click here to view code image

```
D* dbp = static_cast<D*>(bbp); // erroneous down-cast not detected
D* ddp = static_cast<D*>(dbp); // correct down-cast (not checked)
```

Since no run-time checks are performed, it is our responsibility as programmers to only refer to objects of the right type. bbp points to an object of type B, and when we dereference the pointer dbp, we risk data corruption and program crashes. In this small example, a smart compiler might detect the erroneous down-cast by static analysis and emit a warning. In general, it is not always possible to back-trace the actual type referenced by a pointer, especially as it can be selected at run time:

Click here to view code image

```
B* bxp = (argc > 1) ? new B : new D;
```

In Section 6.6.1, we will see an interesting application of a static down-cast that is safe since type information is provided as a template argument.

dynamic_cast performs a run-time test whether the actually casted object has the target type or a sub-type of it. It can only be applied to a polymorphic type (a class that defines or inherits one or more virtual functions, §6.1):