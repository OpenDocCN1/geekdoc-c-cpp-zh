
PETRA: But they asked for formatted text?
STEVE: Don’t worry, that’s another story—it just comes later, after plain text has been delivered.
PETRA: Okay. As a room member, I want to send formatted text messages to other room members.
STEVE: That’s two. Any more?
DAVID: I want to create rooms?
DIANNE: Yes. I think this will surely make that person a room owner, won’t it? As a room owner, I want to create rooms for categorizing conversations?
STEVE: Good.
TOM: They said they wanted to send images and files, too.
PETRA: Yes, that’s another story.
STEVE: One more: I want to create read-only conversations.
DIANNE: That’s the last sentence covered. I think we’re done.

## Story point estimation

By now, the team members agree that they have found the user stories from the client’s requirements.

They create user story cards from each of the following bullet points:

- I want to send plain text messages to other room members.
- I want to create rooms for categorizing conversations.
- I want to send formatted text to other room members.
- I want to send images and/or files.
- I want to create read-only conversations.

The team arranges the cards on the table ready for assigning story points. There are only five stories, so the team decides to use planning poker to estimate the effort required.

PETRA: Sending plain text messages can’t be too difficult, surely?
DAVID: It would only take me an hour! [Steve and Dianne raise their eyebrows. Tom rolls his eyes.]
STEVE: Well, you can’t really do this one first. Without rooms, you have no participants.
DIANNE: True, there’s a dependency there, but it doesn’t alter the size. [Steve nods in agreement.]
PETRA: Is everyone ready?

After some final card shuffling, the team members show their cards:

| PETRA | TOM | STEVE | DIANNE | DAVID |
| --- | --- | --- | --- | --- |
| 3 | 3 | 5 | 5 | 1 |

PETRA: Hmm, that’s a bit of a mix. David, why one?
DAVID: There’s almost nothing to do here: it’s just taking some input and writing it to the screen.
DIANNE: Not exactly, David. There’s more to it than that. We need to save the text somewhere and be able to read it back. Other room members need to read it, too.
STEVE: Indeed, Dianne’s right. We need to think about the architecture here.
DAVID: Oh, yeah. I thought it was just about writing it out to the browser window. But, of course, that’s only going to be viewed by the person who wrote it—not shared. Wow, that’s much harder!
PETRA: Okay, shall we re-estimate?

The team members count down from three and show their cards again:

| PETRA | TOM | STEVE | DIANNE | DAVID |
| --- | --- | --- | --- | --- |
| 5 | 5 | 5 | 5 | 5 |

STEVE: Can we split this story up into “reading” and “writing”?
DIANNE: Sorry—I’m not sure what you mean.
TOM: I think he means that we could have a story for viewing the messages that have been sent to a room and another story for sending messages to that room. Right, Steve?
STEVE: Yes. I just think it would help for us to start really small. I know an estimate of five is not all that large, but it is significant at such an early stage of development.
DIANNE: Okay, I’m happy with that. Shall we re-estimate sending messages?

| PETRA | TOM | STEVE | DIANNE | DAVID |
| --- | --- | --- | --- | --- |
| 3 | 3 | 3 | 3 | 3 |

DIANNE: And now let’s estimate just viewing the messages already sent to a room.

| PETRA | TOM | STEVE | DIANNE | DAVID |
| --- | --- | --- | --- | --- |
| 2 | 3 | 2 | 2 | 1 |

STEVE: Tom, David—will you accept a two?
TOM: Yes, two is fine.
DAVID: I agree. Two makes sense.
STEVE: Excellent. Two it is. [Steve marks a two on the user story and reads out the next.] I want to create rooms for categorizing conversations.
DIANNE: How do we demonstrate this?
TOM: Petra and I spoke about this, and one of the acceptance criteria is that we should be able to view the list of the rooms that have been created.
DIANNE: Another candidate for splitting into “read” and “write” stories?
STEVE: I think so, yes.
DIANNE: Let’s estimate the read part first: I want to view a list of rooms that represent conversations.

The team members show their cards:

| PETRA | TOM | STEVE | DIANNE | DAVID |
| --- | --- | --- | --- | --- |
| 2 | 2 | 2 | 2 | 2 |

DIANNE: Wow! Unanimous. And now the story for creating new rooms?

The team members show their cards:

| PETRA | TOM | STEVE | DIANNE | DAVID |
| --- | --- | --- | --- | --- |
| 2 | 2 | 2 | 2 | 1 |

