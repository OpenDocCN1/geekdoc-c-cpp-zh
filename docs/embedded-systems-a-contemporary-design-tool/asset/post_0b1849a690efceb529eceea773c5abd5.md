
The circuit in the first diagram has left the unused input open. The two parasitic capacitors, C1 and C2, form a voltage divider, as shown in the circuit in Figure 2.52.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_154_0.png)

The resulting voltage on C2 is now given in Eq. (2.44) as:

```
V_out(s) = \left\{ \frac{ \frac{1}{C_2 s} }{ \frac{1}{C_1 s} + \frac{1}{C_2 s} } \right\} V_in(s)
= \left( \frac{C_1}{C_1 + C_2} \right) V_in(s)
(2.44)
```

If the voltage on C2 is sufficiently high, the AND gate will function as expected. If the voltage drops below VIH,min, the device will hold a constant logical 0 as its output state. Sometimes the circuit may work and sometimes it may not.

In the design of the second circuit, two of the inputs are connected together, thereby eliminating the floating input. Logically, such a practice will give the desired result. However, the two parasitic capacitors are now in parallel. Since parallel capacitors add, the net value is now C1 + C2. The voltage going into the device on the combined pins is now given as:

```
V_out(t) = V_in(t) \left( 1 - e^{-\frac{1}{RC}t} \right)
(2.45)
```

where the value of C in the time constant is now C1 + C2. If the two capacitors have the same value, the time constant has doubled, thereby substantially slowing the rising or falling edge of the input signal. Doing so can induce metastable behavior when the device switches and can potentially damage the part.

In the third circuit, the design uses a pull-up resistor to define the state of the unused input. Although the parasitic capacitance associated with the unused input is still there, the value of the voltage stored on the capacitor is held at the supply voltage. It will cause no problems.

## 2.8 TESTING COMBINATIONAL CIRCUITS – INTRODUCTION AND PHILOSOPHY

- **Debugging** Debugging is the process of identifying errors in a new or modified circuit or system, **Troubleshooting** Troubleshooting is identifying failures in a previously working system. **Testing** Testing is a bit different. We generally find that there are four main reasons why we have to test. First, we want to verify that any hardware or software modules, prototypes, subsystems, collections of subsystems, or the final integrated system perform as it was designed. Once the initial functionality is confirmed, testing efforts shift to ensuring that the completed system meets all requirements and design specifications. Any system will change and grow with time as modifications are made or as new features and capabilities are added to satisfy new and changing customer requirements. As with the original design, one must make certain that the completed system, with all its new features and capabilities, also satisfies all specifications. Meeting all specifications means making certain that the original behavior of the system has not been modified in unintended or unexpected ways as a result of the changes. Finally, because no manufacturing process is perfect yet, we must make certain that the system functions properly after being built.

### Test suites

When we are thinking about testing and when we are putting test suites together, a good way to think about them is in terms of the amount of information that can be gained with each step. When a step within a test fails, what is it saying? What is the maximum amount of information that can be gained from the failure? When a test succeeds, what does it say about the circuit or system being tested? Are we closer to proving that it performs as we desire? If yes, then good. If not, then why did we include that step?

## 2.9 MODELING, SIMULATION, AND TOOLS

As we have seen in our studies so far, modeling and simulation play a critical role in the design of modern-day digital circuits and systems. We have learned about several different kinds of tools as well as how and when we apply them. When we move to test, those tools should follow; they are just as important during the test portion of the development as they were during the design portion. Today one would not think about attacking a complex design without modeling tools like Spice, VHDL, or Verilog. Test problems should be attacked with the same formal methods.

As we learned earlier, models and modeling are essential to the design, development, and test of today's complex digital systems. One can use models to break a problem down into parts that are simpler and easier to manage. During the early stages in the design of a circuit or system, models can serve as aids to understanding and dealing with the complexity of the problems to be solved. During test, models serve as aids in understanding the behavior of the hardware or software under faulted conditions and as guides in developing a solid testing strategy and the subsequent tests.

