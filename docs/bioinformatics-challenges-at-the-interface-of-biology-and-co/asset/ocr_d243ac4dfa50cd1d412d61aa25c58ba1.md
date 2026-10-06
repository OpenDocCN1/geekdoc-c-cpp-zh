Re-running BLAST just on the Swiss-Prot component of UnProtKB gives very
different answer: in 2015, the output shows top matches to FMRF amide
toceptor, GPCR 182 and to a μ- and κ-type opioid receptors (by the time
y run the BLAST search, the results might look slightly different again). Aligning
half-a dozen of these gives a result that looks like Figure 5.17.

There are similarities between the results, but there are also significant differences.\ Clearly, TremBL is larger than Swiss-Prot; the TremBL search revealed
sequences more than the Swiss-Prot search had access to. Most of
the retrieved matches from Swiss-Prot were μ- and κ-type opioid receptors, just as
they must have been when Q32393 was first deposited in TremBL; but it's clear that
this sequence doesn't share a key of features (e.g., the DRY motif). Similu-
larly, the aligned sequences from the TremBL search were all annotated as rec-
of some sort; but again, Q32393 doesn't share various features (e.g., the WRY
mot). In both alignments, Q32393 appears to be an outlier – it shares similarities
with both sets of sequences, but it isn't the same as either. A fingerprint scan of
the sequence hits the rhodopsin-like GPCR superfamily (the graphical output depicted
in Figure 5.18 shows a weak partial match); but no family or subfamily is
matched. Thus, taken together, the results suggest that Q22393 could be a receptor,
but that's functional GPCR not conclusive.

![](bbox=[0.159, 0.435, 0.529, 0.706])

Figure 5.18
A fingerprint scan of Q22393.

# # Chapter 6

1 This algorithm takes a similar approach to that of bubble sort, with each pass iter-ating through the entire list in order to guarantee a single correctly-placed value.
Because of that, it requires the same number of potential candidates as a naive
bubble sort, giving it a time complexity of O(n²). Unlike bubble sort, however,
we were able to manage optimisation by progressively comparing one fewer value

> http://www.bioinfo.manchester.ac.uk/cgi-bin/dbbrowser/fingerPRINTs/FPScan_fam.cgi