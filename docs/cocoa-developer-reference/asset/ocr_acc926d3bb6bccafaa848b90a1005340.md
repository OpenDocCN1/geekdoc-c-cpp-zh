# Using Objects in Objective-C

This overview outlines a first look at objects in Objective-C, but Objective-C uses objects in unusual ways. A key point is that the relationship between objects, messages, and data is kept as loose as possible. Connections that are defined at compile-time in most languages can be changed at run time in Objective-C. For example, Objective-C allows loose typing, and includes class management features that can read an object's class at run time, or test if it's a member of a class hierarchy.

Table 5.3 introduces Objective-C's more creative elements. This list isn't a complete summary of Objective-C's more creative options, but it lists the features that are widely used in Cocoa applications.

| Feature | Summary |
|---|---|
| Object-oriented architecture | Objects can be defined, instantiated, and destroyed. Subclassing and method overrides are widely used. |
| Explicit and implicit object creation | Object instances can be created in code, or they can be defined as resources in an Interface Builder file and loaded automatically when the application runs. The loading process can be spread across multiple files. |
| Dynamic loading | Objects can be loaded when needed and released dynamically to minimize memory use. |
| Loose typing in message parameters using `id` | Type information in message parameters can be enforced, ignored, retrieved dynamically, or implied at run time using a placeholder `id` data type. |
| Loose links between objects and messages | Messages and objects are loosely bound - a named message can be sent to any target object that supports it. Target objects can be selected at run-time. Certain objects allow explicit nomination of a target object for certain messages. |
| Message selectors | A selector data type is available as a container/handle for each method. Code can use selectors to choose messages dynamically at run time. |
| Automatic message creation | Messages can be generated automatically without explicit code — for example, when an object property is updated. |
| Self-messaging | Objects can trigger internal methods by sending messages to `self`. |
| Abstract classes | Cocoa includes a small number of abstract classes, mostly used as bundles of methods that must be overridden manually. |
| Delegation | Related messages can be collected into protocols and adopted by any object, which acts as a delegate that implements handlers for the group. Delegate objects can be assigned and reassigned dynamically. |