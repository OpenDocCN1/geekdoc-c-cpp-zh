
0   rule-2: f-1
For a total of 2 activations.
CLIPS> (agenda RECOVERY)
0   rule-3: f-0, f-3
0   rule-3: f-0, f-1
0   rule-3: f-2, f-3
0   rule-3: f-2, f-1
For a total of 4 activations.
CLIPS> (agenda *)
MAIN:
DETECTION:
0   rule-1: f-2
0   rule-1: f-0
ISOLATION:
0   rule-2: f-3
0   rule-2: f-1
RECOVERY:
0   rule-3: f-0, f-3
0   rule-3: f-0, f-1
0   rule-3: f-2, f-3
0   rule-3: f-2, f-1
For a total of 8 activations.
CLIPS>

## The Focus Command

Now that there are rules on three separate agendas, what happens when a run command is issued?

```
CLIPS> (unwatch all)
CLIPS> (watch rules)
CLIPS> (run)
CLIPS>
```

No rules fire! In addition to the current module, which CLIPS uses to determine where new constructs are added and which constructs are used or affected by commands, CLIPS also maintains a current focus, which determines which agenda the run command uses during execution. The reset and clear commands automatically set the current focus to the MAIN module. The current focus does not change when the current module is changed. Thus, in the current example, when the run command is issued, the agenda associated with the MAIN module is used to select rules to execute. Since this agenda is empty, no rules are fired.

The focus command is used to change the current focus. Its syntax is:

```
(focus <module-name>+)
```

In the simple case in which only one module name is specified, the current focus is set to the specified module. By setting the current focus to the DETECTION module and then issuing a run command, the rules on the DETECTION module's agenda will be fired:

```
CLIPS> (focus DETECTION)
TRUE
CLIPS> (run)
FIRE    1 rule-1: f-2
FIRE    2 rule-1: f-0
CLIPS>
```

Using the focus command not only changes the current focus but also recalls the previous value of the current focus. The current focus is really the top value of a stack data structure called the focus stack. Whenever the focus command changes the current focus, it is actually pushing the new current focus onto the top of the focus stack, displacing the previous current focuses. As rules execute, when the agenda of the current focus becomes empty, the current focus is popped (removed) from the focus stack and the next module becomes the current focus. Rules are then executed from the agenda of the new current focus until a new module is focused on or until there are no rules left on the agenda of the current focus. Rules will continue to execute until there are no modules left on the focus stack or the halt command is issued.

Continuing the current example, focusing first on the ISOLATION module and then on the RECOVERY module will cause all of the rules on the RECOVERY module's agenda to fire, which will be followed by the firing of rules on the ISOLATION module's agenda. The list-focus-stack command (which takes no arguments) is used to display the modules on the focus stack:

```
CLIPS> (focus ISOLATION)
TRUE
CLIPS> (focus RECOVERY)
TRUE
CLIPS> (list-focus-stack)
RECOVERY
ISOLATION
CLIPS> (run)
FIRE    1 rule-3: f-1, f-4
FIRE    2 rule-3: f-1, f-2
FIRE    3 rule-3: f-3, f-4
FIRE    4 rule-3: f-3, f-2
FIRE    5 rule-2: f-4
FIRE    6 rule-2: f-2
CLIPS> (list-focus-stack)
CLIPS>
```

Using two focus commands to push the ISOLATION and RECOVERY modules causes the RECOVERY rules to execute before the ISOLATION rules. However, when more than one module is specified in a single focus command, the modules are pushed onto the focus stack from right to left. For example:

```
CLIPS> (focus ISOLATION RECOVERY)
TRUE
CLIPS> (list-focus-stack)
ISOLATION
RECOVERY
CLIPS> (focus ISOLATION)
TRUE
CLIPS> (list-focus-stack)
ISOLATION
RECOVERY
CLIPS> (focus RECOVERY)
TRUE
CLIPS> (list-focus-stack)
RECOVERY
ISOLATION
RECOVERY
CLIPS>
```

Notice that the same module can be on the focus stack more than once, but focusing on a module that is already the current focus has no effect.

