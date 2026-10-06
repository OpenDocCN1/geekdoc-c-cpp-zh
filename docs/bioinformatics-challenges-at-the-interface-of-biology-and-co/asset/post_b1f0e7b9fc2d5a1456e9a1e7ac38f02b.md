
## Box 5.3 Colour schemes for encoding amino acid properties

Over the years, an assessment of different colour schemes has been used to denote amino acid properties, particularly for comparison purposes in multiple sequence alignments; a sample of the available schemes is shown in Figure 5.9. The thing to notice is the lack of agreement between them: most depict cysteine (a sulphur-containing residue) as yellow, except the scheme used in ClustX; most depict the polar amino acids as green, except Taylor, who render them in various shades of orange and magenta; most depict the basic amino acids as blue, except ClustX, which tends to use red, the colour used by the other schemes to denote aliphatic properties! There is no correspondence between the colours used to denote aliphatic amino acids, nor is there much agreement on the used used for aromatic properties, although the Taylor and ClustX schemes use various shades of blue for Tr and Tyr.

| | A R N D C Q E G H I L K M F P S T W Y |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| ClustX | 🟦 | 🟦 | 🟦 | 🟦 | 🟩 | 🟩 | 🟩 | 🟩 | 🟩 | 🟩 | 🟦 | 🟦 | 🟦 | 🟥 | 🟥 | 🟥 | 🟥 | 🟥 | 🟥 |
| Zapo | 🟨 | 🟨 | 🟨 | 🟨 | 🟨 | 🟨 | 🟨 | 🟨 | 🟨 | 🟨 | 🟨 | 🟨 | 🟨 | 🟨 | 🟨 | 🟨 | 🟨 | 🟨 | 🟨 |
| Taylor | 🟧 | 🟧 | 🟧 | 🟧 | 🟩 | 🟩 | 🟩 | 🟩 | 🟩 | 🟩 | 🟦 | 🟦 | 🟦 | 🟥 | 🟥 | 🟥 | 🟥 | 🟥 | 🟥 |
| 'Standard' | 🟥 | 🟥 | 🟥 | 🟥 | 🟩 | 🟩 | 🟩 | 🟩 | 🟩 | 🟩 | 🟦 | 🟦 | 🟦 | 🟥 | 🟥 | 🟥 | 🟥 | 🟥 | 🟥 |

Figure 5.9

Selected colours used to denote amino acid properties.

What's important here is not that one scheme is 'better' than another; the issue is the relative different schemes we use when trying to understand what the particular colour we mean. In turn, determines how easy it is for users to switch between their mental models when trying to compare, an alignment visualisation using the ClustX scheme versus using the Taylor scheme. The benefit of the 'standard' scheme is that it reduces cognitive burden by using colours that are intuitive, many relate to mental models we already possess (as positive-blue, negative-red) and map to schemes that are already familiar to us for depicting atoms in 3D models (N-blue, O-red, S-yellow). Our brains are therefore freed up to concentrate on the information of an alignment, instead of being distracted by the choice of colour-translation.

As mentioned earlier, the sequences here are a mix of known and putative GPCRs–we'd expect to see hydrophobic regions (TM domains) interspersed by short hydrophobic loops). One of the defining characteristics of GPCRs is the presence of an acidic-GR motif (sometimes called the DRY motif) at the C-terminal of the third TM – the conserved Arg is the point of interaction with G proteins. Therefore, with the standard colour scheme, we'd expect to find a Red-Blue-Purple triplet just before a hydrophobic loop. In the CINEMA representation, this is evident in the N-terminal of the central hydrophobic domain. We see that the triplet is present in the known GPCRs (OPSD, ACM1, OPRM, C5AR), but not in the putative GPCRs (Q23293, GP153, GP162, UL78). This is harder to see in the ClustX representation, as we have to end our mental model to look for a Purple-Red-Bluish triplet. Having located the relevant regions, it is up to us to determine whether sufficient contextual evidence in the alignment suggest that the putative GPCRs are likely to be G proteins. We will leave you to form your own conclusions!

Chapter 5 The gap

## 5.8.3 How similar are my sequences?

Earlier in this section, we mentioned that one of the reasons for wishing to align sequences, aside from wanting to help detect structural or functional features, is to allow us to make inferences about their relatedness: i.e., we often create alignments to determine how similar given sets of sequences are. So how are the sequences in Figures 5.5 and 5.8? As you can see, it is very hard to say anything meaningful. They don't look similar, do they? But there's a twist. If we want to persuade that the sequences are similar, we can do so by changing the colour scheme to a consensus approach. Figure 5.10.

Two interests are about this figure. The first is how hard, relatively, the colour schemes make us work to identify the conserved residues. With two positions stand out completely (R and A); others comprising V and W. With the PRALINE scheme, we see that R is conserved, but it appears that the A isn't; the V and W positions are also well conserved, but it seems that the P isn't – otherwise, we have to work a bit to interpret what the alignment is telling us about the degree of conservation of the sequences. Part of the challenge is that (unlike the example from physics and chemistry that we see in Section 5.8) we're hard-wired to equate red with hot and blue with cold, so we'd usually think of a blue-to-red scheme as running

