# 864 Introduction to C++

```
struct Msg /* This structure is used as an argument in function calls. */
{
    int code;
    int CRV;
    int call index;
    /* Normally, the structure contains many members that correspond
to the information elements conveyed by each message. */
}
```

```
class Call // Each call is represented by a Call object.
{
private:
    int CRV; // It holds the identifier of the call.
    int state; // It holds the state of the call.
    /* Normally, the class contains many members related to the
call, such as the phone numbers of the two parties and the duration of the
call. */
ublic:
    Call(int crv);
    int fsm(Msg *p);
    int send_msg(Msg *p);
}
```

```
class Prctl
private:
    vector<Call> calls; // We use a vector to store the calls.
    map<int,int> map_CRV; /* Mapping of the key, which is the CRV value
of each call with the position of the object in the vector. Thus, we find the
position of the object that corresponds to a CRV value. */
public:
    int handle_up_msg(Msg *p); /* It is used for communication with the
upper layer. */
    int handle_low_msg(int data[]); /* It is used for communication with the
lower layer. */
    int find_call(int CRV) const;
    void show() const { cout << "\nCalls: " << calls.size() << '\n'; } /* As
you see we define the function in the header file. It displays the number
of the established calls. */;;
```

```
#endif
```

With the object-oriented approach makes sense each call to be represented by a respective object.
In example, each call is represented by an object of the Call class. It also simplifies the design to
have another class to manage the calls. In our example, the Prctl class manages the calls and provides
t functions with communication with the outside world, which is, with the upper and lower layers. To store
the calls we use a vector. Let us see the prctl.cpp.

```
#include "general.h"
#include "fsm.h"
Prctlctl; /* I declare it as global, to show you how to use it as extern
of other files. */
```