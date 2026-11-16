21. I am using the words *game fictions* generally, to refer to fictions within games. In *More Than a Game*, Barry Atkins uses the words *game fiction* to refer to those games he sees as 'having a central narrative impetus, that developed story over time ...'

Notes continued at end of this chapter.

is defined as a “state” (e.g., patrol, attack, or retreat) with particular rules for transitioning from the current state to other states. For example, an NPC could be designed to move through a patrol animation (a patrol state) until an enemy is noticed (transition to an attack state) and continue attacking until the enemy is defeated (transition to patrol state) or the NPC’s health is below a defined threshold (transition to a retreat state). There might be no rule allowing for direct transition from patrol to retreat—which would make sense generally, but not if the NPC is already badly wounded from previous combat.

As with quest flags and dialogue trees, FSMs are simple to explain, easy to implement in software, low in their use of computational resources, and an authoring nightmare over a certain level of complexity. Luckily, they're a perfect fit for the exceedingly simple behavior of sand demons, who attack on sight and never retreat, as found in *PoP*.

The end result, for *PoP*, is an experience elegantly designed to compensate for the crippling limitations of the processes used to represent story and character in today's computer games. And this opens up the next question.

# The Game Fiction Dilemma

Authors of game fictions have worked hard—through conventions such as the quest-tracking journal and tree-driven conversations presented as menus—to avoid the *Eliza* effect. Rather than conceal the operations of their processes, game fiction authors seek to expose them to the audience. But, despite this, game fiction still face a dilemma remarkably similar to that outlined at the end of the previous chapter.²

Both *KatOR* and *PoP* take advantage of what games do