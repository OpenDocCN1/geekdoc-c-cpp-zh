Try to avoid exception handling when possible. As you saw in this chapter, it's much better (and faster) to avoid an exception in the first place. For example, you can easily avoid the DivideByZeroException by checking for a value of zero before carrying out the division.

Be as explicit as possible with the Exception types you catch in Try/Catch blocks. Try to avoid catching generic Exception types and set up multiple, explicit Catch blocks for each specific type you anticipate.

# SUMMARY

No matter how carefully you program, your site is likely to contain some bugs or throw exceptions at run time. To minimize these exceptions and build a site that runs smoothly as possible, you can do a number of things.

First of all, you can use exception-handling techniques, where you write code that is able to catch exceptions that you foresee and handle them appropriately.

To write code with few bugs as possible, VS offers you a great set of debugging tools. The ability to break into your code and analyze and change the execution environment from client-side all the way to the server is a great aid in your bug-ging adventures.

Even if you have developed your application thoroughly, there's still a chance your site may have issues in production, when they are related to performance, logic errors, or other unexpected results. In cases, you can use the ASP.NET tracing facilities that let you track information about running pages. Analyzing this trace information can bring you a long way in fixing the underlying issues.

Now that your website is complete and highly-free, the next step is to put it online. You see how to deploy your ASP.NET website in the next chapter.

# EXERCISES

+   1. What's the difference between debugging and tracing?

+   2. Imagine you have some code that could potentially throw an exception. For example, you try to send an e-message to a mail server. What kind of exception-handling strategy would you use to avoid the exception being displayed in the browser? What code would you need?

+   3. You're taking over a website that has been built by another developer who had never heard of exception handling. Your client is complaining about the quality of the site and the large number of "Yellow Screens of Death" you sees. After analyzing the code for the entire application, what would be a quick solution to get information about the errors and the locations where they occur? And how can you shield the site's users from the dirty details of the exception messages?

You can find answers to these exercises in Appendix A.