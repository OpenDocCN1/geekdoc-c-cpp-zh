# Bioinformatics challenges at the interface of biology and computer science

is that they increase the sensitivity of sequence comparisons; their inherent disadvantage is that they weigh all possible amino acid substitutions, regardless of whether they occur in the types of sequence being compared; hence, the background noise they introduce may mask the biological signals they designed to find.

| | K Y F P H F D L S G A Q V K H G |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|n| K | x | x | x | x | x | x | x | x | x | x | x | x | x | x | x | x | x |
| T | x | x | x | x | x | x | x | x | x | x | x | x | x | x | x | x |
| Y | x | x | x | x | x | x | x | x | x | x | x | x | x | x | x | x |
| P | x | x | x | x | x | x | x | x | x | x | x | x | x | x | x | x |
| F | x | x | x | x | x | x | x | x | x | x | x | x | x | x | x | x |
| H | x | x | x | x | x | x | x | x | x | x | x | x | x | x | x | x |
| D | x | x | x | x | x | x | x | x | x | x | x | x | x | x | x | x |
| L | x | x | x | x | x | x | x | x | x | x | x | x | x | x | x | x |
| S | x | x | x | x | x | x | x | x | x | x | x | x | x | x | x | x |
| G | x | x | x | x | x | x | x | x | x | x | x | x | x | x | x | x |
| A | x | x | x | x | x | x | x | x | x | x | x | x | x | x | x | x |
| Q | x | x | x | x | x | x | x | x | x | x | x | x | x | x | x | x |
| V | x | x | x | x | x | x | x | x | x | x | x | x | x | x | x | x |
| K | x | x | x | x | x | x | x | x | x | x | x | x | x | x | x | x |
| H | x | x | x | x | x | x | x | x | x | x | x | x | x | x | x | x |
| G | x | x | x | x | x | x | x | x | x | x | x | x | x | x | x | x |

![](bbox=[0.558, 0.376, 0.816, 0.413])

The dotplot is effectively a signal-to-noise landscape, offering a tangible, graphic expression of the challenge of discriminating signal from noise. When substitution matrices are used in dotplots like this (especially for more realistic, full-length sequences), it becomes easier to filter out the background noise. In practice, this can be done by implementing a sliding-window calculation as a smoothing function, which improves the signal-to-noise ratio.

The pivotal concept behind her was the 'accepted point mutation': i.e., an amino acid replacement (arising from a mutation in the parent gene) has been accepted by natural selection as the predominant form within a species. Under circumstances, the new amino acid is likely to share similar physicochemical properties and has a related function to the one it replaced. As of Dayhoff’s study, not only was the frequency of each amino acid exchange with every other amino acid considered, but also the propensity of each to remain unchanged during a given evolutionary interval – in words, the amino acid 'relative mutability' was also evaluated. Information from the different types of mutation observed, coupled with the relative mutabilities of the amino acids, was ultimately combined into a distance-dependent probability matrix. The evolutionary interval was 1 PAM (Point Accepted Mutation), equivalent to 1 accepted point mutation per 100 amino acids.

With this approach, different mutation matrices can be derived for any evolutionary distance measured from PAMs, by essentially multiplying the 1 PAM matrix by itself. For a larger evolutionary distance is encapsulated in the mutation probability matrix for 250 PAMs. Sequences reflected in this matrix can be considered to have undergone 250 mutation events per 100 residues, leaving 20 cent of their amino acids unchanged. The latter broadly corresponds to the Twilight Zone of sequence similarity (see Box 4.3), and hence led PAM 250 to become the default scoring-matrix in many sequence analysis and alignment packages.