# MULTIPROCESSOR SCHEDULING (ADVANCED)

119

So what should a poor multi-queue multiprocessor scheduler do? How can we overcome the insidious problem of load imbalance and defeat the evil forces of the Decepticons? How do we stop asking questions that are hardly relevant to this otherwise wonderful book?

# CRUX: HOW TO DEAL WITH LOAD IMBALANCE

How should a multi-queue multiprocessor scheduler handle load imbalance, so as to better achieve its desired scheduling goals?

The obvious answer to this question is to move around, a technique which we (once again) refer to migration. By migrating a job from CPU to another, true load balance can be achieved.

Let's look at a couple of examples to add some clarity. Once again, we have a situation where one CPU is idle and the other has some jobs.

![](bbox=[0.276, 0.406, 0.663, 0.426])

In this case, the desired migration is easy to understand: the OS should simply move one of B or D to CPU 0. The result of this single job migration is evenly balanced and everyone is happy.

A more tricky case arises in our earlier example, where A was left on CPU 0 and B and D were alternating on CPU 1:

![](bbox=[0.276, 0.549, 0.653, 0.569])

In this case, a single migration does not solve the problem. What would you do in this case? The answer, alas, is continuous migration of one or more jobs. One possible solution is to keep switching jobs, as we see in the following timeline. first A is alone on CPU 0, and B and D alternate on CPU 1. After a few time slices, B is moved to compete with A on CPU 0, while D enjoys a few time slices on CPU 1. And thus load is balanced:

| CPU 0 | A | A | A | A | B | A | B | B | B | B |
| CPU 1 | B | D | B | D | D | D | D | A | D | A | D |

Of course, many possible migration patterns exists. for the tricky part: how should the system decide to enact such a migration?

> Little known fact is that the home planet of Cybertron was destroyed by bad CPU scheduling decisions. And now let be the first and last reference to Transformers in this book, for which we sincerely apologize.

© 2008–19, ARPAC-DUSSEAU

THREE
ASY
PIECES