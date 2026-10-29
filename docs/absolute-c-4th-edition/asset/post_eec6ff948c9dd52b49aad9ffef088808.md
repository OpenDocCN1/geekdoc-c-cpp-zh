
# Patterns and UML

> > Einstein argued that there must be simplified explanations of nature, because God is not capricious or arbitrary. No such faith comforts the software engineer. Much of the complexity that he must master is arbitrary complexity.
> >
> > — F. Brooks, “No Silver Bullet: Essence and Accidents of Software Engineering,” *IEEE Computer*, April 1987.

## INTRODUCTION

Patterns and UML are two software design tools that apply no matter what programming language you are using, as long as the language provides for classes and related facilities for object-oriented programming. This chapter presents a very brief introduction to these two topics. It contains no new details about the C++ language.

A pattern in programming is very similar to a pattern in any other context. It is a kind of template or outline of a software task that can be realized as different code in different, but similar, applications.

UML is a graphical language that is used for designing and documenting software created within the object-oriented programming framework.

This chapter uses some material from all of the chapters that come before. However, if you have read most, but not all, of the previous chapters, you can still get all or most of the benefit from reading this chapter.

## 20.1 Patterns

> > I bid him look into the lives of men as though into a mirror, and from others to take an example for himself.
> >
> > — Terence (Publius Terentius Afer, 190–159 B.C.), *Adelphoe*

**Patterns** are design principles that apply across a variety of software applications. To be useful the pattern must apply across a variety of situations. To be substantive the pattern must make some assumptions about the domain of applications to which it applies. For example, the Iterator pattern applies to container classes of almost any kind. Recall that when we discussed iterators in Chapter 19, we first described them in the abstract as ways of cycling through a range of data in any kind of container. We then gave specific applications of
the Iterator pattern, such as list iterator, constant list iterator, reverse list iterator, constant reverse list iterator, vector iterator, constant vector iterator, reverse vector iterator, constant reverse vector iterator, and so forth. Using the overriding pattern of an iterator allowed you to organize your knowledge about container manipulation so that you could easily understand and communicate about software that used the container and iterator classes of the STL.

Imagine the huge amount of detail you would have to digest if we had presented each kind of container iterator separately, with different names for begin(), end(), and ++. Indeed, to make sense of that mountain of detail, you might have had to invent the Iterator pattern yourself. Now that you know about the Iterator pattern, you would surely see that pattern no matter how we presented iterators. However, until somebody had the insight to see and explain the pattern, the various iterators were a large number of different applications that seemed similar but were not organized by any overriding principles. Another related pattern we have been using is the Container pattern. In fact, the way patterns are usually organized, these would be seen as parts of a larger pattern known as the Container-Iterator pattern.

This brief chapter can give only a taste of what patterns are all about. In this section we will discuss a few sample patterns to let you see what patterns look like. There are many more known and used patterns and many more yet to be explicated. This is a new and still developing field of software engineering.

### ADAPTER PATTERN

The Adapter pattern transforms one class into a different class without changing the underlying class, merely by adding a new interface. (The new interface replaces the old interface of the underlying class.) For example, in Chapter 19 we mentioned that the stack and queue template classes of the STL were adapter classes. We described both the stack and queue interfaces and said you could choose the underlying class that would actually store the data. For example, you can have a stack of ints with an underlying vector, stack<int, vector<int> > or a stack of ints with an underlying list, stack<int, list<int> > (or a stack with some other underlying container class, but two is enough for our point). In either case, list or vector, the underlying class is not changed. Only an interface is added.

How might the interface be added? That is an implementation detail that need not be part of the Adapter pattern. There are, however, at least two obvious ways to do it. For example, for a stack adapter the underlying container class could be a member variable of the stack class, or the stack class could be a derived class of the underlying container class.

### THE MODEL-VIEW-CONTROLLER PATTERN

