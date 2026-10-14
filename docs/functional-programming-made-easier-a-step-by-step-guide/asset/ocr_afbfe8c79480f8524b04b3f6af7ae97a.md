![](bbox=[0.14, 0.06, 0.85, 0.4])

All requirements must map somehow to this drawing, e.g. logging on a user will involve the Browser, Server and Accounts.

Another great thing about a drawing is it gives all those working on it a common model to work from. It’s a lot easier for me to put a picture of what’s in my head into your head by just showing you a drawing or diagram, as opposed to trying to do so with lots of words.

Too many people try to write words to convey what a picture can do in a fraction of the time and effort.

In more sophisticated systems, this initial drawing will change many times over as the system is reviewed by others and new issues come up that expose deficiencies in the original design. But this early design is important to get out as fast as possible so that you and your team have something to throw darts at.

I doubt we’ll find too much wrong with this drawing since our application is going to be very simple, but who knows. Time will tell.

Notice the SIGINT in the diagram. This is a way to represent that we’re going to handle Ctrl-C to do a clean shutdown of our server.

Also, notice the icon of a disk. It could be implemented as a File or Database. But at this level of detail, it’s just there to show that the User Accounts are persisted, i.e. they’re not transient and will be remembered upon a restart of our server.

Let’s make some major implementation decisions. The Accounts will NOT be kept in a Database such as Postgres and it won’t be stored in a Key/Value Store like Redis. These would all be perfectly good solutions.

But, I don’t want to get bogged down installing these tools onto your development system when we’re trying