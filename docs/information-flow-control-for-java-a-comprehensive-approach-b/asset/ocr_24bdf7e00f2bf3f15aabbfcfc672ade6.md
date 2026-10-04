# 7.3. INFORMATION FLOW CONTROL

none at all. Note that this has nothing to do with dynamic labeling, labels are created at runtime. Here labels are statically determined, but variables are not partitioned into disjoint sets according to their label. Therefore, we can leverage the original and more general notion of noninterference of Goguen and Mesuer [GM82, GM84].

# 7.3.4 Case Studies

As an initial-benchmark to compare our approach with type-based IFC, let us reconsider the program from Figure 4.6 on page 96. Remember that PDG-based IFC guarantees that there is no flow from the secure variable (annotated P(11) = High to the first output statement in line 19. Hence we analyzed the program from Figure 4.6 using Jif [mCN*]. Jif uses a generalization of Denning's lattices, the so-called decentralized label model. To specify sets of security levels (called "labels") for every statement, and to attach a set of operations to any label. This is written e.g. {o1: r1,o2: r2} and combines access with IFC. Our approach could be generalized to use the decentralized label model as well.

But note that even decentralized labels cannot overcome the imprecision of type-based analysis. As an example, we annotated the first part of Figure 4.6 to Jif syntax and annotation of o and both instances of A with the principal p. The first statement was replaced by an equivalent code that allowed public output. Jif reports that secure data could flow to public channel and this raised a false alarm. In, no annotation is possible that makes Jif accept the first part of Figure 4.6 without changing the source code.

# A Java Applet

As another case study for IFC we chose the Java applet called Wallet⁵ It is only 252 lines long but with the necessary API parts and stuffs the PDG constructed of 18885 edges and 68259 edges. The time for PDG construction was 8 seconds plus 9 for summary edges.

The Wallet stores a balance that is at the user's disposal. Access to this balance is only granted after supplying the correct PIN. We annotated all statements that update the balance with the provided security level High and inserted a declassification to Low into the getBalance method. The methods credit and debit may throw an exception if the maximum would be exceeded or if there is insufficient credit, resp. In cases Java applets throw an exception, and the exception is exactly dependent on the result of a condition involving. The exception is not meant to be caught but percolates to the Java terminal, so we inserted declassifications for these exceptions as well. Besides this intended information flow, which is only possible upon user request and after verifying the PIN, our analysis proved that no further information flow is possible from the balance to the output of the JavaCard.

> ⁵See Table 7.1 on page 160