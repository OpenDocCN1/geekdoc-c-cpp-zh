**TABLE 21.4 Continued**

| Field Name | Type | Description |
| --- | --- | --- |
| PostCmd | Varchar(255) | A command the Controller should run after a test. |
| PostCmdWithRunID | Int | Whether the post-command should be passed the Token, RunID, DatabaseName, UserName, and the NodeName of the test. A 1 indicates that they should be passed; a 0 indicates that they should not be passed. |
| RepeatCmd | Varchar(255) | A command the Controller should run periodically during a test. |
| RepeatCmdWithRunID | Int | Whether the repeat command should be passed the Token, RunID, DatabaseName, UserName, and the NodeName of the test. A 1 indicates that they should be passed; a 0 indicates that they should not be passed. |
| RepeatCmdInterval | Int | The interval, in seconds, that the controller should wait. |
| CommentOne | Varchar(120) | A comment about the test. |
| CommentTwo | Varchar(120) | A comment about the test. |
| CommentThree | Varchar(120) | A comment about the test. |

# Viewing the Results of a Test

Of course, after you run a test, you'll want to see and understand the results. It's easy to get the basics, such as transactions per second and requests sent, because you can see these statistics in the command window while the test is being run, as you saw in Figure 21.3. These numbers are saved to an .out file that you can read with any text editor.

# Summary

Large-scale, enterprise applications are complex. Getting them to perform at an acceptable level can be an enormous challenge, especially when the application load is heavy.

The first thing you must do is to assess your needs. An application that performs up to snuff doesn't need optimization, and you don't want to waste time doing so.

Some relatively simple considerations can make a big difference. On the list of things to note are DSN types, algorithm efficiency, using JIT, Registry use, avoiding memory leaks, language considerations, and middle-tier architecture. And some of these can make a difference of more than 1000%.