# Figure 11.3 Primary Handler Execution Order Determination

Begin with all applicable primary handlers for the message sent to the instance.

Are there any uncalled around handlers?

Invoke the most specific uncalled around handler.

Does the executing handler call-next-handler?

Allow the currently executing primary to finish and return a value. Treat the handler as uncalled.

Are there primary handlers still executing?

Continue executing the most recent primary handler invoked.

The return value from the primary is the return value of the last primary handler executed.