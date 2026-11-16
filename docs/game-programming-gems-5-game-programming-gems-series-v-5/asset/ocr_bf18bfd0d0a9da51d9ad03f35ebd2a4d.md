2. In addition to its somewhat limited scope, classical planning makes some strong assumptions. It assumes that a world behaves as described and that actions will succeed. This is clearly not the case because of randomness, because we abstract the gaming world, and above all, because of the human player. This is why we must replan periodically to reflect the changing world and the failure of earlier plans.

3. Classical planning is not adversarial. It does not take into account that someone may be working to thwart it. However, very few game AI address this problem with more than some basic heuristics and rules. Most of these basic strategies can be reflected as goal selection, with a top-level strategy module picking overall goals that the planner figures out how to accomplish, executing the low-level behavior by instantiating FSMs.

4. The symbolic approach is also not good for making value judgments, like the relative strengths of two creatures. Existing heuristic functions should be used in this case and a predicate used in the planner that calls the heuristic and applies a threshold (e.g., canKill(Creature, Creature) predicate might check that one unit's strength is double that of the other unit).

# Integration with the Game Engine

In addition to these concerns, it is important to consider how to integrate the planner to the game engine. This depends at least partially on how reusable you want the planning code to be, but we will address a few key points.

We first consider the initial state for planning, which must be obtained by the game engine. Subsequent states generated during planning must be copies of this initial state; we don't want to change variables in the game engine directly while planning. There are a few strategies for getting the facts for the initial state.

In a "pull" strategy, the planner requests information from the game engine to construct states. The planner examines all the predicates when we are about to plan, determines their values from the game engine, and stores them in the initial state. However, the expense of repeated copy operations here is nontrivial, and it is possible that a lot of useless state information will be stored

One solution to this is to use a read-on-demand approach. In this case, the value is only read when the predicate is evaluated. Another approach is to use a "push" model, where the game engine sends changes to the planner as they occur. This is a good strategy if planning occurs frequently. With infrequent planning, a lot of update operations will be performed needlessly.

It is also necessary to associate planning objects and actions with the corresponding data structures and functions in the game engine. This mapping is fairly straightforward but should be thought about carefully during design. In addition, different modules should be able to interact with the planner. We built a custom planning language to set up the planning domain (types, objects, predicates, operators) but used Lua, a popular scripting language, to drive the initial state and goals and bind objects