
# Chapter 15 Friends, Exceptions, and More

However, for the compiler to process this statement, it needs to have already seen the Remote definition. Otherwise, it won't know Remote is a class and that set_chan() is a method of class. This suggesting the Remote definition above the Tv definition. But the fact that Remote method Tv objects that the Tv definition should appear above the Remote definition. Part of the way around the circular dependency is to use a forward declaration. To do so, you insert the following statement above the Remote definition:

```
class Tv;
// forward declaration
```

This provides the following arrangement:

```
class Tv; // forward declaration
class Remote { ... };
class Tv { ... };
```

Could you use the following arrangement instead?

```
class Remote; // forward declaration
class Tv { ... };
class Remote { ... };
```

The answer is no. The reason, as mentioned earlier, is when the compiler sees that a Remote method is declared as a friend in the Tv class declaration, the compiler needs to have already viewed the declaration of the Remote class in general and of the set_chan() method in particular.

Another difficulty remains. In Listing 15.1, the Remote definition contains inline code such as the following:

```
void onoff(Tv & t) { t.onoff(); };
```

This calls a Tv method, the compiler needs to see the Tv class declaration at this point so it knows what methods Tv has. As you've seen, declaration necessarily follows the Remote declaration. The solution to this problem is to restrict Remote to method declarations and to place the actual definitions after the Tv class. This leads to the following ordering:

```
class Tv; // forward declaration
class Remote { ... }; // Tv-using methods as prototypes that
class Tv { ... };
// put method definitions here
```

The Remote prototypes look like this:

```
void onoff(Tv & t);
```

All the compiler know when inspecting this prototype is that Tv is a class, and the forward declaration supplies that information. By the time the compiler reaches the actual method definitions, it has already read the Tv class declaration and has the added information needed to compile those methods. By using the inline keyword in the method definitions, you can still make the methods inline methods. Listing 15.4 shows the revised header file.

# Listing 15.4 tvfm.h

```
// tvfm.h -- Tv and Remote classes using a friend member
#ifndef TVFM_H_
#define TVFM_H_

class Tv;

// forward declaration
class Remote
{
public:
    enum State{Off, On};
    enum {MinVal,MaxVal = 20};
    enum {Antenna, Cable};
    enum {TV, DVD};
private:
    int mode;
public:
    Remote(int m = TV) : mode(m) {}
    bool volup(Tv & t); // prototype only
    bool vol(Tv & t);
    void onoff(Tv & t);
    void chanup(Tv & t);
    void chandown(Tv & t);
    void set_mode(Tv & t);
    void set_input(Tv & t);
    void set_chan(Tv & t, int c);
};

;
```

```
class Tv
{
public:
    friend void Remote::set_chan(Tv & t, int c);
    enum State{Off, On};
    enum {MinVal,MaxVal = 20};
    enum {Antenna, Cable};
    enum {TV, DVD};

Tv(int s = Off, int mc = 125) : state(s), volume(5);
maxchannel(mc), channel(2), mode(Cable), input(TV) {}
void onoff() {state = (state == On) ? Off : On;}
bool ison() const {return state == On;}
bool volup();
```

```
bool voldown();
void chanup();
void chandown();
void set_mode() {mode = (mode == Antenna)? Cable : Antenna;}
void set_input() {input = (input == TV)? DVD : TV;}
void settings() const;
```

```
private:
int state;
int volume;
int maxchannel;
int channel;
int mode;
int input;
```

```
// Remote methods as inline functions
inline bool Remote::volup(TV & t) { return t.volup(); }
inline bool Remote::voldown(TV & t) { return t.voldown(); }
inline void Remote::inoff(TV & t) { t.inoff(); }
inline void Remote::chanup(TV & t) {t.chanup(); }
inline void Remote::chandown(TV & t) {t.chandown();}
inline void Remote::set_mode(TV & t) {t.set_mode(); }
inline void Remote::set_input(TV & t) {t.set_input(); }
inline void Remote::set_chan(TV & t, int c) {t.channel = c;}
```

> If you include tfvm.h instead of tv.h in tv.cpp and use_tv.cpp, the resulting program has the same as the original. The difference is that one of Remote methods—is a friend to the TV class. Figure 15.1 illustrates this difference.

Recall that inline functions have internal linkage, which means the function definition must be in the file that uses the function. Here, the inline definitions are in the header file, so including the header file in the file that uses the definitions places the definition in the right place. You could place the definitions in the implementation file instead, provided that you remove the inline keyword, which gives the functions external linkage.

By the way, the entire Remote class as a friend doesn't need a forward declaration because the friend statement itself identifies Remote as a class:

```
friend class Remote;
```

# Other Friendly Relationships

Other combinations of friends and classes besides the ones discussed so far in this chapter are possible. Let's take a brief look at some of them.

```
class Tv {
    friend class Remote;
    ...
};
class Remote {
    private:
    };
```

Tv class determines who its friends are

![](img/cd111a87c1db9aff4db4b18834327463_901_0.png)

Remote object
Tv object
All Remote methods can affect private Tv members.

```
class Tv;
class Remote {
    ...
};\class Tv {
    friend void Remote::set_chan(Tv & t, int c);
};
// Remote methods here
```

Tv class determines who its friends are

![](img/cd111a87c1db9aff4db4b18834327463_901_0.png)

void set_chan(Tv & t, int c);
Remote object
Tv object
All Remote methods can affect private Tv members.

Figure 15.1 Class friends versus class friends.

Suppose the advance of technology brings interactive controls. For example, an interactive remote unit might let you enter a response to some question posed on a television, and the television might activate a buzzer in your remote if your response is wrong. Ignoring the possibility of television using such facilities to program the viewers, let's just look at the C++ aspects. The new setup would benefit from mutual friendship, with some Remote methods being able to affect a object, as before, and with some Tv methods being able to affect. This can be accomplished by making the classes friend to each other. That, Tv will be a friend to Remote in addition to being a friend to Tv. One point to keep in mind is that a Tv method that uses a Remote object can be prototyped before the class declaration but must be defined after the declaration so the compiler will have enough information to compile the method. The setup would look like this:

```
class TV {
  friend class Remote;
  public:
    void buzz(Remote & r);
  }
class Remote {
  friend class Tv;
  public:
    void volup(Tv & t) { t.volup(); }
}
inline void Tv::buzz(Remote & r) {
```

The Remote declaration follows the Tv declaration, Remote::volup() can be defined in the class declaration. However, the Tv::buzz() method must be defined outside the Tv declaration so that the definition can follow the Remote declaration. If you don't want buzz() to be inline, you need to define it in a separate method files.

# Shared Friends

Another use for friends is when a function needs to access private data in two separate classes. Logically, such a function should be a member function of each class, but that is impossible. It could be a member of one class and a friend to the other, but sometimes it's more reasonable to make the function a friend to both. Suppose, for example, that you have a Probe class that represents some sort of measuring device and an Analyzer class that represents some sort of analyzing device. Each has an internal clock, and you would like to be able to synchronize the two clocks. You could use something along the following lines:

```
class Analyzer; // forward declaration {
  friend void sync(Analyzer & a, const Probe & p); // sync a to p
  friend void sync(Probe & p, const Analyzer & a); // sync p to a
```
