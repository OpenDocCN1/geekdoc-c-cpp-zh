# ## Assignment Operator and Classes

Suppose that myClock and yourClock are clockType objects, as defined previously. Furthermore, suppose that the values of myClock and yourClock are as shown in Figure 11-3(a).

![](bbox=[0.2, 0.19, 0.91, 0.38])

**FIGURE 11-3** myClock and yourClock before and after executing the statement myClock = yourClock;

The statement:

```
```
myClock = yourClock;        //Line 1
```
```

copies the value of yourClock into myClock. That is,

+   - the value of yourClock.hr is copied into myClock.hr,
+   - the value of yourClock.min is copied into myClock.min, and
+   - the value of yourClock.sec is copied into myClock.sec.

In other words, the values of the three member variables of yourClock are copied into the corresponding member variables of myClock. Therefore, an assignment statement performs a member-wise copy. After the statement in Line 1 executes, the values of myClock and yourClock are as shown in Figure 11-3(b).

# ## Class Scope

A class object can be either automatic (that is, created each time the control reaches its declaration and destroyed when the control exits the surrounding block) or static (that is, created once, when the control reaches its declaration, and destroyed when the program terminates). Also, you can declare an array of class objects. A class object has the same scope as other variables. A member of a class has the same scope as a member of a struct. That is, a member of a class is local to the class. You access a class member outside of the class by using the class object name and the member access operator (.).