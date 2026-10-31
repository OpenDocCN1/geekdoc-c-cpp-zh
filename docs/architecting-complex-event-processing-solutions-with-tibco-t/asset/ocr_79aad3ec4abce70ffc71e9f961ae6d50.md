![](bbox=[0.234, 0.116, 0.765, 0.186])

*Figure 11-6: Heartbeat Recognition*

determine whether the component is still operational (Figure 11-6). For example, the component might send a heartbeat event once every three seconds. The pattern might be that there should be at least one heartbeat in a ten-second sliding window of time. The absence of heartbeats for ten seconds would then constitute a failure of the pattern.

# Summary

Complex patterns can be difficult to recognize using rules and hand-crafted state machines. For this reason the TIBCO BusinessEvents Event Stream Processor extensions provide a pattern recognition language that makes it easy to define patterns of interest. This language is used to automatically create state machines that recognize the specified patterns.

Patterns are deployed by inference agents. Events must be explicitly sent to the pattern matcher either by the preprocessor or the action part of a rule. When a match is made, the completion listener callback function is invoked; and if the pattern fails to match, the failure listener callback function is invoked.

The life cycle of a pattern is managed by code running in the inference agent. This code defines the pattern, creates instances, sets the callback functions and variable values, and deploys the pattern. The code performing these functions can be located in start-up functions, preprocessor functions, or the action part of a rule.

Patterns can be used for component liveness monitoring. If a component is expected to send a heartbeat periodically, a pattern can be used to recognize the absence of the heartbeats and conclude that the component is no longer operational.