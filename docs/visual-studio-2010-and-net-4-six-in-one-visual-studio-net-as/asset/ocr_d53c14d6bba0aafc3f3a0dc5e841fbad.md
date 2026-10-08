# 11
Enhancements to the .NET
Workflow Framework

In the "good old days" of application programming, the imperative approach ruled the world of software development. Today, you can find a number of other paradigms as replacements (or augmentations) to the traditional imperative model. The .NET family of languages is moving toward functional programming support (not only F#, also C# and Visual Basic). The .NET run-time supports the declarative approach from the beginning — just think about decorating types, members, and parameters. There are also several tools helping developers to apply aspect-oriented programming.

From the release of .NET 3.0 in 2006, workflow-based development appeared in the palette of paradigms supported by the framework — and, of course, by Visual Studio. The Windows Workflow Foundation (WF) was the run-time library that puts workflows into the hands of developers. In contrast to the traditional imperative approach, this new paradigm manages coordination and operations differently:

+   - workflows use a declarative model of writing applications by linking together building blocks activities rather than line-by-coding code.

+   - workflows usually have a visual counterpart that allows a flowchart-like description of their logic.

+   - instead keeping units of work in memory, workflows can handle long-running work by persisting themselves to a durable storage (such as a database) when idle, and by loading them when there is work to be performed.

+   - business rules for workflows can be defined separately from other code (infrastructure code, UI code, and so on), making it easier to modify them.

Since its first release, WF went through a number of essential changes. The new version (Workflow Foundation 4.0, or simply WF 4.0) saw enormous changes relative to the previous versions — actually, it was totally redesigned and rewritten.