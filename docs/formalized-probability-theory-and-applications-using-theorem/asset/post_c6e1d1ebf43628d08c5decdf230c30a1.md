
From the automated theorem proving user's perspective, formal verification can be done by developing a formal model of the system under verification using the available logic, i.e., propositional or first-order logic. The next step is to formally specify the property that needs to be verified for the given system. This property can then be verified using the automatic verification utilities like SMT solvers. Thus, the main challenge in using automated theorem proving for system analysis is the formal specification of the system model and the properties.

In system analysis, we often come across systems, such as analog circuits or optical systems, whose behavior can only be described in terms of more general mathematics involving sets, real numbers, etc. As described earlier, first-order logic cannot be used to model these kinds of systems and thus we have to use higher-order logic (Gordon, 1989) and interactive theorem proving, where the user is involved in the formal verification process along with the machine. Edinburgh LCF (Logic for Computable Functions) (Gordon, 1989) is one of the most commonly used methods for developing interactive theorem provers. LCF style theorem provers are implemented using the strongly-typed functional programming language ML (Meta Language) (Paulson, 1996) or its variants. An ML abstract data type is used to represent higher-order-logic theorems and the only way to interact with the theorem prover is by executing ML procedures that operate on values of these data types. Interactive theorem provers usually include many automatic proof assistants and automatic proof procedures to assist their user in the verification process. The user interacts with a proof editor and provides it with the necessary tactics to prove goals while using automatic proof procedures whenever the problem is reduced to a decidable subset. This process could be very tedious and usually takes thousands of lines of proof script and hundreds of man-hours for verifying the mathematical analysis presented in a couple of pages using paper-and-pencil proof methods. However, the ability to build upon already verified results is a big strength of interactive theorem proving.

For illustration purposes, consider the formal verification of an algorithm that returns the minimum value of an array of real numbers. Due to the involvement of real numbers and an arbitrary number of elements, higher-order logic theorem proving is used for the verification. The first step in analyzing this algorithm is to formalize it in higher-order logic. This can be mainly done by the following recursive definition:

```
⊢ ∀ x. min_list [] (x: real) = x ∧
∀ h t x. min_list (h:: t) x = minimum (min_list t h) x
```

where the function minimum takes two real numbers and returns the lesser one out of them and the symbol :: denotes the cons operation between the head and tail of an array. The function recursively finds the minimum real number of a list of real numbers and another real number x.

The next step after the formalization of the algorithm is to formalize the property of interest as a proof goal in the theorem prover. The following property serves this purpose:

```
⊢ ∀ (L: real list) x. MEM x L ⇒ min_list (TL (L)) (HD L) ≤ x
```

The predicate MEM x L ensures that x is a member of list L and the functions HD and TL return the head and tail of their list argument, respectively. Thus, the goal guarantees that the value returned by the function min_list is less than or equal to all values of list L. This theorem can now be verified in a theorem prover using induction on the variable L. The rest of the reasoning is based on the above-mentioned definitions and properties of real numbers and lists. The main strength of the analysis presented above is its generic nature, which is evident from the usage of the “for all” quantifier for variables L and x, and guaranteed accuracy, based on the inherent soundness of a theorem prover. However, on the downside, the formalization involves the understanding of higher-order logic and the theories of real numbers and lists. Moreover, the verification required human guidance and was done interactively.

For probabilistic analysis, we need to formalize (mathematically model) random variables as functions and formalize characteristics of random variables, such as CDF and expectation, etc., by quantifying over random variables (Hasan, 2008). Henceforth, first-order logic does not support such formalization and we need to use higher-order logic to formalize probabilistic analysis. The first step in this regard would be to model the behavior of the system that needs to be analyzed in higher-order logic, while expressing its random or unpredictable elements in terms of formalized random variables. The second step is to use this formal model to express the probabilistic and statistical properties, regarding the system, in higher-order logic. Finally, these probabilistic and statistical properties of the system model can be mechanically checked for correctness in a theorem prover. Based on these principles, formal reasoning support for probability theory and its related mathematical foundations has been developed in various higher-order logic theorem provers, including HOL4 (HOL4, 2015), Isabelle/HOL (Isabelle/HOL, 2015) and PVS (PVS, 2015).

