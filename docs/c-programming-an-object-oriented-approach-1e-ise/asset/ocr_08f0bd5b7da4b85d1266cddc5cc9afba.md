![](bbox=[0.314, 0.089, 0.767, 0.173])

**Figure 7.1** A type and its instances

Any instance we encounter in this world has a set of attributes and a set of behaviors.

# Attributes

In real life an attribute is a characteristic ascribed to an instance. In computer science, an attribute is any characteristic that interests us in an instance. For example, if the instance is an employee, we may be interested only in the employee’s *name*, *address*, *position*, and *salary*. On the other hand, if the instance is a student in a university, we may be interested only in the student’s *name*, *year*, *courses taken*, and *grades*. If the instance is a circle, we may be interested only in its *radius*, *perimeter*, and *area*.

> An attribute is a characteristic of an instance that we are interested in.

# Behaviors

When we think about instances, we also think about their behaviors. In this sense, a *behavior* is an operation that an instance can perform on itself. For example, if an instance is an employee, we assume that she can give her *name*, her *address*, and her *salary*. On the other hand, if an instance is a circle, we assume that it can give its *radius*, its *perimeter*, and its *area*. Note that in object-oriented programming, we assume that an instance is capable of performing an operation on itself.

> A behavior is an operation that we assume an instance can perform on itself.

# 7.1.2 Classes and Objects in Programs

In object-oriented programming, we still use the terms *type* and *instance*. In C++, a user-defined type can be created using a construct named *class*. An instance of a class is referred to as an *object*. This means that we use *type* and *class*. We also use *instances* and *objects*. In object-oriented programming, attributes and behaviors of an object are represented as *data members* and *member functions*.

# Data Members

A **data member** of an object is a variable whose value represents an attribute. For example, the radius of a circle object can be represented by the value of a variable of type *double*. In other words, the attribute of an object of type *circle* can be effectively represented as a variable of type *double* that holds the value of the radius for that instance. However, some attributes of an instance are not independent; they may depend on values of other attributes. For example, the perimeter and the area of a circle may be two attributes for a mathematician, but we do not represent them as data members because both depend on the value of the radius.