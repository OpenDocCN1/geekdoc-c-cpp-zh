
```
CLIPS> (make-instance [b] of B)
[b]
CLIPS> (send [a print])
[a] of A
(x 3)
(y nil)
(z 4)
CLIPS> (send [b print])
[b] of B
[x nil]
(y 5)
(z 6)
CLIPS>
```

Note that slot x of instance b is given a default value of nil instead of 3. This is because the absence of a default value for slot x of class B completely overrides the default of 3 given to slot x in class A. The source slot attribute can be used to allow slot attributes to be inherited from superclasses. If this attribute is set to :exclusive, which is the default, then attributes for a slot are determined by the most specific class defining the slot. In a single-inheritance hierarchy, this will be the class having the fewest superclasses. If the source attribute is set to :composite, then attributes that are not explicitly defined in the most specific class defining the slot are taken from the next most specific class that defines the attribute. For example, if the prior A and B defclasses are redefined as follows:

```
(defclass A
  (is-a USER)
  (slot x '(default 3))
  (slot y)
  (slot z (default 4))))
```

```
(defclass B
  (is-a A)
  (slot x (source composite))
  (slot y (default 5))
  (slot z (default 6))))
```

then creating an instance of classes A and B produces the following results:

```
CLIPS> (make-instance [a] of A)
[a]
CLIPS> (make-instance [b] of B)
[b]
CLIPS> (send [a print])
[a] of A
(x 3)
(y nil)
(z 4)
CLIPS> (send [b print])
[b] of B
(x 3)
(y 5)
(z 6)
CLIPS>
```

Now that slot x of class B is defined with the source attribute set to composite, it can inherit the default attribute of class A and the default resulting value for the x slot of the instance b is set to 3.

It's also possible to disable the inheritance of a slot using the propagation slot attribute. If this attribute is set to inherit, which is the default, then the slot will be inherited by subclasses. If this attribute is set to no-inherit, then the slot will not be inherited by subclasses. For example, defining classes A and B as follows:

```
(defclass A
(is-a USER)
(slot x (propagation no-inherit))
(slot y))
```

```
(defclass B
(is-a A)
(slot z))
```

then creating an instance of classes A and B produces the following result:

```
CLIPS> (make-instance [a] of A)
[a]
CLIPS> (make-instance [b] of B)
[b]
CLIPS> (send [a print])
[a] of A
(x nil)
(y nil)
CLIPS> (send [b print])
[b] of B
(y nil)
(z nil)
CLIPS>
```

Instance b of class B inherits slot y from class A, but it does not inherit slot x from class A because its propagation attribute is no-inherit.

## Abstract and Concrete Classes

It's possible to define classes that can be used only for inheritance. Such classes are called abstract classes. It's not possible to create instances of abstract classes. By default, classes are concrete. The role class attribute is used to specify whether a class is abstract or concrete. The role class attribute must be specified after the is-a class attribute but before any slot definitions. For example:

```
(defclass ANIMAL
  (is-a USER)
  (role abstract))

(defclass MAMMAL
  (is-a ANIMAL)
  (role abstract))

(defclass CAT
  (is-a MAMMAL)
  (role concrete))

(defclass DOG
  (is-a MAMMAL)
  (role concrete))
```

Classes ANIMAL and MAMMAL are abstract. Classes CAT and DOG are concrete. The role attribute is inherited, so while it was not necessary to declare MAMMAL as abstract because it inherits this attribute from ANIMAL, it was necessary to declare the CAT and DOG classes as concrete since they would otherwise be abstract. Attempting to create an instance of an abstract class will generate an error message:

```
CLIPS> (make-instance [animal-1] of ANIMAL)
[INSNGR3] Cannot create instances of abstract
class ANIMAL.
CLIPS> (make-instance [cat-1] of CAT)
[cat-1]
CLIPS>
```

It's never necessary to declare a class abstract, but doing so when appropriate makes the code more maintainable and easier to reuse. You simply don't want someone using a class to create instances if the class was not intended for that purpose. If someone were to use that class, you would be prevented in future implementations from removing it without breaking existing code.

