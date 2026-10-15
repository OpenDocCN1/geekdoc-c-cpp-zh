# Chapter 10 How to Explore Different Types of Loops

Now that we have a working knowledge of loops, let's start to explore some variations or alternative types of these statements. I briefly mentioned that there are four types of loops. We already looked at the standard for loop, so now let's explore these other three. All of these options achieve basically the same thing, they repeatedly run a block of code, but each has advantages in specific situations.

```
foreach (var customer in mailingList)
{
    SendEmail(customer);
}
```

First, let's look at the foreach loop, which is arguably the easiest type of loop to work with in C#. This option streamlines the for loop we looked at in the previous chapter using the special foreach keyword. Rather than having to initialize a variable and use specific incrementors, this type of loop takes care of all of that for us. We simply specify a name for the current item we are working with as we move through a collection. It then executes a block of code for each item in that collection. So in this example, we want to email a survey to every customer in the mailing list. One quirk to be aware