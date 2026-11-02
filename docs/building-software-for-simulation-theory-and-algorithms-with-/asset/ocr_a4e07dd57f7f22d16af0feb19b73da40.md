versa) has two discrete effects: (1) the angular velocity ω changes instantaneously to and remains at zero when the tracks stick and the turn ends, and (2) the rolling resistance of the tank changes instantaneously when the tank starts and ends a turn. The Boolean variable *turning* is used to change the set of equations. The equations that model the motion of the tank are

turning = { true  if (B/2)|F_l − F_r| ≥ S_l; false  otherwise }  (2.1)

v̇ = { (1/m_t)(F_l + F_r − (B_r + B_l)v)  if turning = true; (1/m_t)(F_l + F_r − B_r v)  if turning = false }  (2.2)

ω̇ = { (1/J_t)((B/2)(F_l − F_r) − B_l ω)  if turning = true; 0  if turning = false }  (2.3)

θ̇ = ω  (2.4)

ẋ = v sin(θ)  (2.5)

ẏ = v cos(θ)  (2.6)

If turning = false then ω = 0  (2.7)

When *turning* changes from false to true, every state variable evolves from its value immediately prior to starting the turn, but using the equations designated for *turning* = true. When *turning* changes from true to false, every state variable except ω evolves from its value immediately prior to ending the turn, but using the equations designated for *turning* = false; ω changes instantaneously to zero and remains zero until the tank begins to turn again.

These differential equations describe how the tank moves in response to the propulsive force of the tracks. The track forces F_l and F_r are inputs to this model, and we can take any function of the state variables—v, ω, θ, x, and y—as output. For reasons that will soon become clear, we will use the speed with respect to the ground of the left and right treads; Figure 2.2 illustrates the desired quantities. The speed v_l of the left tread and speed v_r of the right tread are determined from the tank's linear speed v and rotational speed ω by

v_l = v + Bω/2  (2.8)

v_r = v − Bω/2  (2.9)