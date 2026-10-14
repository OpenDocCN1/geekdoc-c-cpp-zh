# Chapter 11. Adaptive sample: Sprint 1

# In this chapter, you will

+   - Observe the team’s first sprint planning session.
+   - Follow the implementation and evolution of the first user stories.
+   - Observe the team’s sprint demo and retrospective.

In this chapter, the Trey Research team implements its first four user stories. These are the only stories that the team has assigned to Sprint 1 of the project. The team has set the following sprint goal:

> To demonstrate a dynamic list of rooms, to be able to create a new room, to view the messages written in a room, and for at least two users to be able to share messages in the room

By defining a sprint goal, the team set something challenging but achievable to be completed within the sprint. All work should be aligned to the sprint goal so that the team knows that it is on track and working on only what the client has asked for.

# Planning

The team arranges a planning meeting for the sprint and takes to it the stories that relate to the sprint goal. For this sprint, the stories that the team will implement are:

+   - I want to create rooms for categorizing conversations.
+   - I want to view a list of rooms that represent conversations.
+   - I want to view the messages that have been sent to a room.
+   - I want to send plain text messages to other room members.

The team begins its discussion.

PETRA: Okay, four stories to talk about, but these are the first to be implemented, so I expect there are some key decisions to be made here.

STEVE: Perhaps, yes. Certainly we need to consider a few technologies before we begin. Does anyone have any suggestions?

DIANNE: This is a web application, so we should probably go with something that we are all comfortable and familiar with. ASP.NET MVC seems the obvious choice. Does everyone agree?

STEVE: I’m happy with that.

DAVID: Hmm. I think this is a perfect Node.js application, to be honest.

TOM: I have no experience with Node, unfortunately. Does anyone else?

STEVE: Not really, no. I think Dianne is right to say that we should stick to what we know.

DIANNE: With MVC, we already have much of the code structure set out for us. Look at this sequence diagram.

Dianne shows the team the UML sequence diagram in Figure 11-1.