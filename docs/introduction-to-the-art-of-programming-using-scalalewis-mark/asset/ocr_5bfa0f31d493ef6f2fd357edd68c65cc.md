you to understand different parts of the API and you will be expected to go into the API to get information on what you can do with the libraries.

We have already learned enough to help a bit with understanding what some things mean in the API. When you open up the API, the left side has a frame that looks like figure 16.1. We have used the generic word “type” to describe the things that are listed in this frame. Now we can be more specific. There are really three different declaration styles in Scala that appear over there and the API indicates which one you are dealing with.

The circles next to the names contain one of three letters in them. The meaning of these letters is as follows.

+   - c - For a class.
+   - o - For an object.
+   - t - For a trait, which we will learn about in chapter 19. For now you can think of a trait as being like a class.

When you click on one of these, you are shown the methods and members that are defined in them, whether it be a class, an object, or a trait. The API itself is built by running a program called scaladoc on Scala code to generate Hyper-Text Marup Language (HTML) descriptions of what is in the code.

When there is an “o” next to a “c” or a “t” it is a companion object. If you want to know if you can build objects without a direct use of new, look there and see if there is an apply method defined. If there is, it generally implies that is the preferred way to make instances of that type.

# 16.3 Meaning of case classes

The first usage of the term class that we encountered was back in chapter 10 when we looked at case classes. Now that you know a bit about regular classes, you might wonder what case keyword does for a case class. It does not do anything that you could not do without the use of case, it simply adds a lot of code for you.

First, all the data passed into the case class are turned into public vals instead of just being arguments. Second, it automatically creates a companion object that has an apply method that you can use to make instances of the case class without using new. It also adds a copy method to the class that has default arguments for all the values. There are a few other things added in that allow the pattern matching that we have not talked about yet.

# 16.4 import Options

The usage of import that we have seen so far with all the import statements at the top of the file giving full package names is the most basic usage in Scala. It mirrors the way import has to be used in Java. There are a lot of additional options in Scala that we have not really considered. Here is a list of some details of import starting with the general usage. Each one includes situations where you might want to use it.