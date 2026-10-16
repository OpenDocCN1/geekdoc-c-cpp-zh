LS::window. But that does not affect our class hierarchy design discussion, so to simplify I ignore naming and namespace issues.

Another problem is that every derived class shares the basic data declared in Ival_box. That data is, of course, an implementation detail that also crept into our Ival_box interface. From a practical point of view, it is also the wrong data in many cases. For example, an Ival_slider doesn’t need the value stored specifically. It can easily be calculated from the position of the slider when someone executes get_value(). In general, keeping two related, but different, sets of data is asking for trouble. Sooner or later someone will get them out of sync. Also, experience shows that novice programmers tend to mess with protected data in ways that are unnecessary and that cause maintenance problems. Data members are better kept private so that writers of derived classes cannot mess with them. Better still, data should be in the derived classes, where it can be defined to match requirements exactly and cannot complicate the life of unrelated derived classes. In almost all cases, a protected interface should contain only functions, types, and constants.

Deriving from BBwidget gives the benefit of making the facilities provided by BBwidget available to users of Ival_box. Unfortunately, it also means that changes to class BBwidget may force users to recompile or even rewrite their code to recover from such changes. In particular, the way most C++ implementations work implies that a change in the size of a base class requires a recompilation of all derived classes.

Finally, our program may have to run in a mixed environment in which windows of different user-interface systems coexist. This could happen either because two systems somehow share a screen or because our program needs to communicate with users on different systems. Having our user-interface systems “wired in” as the one and only base of our one and only Ival_box interface just isn’t flexible enough to handle those situations.

# 21.2.2 Interface Inheritance

So, let’s start again and build a new class hierarchy that solves the problems presented in the critique of the traditional hierarchy:

+   [1] The user-interface system should be an implementation detail that is hidden from users who don’t want to know about it.  
+   [2] The Ival_box class should contain no data.  
+   [3] No recompilation of code using the Ival_box family of classes should be required after a change of the user-interface system.  
+   [4] Ival_boxes for different interface systems should be able to coexist in our program.

Several alternative approaches can be taken to achieve this. Here, I present one that maps cleanly into the C++ language. First, I specify class Ival_box as a pure interface:

```
class Ival_box {
public:
    virtual int get_value() = 0;
    virtual void set_value(int i) = 0;
    virtual void reset_value(int i) = 0;
```