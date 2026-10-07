# CHAPTER 3
Adding Behavior to Cocoa Program

> **Important:** If you are implementing a getter accessor method to load the value of an instance variable lazily—that is, when it is requested—do not call the corresponding setter method in your implementation. Instead, set the value of the instance variable directly in the getter.

The setters of a class are implemented as shown in either Listing 3-5 (page 126) or Listing 3-7 (page 126), to deallocate an instance variable in the class's `dealloc` method, all you need to do is invoke the appropriate setter method, passing in `nil`.

# Key-Value Mechanisms

Several mechanisms with "key-value" in their names are fundamental parts of Cocoa: key-value binding, key-value coding, and key-value observing. They are essential ingredients of Cocoa technologies such as bindings, which automatically communicate and synchronize values between objects. They also provide at least part of the interface for making scriptable—that is, responsive to AppleScript commands. Key-value coding and key-value observing are especially important considerations in the design of a custom subclass.

> **Note:** The classes used in bindings (NSViewController and subclasses) and in application scriptability are defined only by AppKit and UIKit.

The term key-value refers to the technique of using the name of a property as the key to obtain its value. The term is part of the vocabulary of the object modeling pattern, which is derived from "Storing and Accessing Properties" (page 123): Object model used for describing relational data. In object modeling, objects—particularly the data-bearing model objects of the Model-View-Controller pattern—have properties, which usually (but not always) take the form of instance variables. A property can be an attribute, such as name or color, or it can be a reference to one or more other objects. These references are known as relationships, and relationships can be one-to-one or one-to-many. The network of objects in a program form an object graph through its relationships with each other. In object modeling you can use paths—strings of de-separated keys—to traverse the relationships in an object graph and access the properties of objects.

> **Note:** For a full description of object modeling, see "Object Modeling" (page 167).

Key-value binding, key-value coding, and key-value observing are essential mechanisms for this traversal.

+   - Key-value binding (KVB) handles bindings between objects and also removes and advertises those bindings. It makes use of informal protocols. For a binding property must specify the object and a key to the path.
- Key-value coding (KVC), through an implementation of the `KeyValueCoding` informal protocol, makes it possible to get and set the values of an object's properties without having to invoke that object's accessor methods directly (Cocoa provides a default implementation of the protocol). A key typically corresponds to the name of an instance variable or accessor in the object being accessed.
- Key-value observing (KVO), through an implementation of the `NSKeyValueObserving` informal protocol, allows objects to register themselves as observers of other objects. The observed object notifies its observers when there are changes to any of its properties. Cocoa implements automatic notifications for any property of a KVO-compliant object.

128 Basic Subclassing Design
2010-12-13 | © 2010 Apple Inc. All Rights Reserved.