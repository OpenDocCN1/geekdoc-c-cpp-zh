# Legal Applications of KBS

synthetic statements discussed earlier and sets limits on what can meaningfully be said in rules or constraints. A class hierarchy of this sort achieves the aim of sensibly decomposing the objects into the domain types with characteristic bundles of attributes, and provides a wellfounded language in which additional information about the domain can be expressed. Classes in such a system correspond to logical types rather than the 'typical members' of the conventional frame systems. Readers familiar with the KRYPTON system of Brman et al. [1983] notice some similarities with that system: in fact the Toolkit was designed independently of reference to that system, and the similarities arose out of a common motivation for the two formalisms.

Such class defines its instances by specifying the names and types of the slots which its contains. Some of this information may be contained directly within the class definition, and some may be found by inheritance from one or more subclasses. A class always embodies a more specific definition than any of its superclasses — slots may be added but not deleted, and inherited slots must have the same, or a more restrictive (but compatible), type that was given in the superclass. If a slot is inherited from more than one superclass, this type must result from the intersection of the types of the inherited versions of the slot (or a further restriction on this). The strictness of this inheritance mechanism means that it does represent genuine necessity, rather than the more nebulous notion associated with cancelable inheritance.

The available slots were:

+   1. Numeric, with type giving permitted range.

+   2. Literal, with type enumerating a set of mutually exclusive values (Boolean attributes were represented using literal slots with values True, False).

+   3. Instance-valued, with type giving the permitted class of instances (instances of subclasses of the named class were also, logically, instances of the named class, and so might be held in the slot).

The claim assertion and advice applications needed to be able to reason in the face of incomplete information about individuals. The policy application needed to reason about groups of people rather than individuals. Both these requirements were met by allowing attributes to hold ranges of possible values, and reasoning on the basis of these.

Values in linear and numeric slots represented the current set of values for the attribute represented by the slot. This interpretation of slot values enabled negation to be handled by taking the complement of the denied value with respect to the slot type. Values in instancevalued slots were divided into the names of instances known to be in the slot, and the names of instances known not to be in the slot (allowing an appropriate, though incomplete, treatment of negation).