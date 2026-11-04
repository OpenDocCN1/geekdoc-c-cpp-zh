```
int i = WaitHandle.WaitAny(new[] { cancel, event1, event2 });
if (i == 0)
    // Indicates the cancellation event was signaled.
```

Although this pattern works well in practice, it adds unnecessary burden to your code. In other places where cancellation was desired (for instance, cooperatively inside a thread), yet a different mechanism was needed (for example, using a cancellation Boolean flag). In the world of TPL, all cancellation scenarios are unified using cancellation tokens.

# How the Task Scheduler Works

A thorough discussion of scheduling is beyond the scope of this discussion, but a basic understanding of task scheduling in the TPL is good to have. For more in-depth information, refer to MSDN documentation.

First, note that scheduling in the TPL is extensible because you can create your own subtype of TaskScheduler. In fact, a scheduler is fairly easy to create by implementing just three methods. Figure 30.7 shows the class diagram for the abstract base class used to implement schedulers. Italicized methods indicate abstract ones. The QueueTask method is the most essential one, allowing a new Task object to be scheduled for execution. TPL abstractions call into this method to spawn work.

![](bbox=[0.04, 0.65, 0.32, 0.82])

FIGURE 30.7 Custom TaskScheduler implementations can be provided.

We do not cover how to go about such a scheduler implementation, but we do continue to sketch how the default TPL scheduler does its work.