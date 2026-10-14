
TOM: I think so. It’s just too difficult for me to guarantee that I can be here at 9:00 A.M..

PETRA: I’ll inform management that we should look into flexible working hours, Tom.

TOM: Thanks—that would be great.

DAVID: I think we need to do the demo less often. The client expressed surprise that they had to be here every week and also that we were showing them a small amount of functionality. Why not tackle both issues at the same time by demonstrating once every fortnight, instead?

STEVE: That’s a good idea—definitely worth looking in to. However, I think the demo is a great motivator for delivery. I would like to retain the weekly demonstration, but what do you think about limiting the demos for the client to every other week, with internal demos in between? We don’t need to involve management, just this team.

PETRA: I think that would work. It would allow us to perfect the demo process and show off more functionality to the client at the same time.

David looks happy, and Steve marks the following on the whiteboard:

- Dianne and Steve to commit to the Proseware project and focus on story delivery.
- Demonstrate once a fortnight to the client.
- Demonstrate in between just to the team.
- Take an extra half-hour before the demo to run through the agenda and check that everything is working.

## Things to keep?

Sometimes, the best course of action is inaction—in other words, making a note of something positive that a team does but that is not yet habitual. This is the topic of the “things to keep” question.

STEVE: What about things to keep? Is there anything that we took initiative on that we should keep doing?

Everyone remains quiet.

STEVE: Okay, if anyone thinks of anything after this meeting, let me know and we’ll create an action item.

## Surprises?

Almost every sprint will have revealed some surprises. The team could have discovered an antiquated process that needs updating, a requirement that wasn’t properly captured, or a piece of software that suddenly stopped working. The “surprises” section of the sprint retrospective aims to capture all of these items so that they cannot be classed as surprises in the future.

STEVE: How about surprises?

DAVID: I was quite surprised that they liked my content filter idea!

DIANNE: I think it makes great sense, to be honest. They’re targeting Proseware at a certain demographic, and it is likely to represent a lot of value to them.

PETRA: I agree, it was a great idea. Perhaps that’s something that we should keep doing: keep thinking of ideas.

Steve writes it down in the appropriate column on the whiteboard.

TOM: It surprised me that Steve and Dianne weren’t working on this project full time.

PETRA: Okay, anyone else?

DIANNE: It surprised me, too. I was under the impression that I was to be a full-time part of Proseware, but Steve and I needed to put out a fire on another project.

STEVE: We should get some kind of agreement from management that someone else will pick that up next sprint, rather than us.

DIANNE: Good plan.

Steve notes this down on the whiteboard.

STEVE: Okay, thanks guys. A good sprint overall and great start to this project. Let’s keep it up.

PETRA: I agree. Let’s make the changes agreed in this retrospective and ensure that we continue on this same path next week.

The meeting ends and the team departs.

## Summary

The first sprint has been a qualified success for the team. Although not everything has gone according to plan, the team has gathered some valuable feedback in a short amount of time. This is a key part of any Agile process: the constructive criticism required to take corrective action is always nearby.

In the next chapter, the team continues working on sprint two and carries forward the stories that have not yet been implemented.

## Chapter 12. Adaptive sample: Sprint 2

## In this chapter, you will

- Observe the team’s second sprint planning session.
- Follow the implementation and evolution of the next user stories.
- Observe the team’s second sprint demo and retrospective.

In this chapter, the Trey Research team continues to implement user stories for the Proseware project. The direction has changed slightly due to the feedback received from the client at the sprint demonstration during sprint 1. The team has set the following sprint goal:

> To add optional markdown-formatted text to conversations, to filter message content so that it is appropriate, and to ensure that 300 users can be served concurrently

This sprint goal incorporates all of the stories that the team has committed to completing during the sprint. As usual, the team will conclude the sprint with a demonstration to the client—to elicit feedback and to inform the client of progress—and a sprint retrospective in which the team will address any problems that the sprint presented and to acknowledge the good work that the team did during the sprint.

First, though, the team begins the sprint with a planning session.

## Planning

The second planning meeting for the project allows the members of the team to discuss the user stories that they have committed to in their sprint goal. The second sprint includes the following user stories:

- I want to send markdown that will be correctly formatted.
- I want to filter message content so that it is appropriate.
- I want to serve hundreds of users concurrently.

With the whole team assembled in a meeting room, the discussion begins:

PETRA: We’ve got a new story on the backlog as a result of the feedback from the sprint demo in the last sprint.

STEVE: Instead of implementing read-only conversations, the client wants us to prioritize the content filter.

DIANNE: So we should estimate this story now.

STEVE: Yes, if we get an estimate for this story we can understand how much capacity we have for this sprint.

DIANNE: Okay, so on the count of three, let’s show our estimates.

Everyone shuffles their cards before showing them.

| PETRA | TOM | STEVE | DIANNE | DAVID |
| 3 | 3 | 8 | 5 | 8 |

STEVE: Wow, we have a bit of variety here. Tom, could you explain your three?

TOM: I chose three mainly because I can automate the testing for this fairly easily.

Providing a text message with a disallowed word in it and asserting that you could not post the message is simple enough. If there’s more technical complexity to the implementation, I’d be happy to increase the estimate.

STEVE: David, would you like to explain your eight? Then I’ll explain mine.

DAVID: Yes, I think this is difficult because we need to add another table to data storage for the disallowed words. This is going to take some time to implement.

STEVE: Yes, I thought that, too. I also considered that we don’t want to limit disallowed words to the messages users write in conversations—we should also include the names of the rooms. In fact, any time we take input from the user we should submit it to the content filter.

DIANNE: How about instead of implementing a data-driven content filter right away, we just simplify it and hardcode the blocked list of words?

STEVE: Okay, I think that’s a good idea. Later we can add stories to target administration of the content filter.

PETRA: Great—shall we re-estimate or take the five?

TOM: I’m happy with a five.

STEVE: Yes, a five seems fair.

DAVID: I agree, five it is.

PETRA: Excellent, thanks everyone. Let’s make sure we hit all our goals this sprint so we can show the client a great demo this week.

Everyone files out of the meeting room ready to get to work.

## “I want to send markdown that will be correctly formatted.”

Before he starts this story, David asks Steve about parsing markdown.

DAVID: I assume I should be using a third-party library for parsing markdown and transforming it into HTML, but I’m not sure which library to use.

STEVE: Okay, hold on. I think Dianne has some experience in this area—we’ll ask her.

Steve beckons Dianne over to quiz her about markdown libraries.

STEVE: Dianne, you’ve used some markdown libraries before, right? Which one did you prefer?

DIANNE: I evaluated a few previously. Try MarkdownDeep—it seemed simple enough to use. There’s a NuGet package for it, too.

STEVE: Thanks, Dianne. David, try MarkdownDeep. Also, make sure you create a new class library project for any classes that depend on this library.

DAVID: Okay—thanks.

David sets to work on implementing the markdown transform for the application. After a few hours, he is ready to show Steve and Dianne his work. He asks them to peer review what he has done.

DAVID: I wondered where the best place to put the implementation of the markdown transform was. I knew I wanted to intercept the room message text by implementing a decorator for an existing interface. I thought that if I implemented it on the
