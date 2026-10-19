![](bbox=[0.12, 0.08, 0.22, 0.18])

None of these terms are magical or sacred. Learn the ideas rather than the terminology. It’s nearly always possible to write routines with functional cohesion, so focus your attention on functional cohesion for maximum benefit.

# 7.3 Good Routine Names

Cross-Reference For details on naming variables, see Chapter 11, "The Power of Variable Names."

A good name for a routine clearly describes everything the routine does. Here are guidelines for creating effective routine names:

# Describe everything the routine does

In the routine’s name, describe all the outputs and side effects. If a routine computes report totals and opens an output file, ComputeReportTotals() is not an adequate name for the routine. ComputeReportTotalsAndOpenOutputFile() is an adequate name but is too long and silly. If you have routines with side effects, you’ll have many long, silly names. The cure is not to use less-descriptive routine names; the cure is to program so that you cause things to happen directly rather than with side effects.

# Avoid meaningless, vague, or wishy-washy verbs

Some verbs are elastic, stretched to cover just about any meaning. Routine names like HandleCalculation(), PerformServices(), OutputUser(), ProcessInput(), and DealWithOutput() don’t tell you what the routines do. At the most, these names tell you that the routines have something to do with calculations, services, users, input, and output. The exception would be when the verb “handle” was used in the specific technical sense of handling an event.

![](bbox=[0.12, 0.54, 0.22, 0.64])

Sometimes the only problem with a routine is that its name is wishy-washy; the routine itself might actually be well designed. If HandleOutput() is replaced with FormatAndPrintOutput(), you have a pretty good idea of what the routine does.

In other cases, the verb is vague because the operations performed by the routine are vague. The routine suffers from a weakness of purpose, and the weak name is a symptom. If that’s the case, the best solution is to restructure the routine and any related routines so that they all have stronger purposes and stronger names that accurately describe them.

![](bbox=[0.12, 0.74, 0.22, 0.84])

# Don’t differentiate routine names solely by number

One developer wrote all his code in one big function. Then he took every 15 lines and created functions named Part1, Part2, and so on. After that, he created one high-level function that called each part. This method of creating and naming routines is especially egregious (and rare, I hope). But programmers sometimes use numbers to differentiate routines with names like OutputUser, OutputUser1, and OutputUser2. The numerals at the ends of these names provide no indication of the different abstractions the routines represent, and the routines are thus poorly named.

# Make names of routines as long as necessary

Research shows that the optimum average length for a variable name is 9 to 15 characters. Routines tend to be more com-