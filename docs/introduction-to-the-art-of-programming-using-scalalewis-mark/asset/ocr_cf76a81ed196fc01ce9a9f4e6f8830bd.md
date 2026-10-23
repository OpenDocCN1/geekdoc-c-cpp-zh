+   - Actors can have mutable data. As long as they do not share mutable data there is no chance for race conditions.

+   - Scala comes with support for actors in the scala.actors package.

+   - To create fully functional actors, make classes that extend the Actor trait.

+   - Those classes should implement the act method. This is what is called when an actor is started.

+   - To handle messages, the act method should include a call to receive or react, typically inside of a looping structure.

+   * Both receive and react take a single argument that is a partial function. It should have cases for the different messages that actor should be sent and appropriate handling code.

+   * The receive method if a standard method that blocks until an appropriate message is sent to that actor. It holds onto the actors thread and returns a value so it can be used as an expression.

+   * The react method does not return. Anything after it is unreachable. This allows thread sharing among actors. You need to use loop or loopWhile to make it repeat. A simple while loop will not work.

+   - It is ideal for messages to be immutable and work with pattern matching. For this reason, case classes are often used to create different types of messages.

+   - An example of an actor-based event simulation was written for circuits at the logic gate level.

# 34.4.2 Exercises

+   1. Write a simple actor that uses receive without a loop. Start the actor and verify that it will only handle a single message without a restart.

+   2. Take your actor from the previous exercise and put the call to receive in a while loop then verify that it can now handle multiple messages.

+   3. Write an actor that has the ability to know about another actor of that same type that can cooperatively count down. The actor should handle two messages. One will pass it an actor that will be its friend. The other handles a numeric value and if it is greater than zero it prints the value and then sends a message tot he friend with a value one less than what it printed. Make two of these actors and have them count down. To verify that both actors are involved in the conversation, you can give them names that are printed along with the numeric values.