The above-mentioned theorem proving based probabilistic analysis approach overcomes the limitations of the simulation and model checking based probabilistic analysis approaches. Due to the formal nature of the models and properties and the inherent soundness of the theorem proving approach, probabilistic analysis carried out in this way will be free from any approximation and precision issues. Similarly, the high expressiveness of higher-order logic allows us to analyze a wider range of systems without any modeling limitations, such as the state-space explosion problem in the case of probabilistic model checking, and formally verify analytically complex properties, such as expectation, variance and tail distribution bounds. Furthermore, the use of mechanical theorem provers will increase the confidence in the proofs over the traditional paper-and-pencil approach. Given these benefits of conducting probabilistic analysis using higher-order logic theorem proving, the main scope of this manuscript is to provide a comprehensive guide to its foundational principles and practical utilization.

## 2.4 CONCLUSION

This chapter provided a brief overview of formal verification methods, their strengths, weaknesses and applications. Formal verification provides precise system analysis, which is a dire need in safety-critical system design. However, this precision comes at the cost of extensive engineering time and effort. Theorem proving is one of the most generic formal verification methods as it can automatically handle the analysis of systems that can be expressed using propositional or first-order logic and can also handle complex systems, involving continuous and unpredictable components, using higher-order logic at the cost of significant manual effort. Whereas, model checking requires manual efforts in formal specification of the system and properties but the verification is done automatically. However, it is limited by the state-space explosion problem and thus cannot handle very large systems.

## REFERENCES

Baier, C., & Katoen, J. P. (2008). Principles of model checking. MIT Press.

Boca, P. P., Bowen, J. P., & Siddiqi, J. I. (2009). Formal methods: State of the art and new directions. Springer.

Gordon, M. J. C. (1989). Mechanizing programming logics in higher-order logic. In Current trends in hardware verification and automated theorem proving (pp. 387–439). Springer.

Hall, A. (2007). Realizing the benefits of formal methods. Journal of Universal Computer Science, 13(5), 669–678.

Harrison, J. (2009). Handbook of practical logic and automated reasoning. Cambridge University Press. doi:10.1017/CBO9780511576430

Hasan, O. (2008). Formal probabilistic analysis using theorem proving. (PhD Thesis). Concordia University, Montreal, Canada.

HOL4 Theorem Prover. (2015). Retrieved Feb. 7, 2015 from http://hol.sourceforge.net/

Huth, M. R. A., & Ryan, M. D. (2000). Logic in computer science: Modelling and reasoning about systems. Cambridge University Press.

Isabelle/HOL. (2015). Retrieved Feb. 7, 2015 from http://www.cl.cam.ac.uk/research/hvg/Isabelle/

Kwiatkowska, M., Norman, G., & Parker, D. (2005). Quantitative analysis with the probabilistic model checker PRISM. Electronic Notes in Theoretical Computer Science, 153(2), 5–31. doi:10.1016/j.entcs.2005.10.030

Nieuwenhuis, R., Oliveras, A., & Tinelli, C. (2006). Solving SAT and SAT modulo theories: From an abstract Davis-Putnam-Logemann-Loveland procedure to DPLL. Journal of the ACM, 53(6), 937–977.

Paulson, L. C. (1996). ML for the working programmer. Cambridge University Press. doi: 10.1017/CBO9780511811326

Pentium FDIV Bug. (2015). Retrieved Feb. 7, 2015 from http://www.cs.earlham.edu/~dusko/cs63/fdiv.html

Theorem Prover, P. V. S. (2015). Retrieved from http://pvs.csl.sri.com

YMER. (2015). Retrieved Feb. 7, 2015 from http://www.tempastic.org/ymer/
