This is because the time module works with a second and for a minute to elapse, 60 seconds have to be elapsed; therefore, the subtraction between the end and the beginning has to be greater than or equal to 60, in the affirmative case, True will be returned, and finally, we will get out of the infinite cycle.

Once the alarm module is finished, we proceed to make the program, as we can see below:

We can see that the program imports two modules, the one we have created, the alarm and the time module.

The first thing we do is to create the variable s as an input, which tells the user if he wants to start.

If the answer is affirmative, then the variable h representing the time will be equal to "time.strftime ("%H:%M:%S"),” which means that we are using a function of the time module that returns the hour to use in the specified format so that it can then be printed using the print function.

The next action is to use the alarm module using the command alarm.cron(), which means that the cron() function is being called.

When this function is finished, the time will be assigned to the variable h, again, to finish printing it and being able to observe its correct operation.

As a conclusion of this chapter, we can say that the modules are fundamental for the proper performance of the programmer since they allow to make the code more legible, in addition, that it allows subdividing the problems to attack them from one to one and thus to carry out the tasks easily.