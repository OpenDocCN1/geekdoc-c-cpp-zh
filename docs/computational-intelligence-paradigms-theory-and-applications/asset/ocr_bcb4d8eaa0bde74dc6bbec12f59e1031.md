# *Creation of New Generations*

| | |
|---|---|
| genpop | Creates the initial generation for the GPLAB algorithm |
| generation | Creates a new generation for the GPLAB algorithm |
| pickoperator | Draws a genetic operator to apply in the GPLAB algorithm |
| applyoperator | Apply a genetic operator to create new GPLAB individuals |
| pickparents | Picks parents from pool for a GPLAB genetic operator |
| applysurvival | Choose new generation of individuals for GPLAB algorithm |
| updatestate | Updates the GPLAB algorithm state variables |
| stopcondition | Checks which stop condition the GPLAB algorithm verifies |

# *Creation of New Individuals*

| | |
|---|---|
| initpop | Creates a new population for the GPLAB algorithm |
| fullinit | Creates a new GPLAB population with the full method |
| growinit | Creates a new GPLAB population with the grow method |
| rampedinit | Creates a new GPLAB population with ramped half-and-half method |
| newind | Creates a new individual for the GPLAB algorithm |
| maketree | Creates representation tree for the GPLAB algorithm |

# *Filtering of New Individuals*

| | |
|---|---|
| validateinds | Applies validation procedures to new GPLAB individuals |
| strictdepth | Applies strict depth filters to a new GPLAB individual |
| strictnodes | Applies strict size filters to a new GPLAB individual |
| dyndepth | Applies dynamic depth filters to a new GPLAB individual |
| dynnodes | Applies dynamic size filters to a new GPLAB individual |
| heavydyndepth | Applies heavy dynamic depth filters to a new GPLAB individual |
| heavydynnodes | Applies heavy dynamic size filters to a new GPLAB individual |