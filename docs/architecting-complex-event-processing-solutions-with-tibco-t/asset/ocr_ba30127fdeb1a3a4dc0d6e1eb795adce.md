![](bbox=[0.438, 0.116, 0.552, 0.55])

**Figure 11-1:** *State Machine Pattern Recognizer*

more complex, it becomes increasingly difficult and tedious to craft the state machine—and verify that the pattern that it recognizes is the pattern you are trying to recognize.

Another dimension of complexity is the introduction of time constraints. Consider this variation:

+   - Three red balls within five minutes
+   - Followed by two blue balls within 30 seconds
+   - Followed by a yellow ball within an hour

Again, you could craft a state machine to recognize this pattern (Figure 11-2), but the increasing complexity of doing so is beginning to become apparent.

From a recognition perspective, the state machine is the right tool to use. The problem lies in the crafting of the machine. The traditional computer science answer to this problem is to define a pattern language, an accompanying compiler that automatically generates the