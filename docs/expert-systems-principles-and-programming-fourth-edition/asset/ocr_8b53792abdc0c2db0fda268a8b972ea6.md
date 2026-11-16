In this case, CLIPS searches the current module first for the instance and then checks each module from which defclasses have been imported for the instance. Generally, you'll want to use only the module specifier if you know the instance is defined either in the current module or a single imported module. In this example, the instance [B::name] was found first, but if the order of the import statements had been switched, then [A::name] would have been found first. The conventions for referring to instances in other modules may seem complicated, but in practice you need only general familiarity with how it works. Typically your programs will refer to instances using instance addresses rather than instance names. With instance addresses, there is no ambiguity of which instance is being referred to as there is with instance names. Instance names are typically used when you send a message to an instance from the command prompt and usually the names are unique so you can use just the module separator if the current module imports the defclass associated with the instance.

# 11.17 LOADING AND SAVING INSTANCES

Similarly to facts, there are several commands available for saving and loading instances to and from files. These commands are save-instances, bsave-instances, load-instances, restore-instances, and bload-instances. The syntax of these commands is:

```
(save-instances <file-name>
[<save-scope> [(inherit] <class-names>+])]
(bsave-instances <file-name>
[<save-scope> [(inherit] <class-names>+])]
(load-instances <file-name>)
(restore-instances <file-name>)
(bload-instances <file-name>)
```

where <save-scope> is defined as:

+   visible | local

The load-instances command will load in a group of instances stored in the file specified by <file-name>. The instances in the file should be in the standard format used by the definstances construct for specifying instances. For example, if the file "instances.dat" contained:

```
((Jack of PERSON (full-name "Jack Q. Public")
(age 23))
(of PERSON (full-name "John Doe")
(hair-color black)))
```