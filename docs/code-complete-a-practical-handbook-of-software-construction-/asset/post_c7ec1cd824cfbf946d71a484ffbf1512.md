
Cross-Reference For details on reviews, see Section 21.3, "Formal Inspections," and Section 21.4, "Other Kinds of Collaborative Development Practices."

## Review every line of code

A code review typically involves the programmer and at least two reviewers. That means that at least three people read every line of code. Another name for peer review is "peer pressure." In addition to providing a safety net in case the original programmer leaves the project, reviews improve code quality because the programmer knows that the code will be read by others. Even if your shop hasn’t created explicit coding standards, reviews provide a subtle way of moving toward a group coding standard—decisions are made by the group during reviews, and over time the group derives its own standards.

## Require code sign-offs

In other fields, technical drawings are approved and signed by the managing engineer. The signature means that to the best of the engineer’s knowledge, the drawings are technically competent and error-free. Some companies treat code the same way. Before code is considered to be complete, senior technical personnel must sign the code listing.

## Route good code examples for review

A big part of good management is communicating your objectives clearly. One way to communicate your objectives is to circulate good code to your programmers or post it for public display. In doing so, you provide a clear example of the quality you’re aiming for. Similarly, a coding-standards manual can consist mainly of a set of "best code listings." Identifying certain listings as "best" sets an example for others to follow. Such a manual is easier to update than an English-language standards manual, and it effortlessly presents subtleties in coding style that are hard to capture point by point in prose descriptions.

Cross-Reference A large part of programming is communicating your work to other people. For details, see Section 33.5 and Section 34.3.

## Emphasize that code listings are public assets

Programmers sometimes feel that the code they’ve written is "their code," as if it were private property. Although it is the result of their work, code is part of the project and should be freely available to anyone else on the project who needs it. It should be seen by others during reviews and maintenance, even if at no other time.

![](img/649c8eee28c38ca1e062691e45dc9883_699_0.png)

One of the most successful projects ever reported developed 83,000 lines of code in 11 work-years of effort. Only one error that resulted in system failure was detected in the first 13 months of operation. This accomplishment is even more dramatic when you realize that the project was completed in the late 1960s, without online compilation or interactive debugging. Productivity on the project—7500 lines of code per work-year in the late 1960s—is still impressive by today’s standards. The chief programmer on the project reported that one key to the project’s success was the identification of all computer runs (erroneous and otherwise) as public rather than private assets (Baker and Mills 1973). This idea has extended into modern contexts, including Open Source Software (Raymond 2000) and Extreme Programming’s idea of collective ownership (Beck 2000), as well as in other contexts.

## Reward good code

Use your organization’s reward system to reinforce good coding practices. Keep these considerations in mind as you develop your reinforcement system:

- The reward should be something that the programmer wants. (Many programmers find “attaboy” rewards distasteful, especially when they come from non-technical managers.)
- Code that receives an award should be exceptionally good. If you give an award to a programmer everyone else knows does bad work, you look like Homer Simpson trying to run a nuclear reactor. It doesn’t matter that the programmer has a cooperative attitude or always comes to work on time. You lose credibility if your reward doesn’t match the technical merits of the situation. If you’re not technically skilled enough to make the good-code judgment, don’t! Don’t make the award at all, or let your team choose the recipient.

## One easy standard

If you’re managing a programming project and you have a programming background, an easy and effective technique for eliciting good work is to say “I must be able to read and understand any code written for the project.” That the manager isn’t the hottest technical hotshot can be an advantage in that it might discourage “clever” or tricky code.

## The Role of This Book

Most of this book is a discussion of good programming practices. It isn’t intended to be used to justify rigid standards, and it’s intended even less to be used as a set of rigid standards. Use this book as a basis for discussion, as a sourcebook of good programming practices, and for identifying practices that could be beneficial in your environment.

## 28.2 Configuration Management

A software project is dynamic. The code changes, the design changes, and the requirements change. What’s more, changes in the requirements lead to more changes in the design, and changes in the design lead to even more changes in the code and test cases.

### What Is Configuration Management?

Configuration management is the practice of identifying project artifacts and handling changes systematically so that a system can maintain its integrity over time. Another name for it is “change control.” It includes techniques for evaluating proposed changes, tracking changes, and keeping copies of the system as it existed at various points in time.

If you don’t control changes to requirements, you can end up writing code for parts of the system that are eventually eliminated. You can write code that’s incompatible with new parts of the system. You might not detect many of the incompatibilities until

## Requirements and Design Changes

> Cross-Reference Some development approaches support changes better than others. For details, see Section 3.2, "Determine the Kind of Software You're Working On."

During development, you're bound to be bristling with ideas about how to improve the system. If you implement each change as it occurs to you, you'll soon find yourself walking on a software treadmill—for all that the system will be changing, it won't be moving closer to completion. Here are some guidelines for controlling design changes:

## Follow a systematic change-control procedure

As Section 3.4 noted, a systematic change-control procedure is a godsend when you have a lot of change requests. By establishing a systematic procedure, you make it clear that changes will be considered in the context of what's best for the project overall.

## Handle change requests in groups

It's tempting to implement easy changes as ideas arise. The problem with handling changes in this way is that good changes can get lost. If you think of a simple change 25 percent of the way through the project and you're on schedule, you'll make the change. If you think of another simple change 50 percent of the way through the project and you're already behind, you won't. When you start to run out of time at the end of the project, it won't matter that the second change is 10 times as good as the first—you won't be in a position to make any nonessential changes. Some of the best changes can slip through the cracks merely because you thought of them later rather than sooner.

A solution to this problem is to write down all ideas and suggestions, no matter how easy they would be to implement, and save them until you have time to work on them. Then, viewing them as a group, choose the ones that will be the most beneficial.

## Estimate the cost of each change

Whenever your customer, your boss, or you are tempted to change the system, estimate the time it would take to make the change, including review of the code for the change and retesting the whole system. Include in your estimate time for dealing with the change's ripple effect through requirements to design to code to test to changes in the user documentation. Let all the interested parties know that software is intricately interwoven and that time estimation is necessary even if the change appears small at first glance.

Regardless of how optimistic you feel when the change is first suggested, refrain from giving an off-the-cuff estimate. Such estimates are often mistaken by a factor of 2 or more.

> Cross-Reference For another angle on handling changes, see "Handling Requirements Changes During Construction" in Section 3.4. For advice on handling code changes safely when they do occur, see Chapter 24, "Refactoring."

## Be wary of high change volumes

While some degree of change is inevitable, a high volume of change requests is a key warning sign that requirements, architecture, or top-level designs weren't done well enough to support effective construction. Backing up to work on requirements or architecture might seem expensive, but it won't be nearly as expensive as constructing the software more than once or throwing away code for features that you really didn't need.
