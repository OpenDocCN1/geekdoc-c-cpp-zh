```
(slot eye-color)
(slot hair-color))
```

# Multifield Slots

Slots of a fact that have been specified with the slot keyword in their corresponding deftemplates are allowed to contain only one value (these are referred to as single-field slots). It is often desirable to place zero or more fields into a given slot. Slots of a fact that have been specified with the multifield keyword in their corresponding deftemplates are allowed to contain zero or more values (these are referred to as multifield slots). For example, the name slot of the person deftemplate stores the person's name as a single string value. If the name slot were defined using the multifield keyword in place of the slot keyword, then any number of fields could be stored in it. Thus, the fact:

```
(person (name John Q. Public)
 (age 23)
 (eye-color blue)
 (hair-color brown))
```

is illegal if name is a single-field slot, but legal if name is a multifield slot. A deftemplate can have any combination of single and multifield slots.

# Ordered Facts

Facts with a relation name that has a corresponding deftemplate are called deftemplate facts. Facts with a relation name that does not have a corresponding deftemplate are called ordered facts. Ordered facts have a single implied multifield slot that is used to store all values following the relation name. In fact, whenever CLIPS encounters an ordered fact it automatically creates an implied deftemplate for that fact (as opposed to an explicit deftemplate, created using the deftemplate construct). Since an ordered fact has only one slot, the slot name isn't required when defining a fact. For example, a list of numbers could be represented with the following fact:

```
(number-list 7 9 3 4 20)
```

Essentially this is equivalent to defining the following deftemplate:

```
(deftemplate number-list (multislot values))
```

and then defining the fact as follows:

```
(number-list (values 7 9 3 4 20))
```

Generally, deftemplate facts should be used whenever possible because the slot names make the facts more readable and easier to work with. There are two cases in which ordered facts are useful. First, facts consisting of just a relation name are useful as flags and look identical regardless of whether a deftemplate has been defined. For example, the ordered fact: