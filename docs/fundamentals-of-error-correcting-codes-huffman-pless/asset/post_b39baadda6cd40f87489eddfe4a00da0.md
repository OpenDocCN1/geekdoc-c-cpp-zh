
codes, are defined and some of their properties are given. The connection between codes and lattices is developed in the final section of the chapter.

The theory of the covering radius of a code, first introduced in Chapter 1, is the topic of Chapter 11. The covering radii of BCH codes, Reed–Muller codes, self-dual codes, and subcodes are examined. The length function, a basic tool in finding bounds on the covering radius, is presented along with many of its properties.

Chapter 12 examines linear codes over the ring Z4 of integers modulo 4. The theory of these codes is compared and contrasted with the theory of linear codes over fields. Cyclic, quadratic residue, and self-dual linear codes over Z4 are defined and analyzed. The nonlinear binary Kerdock and Preparata codes are presented as the Gray image of certain linear codes over Z4, an amazing connection that explains many of the remarkable properties of these nonlinear codes. To study these codes, Galois rings are defined, analogously to extension fields of the binary field.

Chapter 13 presents a brief introduction to algebraic geometry which is sufficient for a basic understanding of algebraic geometry codes. Goppa codes, generalized Reed–Solomon codes, and generalized Reed–Muller codes can be realized as algebraic geometry codes. A family of algebraic geometry codes has been shown to exceed the Gilbert–Varshamov Bound, a result that many believed was not possible.

Until Chapter 14, the codes considered were block codes where encoding depended only upon the current message. In Chapter 14 we look at binary convolutional codes where each codeword depends not only on the current message but on some messages in the past as well. These codes are studied as linear codes over the infinite field of binary rational functions. State and trellis diagrams are developed for the Viterbi Algorithm, one of the main decoding algorithms for convolutional codes. Their generator matrices and free distance are examined.

Chapter 15 concludes the textbook with a look at soft decision and iterative decoding. Until this point, we had only examined hard decision decoding. We begin with a more detailed look at communication channels, particularly those subject to additive white Gaussian noise. A soft decision Viterbi decoding algorithm is developed for convolutional codes. Low density parity check codes and turbo codes are defined and a number of decoders for these codes are examined. The text concludes with a brief history of the application of codes to deep space exploration.

The following chapters and sections of this book are recommended as an introductory one-semester course in coding theory:

- Chapter 1 (except Section 1.7),
- Sections 2.1, 2.3.4, 2.4, 2.7–2.9,
- Chapter 3 (except Section 3.8),
- Chapter 4 (except Sections 4.6 and 4.7),
- Chapter 5 (except Sections 5.4.3, 5.4.4, 5.5, and 5.6), and
- Sections 7.1–7.3.

If it is unlikely that a subsequent course in coding theory will be taught, the material in Chapter 7 can be replaced by the last two sections of Chapter 5. This material will show how a compact disc is encoded and decoded, presenting a nice real-world application that students can relate to.

For subsequent semesters of coding theory, we suggest a combination of some of the following blocks of material. With each block we have included sections that will hopefully make the blocks self-contained under the assumption that the first course given above has been completed. Certainly other blocks are possible. A semester can be made up of more than one block. Later we give individual chapters or sections that stand alone and can be used in conjunction with each other or with some of these blocks. The sections and chapters are listed in the order they should be covered.

- Sections 1.7, 8.1–8.4, 9.1–9.7, and Chapter 10. Sections 8.1–8.4 of this block present the essential material relating block designs to codes with particular emphasis on designs arising from self-dual codes. The material from Chapter 9 gives an in-depth study of self-dual codes with connections to designs. Chapter 10 studies the Golay codes and hexacode in great detail, again using designs to help in the analysis. Section 2.11 can be added to this block as the binary Golay codes are lexicodes.

- Sections 1.7, 7.4–7.10, Chapters 8, 9, and 10, and Section 2.11. This is an extension of the above block with more on designs from codes and codes from designs. It also looks at weight distributions in more depth, part of which is required in Section 9.12. Codes closely related to self-dual codes are also examined. This block may require an entire semester.

- Sections 4.6, 5.4.3, 5.4.4, 5.5.5, 5.6, and Chapters 14 and 15. This block covers most of the decoding algorithms described in the text but not studied in the first course, including both hard and soft decision decoding. It also introduces the important classes of convolutional and turbo codes that are used in many applications particularly in deep space communication. This would be an excellent block for engineering students or others interested in applications.

- Sections 2.2, 2.3, 2.5, 2.6, 2.10, and Chapter 13. This block finishes the nonasymptotic bounds not covered in the first course and presents the asymptotic versions of these bounds. The algebraic geometry codes and Goppa codes are important for, among other reasons, their relationship to the bounds on families of codes.

- Sections 1.7 and Chapters 6 and 12. This block studies two families of codes extensively: duadic codes, which include quadratic residue codes, and linear codes over Z4. There is some overlap between the two chapters to warrant studying them together. When presenting Section 12.5.1, ideas from Section 9.6 should be discussed. Similarly is helpful to examine Section 10.6 before presenting Section 12.5.3.

The following mini-blocks and chapters could be used in conjunction with one another or with the above blocks to construct a one-semester course.

- Section 1.7 and Chapter 6. Chapter 6 can stand alone after Section 1.7 is covered.

- Sections 1.7, 8.1–8.4, Chapter 10, and Section 2.11. This mini-block gives an in-depth study of the Golay codes and hexacode with the prerequisite material on designs covered first.

- Section 1.7 and Chapter 12. After Section 1.7 is covered, Chapter 12 can be used alone with the exception of Sections 12.4 and 12.5. Section 12.4 can either be omitted or supplemented with material from Section 6.6. Section 12.5 can either be skipped or supplemented with material from Sections 9.6 and 10.6.

- Chapter 11. This chapter can stand alone.

- Chapter 14. This chapter can stand alone.

## Acknowledgments

The authors would like to thank a number of people for their advice and suggestions for this book. Philippe Gaborit tested portions of the text in its earliest form in a coding theory course he taught at the University of Illinois at Chicago resulting in many helpful insights. Philippe also provided some of the data used in the tables in Chapter 6. Judy Walker's monograph [343] on algebraic geometry codes was invaluable when we wrote Chapter 13; Judy kindly read this chapter and offered many helpful suggestions. Ian Blake and Frank Kschischang read and critiqued Chapters 14 and 15 providing valuable direction. Bob McEliece provided data for some of the figures in Chapter 15. The authors also wish to thank the staff and associates of Cambridge University Press for their valuable assistance with production of this book. In particular we thank editorial manager Dr. Philip Meylor, copy editor Dr. Lesley J. Thomas, and production editor Ms. Lucille Murby. Finally, the authors would like to thank their students in coding theory courses whose questions and comments helped refine the text. In particular Jon Lark Kim at the University of Illinois at Chicago and Robyn Canning at Loyola University of Chicago were most helpful.

We have taken great care to read and reread the text, check the examples, and work the exercises in an attempt to eliminate errors. As with all texts, errors are still likely to exist. The authors welcome corrections to any that the readers find. We can be reached at our e-mail addresses below.

W. Cary Huffman
wch@math.luc.edu

Vera Pless
pless@math.uic.edu

February 1, 2003
