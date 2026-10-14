segregation? At the moment, the GetAllRooms method isn’t transformed, so I just delegate straight down to the wrapped instance.

DIANNE: Should we allow the user to use markdown in the room names, too? That way, the GetAllRooms method would be decorated, too.

STEVE: I think we should leave it as it is for now. Let’s not split the interface or allow markdown in the room names. Depending on the client’s feedback during the demo, we can make a decision either way.

# “I want to filter message content so that it is appropriate.”

Dianne and David have both been assigned to the message content filtering story. Together they will implement the functionality required by using pair programming.

DIANNE: As mentioned in the planning session, we don’t have time to implement a fully data-driven message content filter during this sprint. Instead, we need to make some progress toward that goal.

DAVID: So will we just implement the data access part for this sprint and come back to it next week?

DIANNE: No, we can’t do that. We need to deliver a vertical slice of functionality: something that is demonstrable to the client, but not necessarily complete. Just implementing the data access would not add any value.

DAVID: I don’t understand how we can deliver some value yet not implement the whole content filter.

DIANNE: What we will do is compromise somewhere so that we can be finished in a short amount of time yet provide some value to the client. For this story, the compromise is simple: we should hardcode the list of values that are considered inappropriate, instead of retrieving them from persistent storage like a database.

DAVID: I guess that makes sense. But I’ve always been told that hardcoding things is bad. Isn’t this poor design?

DIANNE: Sort of, yes. It’s technical debt. We are making a prudent decision to compromise on some desirable functionality in order to deliver something sooner rather than later. Perhaps the client knows exactly the list of words that they want to limit and they will never change. If so, we could complete this story just by hardcoding that list.

DAVID: I suppose it’s quite clever, really. Rather than take a lot of time to implement something, we aim for a simpler solution as an objective on the way to the goal.

DIANNE: Exactly! And, as each objective is met, it is possible that the next objective could be totally different—or that the goal itself changes dramatically.

DAVID: Another thing I’m unsure of: how are we going to implement this story? Should we create a decorator for the message writer that throws an exception when an inappropriate word is included in the message?

DIANNE: The trouble with that solution is that it uses exceptions for control flow. Exceptions are better reserved for situations that are truly “exceptional.” This is more of a validation scenario.