## Manipulating and Examining the Focus Stack

CLIPS provides several commands and functions for manipulating the current focus and the focus stack. The clear-focus-stack command removes all modules from the focus stack. The get-focus function returns the module name of the current focus or the symbol FALSE if the focus stack is empty. The pop-focus function removes the current focus from the focus stack (and returns the module name or the symbol FALSE if the focus stack is empty). The get-focus-stack function returns a multifield value containing the modules on the focus stack.

```
CLIPS> (get-focus-stack)
(RECOVERY ISOLATION RECOVERY)
CLIPS> (get-focus)
RECOVERY
CLIPS> (pop-focus)
RECOVERY
CLIPS> (clear-focus-stack)
CLIPS> (get-focus-stack)
()
CLIPS> (get-focus)
FALSE
CLIPS> (pop-focus)
FALSE
CLIPS>
```

The watch command can be used to see changes to the focus stack using the keyword focus as the command's argument:

```
CLIPS> (watch focus)
CLIPS> (focus DETECTION ISOLATION RECOVERY)
==> Focus RECOVERY
==> Focus ISOLATION from RECOVERY
==> Focus DETECTION from ISOLATION
TRUE
CLIPS> (run)
==> Focus DETECTION to ISOLATION
==> Focus ISOLATION to RECOVERY
==> Focus RECOVERY
CLIPS>
```

In the event that the run command is given and the focus stack is empty, the MAIN module is automatically pushed onto the focus stack. This feature is provided mainly as a convenience for the case in which new activations are added after the program has ended because there are no modules left on the focus stack. For example,

```
CLIPS> (clear)
CLIPS> (watch focus)
CLIPS> (watch rules)
CLIPS> (defrule example-1 =>)
CLIPS> (reset)
==> Focus MAIN
==> Focus MAIN
CLIPS> (run)
FIRE 1 example-1: f-0
<= Focus MAIN
CLIPS> (defrule example-2 =>)
CLIPS> (agenda)
0 example-2: f-0
For a total of 1 activation.
CLIPS> (list-focus-stack)
CLIPS>
```

The rule example-2 is on the agenda, but there are no modules on the focus stack. Issuing a run command, however, places the MAIN module on the focus stack, so rule example-2 is able to fire anyway:

```
CLIPS> (run)
==> Focus MAIN
FIRE 1 example-2: f-0
==> Focus MAIN
CLIPS>
```

## The Return Command

One of the drawbacks of controlling the flow of execution by using control facts to represent phases, as discussed in Section 9.4, is that it is not possible to fire some activations in a particular phase, exit that phase, and then return later to the phase and execute the remaining activations on the agenda. This occurs because once the control fact representing the phase is retracted, all of the activations from that phase are removed from the agenda. When the control fact is later reasserted, all of the previous activations for that phase will be reactivated, not just those that didn't fire (this, of course, is assuming that only the control fact and not any other facts were asserted or retracted).

If modules are used to control the flow of execution, it is possible to stop executing the activations from a specific module's agenda prematurely (that is, before the module's agenda is empty). The return command can be used to immediately terminate the execution of a rule's RHS and remove the current focus from the focus stack (thus returning control of execution to the next module on the focus stack). When used from the RHS of a rule, the return command should be passed no arguments (the return command can also used by the procedural programming constructs provided with CLIPS). The following example illustrates the use of the return command:

```
CLIPS> (clear)
CLIPS>
(defmodule MAIN
   (export deftemplate initial-fact))
CLIPS>
(defmodule DETECTION
   (import MAIN deftemplate initial-fact))
CLIPS>
(defrule MAIN::start
   =>
   (focus DETECTION))
CLIPS>
(defrule DETECTION::example-1
   =>
   (return)
   (printout t "No printout!" crlf))
CLIPS>
(defrule DETECTION::example-2
   =>
   (return)
   (printout t "No printout!" crlf))
CLIPS> (watch rules)
CLIPS> (watch focus)
CLIPS> (reset)
==> Focus MAIN
CLIPS>