STEVE: David, are you okay to take a two?
DAVID: Yeah, that’s fine.
STEVE: Next: I want to send formatted text to other room members.
PETRA: So this is just adding in formatted text?
STEVE: Yes—assume that the plain text story has been completed and is a prerequisite to this story.
TOM: What sort of formatting do they want? Embedded images or something?
DAVID: Images is a separate story. I think of this more as bold, italic, underline—things like that.
PETRA: Yes, that’s what the client said that they wanted. HTML was the only format they could think of, but I don’t think we’d want to go there. Just simple text formatting, nothing too strenuous.
STEVE: Okay, ready?

The team members show their cards:

| PETRA | TOM | STEVE | DIANNE | DAVID |
| --- | --- | --- | --- | --- |
| 1 | 1 | 1 | 1 | 1 |

STEVE: Hurray! We’re all agreed on that, then. Next: I want to send images and/or files.
DIANNE: I don’t like the “and/or” bit in this story. Can we be less ambiguous?
TOM: Well, what’s the difference between sending an image and sending a file?
PETRA: From my conversation with the client, they wanted images to be shown in the browser, whereas files would be downloaded to other users’ machines.
DAVID: Then this is surely two different stories, isn’t it? One for downloading files and one for showing images.
DIANNE: Exactly, this is too big at the moment. We should tackle them separately. It feels like files would be the simpler of the two, so we could put that first, with images using it as a prerequisite.
STEVE: I agree. So let’s change this to two stories. I want to send files to other room members. I want to show images to the room. Let’s estimate them separately.

The team members show their cards for the first story:

| PETRA | TOM | STEVE | DIANNE | DAVID |
| --- | --- | --- | --- | --- |
| 5 | 5 | 3 | 3 | 3 |

STEVE: Hmm, why fives?
TOM: Testing this is going to be difficult. There are a lot of unusual test cases that we will need to consider. For instance, what if the file is very large? What if the file is malicious? Will we keep hold of the file on our servers? For how long?
STEVE: I take your point. I was considering only the development effort here, sorry. I can tell now that you will be spending a lot of time trying to break this.
DAVID: Shall we re-estimate, or just take five?
STEVE: I’m happy with five.
DIANNE: Me too.
STEVE: And what about images?
PETRA: This is just about showing the image to the users on the page?
STEVE: Yes, the upload part should have been completed by now, so this is just about showing the image on the page.

The team members show their cards:

| PETRA | TOM | STEVE | DIANNE | DAVID |
| --- | --- | --- | --- | --- |
| 3 | 3 | 3 | 3 | 5 |

STEVE: David, a five?
DAVID: Yes—I think this is a bit harder than it looks. What if the image is inappropriate? What if there are a lot of users and the image takes a long time to download? That will put a load on our servers.
DIANNE: I agree, those are all concerns, but I think they are out of scope for now. Petra, make a note to ask the client what they think of a content filter—not just for images, but for text, too. But, at the moment, we only need to support 20 users. That should not represent a significant load.
PETRA: Good idea about the content filter, David.
STEVE: Happy to take a three, David?
DAVID: Actually, now I think it’s a two! But, yes—a three is fine.
STEVE: Good stuff. Final story: I want to create read-only conversations.

The team members show their cards:

| PETRA | TOM | STEVE | DIANNE | DAVID |
| --- | --- | --- | --- | --- |
| 8 | 1 | 5 | 8 | 3 |

STEVE: Oh dear. That’s all a bit random! Tom, one?
TOM: Sorry, forgot about analysis and development effort. This just seems really, really easy to test in comparison to the other stories.
STEVE: Okay. Petra, Dianne, eight?
DIANNE: At this point, we won’t have roles or permissions, which we’ll need. I think there’s a lot of work here.
DAVID: Oh, I didn’t think we needed roles or permissions at this point. I thought we’d just flag a conversation as read-only.
STEVE: It needs to be read-only on a per-user basis. Still, I don’t think we need any heavy infrastructure for permissions or roles as yet. I think it should be implemented with a very simple solution first, and we can elaborate on it later.
DIANNE: That sounds fine to me.
PETRA: Yeah, I trust you guys.
STEVE: The average here was exactly five. Shall we take that? [Everybody agrees.]
STEVE: David, still think this is a single sprint of work?
DAVID: Hmm... No!
