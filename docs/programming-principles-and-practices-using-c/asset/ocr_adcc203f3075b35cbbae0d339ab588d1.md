# 18.3.1 Copy constructors

So, what do we do? We’ll do the obvious: provide a copy operation that copies the elements and make sure that this copy operation gets called when we initialize one **vector** with another.

Initialization of objects of a class is done by a constructor. So, we need a constructor that copies. Unsurprisingly, such a constructor is called a *copy constructor*. It is defined to take as its argument a reference to the object from which to copy. So, for class **vector** we need

```
vector(const vector&);
```

This constructor will be called when we try to initialize one **vector** with another. We pass by reference because we (obviously) don’t want to copy the argument of the constructor that defines copying. We pass by **const** reference because we don’t want to modify our argument (§8.5.6). So we refine **vector** like this:

```
class vector {
    int sz;
    double* elem;
  public:
    vector(const vector&) ; // copy constructor: define copy
    // ...
};
```

The copy constructor sets the number of elements (**sz**) and allocates memory for the elements (initializing **elem**) before copying element values from the argument **vector**:

```
vector:: vector(const vector& arg
    // allocate elements, then initialize them by copying
    :sz(arg.sz), elem(new double[arg.sz])
    {
    copy(arg.elem,arg.elem+sz,elem); // std::copy(); see §8.5.2
    }
```

Given this copy constructor, consider again our example:

```
vector v2 = v;
```

This definition will initialize **v2** by a call of **vector**’s copy constructor with **v** as its argument. Again given a **vector** with three elements, we now get

![](bbox=[0.32, 0.84, 0.77, 0.92])