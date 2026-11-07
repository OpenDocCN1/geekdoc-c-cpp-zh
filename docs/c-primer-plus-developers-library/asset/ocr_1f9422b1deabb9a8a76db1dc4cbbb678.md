```
class Tv
{
    friend class Remote;
};
Class Remote
{
    ...
};
```

![](bbox=[0.163, 0.2607, 0.6966, 0.7201])

```
class Tv;
class Remote
{
    ....
};
Class Tv
{
    friend void Remote::set_chan(Tv & t, int c);
    ...
};
// Remote methods here
```

Figure 15.1  Class friends versus class member friends.

Suppose the advance of technology brings interactive remote controls. For example, an interactive remote control unit might let you enter a response to some question posed on a television program, and the television might activate a buzzer in your remote control if your response is wrong. Ignoring the possibility of television in using such facilities to program the viewers, let’s just look at the C++ programming aspects. The new setup would benefit from mutual friendship, with some Remote methods being able to affect a Tv