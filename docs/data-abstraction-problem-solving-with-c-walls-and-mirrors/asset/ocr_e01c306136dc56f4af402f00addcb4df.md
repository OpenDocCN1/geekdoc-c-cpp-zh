# 334 C++ INTERLUDE 4 Class Relationships and Reuse

FIGURE C4-1 Inheritance: Relationships among timepieces

![](bbox=[0.248, 0.137, 0.893, 0.435])

A class can derive the behavior and structure of another

Inheritance, in fact, is a relationship among classes. One class can derive the behavior and structure of another class. For example, Figure C4-1 illustrates some relationships among various timepieces. Digital clocks, for example, include the clock in the dashboard of your car, the clock on your microwave oven. All digital clocks have the same underlying structure and perform operations as

+   - Set the time
- Advance the time
- Display the time

A digital alarm clock is a digital clock

A digital alarm clock is a digital clock that also has alarm methods, such as

+   - Set the alarm
- Enable the alarm
- Sound the alarm
- Silence the alarm

Inheritance enables the reuse of existing classes

That is, a digital alarm clock has the structure and operations of a digital clock, and in addition, has alarm and operations to manipulate the alarm.
You can think of the group of digital clocks and the group of digital alarm clocks as classes. The class of digital alarm clock is a derived class, or subclass, of the class of digital clocks. The class of digital clocks is a base class, or superclass, of the digital alarm clocks. Inheritance enables you to reuse software components when you define a new class. For example, you can reuse your design and implementation of an analog clock when you define a cuckoo clock.
In C++, a derived class inherits all the members of its base class, except the constructors and destructor. That is, a derived class has the data members and methods of the base class in addition to what it inherits. A derived class can also revise any inherited method. For example, according to Figure C4-1, a cuckoo clock is a descendant of an analog clock, like the one on a classroom wall.

A derived class inherits the members of its base