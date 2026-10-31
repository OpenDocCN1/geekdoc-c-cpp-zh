independently begin an initiative that will eventually provide more detailed evidence of progress. This is exactly what happened in the telecommunications case study described back in Chapter 2.

# Business Process Timeliness Monitor

The Business Process Timeliness Monitor (Figure 3-9) is an extension of the Track-and-Trace pattern. State machine models can be extended so that the absence of an expected event within some period of time can be recognized. While, of course, you can apply this approach to recognizing that an overall process did not complete on time, the greatest benefit comes from recognizing that some intermediate event did not occur on time, and thus the overall process is in jeopardy of being late. The recognition can be used to trigger an action that will correct the course of the overall process and get it back on track for an on-time completion. The telecommunications case study discussed back in Chapter 2 is an example of this pattern in action.

Detecting the absence of an event requires the establishment of a service-level agreement specifying the maximum amount of time it should take for the process to complete or remain in each intermediate state. When the state machine monitoring the process is started or a particular intermediate state is entered, a timer is started. When the overall process completes, or the intermediate state is exited, the corresponding timer is stopped. However, if the timer expires before the

![](bbox=[0.1, 0.82, 0.95, 0.95])

Figure 3-9: Business Process Timeliness Monitor