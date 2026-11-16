# 25.2 Task Functionality

The task as seen by the scheduler is very simple. There is an initialization function, a cleanup function, and a function to execute the task. To provide the interface for this functionality, tasks are derived from the base class Task, which has the virtual functions Start(), Stop(), and Execute().

The Start() function is called immediately after the task is added to the scheduler's task list. Its purpose is to allow the task to initialize itself before it begins any execution. It is safe (as far as the scheduler is concerned) to remove the task from the scheduler's task list in the Start() function.

The Stop() function is called immediately after the task is removed from the task list. Its purpose is to allow the task to clean itself up. Once the Stop() function is called, the scheduler no longer references the task, so it is safe (as far as the scheduler is concerned) to destroy the task anytime during or after the call to the Stop() function. It is also safe to re-add the task to the scheduler's task list from inside the Stop() function.

The Execute() function is called periodically by the scheduler according to the task's period. The timer is maintained by the scheduler. When a task is finished executing, it returns one of the following values that the scheduler uses to manage the task:

+   - ACTIVE. If this result is reported, the task is requeued for execution again according to its period. This is the normal result.
+   - AGAIN. If this result is reported, the task is requeued to run again in the next frame, regardless of its period. This result is intended to indicate that the task could not finish successfully and should be executed again as soon as possible. It could also be used to force the task to be executed every frame, but