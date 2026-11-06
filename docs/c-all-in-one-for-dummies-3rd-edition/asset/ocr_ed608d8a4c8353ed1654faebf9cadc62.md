![](bbox=[0.05, 0.14, 0.16, 0.21])

# Discovering more about make

If you want to be a serious, diehard, late-into-the-night, big-time "maker," you can read its online manual. You can do tons and tons of things with make, and you could easily stay up all night playing with it all — or, at least, trying to learn it all. You may not ever have a need for all the things you learn, but you never know. Here's the site: http://www.gnu.org/manual/.

Scroll down to find the entry on make. (make will be followed by a hyphen and some numbers representing the version number.) When you click it, you will see an enormous page filled with the wonders of make. Trust us: it's long and boring.

# Getting the most out of Makefiles

Here are some other features you can use when working with Makefiles:

+   - If your lines run long and you want to continue them on the next line without confusing poor old make, you can end a line with a backslash (\) and then continue it on the next line.
+   - Your best bet when working with Makefiles is to start with one that you know works and then change it so that it applies to your current project. The truth is, almost no programmer creates a Makefile from scratch. Programmers don't like to work that hard on auxiliary projects like messing with Makefiles. They'd rather get to their programming. So if you need a starting point, you can find a sample in this appendix.
+   - Most Makefiles will have a rule called all. The idea behind this rule is that it encompasses all the other rules. When you type **make all**, you can build your whole project.
+   - You can include comments in your Makefiles by starting them with a # character. These comments are not used by the Makefile.
+   - Makefiles can include what are called *implicit rules*, which are rules that pertain to a whole set of files with the same file extension (such as .cpp). These comments can help you understand the Makefiles when working with them.
+   - If you don't like Makefiles, you don't have to use them. Development environments such as Code::Blocks and Microsoft Visual C++ make it possible to create great applications without ever touching a Makefile.