A is B squared. So far so good. That the original meaning of ^ is a bitwise exclusive OR does not worry us as we never planned to implement bitwise operations on matrices.

Now we add C to B^2:

```
A = B^2 + C;
```

Looks nice. But it does not work (or does something weird). Why? Because + has a higher priority than ^. Thus, the compiler understands our expression as

```
A = B ^ (2 + C);
```

Oops. Although the operator notation gives a concise and intuitive interface, non-trivial expressions might not meet our expectations. Therefore:

# Respect Priorities

Pay attention that the semantic/intended priority of your overloaded operators matches the priorities of C++ operators.

# 2.7.3 Member or Free Function

Most operators can be defined as members or as free functions. The following operators—any kind of assignment, operator[], operator->, and operator() —must be non-static methods to ensure that their first argument is an lvalue. We have shown examples of operator[] and operator() in Section 2.6. In contrast, binary operators with an intrinsic type as first argument can only be defined as free functions.

The impact of different implementation choices can be demonstrated with the addition operator for our complex class:

```
class complex
{
public:
    explicit complex(double rn = 0.0, double in = 0.0) : r(rn), i(in) {}
    complex operator+(const complex& c2) const
    {
        return complex(r + c2.r, t + c2.i);
    }
    ...
private:
    double r, i;
};
```

```
int main()
{
    complex cc(7.0, 8.0), c4(cc);
    std::cout << "cc + c4 is " << cc + c4 << std::endl;
}
```

Can we also add a complex and a double?

```
std::cout << "cc + 4.2 is " << cc + 4.2 << std::endl;
```