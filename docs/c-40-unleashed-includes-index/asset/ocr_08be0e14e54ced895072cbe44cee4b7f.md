![](bbox=[0.07, 0.12, 0.55, 0.58])

FIGURE 25.37 Type forwarders in System.Core.

# WHEN COMPATIBILITY IS A CORE REQUIREMENT

As usual, the use of a feature gives rise to a balancing act with architectural purity on one side, compatibility on another side, and the burden of carrying out the fix to be considered too. Type forwarders are no different and provide some kind of last-resort fix when you have strong reasons to move a type and absolutely have to keep existing assemblies work (without recompiling them). So if you’re working on something totally new with no compatibility story to take care of, there’s no reason to complicate matters by using type forwarders.

# Reflection Flashback

When we discussed reflection in Chapter 21, “Reflection,” we focused on two main concepts of the technology: discovery of types and members and invocation or interaction with those (for example, to dynamically invoke a method). While we focused on types and their members, we mostly omitted a discussion of reflection on assemblies. Although you saw how to find types that belong to an assembly (a discovery feature), we didn’t pay much attention to reflection operations targeting assemblies.

Earlier in this chapter, you saw one such assembly-level operation, which had to do with the loading of embedded resources. But there’s more. In fact, we can load assemblies through the reflection APIs, too. So far, you’ve seen that assemblies get loaded by the runtime when a type or member is encountered that lives in an assembly that hasn’t yet been loaded. In certain scenarios, such as add-ins, referenced assemblies are no longer a known fact at compile time. Based on application configuration settings, we need to discover and load assemblies dynamically.