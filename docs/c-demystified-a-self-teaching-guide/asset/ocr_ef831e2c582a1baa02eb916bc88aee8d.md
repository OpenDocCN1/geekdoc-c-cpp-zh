# Object-Oriented Programming

Object-Oriented Programming, often known by its acronym, OOP, is a term used more than it is understood. However, understanding OOP principles is important, since OOP really is the next step. Indeed, the previous chapters have given you the foundation to learn OOP.

I am not going to attempt cover the entire subject of OOP in this chapter: entire books are written about OOP. Indeed, one of the companion books in the Demystified series to which this belongs is Object-Oriented Programming Demystified. Nevertheless, let me try to describe OOP.

While game programs are fun, the usual purpose of a program is to provide a solution to real-world tasks, which involve people, places, things, or concepts. Programs use objects to represent a real-world place, person, thing, or concept.

Objects generally are abstractions, simplifying the real-world place, person, thing, or concept they represent. Just as you don't need to know how an internal engine drives a car, you don't need to understand the inner workings of the object to know how to use it.

For example, as recently the last chapter, we used objects, specifically the file stream objects, istream, istream, and istream. We did not need to understand the inner workings of these objects, as detailed in the istream standard library, to use them to open, read, write, and close files.

Objects are not limited to something abstract as a file stream object, however. You are a person object. This book is a object. The car you drive is a character. A game is also an object. The number and variety of possible objects is limited only by the programmer's imagination and creativity.

Real-world objects also have relationships with other real-world objects. These relationships are either an "is a" relationship or a "has a" relationship.

An example of "is a" is that a teacher is a person. Some of my students have questioned this to certain teachers, and then we call it a farce to remind them that a student is "is a" person, even though there are a few I have my doubts about.

An "is a" is important because you have already created a person class, when you write the teacher class not to write code for those attributes that a teacher has common with all persons, such as a name, birthday, height, and weight and so. Furthermore, the teacher class can "inherit" those attributes from the person class, so you only need to write code for those that have a teacher in addition to, for all persons generally, such as tenure status, a higher education, and so on.

This ability of one to inherit is also called, naturally enough, inheritance. Inheritance enables you to reuse code, such as the person class, when classes that represent more specialized objects, like teachers.

An example of a "has a" relationship is that a car has an engine. This type of relationship is also referred to as composition or, the term I will use, containment. Containership also enables you to reuse existing code, such as the engine class, when classes that represent the containing object, like class.