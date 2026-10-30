# 4.2.1 Testing

The next step is to run the program and test if it really works. I compiled and ran this program supplying the values 1,2,3,4 for n, and it did print out the answers 2, 2.5, 2.667, 2.70833. If you did the calculation by hand as suggested earlier, you will realize that these values are indeed correct. You could also try some large value for n, say 10. When I did this, I got the result 2.71828. Since e is a famous number, you should be able to get its value from textbooks, and you will see that 2.71828 is the often quoted value.

# 4.2.2 Correctness Proof

Testing is one way to check if your program is correct. However, testing does not really give you a complete guarantee of correctness. You know what the program does for the input values that you checked; but how can you be sure that the program will not give a wrong answer on other values?

One way to be sure is to prove that the program is correct. This is often not practical for large programs. However, a proof can be written for our small program for computing e. We do this next. It will have some important lessons in general too.

You may be saying at this point, “But our program is obviously correct, after all didn’t we design it so that the variable result has the desired value?” Unfortunately, it isn’t so simple: mistakes can creep in at any stage. Let me confess that when I first wrote the program of Figure 4.1, I forgot to initialize the variable i. As a result, I was getting very strange answers. Forgetting to initialize a variable is a “silly” mistake, but it is very easy to make silly mistakes! This is an important humbling lesson that programming teaches you. Note that if our program is doing something serious, say controlling an aircraft in flight, a mistake of any kind can cause a crash. So we must learn to avoid even silly mistakes.

So as a cross check, we will try to anyway prove the correctness of the program after we have finished writing it. In this proof, we will basically check whether our program is adhering to our plan, i.e. we confirm whether the variables indeed take the values we expect them to take. The proof is based on mathematical induction. The induction hypothesis is what we stated as our plan.

# Induction Hypothesis: The values of i, term, result on the tth entry to the loop are respectively:

t, 1/(t−1)!, 1/0! + … + 1/(t−1)!

For the base case, we consider t = 1, i.e. the values on the first entry. Substituting t = 1 in the values in the Induction Hypothesis, we see that we want i, term, result to be all 1. But the code before the loop indeed initializes all these variables to 1. Thus we have established the base case. Note that when you do this part of the proof, you will discover if you indeed forgot to initialize any variable.

Next we will assume that the Induction Hypothesis is true on the tth entry, and show that it must also hold on the t + 1th entry. Thus we need to prove: