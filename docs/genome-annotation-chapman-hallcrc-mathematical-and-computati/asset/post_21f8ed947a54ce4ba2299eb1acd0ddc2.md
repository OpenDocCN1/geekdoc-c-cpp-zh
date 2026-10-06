
# 76 Genome Annotation

![](img/7da802df4d7c0829a4a41adf9acaf30d_98_0.png)

5.2 Viewing and editing contigs with the Staden Package. After sequence assembly from multiple trace files by the Gap4 package, contigs are shown in Contig Selector (top). Upon selecting a contig (the leftmost one in this case), Cont Editor shows the contig information including the reads used in constructing the consensus (middle), which can be manually edited. The trace around a base of a particular region can be viewed to aid in the editing process (bottom).

file, the trimming of the files to extract the useful information (after the removal of vector sequences, contaminating host DNA sequence, etc.) and the assembly of this information into contiguous sequences (i.e., contigs). In addition, the package provided many other tools, which were developed over time to assist with special tasks. Figure 5.2 shows an example of running Staden packages to build contigs from multiple trace files.

The Staden Package was built in a modular fashion, therefore other tools could be added to the data processing pipeline. Notable here are the Phred and Phrap tools (Ewing and Green, 1998; Ewing et al., 1998), which were created by Phil Green at the University of Washington. Phred allowed the creation of quality assessments for trace data and became more or less the facto standard in this field until next-generation automated DNA sequencing over.

The major tools in the Staden Package (pregap, the tool to manipulate trace data; and gap, the genome assembly program) gained graphical interfaces over time. This was essential, as the sequence assembly could be linked back to the trace data to verify sequence information and resolve any ambiguities through visual inspection.

# 5.3.6 GeneSkipper

The early sequencing efforts needed tools that were capable of analyzing larger contiguous sequence files (contigs) and providing additional information and graphical representations, which reflected the sequencing progress. EMBL Heidelberg was one of the sites involved in the Saccharomyces Yeast Genome Project and therefore Christian Schwager and his team at EMBL created a Windows-based software tool GeneSkipper, which was one of the first tools to graphically represent an analysis of sequenced contigs (i.e., the six protein translation frames and potentially coding regions).

# 5.3.7 Sequencer

Apple Macintosh computers have always been considered to provide one of the most user-friendly interfaces in the computer industry. Eventually, Howard Cash founded a company called GeneCodes, which created a sequence assembly system for the Macintosh environment, called Sequencer (www.sequencer.com). Over time, Windows platform support has been added. This system is still being sold to this date and in use many laboratories around the world.

# 5.4 FROM FAST FILES TO ANNOTATED GENOMES

The Staden Package, GeneSkipper, and Sequencer all included very limited provisions for the genome annotation task. Essentially, they took raw sequence files in, and produced assembled sequence in FAST format (or some other format) as output. Therefore, dedicated tools were developed over time, initially to collect the annotation information, which was being created in a manual or semiautomated fashion (such as the ACeDB family of tools) and later on fully automated tools.

# 5.4.1 ACDeDB

The Arabidopsis thaliana and Caenorhabditis elegans sequencing projects yielded AtDB (an Arabidopsis thaliana database) (Cherry et al., 1992) and ACDeDB (a Caenorhabditis elegans database) (Cherry and Cartinhour, 1994), which collected the information related to the genome annotation and graphically represented this information. Like GeneSkipper, these systems were created at the dawn of widespread Internet access. The genome notations created with the ACeDB system could be downloaded and installed on UNIX machines (others might have been supported early on as well). The maintenance of this system was complicated and therefore creating a data-base for other genomes was undertaken in only a few cases, such as some human chromosomes and Schizosomyces pombe. Especially, ACeDB handled genomic information best, as there was no notion of changing sequence states (from the first assembly to the finished genome) built into the workflow. ACeDB was retrofitted with Web capability later, but the success of this development was rather limited. Still, the systems have a presence to this day and a collection of these is currently maintained at the Sanger Center in the United Kingdom (www.acedb.org).

# 5.4.2 One Genome Project, the Beginning of Three Genome Annotation Systems

In the early days of complete genome sequencing, researchers usually kept the DNA sequence under wraps until it had been published. This, of course, prevented the community at large from access to these sequences and hence there was very little sequence information to go around, which could be used as an example while building bioinformatics could be used to analyze and annotate large stretches of genomic sequence. There were a few notable differences, including the Myoplasma capriculum sequencing project (Dolan et al., 1995). The investigators opened access to early versions of the sequence in draft-mat. This eventually led to the creation of at least three software packages that played a role in the automated genome analysis and annotation field.

To this day, two of the systems, PEDANT (Frishman et al., 2001) and MAGPIE (Gaaster and Sensen, 1996), are still in use, while the third, which was a commercial product called Bioscout, disappeared with the demise of LION Biosciences. PEDANT is now part of the offerings of Biomatik AG in Munich, Germany, where MAGPIE is an open source system, which can be downloaded freely from Sourceforge. All three systems initially produced tabular HTML-based output of the functional assignments to genomic regions. Over time, the systems evolved and also added graphical representations of the analysis results. Some of the latest versions of the graphics-based tools will be introduced in more detail in subsequent chapters.

# 5.5 CONCLUSION

Bioinformatics as a research field is less than 40 years old. Within this timeframe, many useful stand-alone tools were developed, which can be used to characterize sequence information. Over time, they were combined into analysis pipelines, which can provide automated genome analysis and annotation for sequences. Initially, the annotations were listed in tabular format, but over time it became evident that graphical representations were more useful for most users of the annotation pipelines. Bioinformatics has truly adopted the Internet as the vehicle that is used to share the results of genome annotations. Almost every technological approach, from the early HTML-based annotation engines to the latest XML-based systems, has been tried over time. Today, we have efficient tools for the analysis and annotation of even the largest genomes, and systems for comparative approaches of even hundreds of thousands of genomes the size of the human genome are under development, as discussed in subsequent chapters of this book.

# REFERENCES

- Altschul, S.F., Gish, W., Miller, W., Myers, E.W., Lipman, D.J. 1990. Basic local alignment search tool. J. Mol. Biol. 5:403–410.
- Benson, D., Lipman, D.J., Ostvall, J. 1993. GenBank. Nucleic Acids Res. 1:2966–2965.
- Bigelow, C.C. 1967. On the hydrophobicity of proteins and the relation between it and protein structure. J. Theor. Biol. 16:187–211.
- Cherry, J.M., Cartinhour, S.W. 1994. ACEDB, a tool for biological information. In Automated DNA Sequencing and Analysis, eds M. Adams, C. Fields, C. Veter, 347–356. San Diego, CA: Academic Press.
- Cherry, J.M., Cartinhour, S.W., Goodman, H.M. 1992. AtDB, in Arabidopsis database. Mol. Biol. Rep. 10:308–309.
- Dear, S., State, R. 1992. A standard file format for data from DNA sequencing instruments. DNA Seq. 3:107–110.
- Devereux, J., Haeberli, P., Smithies, O. 1984. A comprehensive set of sequence analysis programs for the VAX. Nucleic Acids Res. 12:387–395.
- Dolan, M., Allen, M.S., Gilbert, W., Gillett, P. 1995. Large-scale genomic sequencing: Optimization of genomic chemical sequencing reactions. Biotechnics 19:264–270–274.
- Doolittle, R.F. 1981. Similar amino acid sequences: chance or common ancestry? Science 214:149–159.
- Edman, P. 1949. A method for the determination of amino acid sequence in peptides. Arch. Biochem. 22:475.
