# Chapter 4

# Information Flow Control

Information flow control (IFC) is a technique that asserts the security of a software-system with respect to a security specification. Research on IFC is on the rise of the ubiquity of mobile code and security-relevant applications. Information flow control is often verified with special type systems [SM03]. However, type systems do not exploit the whole repertoire of contemporary program analysis, thus suffer from restrictive languages and a high annotation burden. This chapter will present a new approach for information flow control based on program slicing and the system dependence graph as defined in the last chapters. Contrary to type systems, the presented algorithm is flow-, context-, and object-sensitive as a result of the underlying slicing technology, reducing false alarms. Recent advances in program analysis render this technique feasible and scalable even for realistic languages like Java bytecode.

Previous results from this effort were published in [HKS06, HKN06, HS08].

# ## 4.1 Computer Security

Security in the technical sense is defined as the condition of being protected against danger or loss, with an emphasis on the protection from dangers that originate from the outside. In terms of computer science, three main dimensions of security can be identified, which are commonly depicted in the CIA-triad.

**Confidentiality** is the assurance of data privacy. Only the intended and authorized recipients — individuals, processes or devices — may read confidential data.

**Integrity** is assurance of data non-alteration. Data integrity asserts that the information has not been altered in transmission, from origin to reception, and includes checks of untrustworthy inputs for validity.

**Availability** is assurance in the timely and reliable access to data services for authorized users. It ensures that information or resources are available when required.

*Language-based security* derives security properties from the source or intermediate code. To this end, it leverages programming languages technology,