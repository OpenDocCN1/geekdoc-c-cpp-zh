
## Chapter 4: Introducing Conceptual Database Design (Logical Model) 79

decisions in conceptual database design. A natural key is usually more efficient; sometimes you can eliminate a join, sometimes the query optimizer works efficiently, and so on. But there is no point trying to find a primary key if there is no serious candidate, though in many of these cases indicates that there is something wrong with the model. Many times designers are too cautious to set attributes to not null and are able to define only unique keys. Or the concepts are not understood well enough to really identify the entity. One of the main concerns in designing the database is the data quality. To be able to get good-quality data, you must understand what you are modeling, and you must be able to set any attributes to not null as possible and to find all possible constraints. A surrogate key does not stop users from inserting duplicates in the database, but a natural key does, and the index for a surrogate primary key is often not used (queries are not made based on the surrogate). On the other hand, many times the best solution for data that comes from another system and is not controlled by your organization is a surrogate key because you can never be sure if the other system has changed the data you have considered to be unique not anyone. So, there is no single answer to the question. If you want to have a surrogate key, select the Surrogate Keys box in the Entity Properties or Relationship Properties box.

A foreign key constraint is an attribute or set of attributes that refers to the primary key of an entity, which can be another entity or the same one, as discussed earlier.

You can define constraints for attributes. Domain constraints can define, for instance, data type, length, allowable values, and default values. You can either redefine them in Domains to be used (see Chapter 2) or define them for every attribute separately in Domains in the Attribute Properties dialog (Figure 4-15). Define the name for the constraint and define the default value for it. If you want to use the properties defined in Domains Administration for the associated domain, select Use Domain Constraints. If this option is not selected, you can continue defining the settings. You can specify a constraint for one or more types of databases from the Constraint list. You can specify one or more value ranges for the attribute. You can specify a list of valid values for the attribute. If you select Domain Constraints, all the changes will automatically be done on this attribute. For instance, if a new allowable value is added to a domain constraint, it will automatically be available for this attribute as a candidate for a default value and on the list of allowable values. I recommend using the domains and their settings. That will make maintenance easier.

One more commonly used constraint is a check constraint. An example of a check constraint could be Check (Name=upper(Name)). A constraint can be immediate or deferred, meaning that it will be checked either straight away or later.

## 80 Oracle SQL Developer for Database Design

![img/431f8ac8f273fa89a28377c500ed6d7_106.png]
**15.** Domain constraint

### Entity Views

An entity view is an element in the conceptual model that allows the designer to see a subset of the entity's attributes. This is useful for simplifying the model for specific users.

You can create an entity view by selecting the entity and the attributes you want to include. The inheritance looks like the model in Figure 4-18 if box-in-box notation has been selected. If the box-in-box notation has not been selected, the same inheritance will look like the one in Figure 4.19. In that case, the inheritance relationship properties can be

## 81 Chapter 4: Introducing Conceptual Database Design (Logical Model)

![img/431f8ac8f273fa89a28377c500ed6d7_107.png]
**16.** Entity views

### Inheritance

Sometimes you need to model a case where an entity has multiple subtypes. For example, a person can be both an employee and a customer. In this case, you can use inheritance to represent the different roles a person can play.

Inheritance is a relationship between a supertype and its subtypes. The subtype inherits all the attributes and relationships of the supertype, but can also have its own unique attributes. This is a powerful way to model complex real-world scenarios.

## 82 Oracle SQL Developer for Database Design

![img/431f8ac8f273fa89a28377c500ed6d7_108.png]
**17.** Arc solution

In forward engineering, an arc solution will produce one table for each entity. To be able to forward engineer this setting to the relational model, you must set all foreign keys belonging to the supertype to allow nulls because only one of them can have a value for each row. There will be an additional constraint for implementing the arc. You will learn more about forward engineering in Chapter 5. The arc solution can be a good choice when the subtypes do not have a lot in common and can be used independently.

In many cases, it is easier to model and understand the target when using subtypes and supertypes to express the same need. The modeling tactic with supertypes and subtypes is usually easier for end users to read, and it gives the designer the freedom to decide later how to implement this the relational model. All attributes and relationships of the supertype must belong to all of its subtypes.
