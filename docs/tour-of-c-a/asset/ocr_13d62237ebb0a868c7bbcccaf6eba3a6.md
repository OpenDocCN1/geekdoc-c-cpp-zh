```
double sum = 0;
for (int i=0; i<s; ++i)
    sum+=elem[i];
return sum;
```

ll compute the elements

There is a long way to go before Vector is as elegant and flexible as the standard-library vector. In particular, a user of Vector has to know every detail of Vector's representation. The rest of this chapter and the next introduced Vector as an example of language features and techniques. Chapter 12 presents the standard-library vector, which contains many nice improvements.

I use vector and other standard-library components as examples

+   * to illustrate language features and design techniques,
* to help you learn and emulate the standard-library components.

Don't reinvent standard-library components such as vector and string; use them. The standard-library types have lower-case names, to distinguish names of types used to illustrate design and implementation techniques (e.g., Vector and String), I capitalize them. We (do) use struct members through a name (and through a reference) and -> to access struct members through a pointer. For example:

Click here to view code image

```
void f(Vector v, Vector& rv, Vector* pv) {
    int i1 = v.sv;
    int i2 = rv.sv;
    int i3 = pv->sv;
}
```

# 2.3 Classes

Having data specified separately from the operations on it has advantages, such as the ability to use the data in arbitrary ways. However, a tighter connection between the representation and the operations is needed for a user-defined type to have all the properties expected of a "real type.\ In particular, we want to keep the representation inaccessible to users so as to simplify, guarantee consistent use of the data, and allow us to improve the representation. To do that, we have access to the inaccessible data. The language mechanism for that is called a class. A class has a set of members which can be data, function, or type members.

The interface of a class is defined by its public members, and the private members are accessible only through that interface. The public and private parts of a class declaration can appear in any order, but conventionally we the public first and the private declarations later, except when we want to emphasize the representation. For example:

Click here to view code image

```
class Vector {
public:
    Vector(int s) :elem(new double[s]), sz(s) {} // construct Vector
```