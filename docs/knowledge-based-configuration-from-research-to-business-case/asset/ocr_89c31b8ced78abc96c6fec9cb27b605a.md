are presented in Haselböck and Schenner (2014),⁴ Krebs (2014),⁵ and Hotz and Günter (2014).⁶ The major difference between WEEVIS and other configuration knowledge base development environments is that we can expect that more users are able to deal with modeling configurators in Wikipedia compared to the alternative of defining knowledge bases with (provider-) specific environments. However, admittedly, the major drawback of WEEVIS is its limited expressiveness compared to more general knowledge representation formalisms (see Hotz et al., 2014⁷). Furthermore, graphical constraint management facilities have to be integrated in order to achieve widespread use.

*Anomaly Management.* Most of the existing configuration environments include different types of anomaly detection (see Felfernig et al., 2014⁸) or at least consistency management functionalities. In a similar fashion, WEEVIS includes a basic implementation of the FASTDIAG diagnosis algorithm (Felfernig et al., 2012), which supports users in situations where no solution can be found. Furthermore, WEEVIS allows the specification of test cases that can be exploited for the purposes of regression testing. The integration of further quality assurance mechanisms such as the automated debugging of WEEVIS knowledge bases, redundancy detection (Felfernig et al., 2011), and diagnosis discrimination (Shchekotykhin et al., 2012) is within the scope of future work.

# 25.5 Conclusion

In this chapter we have introduced the WEEVIS environment for the Wiki-based development and maintenance of simple configuration knowledge bases. WEEVIS is especially useful in scenarios where groups or communities of users are interested in commonly providing a configurator application to the whole public or to a specific group of users. From the technological point of view the major advantage of WEEVIS is the development and maintenance of configuration knowledge bases without the overhead of getting acquainted with a completely new technology. Major issues related to the further development of WEEVIS are the integration of personalization concepts (Ardissono et al., 2003; Tiihonen and Felfernig, 2010) that help to rank the set of determined solutions (configurations), the integration of additional quality assurance mechanisms (beside the basic versioning concept of Wikipedia), and the further development of the WEEVIS language itself in the sense of improving the understandability and reducing the cognitive complexity of the provided modeling concepts.

# Acknowledgments

The work presented in this chapter was partially funded by the Austrian research promotion agency (grant number: 827587).

⁴ Chapter 22.
⁵ Chapter 23.
⁶ Chapter 24.
⁷ Chapter 6.
⁸ Chapter 7.