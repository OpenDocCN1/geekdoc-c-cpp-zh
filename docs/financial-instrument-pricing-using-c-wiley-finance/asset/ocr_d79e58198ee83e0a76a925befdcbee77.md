# 10.5 BOOST DATE AND TIME

We now introduce the Boost library that supports date and time entities. It is an understatement to say that having access to data structures and C++ classes that model *temporal entities* is important in many kinds of scheduling, management information and calendar-driven applications. To this end, the *Boost date–time* library has extensive support for many use cases, for example:

+   - Creating dates and times based on Gregorian, Posix and local time regimes.
+   - Date iterators; for example, iterating over the days in a week.
+   - Date generators and algorithms.
+   - Local and UTC (*Coordinated Universal Time*) support.
+   - Date and time input/output and serialisation.

The approach that we take in this book is to discuss the main features in the library and to give a number of ‘101’ examples. We then continue by examining several extended examples and applications in which dates and times are used. For example, one project is to migrate and extend legacy code for computational finance applications to the current library (see Duffy, 2004B).

This chapter takes a hands-on approach and we discuss numerous examples to show the usefulness of the *Boost date–time* library. It is a large library.

# 10.5.1 Overview of Concepts and Functionality

Date and time abstractions are of fundamental importance in many kinds of applications. In particular, systems that incorporate *temporal logic* are numerous. Instead of defining our own libraries and functions to process dates and times we now use the *Boost date–time* library and extend it to suit the needs of specific application areas. To this end, we discuss the most important classes and functionality in the library. We can view time as a one-dimensional line or continuum.

There are three basic *temporal types*:

+   - *Time Point*: this is a specifier for a location in the time continuum.
+   - *Time Duration*: this is a length of time that is unattached to any point in the time continuum. It is a ‘floating’ quantity with a magnitude.
+   - *Time Interval (Time Period)*: this is a duration of time that is attached to a specific point in the time continuum.

Corresponding to each of these concepts is a so-called *resolution* that is defined as the smallest representable duration. We define a *Time System* as a set of temporal types in combination with rules and operations to label and compute with these temporal types. A *Calendar System* is a time system with a resolution of one day. In this chapter we focus on the *Gregorian Calendar System* because it is the most widely used system. We also discuss the UTC calendar system that is used in civil time applications. *Local time systems* are based on UTC and are adjusted for the rotation of the earth so that daylight hours are similar everywhere. Finally, a *Clock Device* is a software component that is tied to hardware and that provides the current date or time in a time system.