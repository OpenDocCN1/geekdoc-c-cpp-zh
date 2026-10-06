
## Chapter 5 The gap

patterned the protein as a G protein-coupled receptor belonging to the opsin family. Up to this, the situation seems straightforward — the protein looks like a blue-sensitive opsin.

Later that year, however, the annotation was revised (entry version 4) with further information regarding the tissue specificity of the protein: *i.e.*, it resides in rod-shaped photoreceptor cells, whose role is to mediate vision in dim light. What, then, is the function of the protein and what does this extra effort mean? Opsins, the pigments that normally mediate colour vision, are found in cone-shaped photoreceptors; rhodopsins, on the other hand, which mediate achromatic vision in dim light, are found in **rod photoreceptors**. How could this protein be a cone-photoreceptor opsin, but reside in rod-shaped cells? An Pfam cross-reference also appears in this database record, but doesn't help us resolve our functional dilemma, because Pfam *7TM_1* makes generic donations for rhodopsin-like GPCRs — it provides no family or subfamily insights.

This conflicting functional annotation persists in the 'current' UniProtKB version 73. This entry, however, we now find 14 family and domain database cross-references: one each from PROSITE and Pfam, some from InterPro and three from PRINTS. The additional evidence from PRINTS and, from Here, suggests that this protein has sequence characteristics that are rhodopsin-like rather than blue-sensitive opsin-like (*n.b.*, PRINTS also contains a blue-sensitive opsin fingerprint, but the sequence doesn't match it, according to the database cross-references listed here). So, is it an opsin or rhodopsin?

Further could be found by referring to these database entries specifically, Archer and Hirano, 1996. Here, the authors explain that the Cong has a pure retina with a visual pigment maximally sensitive to light. The protein is found in rod photoreceptor cells (not cones, as suggested by the UniProtKB/SwissProt annotation), and *does* have an amino acid sequence characteristic of rhodopsins, which has undergone spectral fine-tuning to create a rhodopsin-like class of receptors with the functional specificity of blue-sensitive pigments.

In this fascinating scenario, we've seen a particular protein sequence undergone some degree of functional 'finesning' — the high-level function has remained the same (photception), but the specificity has been altered such that the protein appears to have the 'wrong' sequence for that function!

A more subtle, and perhaps more taxing arises when we find the same protein possessing very different functions in different contexts — this phenomenon, termed gene sharing or 'protein moonlighting'⁵³,, is explored in detail in Box 5.5. Unravelling how protein sequences can share high degrees of similarity yet exhibit divergent or different functions is a challenge for humans; injecting the spark of intelligence to allow computers to reason with the data and make the same leap in understanding is an undertaking beyond what can be achieved at present.

> ⁵³http://en.wikipedia.org/wiki/Protein_moonlighting

## Box 5 Protein moonlight

In 1987, members of a family of what were considered straightforward proteins – crystallins – were shown to exhibit taxon-specific functional differences: they were not only the components of vertebrate eye, but also behave as enzymes (Wistow and Piatorski, 1987). In fact, Wistow and Piatorski showed that δ-crystallin is -70 per cent to human argosine lyase – an idea of how these sequences are seen by the alignment in Figure 5.14 (which includes turkey, chicken and δ-crystallins, and duck, chicken and goose argosine lyases – the sequences are so similar it's extremely difficult to tell them apart). Adding to the complexity, note that UnProtKB labels ARYL2_CHICK and ARYL1_CHICK (P05083) chicken argosine lyase, which was originally named anapl (P02521) which is δ-crystallin.

| ID | Sequence |
| :--- | :--- |
| ARYL1_MELGA | QQQKNNDDSLEISKAGVFRGRLAIMLVKG |
| ARYL1_CHICK | QQQKNNDDSLEISKAGVFRGRLASISMLVKG |
| ARYL1_ANAP | QQQKNNDDSLEISKAGVFGGRLASISMLVKG |
| ARYL2_ANAP | QQQKNNDDSLEISKAGVFGGRLASISMLVKG |
| ARYL2_CHICK | QQQKNNDDSLEISKAGVFGGRLASISMLVKG |
| ARYL2_ANSAN | QQQKNNDDSLEISKAGVFGGRLASISMLVKG |
| Consensus | QQQKNNDDSLEISKAGVFRGRALMLVKG |

Figure 5.14
Alignment of selected avian δ-crystallins and argosine lyases.

What made this observation particularly striking was that the crystallin sequences were similar to those of enzymes, but they were actually proteins of the same genes (Piatorski and Wistow, 1989). Piatorski and Wistow demonstrated this phenomenon, whereby a gene may encode a protein that has two entirely different functions (‘gene sharing’; in order to differentiate it through mechanisms as alternative splicing, post-translational processing, gene fusion, or exon shuffling, which were known to be generated from the same protein. Gene sharing allows both functions to occur and maintain an alternative function, without the necessity for gene duplication and loss of the original, primary function (Piatorski and Wistow, 1989). For these proteins, then, gene sequences required to maintain their respective catalytic functions and the intermolecular interactions required for tens affinity.

Following the revelation of these findings, many examples of proteins with two or more different functions were discovered – which were subsequently renamed ‘moonlighting proteins’, by people who perform multiple tasks (Jeffery, 1999; Huberts et al., 2010). The listing of such proteins revealed that their functions can vary in response to changes in oligomeric state, cellular localisation or cell type, or to cellular concentrations of ligands, substrates or costly; however, a combination of these methods may be used by proteins to switch between.

Various consequences arise from these observations. First, they compel our understanding of concepts such as gene expression and protein function – the idea that one gene encodes a single protein with a single function is clearly over-simplistic. However, as it’s possible for a moonlighting protein to have an unexpected link, say between metabolic and signalling pathways, this has profound implications not just for systems biology but for biomedical science in particular – a moonlighting function could conceivably explain the correlation of protein functions with that of disease, and cause a new drug, to target the wrong

function, with potentially toxic consequences (Jeffery, 2004). Finally, in the context of genome annotation, it shows that a well known protein may harbour other, as yet unknown, functions, and sequences that appear to be almost identical may not have the same function - i.e., the things we know, we may not know, because our knowledge may be incomplete; and the things we've found, may not be what we think they are, because they might be moonlighting something else; Or as Huberts et al., put.

Moonlighting is a phenomenon that illustrates nature ingenuity. It is a source of inspiration that should remind scientists to always keep the unexpected in mind, even on familiar ground (Huberts et al., 2010).

This provides us with a salutary to think ever more carefully about the functions we find associated with proteins in biological databases, the vast majority which are determined by automatic annotation transfer similarity searches, and inheritance of GO terms; us to keep thinking critically, remain alert to the problems that are not as simple as they first appear; and it also continues with the question of how useful our simple compute-annotation pipelines are likely to be true, as we discover more and more about the incredible complexity of molecular functions. Perhaps is why the guardians of UniProt and a number of our collaborators are in the process of trying to create a new Gold Standard Database (GDB), the functions of whose proteins have been determined experimentally and whose exact nucleotide/protein sequences are known for those precisely experimentally functions; the proteins will also be accompanied by literature references so the source of this information can be traced.

## 5.11 Functions of domains, modules and their parent proteins

Some of the issues we've just discussed relate to the evolutionary fate of genes that acquire new functional specificities in different species. Another complication to consider is what happens when we swap a gene-family or sequence-based perspective for a structural one, and instead think in terms of 'domain' families. The issue is that, domain families share sequence and structural similarity, they are likely to encompass diverse gene families - i.e., they don't shed light on their constituent functional strata, but focus the functional spotlight just on the domain. It is important to understand the implications of this, especially when we consider resources like InterPro. As we've seen, InterPro attempts to equate 'families' from a more defined resources, however, the merged entries into which we infer the functions of newly defined entries adopt different sequence and domain-based views, rationalising their constituent families and arriving at a common understanding of functions isnt straightforward, as highlighted by InterPro family IPR017452.

A number of problems can arise if we don't deal effectively with the domain and/ 'modular' nature of some proteins. Modules are autonomous functioning units that have used protein building-blocks to create a variety of functions on a parent protein, either by using multiple instances of the same module, or by using combinations of a variety of different modules to form mosaics. This may present difficulties for database searches, because the best hit could be a match to a single domain within a multidomain protein or to a single module within a mosaic protein. In such cases, inheriting
