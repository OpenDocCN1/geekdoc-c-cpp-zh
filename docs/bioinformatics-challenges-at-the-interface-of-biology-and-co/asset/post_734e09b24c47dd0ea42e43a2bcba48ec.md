
# Chapter 8 Linking data and scientific literature

291

structure of the original sentence: where is 'the cat'? It's 'on the mat'. What is the mat? A And so on. So far so good; real language is seldom so simple and unambiguous.

Let now examine an idiomatic pathological case at the other extreme. The sentence, 'Buffalo buffalo Buffalo buffalo buffalo Buffalo Buffalo buffalo' is a popular illustration of a seemingly intractable piece of grammatically and somewhat correct English. The capitalisations offer a clue to the meaning of some instances of the 'buffalo', being used here as a proper noun – the name of a North American city. It is also used in its more commonly known form as the name of a bison-like herd animal. The most obscure use of 'buffalo' is as a verb, meaning something like bully or harness? Thus, deduced, the heavily contrived sentence reveals that 'Buffalo bison buffalo Buffalo than Buffalo bison, also Buffalo bison'. For a human reader, accurate parsing of the sentence requires a sound understanding of grammar, and access to a good dictionary (and, arguably), a little geographical knowledge); for a computer to devolute the sentence, a parse tree to show in Figure 8.4 would be required. Even slightly more realistic phrases and sentences, such as 'My hair need cutting daddy', 'Stolen dog found using Facebook' (BBC News), 'Round tables', 'Fruit flies like a banana', and many others like them, pose interpreting for machine interpretation.

We might expect scientific rigour to encourage prose that's unambiguous and formally structured. However, although it may be that extracting meaning from scientific text is perhaps more straightforward than poetry and other forms of creative writing, the scientific literature nonetheless poses problems of its own what it makes hard for machines to penetrate; automating the recovery of meaning from scientific writing, post hoc, thereafter remains challenging. Let's take a (fairly randomly selected) sentence from a scientific article:

In the present paper, we report the crystal structure of LpGT, which reveals a GT-A fold, demonstrating how the enzyme interacts with UDP-glucose (Hurtado-Guerrero et al., 2010).

![](img/1af42ff402ef4720886c50af0bb8e9b5_310_0.png)

> ^6http://en.wikipedia.org/wiki/Buffalo_buffalo_Buffalo_buffalo_buffalo_Buffalo_buffalo

# Bioinformatics challenges at the interface of biology and computer science