The Model-View-Controller pattern is a way of dividing the I/O task of an application from the rest of the application. The Model part of the pattern performs the heart of the application. The View part is the output part; it displays a picture of the Model's
state. The Controller is the input part; it relays commands from the user to the Model. Normally each of the three interacting parts is regarded as an object with responsibilities for its own tasks. The Model-View-Controller pattern is an example of a divide-and-conquer strategy: One big task is divided into three smaller tasks with well-defined responsibilities. Display 20.1 diagrams the Model-View-Controller pattern.

As a very simple example, the Model might be a container class, such as a stack. The View might display the top of the stack. The Controller gives commands to push or pop data on the stack. The Model (the stack) notifies the View to display a new top-of-stack value whenever the stack contents change.

Any application can be made to fit the Model-View-Controller pattern, but it is particularly well suited to GUI (graphical user interface) design projects, where the View can indeed be a visualization of the state of the Model. (A GUI is simply a windowing interface of the form you find in most modern software applications, as opposed to the simple text I/O we have used in this book.) For example, the Model might be an object to represent your list of computer desktop object names. The View could then be a GUI object that produces a screen display of your desktop icons. The Controller relays commands to the Model (which is a desktop object) to add or delete names. The Model object notifies the View object when the screen needs to be updated.

We have presented the Model-View-Controller pattern as if the user were the Controller, primarily to simplify the example. The Controller need not be under the direct control of the user, but could be some other kind of software or hardware component.

### Display 20.1  Model-View-Controller Pattern

![](img/9505fd46e120aa9c1406715936ff6251_832_0.png)

## Example

### A SORTING PATTERN

The most efficient sorting algorithms all seem to follow a similar pattern. Expressed recursively, they divide the list of elements to be sorted into two smaller lists, recursively sort the two smaller lists, and then recombine the two sorted lists to obtain the final sorted list. In Display 20.2 this pattern is expressed as a template function to sort an array into increasing order using the < operator.

Our Sorting pattern uses a divide-and-conquer strategy. It divides the entire collection of elements to be sorted into two smaller collections, sorts the smaller collections by recursive calls, and then combines the two sorted collections to obtain the final sorted array. The following is the heart of our Sorting pattern:

```
int splitPt = split(a, begin, end);
sort(a, begin, splitPt);
sort(a, splitPt, end);
join(a, begin, splitPt, end);
```

Although the pattern imposes some minimum requirements on the functions split and join, the pattern does not say exactly how the functions split and join are defined. Different definitions of split and join will yield different sorting algorithms.

Array indexes are examples of iterators, and we will use the notation [begin, end) from Chapter 19 to comment the pattern and indeed to think about and derive the pattern.

The function split rearranges the elements in the interval [begin, end) and then divides the interval at a split point, splitPt. The two smaller intervals [begin, splitPt) and [splitPt, end) are then sorted by a recursive call to the function sort. Note that the split function both rearranges the elements in the array interval [begin, end) and returns the index splitPt that divides the interval [begin, end). After the two smaller intervals are sorted, the function join then combines the two sorted intervals to obtain the final sorted version of the entire larger interval.

The pattern says nothing about how the function split rearranges and divides the interval [begin, end). In a simple case, split might simply choose a value splitPt between begin and end and divide the interval into the points before splitPt and the points after splitPt, with no rearranging. We will see an example that realizes the Sorting pattern by defining split this way. On the other hand, the function split could do something more elaborate, such as moving all the “small” elements to the front of the array and all the “large” elements toward the end of the array. This would be a step on the way to fully sorting the values. We will also see an example that realizes the Sorting pattern in this second way.

The simplest realization of this Sorting pattern is the merge sort realization given in Display 20.3. A test program is given in Display 20.4. The merge sort is an example in which the definition of split is very simple. It divides the array into two intervals with no rearranging of elements. The join function is more complicated. After the two subintervals are sorted, it merges the two sorted subarrays, copying elements from the array to a temporary array. The merging starts by comparing the smallest elements in each smaller sorted interval. The smaller of these two ele-
