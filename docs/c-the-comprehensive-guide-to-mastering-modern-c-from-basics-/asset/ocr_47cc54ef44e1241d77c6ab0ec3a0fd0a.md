include an entire namespace with using namespace locally
—for example, within a function—but never globally in a
*.cpp file—and certainly not in a header file.

Because fir is a local variable in main, you can call print
as as a method:

```
fir.print(std::cout); std::cout << "\n";
```

It's a bit trickier with operator<<. If you simply write
std::cout << tanne, it will cause an error because the
compiler looks for a suitable free function in all available
namespaces (for operators, std is also searched). So it
looks for the following:

+   :operator(std::ostream&, const Tree&);—globally, the
level where main is

+   std::operator<<(std::ostream&, const Tree&);—where std
is searched

+   plant::exampleNames::operator<<(std::ostream&, const
Tree&)—because using namespace plant::exampleNames
was previously declared

The overload for Tree is in namespace plant:

plant::operator<<(std::ostream&, const Tree&);

To use an operator defined within a namespace, you
must first make it available so that it is included in the
search. There are two options here:

+   using plant::operator<<—to only fetch the operator