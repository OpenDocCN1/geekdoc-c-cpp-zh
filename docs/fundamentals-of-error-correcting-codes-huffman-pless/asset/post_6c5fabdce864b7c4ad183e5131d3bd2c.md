
## 8 Designs
- 8.1 t-designs 291
- 8.2 Intersection numbers 295
- 8.3 Complementary, derived, and residual designs 298
- 8.4 The Assmus–Mattson Theorem 303
- 8.5 Codes from symmetric 2-designs 308
- 8.6 Projective planes 315
- 8.7 Cyclic projective planes 321
- 8.8 The nonexistence of a projective plane of order 10 329
- 8.9 Hadamard matrices and designs 330

## 9 Self-dual codes
- 9.1 The Gleason–Pierce–Ward Theorem 338
- 9.2 Gleason polynomials 340
- 9.3 Upper bounds 344
- 9.4 The Balance Principle and the shadow 351
- 9.5 Counting self-orthogonal codes 359
- 9.6 Mass formulas 365
- 9.7 Classification 366
- 9.7.1 The Classification Algorithm 366
- 9.7.2 Gluing theory 370
- 9.8 Circulant constructions 376
- 9.9 Formally self-dual codes 378
- 9.10 Additive codes over F4 383
- 9.11 Proof of the Gleason–Pierce–Ward Theorem 389
- 9.12 Proofs of some counting formulas 393

## 10 Some favorite self-dual codes
- 10.1 The binary Golay codes 397
- 10.1.1 Uniqueness of the binary Golay codes 397
- 10.1.2 Properties of binary Golay codes 401
- 10.2 Permutation decoding 402
- 10.3 The hexacode 405
- 10.3.1 Uniqueness of the hexacode 405
- 10.3.2 Properties of the hexacode 406
- 10.3.3 Decoding the Golay code with the hexacode 407
- 10.4 The ternary Golay codes 413
- 10.4.1 Uniqueness of the ternary Golay codes 413
- 10.4.2 Properties of ternary Golay codes 418
- 10.5 Symmetry codes 420
- 10.6 Lattices and self-dual codes 422

## 11 Covering radius and cosets 432
- 11.1 Basics 432
- 11.2 The Norse Bound and Reed–Muller codes 435
- 11.3 Covering radius of BCH codes 439
- 11.4 Covering radius of self-dual codes 444
- 11.5 The length function 447
- 11.6 Covering radius of subcodes 454
- 11.7 Ancestors, descendants, and orphans 459

## 12 Codes over Z4 467
- 12.1 Basic theory of Z4-linear codes 467
- 12.2 Binary codes from Z4-linear codes 472
- 12.3 Cyclic codes over Z4 475
- 12.3.1 Factoring x^n - 1 over Z4 475
- 12.3.2 The ring R_k = Z4[x]/(x^k - 1) 480
- 12.3.3 Generating polynomials of cyclic codes over Z4 482
- 12.3.4 Generating idempotents of cyclic codes over Z4 485
- 12.4 Quadratic residue codes over Z4 488
- 12.4.1 Z4-quadratic residue codes: p ≡ -1 (mod 8) 490
- 12.4.2 Z4-quadratic residue codes: p ≡ 1 (mod 8) 492
- 12.4.3 Extending Z4-quadratic residue codes 492
- 12.5 Self-dual codes over Z4 495
- 12.5.1 Mass formulas 498
- 12.5.2 Self-dual cyclic codes 502
- 12.5.3 Lattices from self-dual codes over Z4 503
- 12.6 Galois rings 505
- 12.7 Kerdock codes 509
- 12.8 Preparata codes 515

## 13 Codes from algebraic geometry 517
- 13.1 Affine space, projective space, and homogenization 517
- 13.2 Some classical codes 520
- 13.2.1 Generalized Reed–Solomon codes revisited 520
- 13.2.2 Classical Goppa codes 521
- 13.2.3 Generalized Reed–Solomon codes 524
- 13.3 Algebraic curves 526
- 13.4 Algebraic geometry codes 532
- 13.5 The Gilbert–Varshamov Bound revisited 541
- 13.5.1 Goppa codes meet the Gilbert–Varshamov Bound 541
- 13.5.2 Algebraic geometry codes exceed the Gilbert–Varshamov Bound 543

## 14 Convolutional codes 546
- 14.1 Generator matrices and encoding 546
- 14.2 Viterbi decoding 551
- 14.2.1 State diagrams 551
- 14.2.2 Trellis diagrams 554
- 14.2.3 The Viterbi Algorithm 555
- 14.3 Canonical generator matrices 558
- 14.4 Free distance 562
- 14.5 Catastrophic encoders 568

## 15 Soft decision and iterative decoding 573
- 15.1 Additive white Gaussian noise 573
- 15.2 A Soft Decision Viterbi Algorithm 580
- 15.3 The General Viterbi Algorithm 584
- 15.4 Two-way APP decoding 587
- 15.5 Message passing decoding 593
- 15.6 Low density parity check codes 598
- 15.7 Turbo codes 602
- 15.8 Turbo decoding 607
- 15.9 Some space history 611

- References 615
- Symbol index 630
- Subject index 633

## Preface

