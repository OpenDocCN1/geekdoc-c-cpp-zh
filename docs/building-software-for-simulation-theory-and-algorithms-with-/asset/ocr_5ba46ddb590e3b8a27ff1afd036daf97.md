**TABLE 2.1** Value of Parameters Used in the Tank’s Equations of Motion

| Parameter | Value | Description |
| --- | --- | --- |
| m_t | 0.8 kg | Mass of the tank |
| J_t | 5 × 10^-4 kg·m^2 | Angular mass of the tank |
| B | 0.1 m | Width of the tank from track to track |
| B_r | 1.0 N·s/m | Mechanical resistance of the tracks to rolling forward |
| B_t | 14.0 N·s/m | Mechanical resistance of the tracks to sliding forward |
| B_l | 0.7 N·m·s/rad | Mechanical resistance of the tracks to turning |
| S_f | 0.3 N·m | Lateral friction of the tracks |

# ### 2.2.1 Equations of Motion

The model of the tank’s motion is adapted from Anh Tuan Le’s PhD dissertation [74]. The model’s parameters are listed in Table 2.1, and the coordinate system and forces acting on the tank are illustrated in Figure 2.2. The model assumes that the tank is driven on a hard, flat surface and that the tracks do not slip. The position of the tank is given by its x and y coordinates. The heading θ of the tank is measured with respect to the x axis of the coordinate system and the tank moves in this direction with a speed v.

The left track pushes the tank forward with a force F_l; the right track, with a force F_r; and B_r is the mechanical resistance of the tracks to rolling. The tank uses skid steering; to turn, the motors must collectively create enough torque to cause the tracks to slide sideways. This requires overcoming the sticking force S_f. When sufficient torque is created, the vehicle begins to turn. As it turns, some of the propulsive force is expended to drag the tracks laterally; this is modeled by an additional resistance B_l to its turning motion and B_t to its rolling motion.

The tank’s motion is described by two sets of equations, one for when the tank is turning and one for when it is not. The switch from turning to not turning (and vice

![](bbox=[0.12, 0.72, 0.89, 0.92])