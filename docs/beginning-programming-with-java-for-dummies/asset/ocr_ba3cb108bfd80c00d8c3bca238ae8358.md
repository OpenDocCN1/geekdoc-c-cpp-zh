# Chapter 17

# Programming with Objects and Classes

# In This Chapter

+   - Programming with class (and with style and finesse)
+   - Making objects from classes
+   - Joining the exclusive "I understand classes and objects" society

Chapters 6, 7, and 8 introduce Java's primitive types — things like int, double, char, and boolean. That's great, but how often does a real-world problem deal exclusively with such simple values? Consider an exchange between a merchant and a customer. The customer makes a purchase, which can involve item names, model numbers, credit card info, sales tax rates, and lots of other stuff.

In older computer programming languages, you treat an entire purchase like a big pile of unbundled laundry. Imagine a mound of socks, shirts, and other pieces of clothing. You have no basket, so you grab as much as you can handle. As you walk to the washer, you drop a few things — a sock here and a washcloth there. This is like the older way of storing the values in a purchase. In older languages, there's no purchase. There are only double values, char values, and other loose items. You put the purchase amount in one variable, the customer's name in another, and the sales tax data somewhere else. But that's awful. You tend to drop things on your way to the compiler. With small errors in a program, you can easily drop an amount here and a customer's name there.

So with laundry and computer programming, you're better off if you have a basket. The newer programming languages, like Java, allow you to combine values and make new, more useful kinds of values. For example, in Java, you can combine double values, boolean values, and other kinds of values to create something that you call a Purchase. Because your purchase info is all in one big bundle, keeping track of the purchase's pieces is easier. That's the start of an important computer programming concept — the notion of object-oriented programming.