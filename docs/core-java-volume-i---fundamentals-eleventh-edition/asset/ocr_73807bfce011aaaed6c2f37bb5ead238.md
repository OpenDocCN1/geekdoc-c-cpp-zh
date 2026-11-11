# # CHAPTER 7

# # Exceptions, Assertions, and Logging

# ## In this chapter

+   - 7.1 Dealing with Errors, page 372
+   - 7.2 Catching Exceptions, page 381
+   - 7.3 Tips for Using Exceptions, page 396
+   - 7.4 Using Assertions, page 399
+   - 7.5 Logging, page 403
+   - 7.6 Debugging Tips, page 425

In a perfect world, users would never enter data in the wrong form, files they choose to open would always exist, and code would never have bugs. So far, we have mostly presented code as if we lived in this kind of perfect world. It is now time to turn to the mechanisms the Java programming language has for dealing with the real world of bad data and buggy code.

Encountering errors is unpleasant. If a user loses all the work he or she did during a program session because of a programming mistake or some external circumstance, that user may forever turn away from your program. At the very least, you must:

+   - Notify the user of an error;