For the reader, the meaning is clear enough: the authors are describing the crystal structure of a molecule (enzyme), which they refer to LpGT; they claim that this molecule has a GT-A fold, and that this GT-A fold enables the enzyme to interact with another molecule, UDP-glucose; for computation to achieve the same level of understanding is much trickier. Leaving aside the biology for a moment, consider the grammatical structure (the syntax) of the sentence. There are three commas: these could form a list, surround a sub-clause, or be aesthetic. However, there could be many interpretation of these, with each combination yielding a different interpretation of the sentence (and note, we've presented a simple sentence that we're taking to be grammatically correct, it's not a safe assertion for innumerable sentences published in the scientific literature - if you need convincing, look at some of those highlighted in Box 8.3). Regardless, for humans, it's quite easy to spot what the authors intended; but for a machine, even this syntactic construct poses problems.

Unambiguously recognizing entities in scientific text too to be horribly difficult. In this simple sentence, for example we have three biological concepts: LpGT, ‘GT-A fold’ and ‘UDP-glucose’. The authors define LpGT elsewhere in the paper to be ‘L. pneumophila glycosyltransferase’, and in a footnote that states, ‘The structural-coordinates reported will appear in the Protein Data Bank under accession codes 2WZF and 2WZG’, which they indeed do not. For a human, the link between the article’s narrative and the electronic description of the molecules in years

> Box 8.3 The literature isn't always as intelligible as it should

the increased rate of scientific articles has placed significant strain on the processing process, so much that, in cases, levels of editorial processing are perhaps no longer what they used to be. In the following, randomly chosen, if we insert a few commas and/or hyphens, we can work out the intended meaning of the sentences; however, they are trickier than – if humans find them difficult to parse, how much more difficult would it be for a text-mining algorithm to ascertain their meaning:

- Treatment of cells from newly diagnosed CML patients in chronic phase as BCR-ABL cells with itinib inhibitedF8 transcription (Weight et al., 2014);
- The in vitro blood stage amastigoid activity of a series of allylated chalcones from the licochalone was investigated against chloroquine (CQ) sensitive PSD7 and CQ resistant PINDO strains of Plasmodium falciparum using SYBR Green I assay (Sharma et al., 2014);
- Literatures and studies published on anti-leishmanial drug resistance, new discovery for leishmanial resistance etc., in PubMed, Medina and Google search and reviewed thoroughly (Mohapatra, 2014);
- The sampling location in this study is a tourism hotspot with great human mobility, which may result in the tetr resistance gene or bacteria released from human beings into the environment (water and soil) in Tibet (Li et al., 2014);
- ‘Human castration resistant prostate cancer rather than decreased 5-reductase activity’ (Kosaka et al., 2013).

> 7http://www.rcsg.org/pdb/explore.do?structureId=2WZF
> 8http://www.rcsg.org/pdb/explore.do?structureId=2WZG

# Chapter 8 Linking data and scientific literature

293

The PDB may be clear enough; but for a machine to join together these disconnected fragments of text to make this connection is non-trivial. It muddies the waters further, it's common in some fields of biology, for example, to refer to a gene by its given name, but by its protein product; and as we saw in Chapter 5, the ‘same' gene in different species can have different names. For a scientist in a given field, the translation from protein-to-name may be implicit; for a machine, it’s deeply confusing. Terminology varies dramatically from domain to domain (even the ‘word’, used here in a ‘computer science’ to mean ‘scientific field’), with different connotations in the life sciences, where it can be interpreted as referring to various biological concepts.

If unambiguous ‘entity’ recognition is hard for computers, extracting scientific assertions at a level that’s sufficiently straightforward to be processed automatically – e.g., ‘A does to C’ is easier. The difficulties are exacerbated by what’s generally regarded as publishing ‘gameplay’. For example, a scientist may have concluded that A does to C; however, making such an assertion in an article is risky. To validate, the assertion must be in context (A does B to C in the context of D and under conditions E); the scientist, fearing that ‘over claiming’ (or, worse, contradicting the opinion of an anonymous reviewer) might cause the article to be rejected, may strategically soften the claim: ‘it is possible, that within the limits of our experimental conditions, E and C sometimes interact in a B-like way in a D-like context’. This practise is referred to as ‘hedging.’ In following sentences, extracted from a range of scientific articles, we emphasised the use of hedging phrases:

- Targets suggest a possible indication for gene products produced with calcvarial growth and homeostasis as well as craniostosis (Cray et al., 2013);
- Preirradiation treatment of TCE significantly reduced LPO at all the autopsy intervals in comparison to irradiated control, which testifies to our belief that one of the possible mechanisms of radioprotection by TCE was owing to the scavenging of free radicals by radiation exposure and the formation of endoperoxidation (Sharma et al., 2011);
- Expression patterns of CYC-like genes are suggestive of participation in the control of pseudanthium, in a manner analogous to the distantly related Asteraceae (Claßen-Bockhoff et al., 2013);
- Micromolar patterns of topical caffeine have been found to be significantly effective in inhibiting the formation of galactose cataract, strongly suggesting its possible usefulness against diabetic cataracts (Varma et al., 2010);

In some cases, hedged terms even appear in the article title, as in the following examples:

- An evaluation of the possible interaction of gastric acid suppressing medication and the EGFR tyrosine kinase inhibitor erlotinib (Hilton et al., 2013);
- Severe hypoglycemia due to possible interaction between glibenclamide and sorafenib in a patient with hepatocellular carcinoma (Holstein et al., 2013);
- The unique pseudanthium of Actinodium (Myrtaceae) – morphological reinvestigation and possible regulation by CYCLODEA-like genes (Claßen-Bockhoff et al., 2013).
