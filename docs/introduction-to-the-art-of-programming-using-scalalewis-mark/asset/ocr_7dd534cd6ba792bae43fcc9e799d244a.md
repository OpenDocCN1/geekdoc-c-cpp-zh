# # Chapter 16

# ## Object-Orientation

+   16.1  Basics of Object-Orientation ........................................ 394
+     16.1.1  Methods and Members ............................................... 394
+       16.1.1.1  Parameters as Members ......................................... 395
+       16.1.1.2  Visibility .................................................... 396
+     16.1.2  this Keyword ...................................................... 399
+     16.1.3  Encapsulation/Separating Interface from Implementation ........... 399
+     16.1.4  Special Methods ................................................... 400
+       16.1.4.1  Operator Methods ............................................. 400
+       16.1.4.2  Unary Operators .............................................. 402
+       16.1.4.3  Property Assignment Methods .................................. 403
+       16.1.4.4  The apply Method .............................................. 404
+       16.1.4.5  The update Method ............................................. 405
+       16.1.4.6  Overloading Methods ........................................... 405
+       16.1.4.7  Vector Example ................................................ 406
+     16.1.5  Object Declarations .............................................. 408
+       16.1.5.1  Applications .................................................. 408
+       16.1.5.2  Introduction to Companion Objects ............................. 409
+     16.1.6  Object Decomposition ............................................. 409
+   16.2  Revisiting the API ................................................... 409
+   16.3  Meaning of the class .................................................. 410
+   16.4  import Options ........................................................ 410
+   16.5  End of Chapter Material ............................................... 412
+     16.5.1  Summary of Concepts ............................................... 412
+     16.5.2  Exercises ........................................................ 414
+     16.5.3  Projects ......................................................... 415

From the beginning we have said that Scala is a completely object-oriented language. You have been using objects and calling methods on them since back in chapter 3 when we were taking our first steps in the language. Despite this, we have actually done very little with object-orientation. This has been intentional. So far we have been building up your logic skills and teaching you to break problems up into different functional units. Now that your problem-solving skills have reached a sufficient level, we will take the next step to have you doing full object-oriented decomposition of problems. Beginning with this chapter we will also start really revealing many of the details behind things that we have been using all along.