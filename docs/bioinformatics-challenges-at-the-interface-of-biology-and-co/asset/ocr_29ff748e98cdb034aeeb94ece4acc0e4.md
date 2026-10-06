serve us well. The matching becomes more complex, or the XML is no longer under control, regular expressions fails to be useful, and a proper XML parser should be used.

+   5 The BLAST algorithm exhibits a number of qualities that make it difficult to implement in generic languages. The heavy use of matrix calculations, the large (and ever-increasing) data-sets over which it runs, and the repetitive nature of the algorithm make the task difficult to do quickly. We therefore need to choose a language that will allow us to optimise as much of the algorithm as possible, and that that relatively low-level access to processing hardware.

Matrix calculations can be done in optimised on some processors, but if only the language has access to such methods, which discounts most scripting and interpreted languages. In order to have very control over exactly what memory is used, the ability to work around it is also needed. This leaves only the low-level languages such as C and C++, languages that hide any (or much) complexity from the user.

There is, however, a readily available class of processors that excel in massively repetitive tasks, including such as matrix multiplication: Graphical Units (GPUs). These processors, designed primarily for dealing with 2D and 3D graphics tasks, provide the right kind of tools to implement the BLAST algorithm. Programming them with languages such as NVIDIA's CUDA, or the Computing Language (OpenCL), is not a simple task, but done correctly, can speed up the execution of the BLAST algorithm by an order of magnitude or more.

# Chapter 7

+   1 The MD5 ('Message Digest Version 5') hashing algorithm takes a variable-length sequence of 512-bit blocks, and using some fairly-hard math, generates a 128-bit 'signature' (that's represented as a 32-bit hexadecimal number). Assuming that we are encoding amino acids as 8-bit characters, which means 64 amino acids per block, with some padding necessary to make up the block length. The intention of the algorithm was that no two different inputs give the same result, so the signature could be used as a reliable and compact checksum for chunks of data.

For example, if we have a case for rhodopsin (P02699) that consisted of the characters

```
MNGTEGFNIVFSNKTGVRSPFEAPQQYLAWPQFSMAYFLLIM
GFIPFLTLTVYHKKLTPYINLNMADVLVMQGFGFTTTTYLMS
GFYPGPFTCQHRLLATIGSLVLAIERYVVCKMSNFNRGE
NHAMAGAGTVMFTAAPLQLQWSYIPEGMQCSCGQIYTPHETEEN
ESFVFTMFPVHLLPIVPHLCQQTYFTVKQEEAAQQSATTAKEKQ
TRIMYMVIAELICVPYQAGYFTIFTRQSDQGFIPMTPAFAKTSAV
```

in a text file containing these characters (i.e., no line breaks or extraneous whitespace), and the MD5 algorithm over this, we would get the result 2277dd9e8b2fc17d01908fb33fa8, represented in hexadecimal, as a signature. While there is no way of reversing this process to turn the signature back