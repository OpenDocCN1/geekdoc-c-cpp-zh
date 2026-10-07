# Answers to Chapter Review for Chapter 14 1357

```
2. Gloam::Gloam(int g, const char * s) : glip(g), fb(s) { }
Gloam::Gloam(int g, const Frabious & fr) : glip(g), fb(fr) {
// note: the above uses the default Frabious copy constructor
void Gloam::tell()
{
  fb.tell();
  cout << glip << endl;
}
```

```
3. Gloam::Gloam(int g, const char * s) : glip(g), Frabious(s) { }
Gloam::Gloam(int g, const Frabious & fr) : glip(g), Frabious(fr) {
// note: the above uses the default Frabious copy constructor
void Gloam::tell()
{
  Frabious::tell();
  cout << glip << endl;
}
```

```
4. class Stack<Worker *> {\private:
  enum {MAX = 10}; // constant specific to class
  Worker * items[MAX]; // holds stack items
  int top; // index for top stack item
public:
  Stack();
  Boolean is();
  Boolean isfull();
  Boolean push(Worker * & item); // add item to stack
  Boolean pop(Worker * & item); // pop top into item
};
```

Listing 14.18 generates four templates: ArrayTP<int, 10>, ArrayTP<double, 10>, ArrayTP<int, 5>, and Array<int, 5, 10>.

6. If two lines of inheritance for a common ancestor, the class winds up having two copies of the ancestor's members. Making the ancestor class a virtual base class to its immediate descendants solves problem.