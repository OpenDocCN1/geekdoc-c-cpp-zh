B_{k=0} = 100 - \frac{.0001}{.0002} \cdot 100 = 50 (3.3.32)

# How Long Does the Combat Last?

The combat in this scenario lasts forever because as the number of units in an army gets smaller, the units are less likely to be hit. However as time goes to infinity, the number of units in one or both armies always approaches 0. A modification to this scenario that would limit the time of combat would be to declare a winner when the number of remaining units in an army is less than a certain number or less than a percentage of the army's original size.

# Scenario 4: The Boss

In an RPG, a boss with 5,000 points fights three members of a party with a total of 1,000 points. In this system, the boss does a constant amount of damage, 90 points per turn, and each character does an amount of damage proportional to its health, 1 point per health point per turn.

In this scenario, the Blue side is fighting a single Red boss unit. The boss is destroyed when its "health" reaches 0, and the party is destroyed when its combined health reaches 0. This scenario is a combination of scenarios 1 and 2, except in this case, the number of units remaining is replaced by the number of points remaining. This scenario is also an example of how a combat system can be modeled when the rules are different for each side. The following system of equations describes this scenario.

dB = -c_r dt
dR = -c_b B dt. (3.3.33)

In this scenario, B_0 is 1,000, R_0 is 5000, c_p is 1, and c_k is 90.

# Who Wins?

Blue wins if B > 0 when R = 0, which is the case when,

R_0 < \frac{1}{2} \frac{c_b}{c_k} B_g^2. (3.3.34)

In this scenario, the party defeats the boss, but it is close.

5000 < \frac{1}{2} \cdot \frac{1}{90} \cdot 1000^2, \quad 5000 < 5556. (3.3.35)