Coding theory originated with the 1948 publication of the paper “A mathematical theory of communication” by Claude Shannon. For the past half century, coding theory has grown into a discipline intersecting mathematics and engineering with applications to almost every area of communication such as satellite and cellular telephone transmission, compact disc recording, and data storage.

During the 50th anniversary year of Shannon’s seminal paper, the two volume Handbook of Coding Theory, edited by the authors of the current text, was published by Elsevier Science. That Handbook, with contributions from 33 authors, covers a wide range of topics at the frontiers of research. As editors of the Handbook, we felt it would be appropriate to produce a textbook that could serve in part as a bridge to the Handbook. This textbook is intended to be an in-depth introduction to coding theory from both a mathematical and engineering viewpoint suitable either for the classroom or for individual study. Several of the topics are classical, while others cover current subjects that appear only in specialized books and journal publications. We hope that the presentation in this book, with its numerous examples and exercises, will serve as a lucid introduction that will enable readers to pursue some of the many themes of coding theory.

Fundamentals of Error-Correcting Codes is a largely self-contained textbook suitable for advanced undergraduate students and graduate students at any level. A prerequisite for this book is a course in linear algebra. A course in abstract algebra is recommended, but not essential. This textbook could be used for at least three semesters. A wide variety of examples illustrate both theory and computation. Over 850 exercises are interspersed at points in the text where they are most appropriate to attempt. Most of the theory is accompanied by detailed proofs, with some proofs left to the exercises. Because of the number of examples and exercises that directly illustrate the theory, the instructor can easily choose either to emphasize or deemphasize proofs.

In this preface we briefly describe the contents of the 15 chapters and give a suggested outline for the first semester. We also propose blocks of material that can be combined in a variety of ways to make up subsequent courses. Chapter 1 is basic with the introduction of linear codes, generator and parity check matrices, dual codes, weight and distance, encoding and decoding, and the Sphere Packing Bound. The Hamming codes, Golay codes, binary Reed-Muller codes, and the hexacode are introduced. Shannon’s Theorem for the binary symmetric channel is discussed. Chapter 1 is certainly essential for the understanding of the remainder of the book.

Chapter 2 covers the main upper and lower bounds on the size of linear and nonlinear codes. These include the Plotkin, Johnson, Singleton, Elias, Linear Programming, Griesmer, Gilbert, and Varshamov Bounds. Asymptotic versions of most of these are included. MDS codes and lexicodes are introduced.

Chapter 3 is an introduction to constructions and properties of finite fields, with a few proofs omitted. A quick treatment of this chapter is possible if the students are familiar with constructing finite fields, irreducible polynomials, factoring polynomials over finite fields, and Galois theory of finite fields. Much of Chapter 3 is immediately used in the study of cyclic codes in Chapter 4. Even with a background in finite fields, cyclotomic cosets (Section 3.7) may be new to the student.

Chapter 4 gives the basic theory of cyclic codes. Our presentation interrelates the concepts of idempotent generator, generator polynomial, zeros of a code, and defining sets. Multipliers are used to explore equivalence of cyclic codes. Meggitt decoding of cyclic codes is presented as are extended cyclic and affine-invariant codes.

Chapter 5 looks at the special families of BCH and Reed-Solomon cyclic codes as well as generalized Reed-Solomon codes. Four decoding algorithms for these codes are presented. Burst errors and the technique of concatenation for handling burst errors are introduced with an application of these ideas to the use of Reed-Solomon codes in the encoding and decoding of compact disc recorders.

Continuing with the theory of cyclic codes, Chapter 6 presents the theory of duadic codes, which include the family of quadratic residue codes. Because the complete theory of quadratic residue codes is only slightly simpler than the theory of duadic codes, the authors have chosen to present the more general codes and then apply the theory of these codes to quadratic residue codes. Idempotents of binary and ternary quadratic residue codes are explicitly computed. As a prelude to Chapter 8, projective planes are introduced as examples of combinatorial designs held by codewords of a fixed weight in a code.

Chapter 7 expands on the concept of weight distribution defined in Chapter 1. Six equivalent forms of the MacWilliams equations, including the Pless power moments, that relate the weight distributions of a code and its dual, are formulated. MDS codes, introduced in Chapter 2, and coset weight distributions, introduced in Chapter 1, are revisited in more depth. A proof of a theorem of MacWilliams on weight preserving transformations is given in Section 7.9.

Chapter 8 delineates the basic theory of block designs particularly as they arise from the supports of codewords of fixed weight in certain codes. The important theorem of Assmus-Mattson is proved. The theory of projective planes in connection with codes, first introduced in Chapter 6, is examined in depth, including a discussion of the nonexistence of the projective plane of order 10.

Chapter 9 consolidates much of the extensive literature on self-dual codes. The Gleason-Pierce-Ward Theorem is proved showing why binary, ternary, and quaternary self-dual codes are the most interesting self-dual codes to study. Gleason polynomials are introduced and applied to the determination of bounds on the minimum weight of self-dual codes. Techniques for classifying self-dual codes are presented. Formally self-dual codes and additive codes over F4, used in correcting errors in quantum computers, share many properties of self-dual codes; they are introduced in this chapter.

The Golay codes and the hexacode are the subject of Chapter 10. Existence and uniqueness of these codes are proved. The Pless symmetry codes, which generalize the ternary Golay
