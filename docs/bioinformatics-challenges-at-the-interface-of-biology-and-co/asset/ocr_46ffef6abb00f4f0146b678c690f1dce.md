# Chapter 4 Biological sequence analysis

A consensus sequence runs down the left-hand side of the profile (HLT-PAEKT...). It's difficult to reconcile this with the consensus that's discernible in Figure 4.28, largely because those haemoglobin α chains constitute a small subset of the sequences matched by this very potent profile (which includes α, β, γ, δ and ε hemoglobin chains, together with myoglobins, neuroglobins, cytoglobins, leghaoglobins, erythrocrins, and so on): 1,152 members in total.

Conceptually, profiles are analogous to Hidden Markov Models (HMMs), which are the base of the Pfam database. The main difference between them relates to how the parameters are interpreted. Most profile scores can be mapped to parameters of HMMs as described by Krogh et al. (1994); the principal difference is that HMM parameters represent log probabilities. The mathematical theory behind HMMs is substantial and has been described in numerous excellent books. Here, it is sufficient to note that HMMs are probabilistic models that consist of several interconnecting states in essence, they they can be thought of as linear chains of state that encode conserved domains in sequence alignments. With profiles, match states are assigned to conserved residue positions, insert states allow insertions relative to match states, and delete states allow match positions to be skipped. Hence, building an HMM from a multiple alignment requires each position to be assigned to a match, delete or insert state, as illustrated in Figure 4.36.

The complexity of HMMs renders them very powerful tools for encapsulating the sequence information in multiple alignments; like profiles, they find their strength in modelling divergent domain families and superfamilies, diagnosing outliers with greater sensitivity can be achieved with consensus expressions or fingerprints. However, their sensitivity also brings a number of issues. The most important caveat is that the methods used to define the diagnostic HMM in Pfam are not as supervised as the manual methods used in PROSITE and PRINTS. Family membership is determined by specific cut-off values¹⁴. Superfamilies and domain families with thousands of members can into how confident we can be that all sequences

![](bbox=[0.148, 0.584, 0.827, 0.781])

Figure 4.36

Linear hidden Markov model. M match states; I are insert states; D are delete states; B and E define the beginning and end of the domain; J allows the domain to be repeated; N and C allow for N- and C-terminal extensions; S and T denote the start and termination of the model respectively.

> ¹⁴http://pfam.xfam.org/help?tab=helpScoresBlock#tabview=tab5