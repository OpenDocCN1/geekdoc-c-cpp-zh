+   14. What is an inheritance diagram?
15. What is the difference between a protected member and a private one?
16. What members of a class can be accessed from a class derived from it?
17. How does a pure virtual function differ from other virtual functions?
18. Why would you make a member function virtual?
19. Why would you make a virtual member function pure?
20. What does overriding mean?
21. How does interface inheritance differ from implementation inheritance?
22. What is object-oriented programming?

# Terms

abstract class 
access control 
base class 
derived class 
dispatch 
encapsulation 
inheritance 
mutability 
object layout 
object-oriented 
override 
polymorphism 
private 
protected

public 
pure virtual function 
subclass 
superclass 
virtual function 
virtual function call 
virtual function table

# Exercises

+   1. Define two classes Smiley and Frowny, which are both derived from class Circle and have two eyes and a mouth. Next, derive classes from Smiley and Frowny which add an appropriate hat to each.
2. Try to copy a Shape. What happens?
3. Define an abstract class and try to define an object of that type. What happens?
4. Define a class Immutable_Circle, which is just like Circle but can’t be moved.
5. Define a Striped_rectangle where instead of fill, the rectangle is “filled” by drawing one-pixel-wide horizontal lines across the inside of the rectangle (say, draw every second line like that). You may have to play with the width of lines and the line spacing to get a pattern you like.
6. Define a Striped_circle using the technique from Striped_rectangle.
7. Define a Striped_closed_polyline using the technique from Striped_rectangle (this requires some algorithmic inventiveness).
8. Define a class Octagon to be a regular octagon. Write a test that exercises all of its functions (as defined by you or inherited from Shape).
9. Define a Group to be a container of Shapes with suitable operations applied to the various members of the Group. Hint: Vector_ref. Use a