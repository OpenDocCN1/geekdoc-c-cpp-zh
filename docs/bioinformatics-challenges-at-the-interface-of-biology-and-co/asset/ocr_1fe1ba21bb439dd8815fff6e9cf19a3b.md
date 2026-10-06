# Bioinformatics challenges at the interface of biology and computer science

invokes an image pop-up of the hydropathy profiles presented by Liu et al. as part of Supplementary Figure S1 A. Clicking on the shaded hydropathy profile below (Figure 8.10 (d)) pops up a hydropathy profile for the sample genome (GCR2) using the same analysis software (DAS), allowing direct comparison of Liu et al.’s with the actual result from the TM prediction software– from which the manipulations are apparent in the Published Figure.

Clicking on the ‘pop out’ on the right-hand side of the play button brings the second blue highlighted region (Figure 8.10 (c)) pops up a new window containing multiple sequence alignment of GCR2 with homologous members of the Lanc-like enzyme family. The popped-out window is an interactive editor– it is therefore possible to scroll through the alignment and witness to, at first hand, the similarity these sequences share and, in particular, the occurrence of several conserved Gxx motifs, which are the canonical features of zinc-binding proteins.

Clicking on the play button brings the 3D structures shown in Figures 8.10 (c) and each of the static images with interactive molecular views, which can be zoomed in and out – grabbing part of the molecule allows controlled rotation of the views, or can be used to set the molecules spinning. As the alignment example above, clicking on the ‘pop out’ on the right-hand side of each of the play buttons pops the 3D molecular viewer out into a new window, which can then be re-sized and explored by their greater size, the popped out views are rather easier to manipulate than the in-frame views, hence the striking differences between the structures are easier to visualise.

Finally, clicking on the shaded panel in Figure 8.10 (f) invokes the UniProtKB/TrEMBL entry for GCR2. This allows comparison of the ‘current’ database entry (version 39 of F4EI1MS_ARATH at the time of writing) with the version that was at the time of publication of the 2009 Biochemical article (version 35 of Q9C929_ARATH). The latter bears the GPCR annotation in its description line, while the former bears the revised description line, ‘Lanc-like protein GCR2’, with alternative name ‘G-protein’ coupled receptor 2 beneath it.

# Making the animations works – behind the scenes

In the scenario, we saw how UD was able to animate different components of a static, composite image: to turn pictures of globular and membrane proteins into ‘live’ spinning in 3D, to force from an interactive alignment editor, and to allow additional images or information from a database to pop out of the page. A number of things had to happen behind the scenes to make these interactive features possible.

+   1. Invoking images of hydropathy profiles. In Figure 8.10 (a), a screen-grab of the hydropathy profile shown in Liu et al.’s Supplementary Figure S1 A was manually associated with a relevant portion of text (below), highlighted blue in the Figure 8.10 (a),

...we started searching the Arabidopsis genome and found a gene, GenBank GCR2 accession At1g52929 encoding a putative GPCR. Transmembrane structure prediction suggests that GCR2 is a membrane protein with seven transmembrane helices (fig. S1, A and B) (of ours).

To achieve the same result automatically would require a text-mining tool that was sufficiently sophisticated to recognise the assertion ‘GCR2 is a membrane protein with seven transmembrane helices’ (the sentence emphasised in the quote above), and