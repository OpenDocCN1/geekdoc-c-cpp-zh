# Object-Orientation

by entering scala BankBranch. Other command-line arguments can be specified after the name of the object.

The application has to be an object because methods in a class can only be called on instances of that class, not the class itself. So in order to call a method you have to have executed on that type. However, main has to be called first, before any other logic has been executed. This is not a problem with an object as the single instance exists without a call to new.

# 2.4.4.2 Introduction to Companion Objects

While making applications with objects is vital, the most common use of objects is as COMPANION objects. A companion object is an object that has the same name as a class. Both the class and its companion object should be placed in the same file. The companion object has access to private members of the class it is with. Similarly, the class can see private elements in the object.

You might have wondered why it is that we are building objects in Scala, sometimes use new and sometimes that we are calling code that. When you use the name of the type without new to instantiate an object, you are calling the apply method on the companion object, and that method is calling the new. The first examples of this that we encountered the simple forms for creating Arrays and Lists. When you write List(1,2,3) in your code, it actually called List.apply(1,2,3), where List refers to the companion object.

Unfortunately, you cannot easily write classes with companion objects in the REPL or in scripts. For us to create our own companion objects, we have to be working in the mode of writing applications, compiling with scalac, and running the compiled files scala.

# 16.3 Revisiting the API

We have already learned enough to help a bit with understanding what some things mean in the API. When you open the API, the left side has a frame that looks like figure 16.1. Thus far have used the generic word "type" to describe the things that are listed in this frame. Now we can be more specific. There are three different declaration styles in Scala that appear over and the API indicates which one you are dealing with.

The circles next to the names contain one of three letters in them. The meaning of these letters is as follows.

+   - c For a class.

+   - o For an object.

+   - t For a trait, which we do not cover in this book, but very similar to classes.

When you click on one of these, you are shown the methods and members that are defined in them, whether it be a class, an object, or a trait. The API itself is built by running a program called scalac on scale to generate HTML descriptions of what is in the code.

When there is an "o" next to a "c" or a "t" it is a companion object. If you want to know if you can build objects without a direct use of new, look there and see if there is an apply