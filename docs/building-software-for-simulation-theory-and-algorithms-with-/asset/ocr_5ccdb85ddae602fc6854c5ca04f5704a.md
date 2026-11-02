The time-shifting operator τ moves the starting and ending times of the trajectory by equal distances. For example, applying τ with the argument 1 to a trajectory z_b[0,2] gives τ1[z_b[0,2]] = z_b[1,3]. The new trajectory z_a is the same as z_b but is defined over a different interval; in this example, z_a(0)=z_b(1), z_a(1)=z_b(2), and z_a(2)=z_b(3). The definition of τ is a generalization of this example:

τ(h, z_a < t1, t2 >) = z_b < t1 + h, t2 + h >   such that   z_a(t) = z_b(t + h)   (3.2)

For brevity, the • operator combines - and τ to concatenate two trajectories z_a[t1, t2] and z_b[t3, t4] that do not necessarily begin and end at the same time. This operation is very common, and the separate notation for shifting and concatenation quickly becomes tiresome. The • operator is defined by

z_a[t1, t2] • z_b[t3, t4] = z_a[t1, t2] • τ(t2 − t3, z_b[t3, t4])   (3.3)

Shifting z_b by t2 − t3 translates its domains from [t3, t4] to [t3 + (t2 − t3), t4 + (t2 − t3)] = [t2, t4 + t2 − t3], giving the two trajectories a common time at which to join.

# 3.1.2 The State Transition and Output Function

The total state transition function Δ moves the system from a state s to a state s′ in response to the input trajectory x[t0, t0]:

s′ = Δ(s, x[t0, t0])   (3.4)

Not all such functions are total state transition functions; Δ must satisfy
Δ(s, x1 • x2) = Δ(Δ(s, x1), x2)   (3.5)
Δ(s, x[t, t]) = s   (3.6)

Equation 3.6 requires that the system not change its state over an empty interval of time. Equation 3.5 is the semigroup property. It states that feeding the system a series of input trajectories x1, x2, …, xn has the same effect as feeding it the single trajectory x1 • x2 • … • xn. It is very common in practice to also require
Δ(s, τ(h, x)) = Δ(s, x)   (3.7)

Equation 3.7 states that the response of the system to an input does not depend on the time at which it is applied. A system that satisfies this property is called time-invariant.

These three properties are mathematical expressions of everyday experience. Of central importance is the semigroup property. To illustrate it, imagine an experiment with a lock and key. If the lock is closed, in a state locked, and the key k is turned, then