Faults and errors in the original design or those introduced during its manufacture are no different in their effects on the behavior of the circuit or system than the components that are designed into the system. We will take a preliminary look how to begin to model such faults and the role such models play during the debug and test of a design. In Chapter 9, we will take a more detailed look when we introduce the co-design process.

- co-design
- intermittent, transient faults
- fault, failures errors

Before we begin, however, let's look at the scope of our problem. The analysis and understanding of *intermittent* (existing only occasionally) or *transient* (occurring only once) faults require detailed statistical information characterizing how they occur and special tools for analyzing the collected data. We will begin with some of the relevant vocabulary before we proceed. A *fault* is any unsatisfactory system condition or state. *Failures* and *errors* are different kinds of faults. A failure is an (undesired) dynamic event occurring at a specific time. An error is static. An error is an inherent characteristic of a system resulting, for example, from a design mistake or oversight. A fault can affect a system in many different ways.

Faults may be random or systematic, and failures are typically random. When a failure occurs in a system, we now have a system that once functioned properly that no longer does so. Failures usually occur in the field when a hardware part breaks or wears out. Random faults can only occur in physical things such as an electrical component. We cannot design them away. Such is not the case for errors. Errors are inherent in the system as the result of a design oversight or mistake. They surface (generally at the most embarrassing times – frequently in front of our best customer) under situations such as unexpected combinations of inputs. Through careful design and thorough testing, one can catch most errors. One further tries to identify potential failure conditions through stress testing.

- logical fault models
- structural faults
- functional faults
- single-fault assumption

A design is characterized as static or dynamic; one does the same with faults in the system. Static faults are independent of time; dynamic faults appear as the result of transients and/or changing signals such as races. As we did in earlier work, we begin by modeling the physical faults. To do so, we develop *logical fault models* as abstract representations of the effect of a real world or physical faults on our system. With such models, one can identify those that affect the logical behavior of the system and those that affect its performance. One can identify the source of faults as originating from the interconnections among components, the *structural faults*, and those arising from within a component, the *functional faults*.

The *single-fault assumption* allows one to assume that when studying structural faults one is working with good components – those that are fault free and vice versa.

## 2.10 STRUCTURAL FAULTS

### 2.10.1 Stuck-at Faults

- net
- stems, branches
- stuck-at fault model
- stuck-at-one (s-a-1)
- stuck-at-zero (s-a-0)
- open
- short

Within a circuit or system, a *net* is defined as a signal or collection of signals connecting two or more elements. Signal paths are made up of *stems* and *branches*. A stem is the origin of a signal, usually the output of a logic device. A branch is one or more signal paths that may fan out off a stem. A branch usually terminates at the input of a logic device.

Structural faults arise from defects in the net interconnecting the components in the system. Such faults may originate at the stem of the net or at one of its branches. One of the models commonly used to study such faults is called the *stuck-at fault model*. In such a model, a signal is interpreted as either permanently held to the logical one state, *stuck-at-one* (s-a-1), or to the logical zero state, *stuck-at-zero* (s-a-0).

An *open* is a signal line that is designed to be connected to a circuit element or other signal line that is not connected. A *short* is a signal line that is not intended to be connected to a circuit element or other signal line that is connected.

Stuck-at faults generally occur because of missing or unintended connections of one kind or another. Examples might include an open circuit, an incorrectly connected wire, or a sliver of printed circuit trace material connecting a signal in a net to one of the power rails or to another signal in the net. In the latter two cases, one can assume that all components of the net are at the same logic level. In the first case, one cannot make that assumption.

An open circuit represents a special kind of stuck-at fault. The open may be the result of a broken wire, damaged printed circuit trace, or bad solder joint. The difficulty with such faults is that they may appear as a stuck-at-zero or a stuck-at-one, depending on parasitic connections to neighboring components or the physical characteristics of the device. Let’s now see how such faults will appear in a design and how they can be modeled.

In the accompanying figures, we will use logic gates to model any conjunctive (AND) or disjunctive (OR) type of relationship and to illustrate the effects of stuck-at faults in each context. We assume a single-fault model; thus, faults such as a stuck-at fault on a stem