In our current example, the argument can be made either way as to whether the ANIMAL and MAMMAL classes should be abstract. If we're going to create an inventory of animals in a zoo, then these classes should probably be abstract. There are no existing animals or mammals that are just that and not a member of a more specific class. However, if we're trying to identify an animal it's conceivable that we might want to create instances of the ANIMAL or MAMMAL class, for example, to indicate what we've been able to determine about the animal.

## Defclass Commands

Several commands are provided for manipulating defclasses. The list-defclasses command is used to display the current list of defclasses maintained by CLIPS. Its syntax is:

```
(list-defclasses [<module-name>])
```

It's worthwhile taking a look at the output from this function:

```
CLIPS> (list-defclasses)
FLOAT
INTEGER
SYMBOL
STRING
MULTIFIELD
EXTERNAL-ADDRESS
FACT-ADDRESS
INSTANCE-ADDRESS
INSTANCE-NAME
OBJECT
PRIMITIVE
NUMBER
LEXEME
ADDRESS
INSTANCE
USER
INITIAL-OBJECT
PERSON
EMPLOYEE
STUDENT
For a total of 20 defclasses.
CLIPS>
```

There are a number of predefined primitive classes: OBJECT, PRIMITIVE, NUMBER, LEXEME, FLOAT, INTEGER, SYMBOL, STRING, MULTIFIELD, ADDRESS, INSTANCE, EXTERNAL-ADDRESS, FACT-ADDRESS, INSTANCE-ADDRESS, and INSTANCE-NAME. You can't use these classes to create other classes. The primitive classes are primarily useful with generic functions, which were discussed in Chapter 10. The remaining predefined classes are USER and INITIAL-OBJECT. USER is the base for creating new classes. INITIAL-OBJECT is a subclass of USER and is used to create the initial-object instance (see Section 11.7). The classes we created (PERSON, EMPLOYEE, and STUDENT) complete the list. Figure 11.1 shows the predefined class hierarchy.

## Figure 11.1 Predefined Classes Overview

![](img/2c460d4de56b7ffaad3834eee20beaa0_654_0.png)

The browse-classes command is used to display the inheritance relationships between a class and its subclasses. Its syntax is:

```
(browse-classes [<class-name>])
```

If no class name is specified, the inheritance relationships for the root class OBJECT are displayed. For example, the following command displays the information contained in Figure 11.1 along with PERSON classes and subclasses used as examples:

```
CLIPS> (browse-classes)
OBJECT
OBJECT
PRIMITIVE
  NUMBER
    INTEGER
    FLOAT
LEXEME
SYMBOL
STRING
MULTIFIELD
ADDRESS
  EXTERNAL-ADDRESS
  FACT-ADDRESS
INSTANCE-ADDRESS *
INSTANCE
INSTANCE-ADDRESS *
INSTANCE-NAME
USER
INITIAL-OBJECT
PERSON
EMPLOYEE
STUDENT
CLIPS>
```

Indentation is used to indicate that one class is a subclass of the first preceding class with less indentation. For example, NUMBER, LEXEME, MULTIFIELD, ADDRESS, and INSTANCE are all subclasses of PRIMITIVE. An asterisk before a class indicates that it is a direct subclass of more than one class. For example, INSTANCE-ADDRESS is a direct subclass of both ADDRESS and INSTANCE.

Specifying a class in the browse-classes command will display inheritance information only for the specified class and its subclasses:

```
CLIPS> (browse-classes PERSON)
PERSON
EMPLOYEE
STUDENT
CLIPS>
```

The ppdefclass (pretty print defclass) command is used to display the text representation of a defclass. The undefclass command is used to delete a defclass. The syntax of these commands is:

```
(ppdefclass <defclass-name>)
(undefclass <defclass-name>)
```

You can't delete a defclass while instances of that class exist. Any instance belonging to that class or any subclass of that class must be deleted before the class can be removed. For example:

```
CLIPS> (undefclass STUDENT)
[PRNTUTIL4] Unable to delete defclass STUDENT.
CLIPS> (send [Jill] delete)
TRUE
CLIPS> (undefclass STUDENT)
CLIPS>
```

## 11.7 OBJECT PATTERN MATCHING

Object patterns provide several capabilities that are not available with deftemplate or ordered fact patterns. First, a single object pattern can match instances
