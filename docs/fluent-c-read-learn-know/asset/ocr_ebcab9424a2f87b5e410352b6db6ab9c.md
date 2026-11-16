# # KINDS OF RELATIONSHIPS

There are four basic categories of relationships that can exist between types in a hierarchy (assuming a relationship exists between the types at all—not every type is directly related to every other). They are:

# ## ISA RELATIONSHIPS

An IsA relationship exists when one thing is a specific example of a more general kind of thing. A Mercedes-Benz IsA Car. So is a Yugo. Lions and Tigers both have IsA relationships with Cat. IsA relationships are usually best modelled by collecting the common characteristics in a base type (usually, but not always, a class) and using inheritance for the more specialized types.

# ## HASA RELATIONSHIPS

A HasA relationship exists when a type contains one or more instances of another. A Car HasA steering wheel. A Cat HasA tail. HasA relationships are usually modelled by exposing the instances of one type as properties of the type that owns it. (Technically, this is called Object Composition.)

# ## CANDO RELATIONSHIPS

CanDo relationships are behaviors that multiple types have in common. It is often the case that the types aren’t related in any other way. CanDo relationships are usually modelled as interfaces. For example, all of the set types we looked at in the last chapter CanDo the things defined by the IEnumerable interface.

# ## CANBE RELATIONSHIPS

CanBe relationships represent mutually exclusive options. For example, a Car CanBe manual or automatic, but not both. CanBe relationships are implicit in type inheritance (a Cat CanBe A Lion or Tiger, but not both). For properties, they are usually best modelled as an enumeration.

> Oops. One of my editors has just pointed out to me that there are cars that are both manual and automatic. Who knew?