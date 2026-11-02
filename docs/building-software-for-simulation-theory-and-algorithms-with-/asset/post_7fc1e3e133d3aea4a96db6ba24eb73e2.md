
```
77  // Save the final image to a file
78  listener->saveImage();
79  // Clean up and exit
80  delete sim; delete listener; delete automaton;
81  return 0;
82  }
```

Wolfram [147] has cataloged all of the one-dimensional cellular automata. Our *BinaryCell* class uses Wolfram's encoding of the transition rule, but produces images with time beginning at the bottom rather than at the top as is done in Wolfram's catalog. Figure 3.11 shows Wolfram's rule 188, which produces diagonal stripes. Figure 3.12 is one of the more vibrant cellular automata that appears in the catalog. The two images in Figure 3.12 appear almost identical, but small differences appear after generation 30, when the cells at the edge first turn black. In both figures, the image on the left is produced by the cellular automaton when wrapped into a ring and the image on the right is produced when the ends are left dangling. The cellular automata in both cases have 60 cells and are simulated for 60 generations.

### 3.6 SUMMARY

This chapter introduced the fundamental concept of a dynamic system, a modeling framework derived from that concept, and a software architecture that satisfies the requirements established in Chapter 1. With very little embellishment, this foundation will support more complicated, but more useful, models of discrete-event and hybrid systems. A solid grasp of the basic concepts, as they are manifest in this relatively tame setting, is therefore crucial to what follows.

![](img/df6085a1b35edf9c9ea818a5c66ccad9_109_0.png)

**FIGURE 3.11** Rule 188: (a) ring; (b) line.

![](img/df6085a1b35edf9c9ea818a5c66ccad9_110_0.png)

**FIGURE 3.12** Rule 210: (a) ring; (b) line.

The discrete-event systems presented in Chapter 4 can both reproduce all of the examples in this chapter and offer an elegant alternative to the vending machine's awkward *wait* input, which was described in Section 3.1.3. Equipped with a good understanding of these discrete-time systems, we find that their reproduction as discrete-event systems is a helpful study aide (a task therefore left to the reader). The cellular automata, too, are reborn as discrete event systems and their scope expanded to permit stepping out of synch, which is an important feature of many agent-based models. Discrete-event systems are also an indispensable stepping stone to simulating hybrid systems, the topic of Chapter 5.

## CHAPTER 4

## DISCRETE-EVENT SYSTEMS

Discrete-event systems are a generalization of discrete-time systems that allow time to be continuous. The trajectories of a discrete-event system are functions from the time base ℝ × ℕ to its sets of input, output, and state. These trajectories change value only a finite number of times in any finite interval. This is the defining characteristic of a discrete-event system; the events that cause these discrete changes give the class of systems its name.

The expanded time base raises two issues that are responsible for the relatively complicated (with respect to discrete-time systems) description of discrete-event systems and their simulators. The first is that events may occur at any instant. Consequently, the model must include machinery to describe the subset of ℝ × ℕ where its events occur. The second is that time advances in a plane. Only the real part of this plane reflects physical time; the discrete part is an artifact of modeling change with instantaneous events (Maler and Manna offer an insightful discussion [82, 83]). The structure imposed on time to permit an orderly evolution of the system, although not complicated, is unlike the additive group typical of discrete time (i.e., with time base ℕ) and differential (i.e., with time base ℝ) systems.

Apart from these issues and their consequences, the basic approach to defining a state transition function and the general organization of the simulation software are unchanged. As with discrete-time systems, an iterative simulation procedure for simulating atomic models is derived from a state transition function, set of primitive segments, and the semigroup property. Likewise, a procedure is defined for reducing networks to their resultants, and this is embodied in a bottom-up simulation engine comprising familiar pieces: the **Network** and **Atomic** classes for building models and the *Simulator* and *EventListener* classes for executing simulations.

### 4.1 ATOMIC MODELS

