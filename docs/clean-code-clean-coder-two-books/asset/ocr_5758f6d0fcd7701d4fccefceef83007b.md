+   13. A critical section is any section of code that must be protected from simultaneous use for the program to be correct.

+   14. See “[Increasing Throughput](page 333).”

+   15. See “[Deadlock](page 335).”

+   16. Did you know that the threading model in Java does not guarantee preemptive threading? Modern OS’s support preemptive threading, so you get that “for free.” Even so, it not guaranteed by the JVM.

+   17. This is not strictly the case. Since the JVM does not guarantee preemptive threading, a particular algorithm might always work on an OS that does not preempt threads. The reverse is also possible but for different reasons.

+   18. [http://www.alphaworks.ibm.com/tech/content](http://www.alphaworks.ibm.com/tech/content)

# Chapter 14

+   1. I recently rewrote this module in Ruby. It was 1/7th the size and had a subtly better structure.

+   2. To prevent further surprises of this kind, I added a new unit test that invoked all the FitNesse tests.

# Chapter 15

+   1. *JUnit Pocket Guide*, Kent Beck, O’Reilly, 2004, p. [43](43).

+   2. See “[The Boy Scout Rule](page 14).”

# Chapter 16

+   1. An even better solution would have been for Javadoc to present all comments as preformatted, so that comments appear the same in both code and document.

+   2. Several of the reviewers of this text have taken exception to this decision. They contend that in an open source framework it is better to assert manual control over the serial ID so that minor changes to the software don’t cause old serialized dates to be invalid. This is a fair point. However, at least the failure, inconvenient though it might be, has a clear-cut cause. On the other hand, if the author of the class forgets to update the