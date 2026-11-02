(Note: There are two values of y for each x and z because the hull is symmetric from starboard to port.)

The cross-sectional area at a point x is called the "section" in nautical parlance. To compute it, let z go from 0 to −T in n increments, each of size T/n. For each value of z, compute the value for y. Then sum the areas of trapezoidal strips. At right are the strips where n = 4.

Write a program that reads in values for B, L, T, x, and n and then prints out the cross-sectional area at x.

![](bbox=[0.78, 0.1, 0.92, 0.32])

# Engineering P4.25

Radioactive decay of radioactive materials can be modeled by the equation A = A₀·2^(-t/(log₂ b)), where A is the amount of the material at time t, A₀ is the amount at time 0, and b is the half-life.

Technetium-99 is a radioisotope that is used in imaging of the brain. It has a half-life of 6 hours.

Your program should display the relative amount A/A₀ in a patient body every hour for 24 hours after receiving a dose.

![](bbox=[0.78, 0.35, 0.92, 0.55])

# Engineering P4.26

![](bbox=[0.08, 0.65, 0.22, 0.88])

The photo at left shows an electric device called a "transformer". Transformers are often constructed by wrapping coils of wire around a ferrite core. The figure below illustrates a situation that occurs in various audio devices such as cell phones and music players. In this circuit, a transformer is used to connect a speaker to the output of an audio amplifier.

![](bbox=[0.38, 0.72, 0.78, 0.88])

The symbol used to represent the transformer is intended to suggest two coils of wire. The parameter n of the transformer is called the "turns ratio" of the transformer. (The number of times that a wire is wrapped around the core to form a coil is called the number of turns in the coil. The turns ratio is literally the ratio of the number of turns in the two coils of wire.)

When designing the circuit, we are concerned primarily with the value of the power delivered to the speakers—that power causes the speakers to produce the sounds we want to hear. Suppose we were to connect the speakers directly to the amplifier without using the transformer. Some fraction of the power available from the amplifier would get to the speakers. The rest of the available power would be lost in the amplifier itself. The transformer is added to the circuit to increase the fraction of the amplifier power that is delivered to the speakers.

The power, Pₛ, delivered to the speakers is calculated using the formula

Pₛ = Rₛ ( n Vₛ / (n² R₀ + Rₛ) )²