While you as the implementer always retain the expedient option of refining a requirement without engaging your customer, my experience indicates that this path invariably leads to rewriting the code repeatedly: once for what you thought the user wanted, once for what the user thought he wanted, and once for what the user actually wanted.

Obviously, for our case study, we only have a hypothetical end user, so we’ll simply do the refinement ourselves. We specify the following:

+   1. The CLI should accept a text command for any command defined for the calculator (those that exists in the command repository plus undo, redo, help, and exit).
+   2. The help command should display a list of all available commands and a short explanatory message.
+   3. The CLI should accept space-separated commands in the order in which they should be processed.