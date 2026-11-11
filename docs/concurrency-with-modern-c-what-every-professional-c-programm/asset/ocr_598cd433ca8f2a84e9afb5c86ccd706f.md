# 9. Synchronization Patterns

![](bbox=[0.337, 0.24, 0.686, 0.503])

The main concern when you deal with concurrency is shared, mutable state or as [Tony Van Eerd](#)¹ put it in his CppCon 2014 talk “Lock-free by Example”: “Forget what you learned in Kindergarten (ie stop Sharing)”.

**Mutable?**

| **Shared?** | **No** | **Yes** |
|---|---|---|
| **No** | OK | OK |
| **Yes** | OK | **Data Race** |

A necessary condition for a [data race](#) is a mutable, shared state. If you handle sharing or mutation, no data race can happen. This is exactly the focus of the next two sections: [Dealing with Sharing](#) and [Dealing with Mutation](#).

¹https://github.com/tvan eerd