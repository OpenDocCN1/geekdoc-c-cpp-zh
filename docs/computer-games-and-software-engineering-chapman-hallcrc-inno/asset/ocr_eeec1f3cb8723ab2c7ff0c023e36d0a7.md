The Pick Up Executor makes a synchronous call to the Key Item Memorizer, but this module is in place and so the call is satisfied.

# ### 10.5.1 Using Trash Receptacles

The new behavior in trash collector is to use trash receptacles. Because the reused Mammoth Listener notifies on every spotted item, the AI is already aware of garbage cans. We can add a new instance of the Key Item Memorizer, called a Trash Can Memorizer to receive these notifications and track garbage cans. However, this creates an unintended connection on the key_item_visible event. Event renaming resolves this, and so we have the Trash Can Memorizer generate trash_can_visible and no_trash_can_visible events instead of key item events.

Once trash has been collected, the NPC must move to the garbage can and drop the trash in the can. Fundamentally, this is the same logic as the Pick Up Executor, which handles moving to and picking up an object. We create a Drop Executor by renaming all events with pick_up into drop, e.g., pick_up_item becomes drop_item, and by changing the target of the synchronous call to the Trash Can Memorizer. The drop_item is currently unconnected and will form the connection to a yet-to-be introduced Drop Actuator.

# ### 10.5.2 Building the NPC

With most behaviors now in place, the only design task left is to fill in missing behaviors with new modules, and connect them all with a new strategizer. Because we have designed our AI in a modular fashion with clearly defined interfaces, we know the exact events available for connection, summarized in Table 10.1.

The trash collector brain will be somewhat different than the squirrel brain. The behavior desired is to pick up a single piece of garbage and throw it in the trash, repeating indefinitely. The brain is thus a simple two-state statechart, alternating between the two goals based upon if the NPC currently has a piece of trash.

A new decider was created to implement the high-level collect goal. The Collect Decider, shown in Figure 10.9, realizes the collect goal by searching for a piece of trash, then picking up a piece of visible trash. When the collection is successful, the brain will stop collection, and start the Discard Decider. It is identical in form to the Collect Decider, searching for a garbage can, then throwing the trash in the can, with the