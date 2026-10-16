```
for(int i = 0; i<9; ++i)
pos.at(i) = arg.pos.at(i); return *this;
}
// ... other operations ...
enum State { empty, nought, cross };
private:
vector<State> pos;
};
```

This was reported to have been part of a real program. It uses the “magic number” 9 to implement a copy assignment that accesses its argument arg without checking that the argument actually has nine elements. Also, it explicitly implements the copy assignment, but not the copy constructor. This is not what I consider good code.

# Section 17.6.3.4 Partially Specified Invariants 523

We defined copy assignment, so we must also define the destructor. That destructor can be =default because all it needs to do is to ensure that the member pos is destroyed, which is what would have been done anyway had the copy assignment not been defined. At this point, we notice that the user-defined copy assignment is essentially the one we would have gotten by default, so we can =default that also. Add a copy constructor for completeness and we get:

```
class Tic_tac_toe {
public:
Tic_tac_toe(): pos(9) {} // always9positions
Tic_tac_toe(const Tic_tac_toe&) = default;
Tic_tac_toe& operator=(const Tic_tac_toe& arg) = default;
~Tic_tac_toe() = default;
// ... other operations ...
enum State { empty, nought, cross };
private:
vector<State> pos;
};
```

Looking at this, we realize that the net effect of these =defaults is just to eliminate move operations. Is that what we want? Probably not. When we made the copy assignment =default, we eliminated the nasty dependence on the magic constant 9. Unless other operations on Tic_tac_toe, not mentioned so far, are also “hardwired with magic numbers,” we can safely add move operations. The simplest way to do that is to remove the explicit =defaults, and then we see that Tic_tac_toe is really a perfectly ordinary type:

```
class Tic_tac_toe {
public:
// ... other operations ...
enum State { empty, nought, cross };
private:
vector<State> pos {Vector<State>(9)}; // always9positions
```