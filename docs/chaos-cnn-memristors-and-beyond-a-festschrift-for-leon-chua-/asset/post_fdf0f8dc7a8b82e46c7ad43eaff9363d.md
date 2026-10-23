
# CHAPTER 6

# FROM RADIO-AMATEURS’ ELECTRONICS
TO TOROIDAL CHAOS

OTTO E. RÖSSLER

*Division of Theoretical Chemistry, University of Tübingen,*
*D-72076 Tübingen, Germany*

CHRISTOPHE LETELLIER

*CORIA UMR 6614 — Rouen University,*
*F-76801 Saint-Etienne du Rouvray cedex France*

On the occasion of Leon Chuas 75th birthday, we offer some new simulations and musings on toroidal chaos.

+   1. Introduction .................................................. 83
+   2. The van der Pol Equation ..................................... 84
+   3. A Related Prototype ............................................ 85
+   4. Conclusions ...................................................... 87
+   References .......................................................... 88

## 1. Introduction

Chaos is addictive. Its essence was recently rediscovered by the famous artist Olafur Eliasson who suspended a running desk-top fan from a long rope. The public was fascinated by the absolute unpredictability of the gadgets elegant motions.

One of the major — and perhaps most natural — roads into understanding chaos, as locally everywhere parallel hairlines, is the design of electronic systems while registering their activity on an oscilloscope. The electronic analog computer is itself an example. When you simulate a fast 2-variable triangle-shaped limit cycle on such a machine, then near the single sharp corner, the light point will tend to follow a highly irregular course that is different (shorter or longer) at every turn. We saw this in

Tubingen jointly with Heinz Karfunkel in 1971 without realizing what it means (that there is a hidden third variable involved and that the “noise” we saw is not at all exogenous).

Chemical and biochemical (biological) systems do themselves consist of coupled smoothly varying variables. Life itself is an example. To model it electronically is in principle impossible because in nature, the state variables (concentrations) are at the same time the hardware. There is no big computer behind on which these variables are “simulated.”

Radio amateurs have a much easier life. They can trust their hardware and bring it to producing beautiful sounds and music, and this at the speed of light across continents. Later, even pictures followed. Electrical engineering is the real home of

chaos theory. The latter was invented by Poincaré in the context of celestial mechanics, but he already used an electronic system in his head, one feels.

The tool kit of astronomical interactions is somewhat less accessible mentally. The optimistic hope that eventually, very few controllable elements — capacitors, resistors, amplifiers — will suffice to get a beautiful nontrivial behavior out of their interaction was slow in coming. The fact that chemical soups and brains follow the same laws becomes fully comprehensible only to an electronics engineer.

Leon Chua is the person at the center. He did not “come from astronomy” like Poincaré, or from brain theory or “chemical soups” but plunged into the central heaven of electronic building elements directly. This made him stronger than other nonlinear scientists who thought of these elements only as analog tools to better understand their own objects of investigation. That these elements constitute heaven itself — the heaven of dynamics — no one saw more clearly than him.

His uniquely beautiful, large-format scientific journal,ᵃ with its primacy of color and simple clear drawings, reflects the powerful esthetic root of his chaos kingdom. No one else encouraged so many creative pictorial minds into taking themselves and their work seriously. No one forced more beautiful “double scrolls” into trajectories laid out in a clarity that removed any fear of the mind that this complexity could never be grasped in full. Hun Tun means “chaos” in Chinese mythology, but also the name of the person who cared most about all, without even having to open his eyes and ears and nose and mouth, because everything was already absolutely clear in his — the first emperor’s — mind.

It is a privilege that we are allowed to offer some quasiperiodic — or no longer quasiperiodic but chaotic — motions on the occasion of Leon’s birthday in this book that is an expression of his mind. The fact that there is a connection to human physiology — and breathing — in some of the simulations makes the connection to Hun Tun even more palpable.

## 2. The van der Pol Equation

The oldest example of complicated behavior found in an unconstrained (non-conservative) dynamical system is that found in the periodically forced van

