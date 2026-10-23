A negative test case c⁻ on the other hand specifies that a CPUD and a CPUS must not be mixed on silver and diamond motherboards.

```
c⁻: CPUD(c1) ∧ CPUS(c2) ∧ (MBSilver(m1) ∨ MBDiamond(m1)) ∧
    cpu-of-mb(c1,m1) ∧ cpu-of-mb(c2,m1).
```

Testing the given knowledge base with these two test cases results in an undesired contradiction—KB_faulty ∪ c⁺ is inconsistent. In particular, Axioms 7, 8 and 9 are unsatisfiable when combined with c⁺. Consequently, one of these axioms must be changed when assuming that the test cases are correct. Note that apart from the faulty Axiom 7 also the correct Axioms 8 and 9 are involved in the contradiction. Therefore, at first sight one of these axioms might also be faulty. However, it will turn out that if we assume either Axiom 8 or 9 to be faulty, there must be an additional faulty axiom.

Let us first assume that Axiom 8 is faulty and all other axioms are correct. Axioms 7 and 9 combined with c⁺ imply that motherboard m1 is of type silver. Consequently, Axioms 7 and 9 and case c⁺ imply c⁻. Remember, however, that c⁻ must be inconsistent with the knowledge base. In other words, the knowledge base has to imply ¬c⁻. Consequently, if we consider Axiom 8 as faulty and all other axioms of KB_faulty as correct, there is no way to extend this set of axioms to an acceptable configuration knowledge base given the test cases. Any change of KB_faulty where only Axiom 8 is deleted or replaced cannot be consistent with the positive case and inconsistent with the negative case. Similar arguments hold for Axiom 9.

It follows that only Axiom 7 is a single fault diagnosis of KB_faulty in the sense that changing Axiom 7 will allow the formulation of a knowledge base such that the positive case is consistent and the negative case is inconsistent. If either Axiom 8 or 9 is subject to a revision, additional axioms must be altered.

# 11.3.2 Defining Configuration and Diagnosis

The task of debugging a configuration knowledge base is to discover those axioms of KB have to be changed. In particular, some of the axioms of a faulty knowledge base must be removed and possibly some axioms must be added. This extension is denoted by EX. We call such a revised knowledge base the target knowledge base. This target knowledge base has to be consistent with all positive test cases and must be inconsistent with all negative test cases. We start with the definition of the instances of a configuration knowledge base diagnosis problem (CKB-diagnosis problem).

Definition (Instances of a CKB-diagnosis problem). A problem instance ⟨KB, C⁺, C⁻⟩ of a configuration knowledge base diagnosis problem is defined by a set of logical sentences KB representing the configuration knowledge base, a set of positive test cases C⁺, and a set of negative test cases C⁻. The elements of C⁺, C⁻ are logical sentences representing test cases.

Based on the instances of a CKB-diagnosis problem we define a diagnosis as a subset of the configuration knowledge base:

Definition (Diagnosis). A set S ⊆ KB is a diagnosis for a CKB-diagnosis problem instance ⟨KB, C⁺, C⁻⟩ iff there exists a set of logical sentences EX extending KB such that

+   - (KB − S) ∪ EX ∪ {c⁺} consistent ∀c⁺ ∈ C⁺ and
+   - (KB − S) ∪ EX ∪ {c⁻} inconsistent ∀c⁻ ∈ C⁻