# Object-Oriented Design

> *If I have seen farther than others, it is because I was standing on the shoulders of giants.*
> 
> -Isaac Newton

This chapter begins with several sections that define and detail the many attributes of the collective data type known as the structure. This aggregated data type includes several options that aid in the removal of literal limitations, and thus help us to further our move into object-oriented programming. Once the basics of these simpler concepts are committed to memory, we’ll want to progress onto the extended topics using classes. Classes, while not meant to totally replace structures, do allow for a greater level of control, which includes the use of reference types. The second portion of this chapter will also offer several new keywords and operators whose potential can only be reached through class manipulations. Finally, we’ll conclude with the underlying classes used to power all the games, and I’ve thrown in two additional games that add a few final touches.

# Structures

*Structures* are user-defined data types that allow for groupings of similar or related data that do not have a single base data type. These groups can include all the basic value data types, as well as a list of methods used to manipulate those values. The data types declared inside a structure are referred to as the structure’s *members* (or *fields*), while their declarations are referred to as its *instances*. The correlations between these internal values and