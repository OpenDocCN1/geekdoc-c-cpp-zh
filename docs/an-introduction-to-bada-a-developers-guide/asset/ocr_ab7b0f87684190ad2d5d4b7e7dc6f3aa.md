components rather than making huge changes to the whole of the underlying operating system. This makes the bada platform quite dynamic and offers lots of possibilities for developers to take advantage of the latest device hardware. All of the functionality provided by this layer is accessed by developers using the APIs defined in the Framework layer.

At the bottom is the Kernel layer. The bada platform is designed to run, for instance, on Linux or on RTOS kernels, which makes the bada platform very flexible. It also offers the possibility of support for a wider range of devices than any other mobile platform. That’s a huge potential market for your bada applications.

# 4.2 bada Coding Idioms

# 4.2.1 C++ and bada

Of all current mainstream programming languages, C++ is the most powerful and flexible. That doesn’t make it the most popular language. In fact, at the time of writing, C++ maintains a steady third place in popularity surveys, behind Java and C.¹

There are good reasons why C++ is unlikely to win a popularity contest. Compared with more recent languages (Python, say, or even Java), it has a complex syntax. There are several reasons for this. One is its retention of C as a proper language subset. Another is the deliberate decision to favour terse and compact (and even cryptic) over verbose and transparent. Yet another is the breadth of the language – both high-level and low-level and everything in between – supporting procedural, object-oriented programming (OOP), and generic (template-based) programming styles. And finally, while the previous point suggests maximalist goals (include everybody!), C++ takes a very minimalist view of what a programming language should aspire to be. Its built-in types are essentially those of C, and there (more or less) the language ends. There are no frameworks, or class libraries, included in the language proper. (Even the minimalist std.h and stdio.h are strictly optional.)

For all of these reasons, C++ is not the kind of language that holds your hand. This probably gives it a more fearsome reputation than it deserves. But it also means that any platform based on C++ must tame the language to suit its own purposes.

¹For example, according to the TIOBE Programming Community Index software survey, April 2010, see www.tiobe.com/index.php/content/paperinfo/tpci/index.html. Intriguingly, in 2010 Java and C have swapped places in the top two places, with C now the most popular language, as Java’s popularity share falls. Objective C meanwhile is roaring up the table. For comparison: C and Java score around 20%; C++ around 10%; and Objective C around 2%.