
If I had any doubts about the value of formal inspections, my experience in creating the second edition of Code Complete eliminated them.

## Inspection Summary

Inspection checklists encourage focused concentration. The inspection process is systematic because of its standard checklists and standard roles. It is also self-optimizing because it uses a formal feedback loop to improve the checklists and to monitor preparation and inspection rates. With this control over the process and continuing optimization, inspection quickly becomes a powerful technique almost no matter how it begins.

Further Reading For more details on the SEI's concept of developmental maturity, see Managing the Software Process (Humphrey 1989).

The Software Engineering Institute (SEI) has defined a Capability Maturity Model (CMM) that measures the effectiveness of an organization’s software-development process (SEI 1995). The inspection process demonstrates what the highest level is like. The process is systematic and repeatable and uses measured feedback to improve itself. You can apply the same ideas to many of the techniques described in this book. When generalized to an entire development organization, these ideas are, in a nutshell, what it takes to move the organization to the highest possible level of quality and productivity.

## CHECKLIST: Effective Inspections

- Do you have checklists that focus reviewer attention on areas that have been problems in the past?
- Have you focused the inspection on defect detection rather than correction?
- Have you considered assigning perspectives or scenarios to help reviewers focus their preparation work?
- Are reviewers given enough time to prepare before the inspection meeting, and is each one prepared?
- Does each participant have a distinct role to play—moderator, reviewer, scribe, and so on?
- Does the meeting move at a productive rate?
- Is the meeting limited to two hours?
- Have all inspection participants received specific training in conducting inspections, and has the moderator received special training in moderation skills?
- Is data about error types collected at each inspection so that you can tailor future checklists to your organization?
- Is data about preparation and inspection rates collected so that you can optimize future preparation and inspections?
- Are the action items assigned at each inspection followed up, either personally by the moderator or with a reinspection?
- Does management understand that it should not attend inspection meetings?
- Is there a follow-up plan to assure that fixes are made correctly?

## 21.4 Other Kinds of Collaborative Development Practices

Other kinds of collaboration haven’t accumulated the body of empirical support that inspections or pair programming have, so they’re covered in less depth here. The collaborations covered in this section includes walk-throughs, code reading, and dog-and-pony shows.

### Walk-Throughs

A walk-through is a popular kind of review. The term is loosely defined, and at least some of its popularity can be attributed to the fact that people can call virtually any kind of review a “walk-through.”

Because the term is so loosely defined, it’s hard to say exactly what a walk-through is. Certainly, a walk-through involves two or more people discussing a design or code. It might be as informal as an impromptu bull session around a whiteboard; it might be as formal as a scheduled meeting with an overhead presentation prepared by the art department and a formal summary sent to management. In one sense, “where two or three are gathered together,” there is a walk-through. Proponents of walk-throughs like the looseness of such a definition, so I’ll just point out a few things that all walk-throughs have in common and leave the rest of the details to you:

- The walk-through is usually hosted and moderated by the author of the design or code under review.
- The walk-through focuses on technical issues—it’s a working meeting.
- All participants prepare for the walk-through by reading the design or code and looking for errors.
- The walk-through is a chance for senior programmers to pass on experience and corporate culture to junior programmers. It’s also a chance for junior programmers to present new methodologies and to challenge timeworn, possibly obsolete, assumptions.
- A walk-through usually lasts 30 to 60 minutes.
- The emphasis is on error detection, not correction.
- Management doesn’t attend.
- The walk-through concept is flexible and can be adapted to the specific needs of the organization using it.

### What Results Can You Expect from a Walk-Through?

Used intelligently and with discipline, a walk-through can produce results similar to those of an inspection—that is, it can typically find between 20 and 40 percent of the errors in a program (Myers 1979, Boehm 1987b, Yourdon 1989b, Jones 1996). But in general, walk-throughs have been found to be significantly less effective than inspections (Jones 1996).

![](img/649c8eee28c38ca1e062691e45dc9883_529_0.png)