An atomic model of a discrete-event system has a set X of input, a set Y of output, a set S of states, and a set Q of total states that is a subset of S × ℝ. The total state (s, e) ∈ Q has two pieces of information: the state s of the system and the real time e for which it has occupied that state. The occupation time is needed to completely define the system’s behavior; unlike a discrete-time system, where input arrives at regular intervals and each state is occupied at exactly one point in time, a discrete-event system can linger in a state indefinitely and the response to input is influenced by the time spent dwelling there.

#### 4.1.1 Time and Trajectories

The structure of time used here has been widely adopted, appearing (albeit implicitly or with different notation) in Matveev and Savkin’s study of hybrid systems [84], Rönngren and Liljenstam’s proposal for ordering events in parallel discrete-event simulations [122], in the abstract simulator described by Chow et al. [25] for parallel DEVS models, and as part of the Ptolemy II simulation environment [75]. Two elements (t₁, c₁) and (t₂, c₂) of the time base are equal if both components are equal; thus, equality is defined by

$$(t_1, c_1) = (t_2, c_2) \iff t_1 = t_2 \land c_1 = c_2 \tag{4.1}$$

Time is ordered firstly by its real part and then by its discrete part; the relation < is defined by

$$(t_1, c_1) < (t_2, c_2) \iff (t_1 = t_2 \land c_1 < c_2) \lor t_1 < t_2 \tag{4.2}$$

The operator φ gives the real part of a pair (t, c):

$$\phi((t, c)) = t \tag{4.3}$$

The advance operator ▷ takes the place of addition in the definition of a discrete-event system. This operator advances its first argument by an amount equal to its second argument according to the following rule:

$$(t, c) \triangleright (h, k) = \begin{cases}(t+h, 0) & \text{if } h \ne 0 \\(t, c+k) & \text{if } h = 0\end{cases} \tag{4.4}$$

The ▷ operator, unlike addition for the real and natural numbers, is not commutative or associative. Observe that

(1, 1) ▷ (0, 1) = (1, 2)

but

(0, 1) ▷ (1, 1) = (1, 0)

and so a ▷ b ≠ b ▷ a; the first and second arguments cannot be interchanged. Also observe that

((1, 0) ▷ (1, 1)) ▷ (0, 1) = (2, 1)

but

(1, 0) ▷ ((1, 1) ▷ (0, 1)) = (2, 0)

and so (a ▷ b) ▷ c ≠ a ▷ (b ▷ c); changing the order in which ▷ is applied changes the outcome of the calculation.

The trajectories of a discrete-event system are functions from ℝ × ℕ to the set X (an input trajectory), Y (an output trajectory), and Q (a state trajectory). The operator ℓ gives the real length of a trajectory, specifically

ℓ(ζ < (t₁, c₁), (t₂, c₂) >) = φ((t₂, c₂)) − φ((t₁, c₁)) = t₂ − t₁    (4.5)

Recall that the trajectories of a discrete-event system change only a finite number of times in any interval of finite length. The input and output trajectories satisfy one additional property—they are equal to the non-event Φ at all except a finite number of points in any finite interval. Trajectories that satisfy this second property are called *event trajectories*, and legitimate discrete-event systems provided an event trajectory at their input produce an event trajectory at their output.¹

Figure 4.1 illustrates an event trajectory. Real time flows from left to right. At each real instant of time there can be a finite number of discrete transitions. Discrete time at each point of real time flows from bottom to top. The value of each event is written at its location in the time plane.

The rules introduced in Section 3.1.1 for concatenating trajectories are unchanged, but the convenience of “translate and concatenate,” the • operator, is lost because without addition trajectories are not easily translated. The · operator is still applicable, and it will play the same role in defining the state transition function of a discrete-event system that it played for discrete-time systems.

¹ A system that, given an event trajectory at its input, does not produce an event trajectory at its output is called illegitimate or, more recently, Zeno. The term illegitimate is due to Zeigler (see, e.g., Ref. 152); Zeno is a modern term, inspired by Zeno’s paradox of Achilles and the Tortoise, for the same concept (see, e.g., Ref. 160).
