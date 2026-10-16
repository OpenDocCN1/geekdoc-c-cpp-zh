# 22.2.4 Recovering an Interface

From a design perspective, dynamic_cast (§22.2.1) can be seen as a mechanism for asking an object if it provides a given interface.

As an example, consider a simple object I/O system. Users want to read objects from a stream, determine that they are of the expected types, and then use them. For example:

```
void user()
{
// ... open file assumed to hold shapes,and attach ss as an istream for that file ...
unique_ptr<Io_obj> p {get_obj(ss)}; // read object from stream

if (auto sp = dynamic_cast<Shape *>(p.get())) {
sp->draw(); // use the Shape
// ...
}
else {
// oops: non-shape in Shape file
}
}
```

The function user() deals with shapes exclusively through the abstract class Shape and can therefore use every kind of shape. The use of dynamic_cast is essential because the object I/O system can deal with many other kinds of objects, and the user may accidentally have opened a file containing perfectly good objects of classes that the user has never heard of.

I used unique_ptr<Io_obj> (§5.2.1, §34.3.1) so that I would not forget to delete the object allocated by get_obj().

This object I/O system assumes that every object read or written is of a class derived from Io_obj. Class Io_obj must be a polymorphic type to allow the user of get_obj() to use dynamic_cast to recover the “true type” of a returned object. For example:

```
class Io_obj {
public:
virtual Io_obj* clone() const =0; // polymor phic
virtual ~Io_obj() {}
};
```

The critical function in the object I/O system is get_obj(), which reads data from an istream and creates class objects based on that data. Assume that the data representing an object on an input stream is prefixed by a string identifying the object’s class. The job of get_obj() is to read that string and call a function capable of reading and creating an object of the right class. For example:

```
using Pf = Io_obj*(istream&); // pointer to function returning an Io_obj*
map<string,Pf> io_map; // maps strings to creation functions
string get_word(istream& is); // read a word from is; throwRead_error if the read failed

Io_obj * get_obj(istream& is) {
```