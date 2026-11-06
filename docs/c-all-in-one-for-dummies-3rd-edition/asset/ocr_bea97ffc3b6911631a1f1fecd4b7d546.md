# # Chapter 5: Boosting up a Step

# ## In This Chapter

+   - Using RegEx to parse strings
+   - Using Tokenizer to break strings into tokens
+   - Converting numbers to other data types
+   - Using Foreach to create improved loops
+   - Using Filesystem to access the operating system

The Boost library is vast. It's doubtful that a typical developer will ever use everything that Boost has to offer. Of course, before you can pick and choose what you want to use, you need to know it exists. Browsing through the help file can reveal classes that you need to add to your toolkit to produce good applications. This chapter helps by taking you on a whirlwind tour of the major Boost categories. Don't expect this chapter to discuss everything — Boost is simply too large for that. If you want to see a list of what Boost has to offer, check out

+   - **All classes in alphabetical order:** http://www.boost.org/doc/libs/1_55_0
+   - **Categorized list:** http://www.boost.org/doc/libs/1_55_0?view=categorized

![](bbox=[0.181, 0.637, 0.251, 0.722])

In addition to reviewing the examples in this chapter and looking through the help file, it also pays to browse the Boost directory for examples. For example, if you look at the \CodeBlocks\boost_1_55_0\libs\regex\example directory, you find three examples of how to use RegEx, one of which is demonstrated in the “Testing the installation” section of Book VI, Chapter 4. Every example directory contains a Jamfile.v2 you can use to build the examples using Boost.Build. If you still haven’t found the example you need, check online for more examples — Boost is extremely popular. Even Microsoft has gotten into the act by providing examples at http://msdn.microsoft.com/library/aa288739.aspx.

Before you begin working through the examples in this chapter, make sure you know how to configure your development environment to use Boost. The “Testing the Installation” and “Building Your First Boost Application Using Date Time” sections of Book VI, Chapter 4 tell how to configure Code::Blocks to use Boost. The “Building Your First Boost Application Using Date Time” section also provides you with a simple example that gets you started working with Boost.