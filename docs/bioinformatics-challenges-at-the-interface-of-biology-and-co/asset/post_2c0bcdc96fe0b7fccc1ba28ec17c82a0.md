
# Chapter 1 Introduction

4 Which was the first enzyme whose amino acid sequence was determined?

+   A Insulin
B Ribonuclease
C Myoglobin
D Haemoglobin

5 Which was the first protein whose structure was determined?

+   A Insulin
B Ribonuclease
C Myoglobin
D Haemoglobin

6 Which of the following statements is true?

+   A The first collection of protein sequences was at the National Center for Biotechnology Information
B The first collection of protein sequences was made by Fred Sanger
C The first collection of protein sequences was the Atlas of Protein Sequence and Structure
D None of the above

7 Who was responsible for the invention of the Difference Engine?

+   A John Napier
B Charles Babbage
C Joseph Marie Jacquard
D George Forsythe

8 What is the smallest number that could be represented using the Babylonian counting scheme?

+   A One
B Two
C 'Seven'
D Zero

9 Binary representation was first conceived by:

+   A George Boole
B Pingala
C Alan Turing
D John Napier

10 Which of the following statements is true?

+   A There is a gap between the ability of computers to manipulate concepts and our desire to use them to manipulate binary numbers
B There is a gap between the ability of computers to manipulate primary numbers and our desire to use them to manipulate concepts
C There is a gap between the ability of computers to manipulate binary numbers and our desire to use them to manipulate concepts
D None of the above

## 1.8 Problems

+   1 Margaret Dayhoff was one of the pioneers of bioinformatics, actively working in the field in the 1960s, long before the discipline that we know today had been named. In Section 1.2.3, we described how she was involved in producing the Atlas of Protein Sequence and Structure, the first published compendium of protein sequences, one that went on to give life to one of the first protein sequence data-bases. In addition, she is known for two other pivotal contributions to bioinformatics. What were they?

+   2 The NCBI, established in 1988, became the new home of the USA’s first national nucleotide sequence database in October 1992. What was that database? How many sequences did the database contain when it was first released, and how many were contained in its first release under the auspices of the NCBI⁵ How many sequences does the database contain today?

+   3 This book is about the gaps we encounter when we explore the interface of bioinformatics and computer science. The nature and types of gaps we'll discuss are many and varied: some are subtle and small; others are large and frightening. What is the gap described by Fraser and Dunstan in their 2010 article (The BMJ, 342, 1314–15), and why is it especially disturbing?

> ⁵Hints: http://www.youtube.com/watch?v=mn98mokVAXI; http://www.ncbi.nlm.nih.gov/genbank/statistics

## Chapter 2

## The biological context

### 2.1 Overview

In this chapter, we look at some of the data-types and biological concepts that provide the foundations of the field of bioinformatics. We review the fundamental molecules of biology, their molecular building-blocks, the alphabets we use to describe, and their physicochemical properties and structural characteristics. We also provide a reminder of the processes of transcription and translation, and their relevance to genome-sequencing projects.

By the end of this, you should be able to list the nucleotide and amino acid building-blocks of nucleic acids and proteins respectively, and you should have an appreciation of how to translate a nucleotide sequence in six reading frames; you should also have an insight into the current scale of biological data production.

### 2.2 Biological data-types and concepts

#### 2.2.1 Diversity of biological data-types

Bioinformaticians deal with large and incredibly diverse range of inter-related data types. To give an idea, we can begin by thinking about the fundamental macromolecules of life, the corners of molecular biology: nucleic acids (deoxyribonucleic acid (DNA) and ribonucleic acid (RNA)) and proteins. If we consider types of data related to nucleic acids, then we can count properties, the genomes they encode, the nucleotide bases that make up their sequences, their genetic mutations, and so on. Thinking about protein-related data, on the other hand, we can enumerate their component amino acids, the linear sequences and 3D structures they form, and the molecules or substrates they interact with to express their native functions.

At another level, we can think of protein or nucleic acid sequences as belonging to related families that share, for example, evolutionarily conserved regions suggestive of possible structural or functional roles. We can compare such sequences by creating multiple alignments, we can create diagnostic models of their conserved features, and we can chart their evolutionary histories by building phylogenetic trees. If we analyse the similarities and differences between closely related amino acid or nucleotide sequences, we may find that some changes lead to disease states. We may then gather information on the genes and proteins that might be involved in these pathogenic processes, and the drugs that might need to be created for them – this would involve collating data relating to their therapeutic efficacy (details of Absorption, Distribution, Metabolism, Excretion, Toxicity (ADME-T)) and to the outcomes of their use in clinical trials.

In terms of the data types introduced in bioinformatics, the above is just the tip of an enormous iceberg. A great deal of information relating to this diverse array of data is presented in the biomedical literature. In addition, through systematic efforts of researchers and bureaucrats over the last 40 years, chunks of this information have also been gathered up and stored in databases. We'll discuss some of these databases in detail later, in Chapter 3. For now, though, to set the scene for these discussions, we'll begin by introducing some of the fundamental concepts and building-blocks of molecular biology.

#### 2.2.2 The central dogma

Today, we tend to take the role of DNA for granted. Yet the identity and nature of the cell's hereditary material were not known before the 1950s: at that time, some scientists believed proteins provided the information for inheritance. Subsequent experiments with a group of viruses that parasite bacteria (so-called bacteriophages – simple organisms that comprised particles of nucleic acid wrapped in protein shells) went on to show that the infective material was largely DNA (Hershey and Chase, 1952). Nevertheless, just how DNA might mediate inheritance was not obvious, at least because no plausible mechanism was known. The first hint came in 1953 when, proposing their radical new idea for the structure of DNA, Watson and Crick has not escaped our notice that the specific [base] pairing we have postulated immediately suggests a possible copying mechanism for the genetic material (Watson and Crick, 1953).

From this rather beginning, Francis Crick went on to propose how the genetic information carried in nucleic acids could be transferred to proteins. In the late 1960s, he formulated his ideas in what he called the central dogma of molecular biology, essentially stating that the transfer of information encoded in DNA is via the sequence of RNA, and then to the sequence of proteins (and not from protein to protein, or from protein to nucleic acid). Despite being a major (and, at the time) over-simplification (Crick, 1970), the central dogma is nevertheless a useful concept for understanding the basic principles of the genetics of proteins.

The molecular sequences of DNA and RNA each have different chemical components. So, in practice, for this 'simple' genetic transfer to work, the information in a sequence of DNA must first be 'transcribed' into the appropriate chemical sequence of RNA, which must be 'translated' into the relevant chemical sequence of proteins. This step is illustrated schematically in Figure 2.1. We use the term 'transcription' to describe the first step, because it involves re-writing one sequence of nucleotides

¹https://www.youtube.com/watch?v=41_Ne5mS2ls
