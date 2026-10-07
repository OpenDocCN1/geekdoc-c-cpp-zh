# Chapter 15 Friends, Exceptions, and More

object, as before, and with some Tv methods being able to affect a Remote object. This can be accomplished by making the classes friend to each other.Thatis, Tv will be a friend to Remote in addition to being a friend to Tv. One point to keep in mind is that a Tv method that uses a Remote object can be prototyped before the class declaration but must be defined after the declaration so the compiler will have enough information to compile the method. The setup would look like this:

```
class TV {
  friend class Remote;
  public:
    void buzz(Remote & r);
  }
class Remote {
  friend class Tv;
  public:
    void Bool volup(Tv & t) { t.volup(); }
}
inline void Tv::buzz(Remote & r) {
```

The Remote declaration follows the Tv declaration, Remote::volup() can be defined in the class declaration. However, the Tv::buzz() method must be defined outside the Tv declaration so that the definition can follow the Remote declaration. If you don't want buzz() to be inline, you need to define it in a separate method files.

# Shared Friends

Another use for friends is when a function needs to access private data in two separate classes. Logically, such a function should be a member function of each class, but that is impossible. It could be a member of one class and a friend to the other, but sometimes it's more reasonable to make the function a friend to both. Suppose, for example, that you have a Probe class that represents some sort of measuring device and an Analyzer class that represents some sort of analyzing device. Each has an internal clock, and you would like to be able to synchronize the two clocks.You could use something along the following lines:

```
class Analyzer; // forward declaration {
  friend void sync(Analyzer & a, const Probe & p); // sync a to p
  friend void sync(Probe & p, const Analyzer & a); // sync p to a
```