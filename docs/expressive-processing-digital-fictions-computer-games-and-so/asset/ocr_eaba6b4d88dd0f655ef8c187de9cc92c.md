# F.E.A.R. Plans

F.E.A.R. (Hubbard, Hewett, Gramlich, et al. 2005) is a first-person shooter designed for an action movie-style experience (figure 6.1). The player is a new member of an elite team—the First Encounter Assault Recon unit—assigned to deal with unusual threats. Like NPCs in NOLF2, the AI enemies in F.E.A.R. have goals that compete for activation, such as KillEnemy, Dodge, and Goto. But rather than each goal having an embedded FSM, each goal can be reached by sequencing actions. As in Strips, these actions have preconditions and effects, and the effects satisfy goals (e.g., AttackFromCover and AttackMelee both satisfy the KillEnemy goal).

This may seem like a simple change, but it has a powerful

![](bbox=[0.18, 0.488, 0.82, 0.858])

Figure 6.1. A.I. enemies in F.E.A.R. work in squads to take cover, lay suppression fire, blind fire, dive through windows to safety, flush out the player with grenades, and otherwise create an “over the top” experience for players.