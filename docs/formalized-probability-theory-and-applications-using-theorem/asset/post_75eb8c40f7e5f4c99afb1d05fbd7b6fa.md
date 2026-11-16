
and utilizes the computers for bookkeeping, to be able to handle complex systems without having to worry about human errors. Formal verification methods, which are primarily based on theoretical computer science fundamentals like logic calculi, automata theory and strongly typed systems, fulfill these requirements. The main principle behind formal analysis of a system is to construct a computer based mathematical model of the given system and formally verify, within a computer, that this model meets rigorous specifications of intended behavior. Due to the mathematical nature of the analysis, 100% accuracy can be guaranteed.

### 1.6 CONCLUSION

This chapter presented a brief introduction to the main principles of probabilistic analysis and the traditionally used probabilistic analysis techniques. The main focus of this book is to present a formal probabilistic analysis approach using theorem proving, which is a widely used formal verification method. A brief overview about formal methods is given in the next chapter to facilitate the understanding of the rest of the book.

## REFERENCES

- Billingsley, P. (1995). *Probability and measure*. John Wiley.
- Grozin, A. (2013). *Computer algebra systems*. Springer.
- MacKay, D. J. (1998). Introduction to Monte Carlo methods. In Learning in graphical models (pp. 175–204). Kluwer Academic Press.
- Mitzenmacher, M., & Upfal, E. (2005). *Probability and computing*. Cambridge University Press. doi:10.1017/CBO9780511813603
- Rose, C., & Smith, M. D. (2002). *MathStatica: Mathematical statistics with mathematical, computational statistics*. Springer. doi:10.1007/978-1-4612-2072-5
- Ross, S. M. (2002). *Simulation*. Academic Press.
- Yates, R. D., & Goodman, D. J. (2005). *Probability and stochastic processes: A friendly introduction for electrical and computer engineers*. Wiley.

## KEY TERMS AND DEFINITIONS

**Continuous Random Variable:** A random variable is called continuous if it can attain an infinite number of values or in other words its range is an interval of real numbers.

**Discrete Random Variable:** A random variable is called discrete if the number of different values that it can acquire, or its range, is finite or at most countably infinite.

**Probabilistic Analysis:** Probabilistic analysis of a system is the process of applying probability theory based reasoning to estimate the probabilities of interesting events associated with the given system.

**Random Variable:** A random variable is a function that maps elements of a probability space to some other measurable space.

## Chapter 2

## Formal Verification Methods

### ABSTRACT

This chapter provides a brief introduction to the domain of formal methods (Boca, Bowen, & Siddiqi, 2009) and the most commonly used verification methods (i.e., theorem proving [Harrison, 2009] and model checking [Baier & Katoen, 2008]). Due to their inherent precision, formal verification methods are increasingly being used in modeling and verifying safety and financial-critical systems these days.

### 2.1 INTRODUCTION

The history of formal methods dates back to Knuth and Dijkstra as both of them advocated the topic. Formal verification methods started to be investigated as CAD tools in the 1970s for software verification. However, the interest was marred by the fact that software bugs can be easily fixed by releasing a software patch and thus the added reliability of software is not worth the rigorous exercise of formal verification. There were some research activity related to the formal verification of security systems funded by the US National Security Agency in the 1980s but the real catalyst for the active research interest in formal verification was their usage in verifying digital hardware systems in late 1980s. This is mainly because hardware descriptions are often more regular and hierarchical than software ones, hardware primitives are less obscure than the ones used in software and the cost of an uncaught design bug in hardware is much more profound than software since the hardware silicon chip once fabricated cannot be fixed by releasing a patch but instead has to be re-designed and re-fabricated, which costs considerable amount of time and money. The Intel FDIV bug in 1994 (Pentium FDIV Bug, 2015) further enhanced the interest in formal hardware verification and the industry started to adopt formal hardware verification tools in their design flows in late 1990s. With the success of formal verification in hardware and due to some interesting developments in the underlying technologies, it started to be used again for software, transportation and security system analysis domains. Moreover, formal verification has recently been explored for accurately analysis of continuous physical systems, such as control systems, robotics and analog circuits. The future of formal methods seems to be quite promising and besides academia, industry giants, like Intel and Microsoft, are also actively participating in the research related to both foundational and practical aspects.

The added benefits of formal verification methods (Hall, 2007) come mainly at the cost of extreme rigor. Generally speaking, the expressiveness of a formal verification method is in direct proportion with the amount of required user intervention. Thus, formal verification of complex systems is more challenging and time consuming. Therefore, the general trend is to use a lightweight approach, i.e., use traditional verification methods, like simulation or testing, where accuracy of the analysis is not a big concern while using formal verification methods for the critical sections of the systems. On similar lines, hybrid formal verification methods are also being developed which allow us to partition the overall system model based on its complexity levels and thus facilitate using automatic formal verification methods for the rather simpler sections of the system while using the interactive methods with the complex sections.

Generally, formal verification methods are classified based on their underlying logic, expressiveness and decidability. The most commonly used formal verification methods include model checking and theorem proving, which are described in detail below:

### 2.2 MODEL CHECKING

Model checking is primarily used as the verification technique for reactive systems, i.e., the systems whose behavior is dependent on time and their environment, like controller units of digital circuits and communication protocols. The inputs to a model checker include the finite-state model of the system that needs to be analyzed along with the intended system properties, which are expressed in temporal logic. The model checker automatically verifies if the properties hold for the given system while providing an error trace in case of a failing property. The main verification principle behind model-checking is to construct a precise state-based model of the given system and exhaustively verify the given property for each state of this model. The analysis is automatic which is why model checking is one of the most widely used formal verification technique. On the other hand, model-checking is limited to systems that can only be expressed as finite-state machines. Another major limitation of the model checking approach is state space explosion. The state-space of a system can be very large, or sometimes even infinite. Thus, it becomes computationally impossible to explore the entire state-space with limited resources of time and memory. This problem is usually resolved by working with abstract, less complex, models of the system by somehow compromising the accuracy of the analysis.

Many efficient methods have been proposed to alleviate the memory and computation requirements of model checking. Symbolic model checking is based on the idea of grouping multiple states together and assigning them a unique symbol and then running model-checking algorithms on this symbolic state-space. Bounded model checking (BMC) (Baier & Katoen, 2008) is an extension of symbolic model checking and the idea is to encode states as propositional logic formulas and then use SAT solvers (Huth & Ryan, 2000) for the analysis. A subset of executions with an upper bound on length, say k, is chosen and the counter-example is searched in this subset in BMC. If the contradiction is not found then the value of k is increased and the algorithm is re-run.

For illustration purposes, consider a simple automatic bank teller machine (ATM): The first step to initiate a transaction is to insert the ATM card. Next, the user may make a request, like requesting and depositing money, or do nothing. If a request is made then it is serviced and the card is ejected else the card is ejected without providing any service to the user. The first step in analyzing