| | A R N D C Q E G H I L K M F P S T W Y |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Without Q02393 | AESRLYLVAGMAFTILS | SANDRDTQSPRAIRAVCPPFAWSS |
| OPRD | IALWSLVLAERVAC | KPSNRLFPGENHAFTNAMACA |
| ACM1 | ASMNVLLISPRDFVST | PLYSRAKKRITRAIMALAGVSLLA |
| OPRM | TISFTCTMSDRYTRIAQ | PVKALDFPRTAKKINNWCSAATUL |
| C5AR | ASLLLTASADPILLVE | PWICQNGEGFKAKAVCAAGVILLT |
| GP103 | ATTCFTASLYSHRMWR | GKKAGVTMWHMIMGISPILST |
| GP162 | ATTCFTASLYSHRMWR | PVYNRNSLSALQAYMGISPILST |
| UL78 | STALFFPLLIDLRISGYLDMR | WTHRENAQAGAYAFWLSAVNA |
| CINEMA | AESRLYLVAGMAFTILS | SANDRDTQSPRAIRAVCPPFAWSS |
| OPRD | IALWSLVLAERVAC | KPSNRLFPGENHAFTNAMACA |
| ACM1 | ASMNVLLISPRDFVST | PLYSRAKKRITRAIMALAGVSLLA |
| OPRM | TISFTCTMSDRYTRIAQ | PVKALDFPRTAKKINNWCSAATUL |
| C5 | ASLLLTASADPILLVE | PWICQNGEGFKAKAVCAAGVILLT |
| OPSD | ASLKLSLERVVQK | PVYNRNSLSAKAKAGVNAMACA |
| ACM1 | ASLKLSLERVVQK | PVYNRNSLSAKAKAGVNAMACA |
| GP103 | ATTCFTASLYSHRMWR | PVYNRNSLSALQAYMGISPILST |
| GP162 | ATTCFTASLYSHRMWR | PVYNRNSLSALQAYMGISPILST |

![](img/142ff402ef4720886c50af0bbe9b5_176_0.png)

Figure 5.10 excerpts from alignments of a group of receptors using tools with different colour schemes. For comparison, the equivalent part of the alignment is shown in each case; note that PRALINE has re-ordered the sequences and the algorithm has produced a slightly different result from the MUSCLE alignment. The CINEMA colour scheme uses a kind of greyscale (the lighter, the more conserved the position), while PRALINE uses a colour scheme that runs from blue to red, red being the most conserved and least biased cold-hot— think of the colours we associate with fundamental things like fire and water/ice, here the colours we've appropriate to denote hot and cold. The PRALINE colour scale, however, runs in the opposite direction: i.e., the mutational hotspots (the most changeable positions) are blue, while the mutational cold (least changeable positions) are red. The issue here isn't that one scheme is inherently right and another wrong; rather, it is about the mental effort required to assimilate the metaphor—some metaphors are more intuitive than others (because we learned when we were younger, because we use them in everyday life, or because our visual perception is wired this way); they can therefore make our lives much easier.

There is, however, a more subtle point here—it's tied up, with the colours perhaps use as shortcuts for concepts like 'hot', but with the semantics we bring to them. For example, what does 'hot' mean to you? A standard definition will speak of degrees of heat or high temperature, however, or perhaps, the degree of spinach in a cup. A dictionary of language, however, will have a much wider semantic intent, capturing meanings such as 'angry', 'stolen', 'attractive', 'talented', 'well-known/popular' and, ironically, 'cool'! In the context of biological sequence and structure analysis, it could be argued that stages of conservation are the 'hot' things to look rather than mutations, because they highlight structural and functional features, and hence they should be red; but it could be argued that mutations are the 'hot' things to look for, given their potential to understand functional and genetic diseases like cancer³⁵. Each of us carries different semantic baggage, and hence what we consider 'hot' is subjective and task dependent. Different colour schemes may then appear to be more or less intuitive, however, will be easier or more difficult to use, depending on the interplay between our personal phenomenal and mental models.

The second interesting thing about Figure 5.10 is that by the changing of manner of visualisation (from colouring per residue, residue group, to colouring column), we can radically influence how we perceive and interpret the result. Relative to the alignments in 5.5 and 5.8, the sequences in Figure 5.10 look more similar. By colouring the alignment per column, we effectively smooth out the background noise and focus on the most conserved regions. Various software tools have been developed to exploit this: use greyscale or colour shading, like above; allow boxes to draw around regions that are the same, or similar, in order to draw our attention to them. Consider the alignment shown in Figure 5.11.

This alignment, published in The Plant journal in 2007, compares the protein GR2 (Q9C29) with n cysteine (Nisc, Q48670³⁵). The authors have gone to some trouble to align the sequence really to the known crystal structure, and have marked up the α-helix and β-strand regions, and have pinpointed the zinc ligands, the identical and similar regions are shaded black and grey. Most of us accept the result
