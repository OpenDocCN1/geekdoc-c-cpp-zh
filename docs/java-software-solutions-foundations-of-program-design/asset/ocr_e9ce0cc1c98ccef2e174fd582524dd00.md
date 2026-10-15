# SELF-REVIEW QUESTIONS (see answers in Appendix N)

SR 10.20 Suppose you are designing classes for a banking-related system. Both checking accounts and savings accounts require deposit and withdraw operations. You decide to provide these behaviors using polymorphism. Which polymorphic mechanism (inheritance or interfaces) is best suited for this situation? Provide support for your choice.

SR 10.21 Suppose you are designing classes to help create aquarium-based screen savers. At times, you will want some aquarium objects to “float” from wherever they are to the top of the tank. You decide to provide this behavior using polymorphism. Which polymorphic mechanism (inheritance or interfaces) is best suited for this situation? Provide support for your choice.

SR 10.22 Suppose you are designing classes to support the modeling of rain forest environments. Animal objects, such as butterflies and monkeys, need to grow older periodically. You decide to provide this behavior using polymorphism. Which polymorphic mechanism (inheritance or interfaces) is best suited for this situation? Provide support for your choice.

# 10.7 Event Processing

Let’s revisit the concept of event processing in a Java GUI and see how it relates to polymorphism. As we’ve seen many times in previous examples, in order to respond to an event, we must establish a relationship between an event listener object and a particular component that may fire the event. We establish the relationship between the listener and the component it listens to by making a method call that adds the listener to the component.

For example, suppose a class called MyButtonListener represents an action listener. To set up a listener to respond to a JButton object, we might do the following:

```
JButton button = new JButton();
button.addActionListener (new MyButtonListener());
```

Once this relationship is established, the listener will respond whenever the button fires an action event (because the user pressed it). Now think about the addActionListener method carefully. It is a method of the JButton class, which was written by someone at Sun Microsystems years ago. On the other hand, we might have written the MyButtonListener class today. So how can a method written years ago take a parameter whose class was just written?