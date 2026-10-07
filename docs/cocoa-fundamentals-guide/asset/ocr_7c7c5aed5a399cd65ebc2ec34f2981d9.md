# CHAPTER 3

# Adding Behavior to a Cocoa Proxy

An exception to the parallel roles of a class whose instances appear on an Interface Builder palette. The general procedure is to define the class in your project, drag the object from the Interface Builder palette into your interface, and then associate that object with your subclass using the Custom Class name of the Interface Builder Info window. However, in this case the `initWithCoder:` method for the subclass is not invoked during unarchiving; an `init` message is sent instead. You should perform any special setup-ups for your custom object in `awakeFromInit:`, which is invoked after all objects in a nib file have been unarchived.

# Storing and Accessing Properties

The word property has a general and a language-specific meaning in Cocoa. The general notion comes from the design pattern of object modeling. The language-specific meaning relates to the feature of declared properties.

As described in [Object Modeling](page 167), a property is a defining characteristic of an object (called in the object modeling pattern an *entity*) and is of its encapsulated data. A property can be of two sorts: an attribute, such as title and location, or a relationship. Relationships can be one-to-one or to-many, and can take many forms, such as an outlet, a delegate, or collector of other objects. Properties are usually, but not always, stored as instances.

Part of the overall strategy for a well-designed class is to enforce encapsulation. Clients should not directly access properties where they are stored, but access them through the interface of the class. The methods that access properties of the object are called accessor methods (or, simply, accessor) and set the values of an object's properties. They function as the getters, regulating access to them and enforcing the encapsulation of the object's instance data. The accessor method that gets a value is a getter, and the method that sets a property's value is a setter method.

The declared properties feature (introduced in Objective-2.0) has brought changes, some subtle, to how you control access to properties. A declared property is a shorthand for declaring the getter and setter methods of a class's property. In the implementation block you can request the compiler to synthesize these methods. As summarized in [Declared Properties](page 61), you declare a property, using the `@property` directive, in the `@interface` block of data. The definition specifies the name and type of the property and may qualifiers that tell the compiler how to implement the accessor methods.

When designing a class, several factors affect how you store and access the properties of the class. You may choose to use the declared properties and have the compiler synthesize accessor methods for you. Or you may implement the class's accessor methods yourself; this is an option even if you use declared properties. Another important factor is whether your code operates in a garbage-collected environment. If the garbage collector is enabled, the implementation of accessor methods is much simpler than it is in memory-managed code. The following sections describe the various alternatives for storing and accessing properties.

# Taking Advantage of Declared Properties

Unless you have a compelling reason to do otherwise, it is recommended that you use the declared properties of Objective-C 2.0 in new projects rather than manually writing all of your accessor methods. First, declared properties relieve you from the tedious burden of accessor-method implementation. Second, by having the compiler synthesize accessor methods for you, you reduce the probability of programming errors and ensure more consistent behavior in your class implementation. Finally, the declarative style of declared properties makes your intent clear to other developers.

Basic subclass Design
2010-12-13 | © 2010 Apple Inc. All Rights Reserved.