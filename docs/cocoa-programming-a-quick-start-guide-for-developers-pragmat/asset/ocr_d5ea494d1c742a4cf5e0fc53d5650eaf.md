# Chapter 14

# Multiple Nibs

So far in our desktop app, everything is in a single nib. In this chapter, we’re going to break the nib up into first two and then three pieces. Although we didn’t worry much about it, we had two nibs files when we created our iPhone web browser. One contained our window and the view controller, and the other contained the view that the view controller controlled.

The purpose of this chapter is to show you how to work with multiple nib files. Just as you split methods or classes when they get to the point where they do too much, you’ll learn to break nibs into smaller, easy-to-describe collections of objects. Just like objects and methods, when you split them into smaller pieces, you will often need to communicate among the pieces. That’s the job of the File’s Owner. By the end of this chapter, you’ll understand how File’s Owner works as well.

# 14.1 Methods, Objects, and Nibs

A nib is one of the organization levels for your project. A nib is a collection of objects and their connections to each other.

Zooming in, each object is a cohesive collection of functionality. An object might include variables, properties, functions, and methods. Of course, this means that objects are state plus behavior, but I like to think of objects in terms of what they can do. This means that to me an object is characterized by its methods.

Methods are the smallest organizational level that I want to think of right now. We create a method when we want to accomplish a task