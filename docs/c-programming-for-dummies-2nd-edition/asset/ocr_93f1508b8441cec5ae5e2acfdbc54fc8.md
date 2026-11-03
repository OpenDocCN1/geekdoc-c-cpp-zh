Listing 8–7 uses the && operator as a logical AND comparison. Both conditions specified must be true for the *if* statement to consider everything in the parentheses to be true.

**Exercise 8–15:** Modify the source code from Listing 8–7 so that a logical OR operation is used to make the condition true when the value of variable *coordinate* is less than –5 or greater than 5.

**Exercise 8–16:** Create source code for a program that asks the popular question, “Do you want to continue (Y/N)?” Process single-character input, testing for Y or N, either upper- or lowercase. Ensure that the program responds properly when neither a Y nor N is input.

+   - Logical operations are often referred to by using all caps: AND, OR. That separates them from the normal words *and* and *or*.
+   - The logical AND is represented by two ampersands: &&. Say “and.”
+   - The logical OR is represented by two pipe, or vertical-bar, characters: ||. Say “or.”
+   - The logical NOT is represented by a single exclamation point: !. Say “not!”
+   - The logical NOT prefixes a value, or an expression in parentheses, to reverse the results, transforming False into True and True into False.

# # The Old Switch Case Trick

Piling up a tower of *if* and *if-else* statements can be effective, but it’s not the best way to walk through some multiple-choice decisions. An alternative offered in the C language is known as the *switch-case* structure.

# ## Making a multiple-choice selection

The *switch-case* structure allows you to code decisions in a C program based on a single value. It’s the multiple-choice selection statement, as shown in Listing 8–8.