work on their own copy of the code and regularly *integrate* their changes with those of other developers. The version control system provides tools to automatically merge files together and to generate reports on the differences between different developers' copies of the code.

+   iv) Tools so that it is possible to create patches to your system. A developer is usually working to add new features, but when bugs occur they need to be patched quickly without testing all the new features.

+   v) Security so that only authorised users can view and edit your code.

Any serious software project will use version control. You should use some form of version control in your projects so that you at least have a full history of your changes and have regular backups.

One popular and free version-control system is called Git. It allows you to store your data on the cloud using services such as GitHub and Bitbucket. This has the advantage that issues such as backing up your data will be dealt with for you.

To their embarrassment, some major banks have forgotten to use version control for their projects! As recently as 2012 I knew of one major bank with a running system where they had lost the source code and so couldn't change or understand the system. As well as being embarrassing, this is an enormous operational risk. What would the bank do if a bug occurred?

# 15.4.2 Bug tracking

When bugs occur in any realistic system, they should be recorded in a bug-tracking database. As well as recording bugs, you should record requests to enhance your software.

A bug-tracking system keeps a record of what bugs are in your system, when they were fixed, who has tested them, and so forth.

On simple projects one might think that you should always fix bugs the moment that they are found, but in practice this is not always possible. For example, a bug that happens on a customer's computer may be hard to re- produce, in which case you may have little choice but to record the details and say that you will keep an eye on the problem.

For larger systems, a tool to help with recording bugs is essential. In particular it allows you to prioritise your work and focus on the most pressing problems. A bug database is also essential to keeping your customers happy. They can use it to record their complaints and monitor the progress you are making on fixing their issues.

# 15.4.3 Testing framework

In this book we have emphasised the importance of testing your code.