Used unintelligently, walk-throughs are more trouble than they’re worth. The low end of their effectiveness, 20 percent, isn’t worth much, and at least one organization (Boeing Computer Services) found peer reviews of code to be “extremely expensive.” Boeing found it was difficult to motivate project personnel to apply walk-through techniques consistently, and when project pressures increased, walk-throughs became nearly impossible (Glass 1982).

I’ve become more critical of walk-throughs during the past 10 years as a result of what I’ve seen in my company’s consulting business. I’ve found that when people have bad experiences with technical reviews, it is nearly always with informal practices such as walk-throughs rather than with formal inspections. A review is basically a meeting, and meetings are expensive. If you’re going to incur the overhead of holding a meeting, it’s worthwhile to structure the meeting as a formal inspection. If the work product you’re reviewing doesn’t justify the overhead of a formal inspection, it doesn’t justify the overhead of a meeting at all. In such a case you’re better off using document reading or another less interactive approach.

Inspections seem to be more effective than walk-throughs at removing errors. So why would anyone choose to use walk-throughs?

If you have a large review group, a walk-through is a good review choice because it brings many diverse viewpoints to bear on the item under review. If everyone involved in the walk-through can be convinced that the solution is all right, it probably doesn’t have any major flaws.

If reviewers from other organizations are involved, a walk-through might also be preferable. Roles in an inspection are more formalized and require some practice before people perform them effectively. Reviewers who haven’t participated in inspections before are at a disadvantage. If you want to solicit their contributions, a walk-through might be the best choice.

![](img/649c8eee28c38ca1e062691e45dc9883_529_1.png)

Inspections are more focused than walk-throughs and generally pay off better. Consequently, if you’re choosing a review standard for your organization, choose inspections first unless you have good reason not to.

### Code Reading

Code reading is an alternative to inspections and walk-throughs. In code reading, you read source code and look for errors. You also comment on qualitative aspects of the code, such as its design, style, readability, maintainability, and efficiency.

![](img/649c8eee28c38ca1e062691e45dc9883_530_0.png)

A study at NASA’s Software Engineering Laboratory found that code reading detected about 3.3 defects per hour of effort. Testing detected about 1.8 errors per hour (Card 1987). Code reading also found 20 to 60 percent more errors over the life of the project than the various kinds of testing did.

Like the idea of a walk-through, the concept of code reading is loosely defined. A code reading usually involves two or more people reading code independently and then meeting with the author of the code to discuss it. Here’s how code reading goes:

- In preparation for the meeting, the author of the code hands out source listings to the code readers. The listings are from 1000 to 10,000 lines of code; 4000 lines is typical.
- Two or more people read the code. Use at least two people to encourage competition between the reviewers. If you use more than two, measure everyone’s contribution so that you know how much the extra people contribute.
- Reviewers read the code independently. Estimate a rate of about 1000 lines a day.
- When the reviewers have finished reading the code, the code-reading meeting is hosted by the author of the code. The meeting lasts one or two hours and focuses on problems discovered by the code readers. No one makes any attempt to walk through the code line by line. The meeting is not even strictly necessary.
- The author of the code fixes the problems identified by the reviewers.

![](img/649c8eee28c38ca1e062691e45dc9883_530_1.png)

The difference between code reading on the one hand and inspections and walk-throughs on the other is that code reading focuses more on individual review of the code than on the meeting. The result is that each reviewer’s time is focused on finding problems in the code. Less time is spent in meetings in which each person contributes only part of the time and in which a substantial amount of the effort goes into moderating group dynamics. Less time is spent delaying meetings until each person in the group can meet for two hours. Code readings are especially valuable in situations in which reviewers are geographically dispersed.

![](img/649c8eee28c38ca1e062691e45dc9883_530_2.png)

A study of 13 reviews at AT&T found that the importance of the review meeting itself was overrated; 90 percent of the defects were found in preparation for the review meeting, and only about 10 percent were found during the review itself (Votta 1991, Glass 1999).
