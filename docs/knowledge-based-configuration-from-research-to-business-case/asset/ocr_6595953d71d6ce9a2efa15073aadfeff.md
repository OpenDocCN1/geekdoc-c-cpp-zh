many of the user requirements are supported by the configuration; for example, configuration conf₁ supports the user requirement v₁ = 1 but not the remaining ones; consequently the support of conf₁ = 1. It should be clear now that we are interested in diagnoses for the given set of requirements—the minimal (cardinality) set of requirements that have to be deleted such that a solution can be identified.

On the basis of the intermediate representation (see Table 7.8) it is straightforward to determine, for example, one minimal cardinality diagnosis. The configuration confᵢ with the maximum support also defines a minimal cardinality diagnosis Δ since there does not exist a diagnosis Δ′ with |Δ′| < |Δ| (if this would be the case then Δ would not have the maximum support value). In our working example, the only minimal cardinality diagnosis is Δ = {v₂ = 1}.

# 7.5 Conclusion

In this chapter, we sketched major concepts, techniques, and algorithms that support anomaly management in constraint-based application development, especially configurator application development. These concepts are the basis for other chapters in this book (see Friedrich et al., 2014⁷ and Felfernig et al., 2014⁸).

# Acknowledgments

The work presented in this chapter was funded by the Austrian research promotion agency (grant number: 827587).

# References

Barker, V., O’Connor, D., Bachant, J., Soloway, E., 1989. Expert systems for configuration at Digital: XCON and beyond. Communications of the ACM 32 (3), 298–318.
Chandola, V., Banerjee, A., Kumar, V., 2009. Anomaly Detection: A Survey. ACM Computing Surveys 41 (3), 1–58.
Felfernig, A., Friedrich, G., Jannach, D., Stumptner, M., 2004. Consistency-based diagnosis of configuration knowledge bases. Artificial Intelligence 152 (2), 213–234.
Felfernig, A., Zehentner, C., Blazek, P., 2011. CoreDiag: eliminating redundancy in constraint sets. In: 22nd International Workshop on Principles of Diagnosis (DX’2011), Murnau, Germany, pp. 219–224.
Felfernig, A., Schubert, M., Zehentner, C., 2012. An efficient diagnosis algorithm for inconsistent constraint sets. Artificial Intelligence for Engineering Design, Analysis and Manufacturing (AI EDAM) 26 (1), 53–62.
Felfernig, A., Schippel, S., Leitner, G., Reinfrank, F., Isak, K., Mandl, M., Blazek, P., Ninaus, G., 2013. Automated repair of scoring rules in constraint-based recommender systems. AI Communications 26 (2), 15–27.
Felfernig, A., Reinfrank, F., Ninaus, G., Blazek, P., 2014. Redundancy detection in configuration knowledge. In: Felfernig, A., Hotz, L., Bagley, C., Tiihonen, J. (Eds.), Knowledge-based Configuration – From Research to Business Cases. Morgan Kaufmann Publishers, Waltham, MA, pp. 157–166 (Chapter 12).
Fijany, A., Vatan, F., 2004. New approaches for efficient solution of hitting set problem. In: Winter International Symposium on Information and Communication Technologies. Trinity College Dublin, Cancun, Mexico, pp. 1–6.

⁷Chapter 11.
⁸Chapter 12.