der Pol oscillator [1]. Cartwright & Littlewood’s results were based on painstaking analytical arguments [2]. Is it, at the same time, also possible to understand their observations in terms of a so-called reinjection principle as we will detail below? The answer is yes. One can even say that Cartwright and Littlewood were the first to make use of the reinjection principle in order to find nontrivial behavior in a simple dynamical system.

In 1938, the Department of Scientific and Industrial Research issued a memorandum to the London Mathematical Society appealing for the assistance of pure mathematicians in solving the type of equations occurring in radio work, laying emphasis on the need to know how the frequencies of the periodic solutions varied with the parameters of the equation (see Cartwright [3] for a brief history of the earliest mathematical studies of this equation). At about the same time the van der Pol equation [4]

```
¨v − ε(1 − v²)˙v + v = 0. (1)
```

arose as a model of the oscillation of the potential in the cavity magnetron discovered at the end of 1939, cf. [5]. Such a device was used to produce the high-frequency oscillations required to develop a powerful radar. By then, the 1934 paper by van der Pol [6] already had a strong impact on radio-engineers [3, 7, 8]. Electronic experiments showed that the driven van der Pol equation has a periodic solution with a period which can be many times a high multiple of the period of the forcing term. Moreover, for some values of the amplitude of the forcing term, the driven van der Pol equation possesses two periodic solutions of different periods. Cartwright and Littlewood showed that the existence of two periodic solutions implies the existence of “bad” solutions which was “very difficult to rule out” [1]. These non-periodic orbits described as a “discontinuously recurrent” motion would be called “chaotic” today. Later Norman Levinson (1912–1995) — who was Leon Chua’s professor at MIT — used a piecewise linear form of the driven van der Pol equation to show the aperiodic character of some of its solutions [9]. It appears that Levinson’s analysis led to Steven Smale’s introduction of the Horseshoe map [10], a very important concept in chaos theory as pointed out in the first paper on chaos by the first author [11]. Following Levinson’s approach,

![](img/039e7d3c23390584a66737067db8b75b_97_0.png)

Fig. 1. Quasi-periodic regime in Eq. (6) obtained by numerical simulation. Parameters: a = 0.2, ω = π and μ = 1.8. Time step: δt = 0.001 s.

Mark Levi investigated rotation numbers of periodic solutions to the driven van der Pol equation [12], thus enabling the topological analysis which was later applied to chaotic attractors.

Using Liénard’s [13] familiar nonlinear transformation (cf. [14]), the periodically forced van der Pol oscillator

```
ẍ − μ ẋ (1 − x²) + x = a cos bt,
```

can be written in the form

```
ε ẋ = x − 1/3 x³ − y
ẏ = x + a cos bt,
```

where ε = 1/μ. Cartwright and Littlewood considered Eq. (2) under the condition of very small values of ε. Later it was shown that such an equation can lead to chaotic behaviors [15].

## 3. A Related Prototype

The matter discussed in this section was mostly extracted from a textbook the first author wrote in the early 1980’s but which was never published. With the help of Reimara Rössler, we found again the first draft of this textbook and we are preparing a publication of it, more than thirty years after its writing. As we will show in this chapter, Otto’s views remain original even when they are considered after a so long time (says Christophe). In what follows, we preserved the content but not the writing.

The purpose was to provide a dynamical system producing a toroidal chaos governed by a mechanism simpler than the process underlying the

van der Pol equation. Let us start from the two-dimensional system

```
ẋ = x/r f(x) + ω y
ẏ = − ω x + y/r f(x)
```

in Cartesian coordinates which may be rewritten as the following two-dimensional system

```
ṙ = 1/2 (2x dx + 2y dy)/√(x²+y²) = (x²/r + y²/r)·f(r) + (ωxy − ωxy)/r = r·f(r)
θ̇ = 1.
```

in polar coordinates. This system defines the evolution of the radius which is associated with a constant angular velocity. Using f(r) = 1, system (3) can be rewritten as the two-variable autonomous system

```
ẋ = x/r + ω y
ẏ = − ω x + y/r,
```

which is an expansive system with a single fixed point which is an unstable focus. To prevent this system from diverging to infinity, a second condition is added to bound the radius. One of the simplest ways is to use, for example,

```
(r − 1) mod (1 + a cos π ω t).
```
