The best thing about standards is that there are so many to choose from.
Andrew S. Tannenbaum

In addition to Basic Regular Expressions (BREs), there are Extended Regular Expressions (EREs) defined in the POSIX regular expression documentation [96]. Some software, such as egrep, uses this version of regular expressions. Unfortunately EREs are not a conservative extension of BREs: ERE syntax is actually inconsistent with BRE syntax! It is an interesting project to extend our pattern language so that the target can be either BREs or EREs.

+   a. What are the significant differences between BREs and EREs that make this a pain? List the differences that must be addressed.

+   b. How can your translator be factored so that your language can translate into either kind of regular expression, depending on what is needed? How can we maintain the abstract layer that is independent of the target regular expression language? Explain your strategy.

+   c. Implement the strategy you devised in part b. Demonstrate your work by making sure that you can run egrep as well as grep, with equivalent results in cases that test the differences found in part a.

# 2.3 Wrappers

Sometimes we can repurpose an existing program by wrapping rather than rewriting it. Consider the problem of computing how the radius of a sphere of gas varies with the temperature, keeping the pressure constant. The ideal gas law is

> $$$PV = nRT,$$