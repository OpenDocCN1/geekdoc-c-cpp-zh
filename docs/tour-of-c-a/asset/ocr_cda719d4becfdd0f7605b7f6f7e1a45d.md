```
Smiley* ps = new Smiley(p,r);
ps->add_eye(e1);
ps->add_eye(e2);
ps->set_mouth(m);
return ps;
```

```
}
```

A program may use that shape reader this:

Click here to view image

```
void user()
{
  std::vector<Shape> v;

  while (cin)
    v.push_back(read_shape(cin));

  draw_all(v);
    rotate_all(v,45);

  for (auto p : v)
    delete p;
}
```

Obviously, the example is simplified – especially with respect to error handling – but it vividly illustrates that user() has absolutely no kind of shapes it manipulates. The user() code can be compiled and used later for new Shapes added to the program. Note that there are no pointers to the shapes outside user(), so user()'s virtual destructor is responsible for deallocating this. Because destructor is virtual, delete operator correctly invokes the Shape's virtual destructor for the most derived class. This is crucial because a derived class may have acquired all kinds of resources (such as file handles, locks, and output streams) that need to be released. In this case, a Smiley deletes its eyes and mouth objects. Once it has done that, it calls Circle's destructor. Objects are constructed "bottom up" (base first) and destructed "top down" (derived) by constructors.

# 5.5.2 Hierarchy Navigation

The read_shape() returns a Shape* that we can treat all Shapes. However, how can we we want to use a member that is only provided by a particular derived class, such as Smiley's wink(); We can ask "is this Shape a kind of Smiley?" using the dynamic_cast operator:

Click here to view image

```
Shape* ps = (read_shape(cin));

if (Smiley* p = dynamic_cast<Smiley*>(ps)) { If ps does point to a Smiley
  Il ... a Smiley; use it ...
}\else {
  Il ... not a Smiley, try something else ...
```