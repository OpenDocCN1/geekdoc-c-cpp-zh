# Verify: Investigating done

Work items in the Investigating sub-column are considered done when:

+   - Automated acceptance tests pass.
+   - Functional testing does not uncover defects.
+   - Functional testing matches the specification of work.
+   - Existing functionality is intact.

# Deliver: Deploying done

Work items in the Deploying sub-column are considered done when:

+   - Features are deployed across all targets.
+   - KPIs are measured and indicate an increase in value.
+   - The features have been in use for at least 24 hours.
+   - No errors or warnings have been reported.

As you can see, these items are rigorous but also fairly generic. As part of the Analyze: Specifying phase, it is expected that further items would be generated that are tailored to each piece of work.

# Event-driven ceremonies

The main event that can cause the scheduling of a meeting is the emptying of a column on the Kan-ban board. If an in-progress column becomes empty, the team will pull across the next ticket from the column immediately to the left of the empty column. Although the words meeting and ceremony imply a certain level of pomp and circumstance (and boredom), these meetings need not be formal.

> **Tip** Of course, the threshold for holding a meeting such as this does not have to be an empty column. Instead, the threshold could be set at one or two tickets remaining. This prevents the team from completely running out of work that can be progressed, in favor of buffering to allow some work to continue in parallel.

Meetings of this kind can be held at the Kanban board, rather than in a meeting room, saving on resources and setup time. These meetings also do not have to include everyone who is part of the team. Only invite and include those team members to whom the meeting is relevant, to avoid forcing a context switch on someone who is busily—and happily—making progress on real work.

If the column that is empty is, for example, the Wait column, the team can assemble and create new tickets for the backlog based on the product roadmap. Otherwise, if the empty column is the Implement column, the highest priority ticket from the Analyze column can be pulled into the Coding