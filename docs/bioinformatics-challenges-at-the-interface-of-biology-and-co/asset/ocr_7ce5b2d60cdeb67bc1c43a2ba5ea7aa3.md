# Box 4.7 Visualising protein fingerprints

Protein fingerprints are most easily understood when viewed graphically. For a given fingerprint, a graph is created when the query sequence is plotted along the x-axis, and scores with the constituent fingerprints are plotted on the y-axis. For each motif, a window whose corresponds to the width of the motif is slid along the query sequence, and its identity score is calculated using the frequency matrix derived from the motifs stored in the PRINTS database. Where a window scores above a given threshold (20 per cent identity), a coloured block is shown to mark the location of the match. If we were merely to plot such motif matches linearly, as shown in Figure 4.31, we could not know whether all the motifs had been matched, unless we used some other visual way to depict 'missing motifs'.

![](bbox=[0.17915, 0.28135000000000004, 0.76955, 0.42935])

Figure 4.31
Plotting consecutive motifs in a fingerprint.

An alternative is to plot the result of each motif scan separately. For true-positive matches, we expect to see a complete set of blocks running diagonally across the plot, from N- to C-terminus. As shown in Figure 4.32, we can immediately see that the query sequence on the left matches all the fingerprint motifs, while the sequence on the right fails to match motifs 4 and 5.

![](bbox=[0.17915, 0.60335, 0.76955, 0.76635])

Figure 4.32
Plots showing complete (left) and partial (right) fingerprint matches.

Fingerprint graphs like this facilitate rapid visual inspection of query sequences, allowing ready identification of complete matches, and of partial matches that fail to match one or more motifs. This renders fingerprinting a more powerful diagnostic tool than methods that use only single motifs.