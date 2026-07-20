![](images/cover.jpg)

![image](images/cover.jpg)

Volker Diekert, Manfred Kufleitner, Gerhard Rosenberger, Ulrich Hertrampf

Discrete Algebraic Methods

De Gruyter Graduate

Also of Interest

![](images/2_1.jpg)

Riemann-Roch Spaces and Computation Alvanos, 2015

ISBN 978-3-11-042613-7, e-ISBN (PDF) 978-3-11-042612-0, e-ISBN (EPUB) 978-3-11-043948-9

![](images/2_2.jpg)

Algebraic Curves and Finite Fields Niederreiter/Ostafe/Panario/Winterhof, 2014

ISBN 978-3-11-031788-6, e-ISBN (PDF) 978-3-11-031791-6, e-ISBN (EPUB) 978-3-11-037955-6

![](images/2_3.jpg)

A Course in Mathematical Cryptography Baumslag/Fine/Kreuzer/Rosenberger, 2015

ISBN 978-3-11-037276-2, e-ISBN (PDF) 978-3-11-037277-9, e-ISBN (EPUB) 978-3-11-038616-5

![](images/2_4.jpg)

Discrete Mathematics and Applications Zubkov (Editor-in-Chief)

ISSN 0924-9265, e-ISSN 1569-3929

![](images/title.jpg)

Mathematics Subject Classification 2010

11-01, 11Y11, 12-01, 14H52, 20E06, 20M05, 20M35, 68Q45, 68Q70, 68R15, 94A60

Authors

| Prof. Dr. Volker Diekert | Prof. Dr. Gerhard Rosenberger |
| University of Stuttgart | University of Hamburg |
| Department of Computer Science | Department of Mathematics |
| Universitätsstr. 38 | Bundesstr. 55 |
| 70569 Stuttgart | 20146 Hamburg |
| Germany | Germany |
| [diekert@fmi.uni-stuttgart.de](mailto:diekert@fmi.uni-stuttgart.de) | [gerhard.rosenberger@math.uni-hamburg.de](mailto:gerhard.rosenberger@math.uni-hamburg.de) |
| PD Dr. Manfred Kufleitner | Prof. Dr. Ulrich Hertrampf |
| University of Stuttgart | University of Stuttgart |
| Department of Computer Science | Department of Computer Science |
| Universitätsstr. 38 | Universitätsstr. 38 |
| 70569 Stuttgart | 70569 Stuttgart |
| Germany | Germany |
| [kufleitner@fmi.uni-stuttgart.de](mailto:kufleitner@fmi.uni-stuttgart.de) | [hertrampf@fmi.uni-stuttgart.de](mailto:hertrampf@fmi.uni-stuttgart.de) |

ISBN 978-3-11-041332-8

e-ISBN (PDF) 978-3-11-041333-5

e-ISBN (EPUB) 978-3-11-041632-9

Library of Congress Cataloging-in-Publication Data

A CIP catalog record for this book has been applied for at the Library of Congress.

Bibliographic information published by the Deutsche Nationalbibliothek

The Deutsche Nationalbibliothek lists this publication in the Deutsche Nationalbibliografie; detailed bibliographic data are available on the Internet at [http://dnb.dnb.de](http://dnb.dnb.de).

© 2016 Walter de Gruyter GmbH, Berlin/Boston

Cover image: John Phelan, Wikimedia Commons. This file is licensed under the Creative Commons

Attribution-Share Alike 3.0 Unported license.

Typesetting: le-tex publishing services GmbH, Leipzig, Germany

[www.degruyter.com](http://www.degruyter.com)

# Preface

This book is based on courses taught by the authors over many years at universities in Dortmund, Hamburg, Munich, and Stuttgart. Two textbooks emerged from the German lecture notes, Elemente der diskreten Mathematik [[28](#Bibliography.xhtml_Bibliography_28)] and Diskrete algebraische Methoden [[27](#Bibliography.xhtml_Bibliography_26)].While the first book has a strong emphasis on combinatorial topics, the second book focuses on algebraic ideas. This English edition is a revised and extended version of the second book.

Essentially, no knowledge beyond high school mathematics is required for reading this book. However, the density of the presentation suggests a certain amount of mathematical maturity, as, for example, required from students in computer science or mathematics studying for a master’s degree. Every mathematically inclined reader should be able to follow the topics, but the effort might vary.

Contents. Discrete algebraic methods are a future-oriented topic and its fundamentals are becoming increasingly significant. The selection of the material is also influenced by the authors’ personal affinities. We begin with a general chapter on algebraic structures, providing the foundation for the rest of the book. Each of the subsequent chapters can be read independently, but there are various connections. For example, the chapter on elliptic curves is motivated by applications in cryptography. Algebraic cryptography is actually a guiding theme, given that cryptography is ubiquitous in modern society. Our focus is on asymmetric cryptographic methods. They are mathematically more interesting and challenging than symmetric procedures, which are designed to optimize performance. We also present Shamir’s attack on the Merkle–Hellman scheme. Due to this attack, the Merkle–Hellman scheme no longer has any practical use. However, the Merkle–Hellman method serves as a lesson on how skeptical we should be regarding unproven security claims. Also, the general question, whether it makes sense to build cryptosystems on NP-hard problems, remains topical. The purely speculative answer we tend to give to this question is “no,” but the margin here is too narrow to include our justification.

The chapter on number theoretic algorithms is central. For example, large random prime numbers are needed in cryptosystems such as Rivest–Shamir–Adleman (RSA). So the method relies on the ability to efficiently generate primes. To date, RSA is the most popular asymmetric cryptographic method. It is named after Rivest, Shamir, and Adleman, who were the first to publish the algorithm in 1977 (although it seems that the scheme was known to British intelligence much earlier). We also study alternatives for RSA, such as the Diffie–Hellman procedure for secure key exchange. If we rely on this procedure, it might be reassuring to understand why known algorithms are unable to compute discrete logarithms on moderate input sizes. For calculations with large numbers, the analysis is often based on the fact that numbers can be multiplied in nearly linear time. We discuss Schönhage and Strassen’s algorithm for integer multiplication, which achieves this time bound.

In the chapter on the recognition of primes, we present the deterministic polynomial time test by Agrawal, Kayal, and Saxena. It is called the AKS test after its inventors. Even though it was only discovered in 2002, it is the archetypical application of discrete algebraic methods. Our presentation of the AKS test follows the exposition of the original article to a large extent. Nevertheless,we incorporate some simplifications compared to the original paper. In particular, we do not use cyclotomic polynomials. All we need is the basic fact that splitting fields exist. This refurbishment makes it possible to discuss the AKS test in a high school study group with a committed teacher and motivated students. We strongly encourage school teachers to undertake such a project.

The chapter on elliptic curves is mainly dedicated to number theoretic and cryptographic applications. Cryptography based on elliptic curves is well established in practice; and this area will be of growing importance in the near future. We provide all the necessary mathematics for this purpose. One big problem for the understanding of elliptic curves is that a great portion of users have no idea why computations should lead to correct results. This applies to a lesser extent to RSA-based methods, because computing modulo n is easily comprehensible. In comparison, elliptic curves constitute inherently complex mathematical objects. A user might easily be able to implement the needed operations on elliptic curves, needing only basic arithmetic operations. The formalism thus is available in the form of recipes, but usually the recipes (and also the books containing them) do not reveal why they are working correctly. This leads to justified skepticism towards elliptic curves. We counter this skepticism by not avoiding the difficult part. The proof of the group structure is presented in full detail and is based entirely upon the chapter on algebraic structures. In particular, we do not expect the reader to have previous knowledge from algebraic geometry or from complex analysis.

Combinatorics on words studies structural properties of sequences, such as repetitions. Motivated by Higman’s lemma on subsequences, we give a concise introduction to Ramsey theory and well-quasi-orderings. The chapter culminates in a proof of Kruskal’s tree theorem.

The chapter on automata leads us to an area of theoretical computer science, in which the theory of semigroups plays a central role. We deal with regular languages in a general context, which is crucial for understanding deterministic and nondeterministic automata. Two key results in this area are the characterization of star-free languages by Schützenberger and the decomposition theorem of Krohn and Rhodes. For both results, we present new and simplified proofs. We also give a recent interpretation of Green’s relations in terms of local divisors. The above-mentioned results concern languages over finite words. However, the need for formal methods in hardware and software verification makes it necessary to analyze systems that do not intend to terminate, leading to the study of infinite words and the connection between logic and automata on infinite objects. Examples of such systems are operating systems, embedded systems in cars, planes, etc. Here, we deal with Büchi automata. In the 1960s, Büchi showed that monadic second-order logic over infinite words is decidable; we give a detailed proof of this result. Two more applications of automata theory follow: decidability of Presburger arithmetic and a simple automata theoretic proof that there is an effective description for the solution set of linear Diophantine systems.

The [final chapter](#chapter08_1.xhtml_chapter08_1_1) is devoted to discrete infinite groups. The chosen topics belong to the algorithmic branch of combinatorial group theory, as developed in the classic book by Lyndon and Schupp. We chose to explain standard constructions using confluent term rewriting systems. This leads to mathematically precise statements and in many cases directly to corresponding algorithms. In the section on free groups, the influence of Serre and Stallings on modern group theory becomes obvious. A particularly nice application of Stallings’ ideas is the geometric proof for the fact that the automorphism group of finitely generated free groups is generated by (finitely many) Whitehead automorphisms.

Authors. Volker Diekert holds the chair of Theoretical Computer Science at the University of Stuttgart. He studied in Hamburg and Montpellier, completing a Diplôme des Études Supérieures with Alexander Grothendieck. He graduated in mathematics in Hamburg and regularly attended seminars offered by Ernst Witt. He earned his PhD with Jürgen Neukirch in Regensburg. These late mathematicians and truly impressive personalities have had an enduring influence in his life.

Manfred Kufleitner studied computer science with a minor in mathematics, and then earned his PhD in computer science in Stuttgart under the supervision of the first author. Shortly after, he spent one year in Bordeaux. He has been a guest professor at Technische Universität München and an acting professor at the University of Hamburg.

Gerhard Rosenberger comes with the greatest life experience among the authors. He has a strong background in teaching mathematics and much experience in writing textbooks. His research work has been enriched by extended stays in Russia and in the United States. In his scientific collaboration, he has co-authors from more than 25 different countries. Currently, he teaches at the University of Hamburg.

Ulrich Hertrampf started his career in pure mathematics. After his diploma thesis in the area of group representations, he earned his PhD in the area of practical computer science, but returned to theoretical research when he completed his habilitation in the structural complexity theory group of Klaus Wagner in Würzburg.

Cover. The title of the book is Discrete Algebraic Methods, or DAM for short; and the book’s cover page shows the Hoover Dam. It is a concrete construction to gather a huge pool of water. The purpose is not to block it, but to provide a continuous stream of water and hydroelectric power. Having this interpretation in mind, we are glad that we are permitted to reproduce the picture by John Phelan.

Miscellaneous. We believe that combining exercises with the study of advanced material deepens the understanding of the subject matter. Exercises can be found at the end of each chapter and complete solutions are given in the appendix. The exercises are of variable difficulty; their order corresponds to the presentation of the topics within a chapter. All chapters end with short summaries to reinforce learning.

We prefer succinct explanations over verbose ones, thus leaving free space for the reader’s own considerations. Throughout, we give complete proofs. Most chapters end with topics which lie beyond standard contents.

For aesthetic reasons, we have intentionally omitted punctuation marks at the end of displayed formulas. Our style of writing is motivated by gender-free mathematics. The use of gender is purely grammatical. Thus, if we speak of “she” or “he” we intend no preference to women or men. If “Alice” and “Bob” appear occasionally, we mean “Person A” and “Person B.” Ifmathematicians are mentioned by name, we include biographical details, whenever it appears appropriate and if publicly available. In some cases, we obtained permission to mention years of birth. In other words, these details are partly missing.

## Acknowledgments

A successful realization of this book would have been impossible without support from the Theoretical Computer Science department at the University of Stuttgart. The entire team was heavily involved in the preparation of the manuscript. Their dedicated participation in proofreading and their help in writing solutions to the exercises are gratefully acknowledged. In particular, the following former and present members made numerous contributions to the completion of the German and English editions of the book: Lukas Fleischer, Jonathan Kausch, Jürn Laun, Alexander Lauser, Jan Philipp Wächter, Tobias Walter, and Armin Weiß. Helpful technical support also came from Heike Photien, Horst Prote, and Martin Seybold as well as from Steven Kerns at the Language Center of the University of Stuttgart. During fall 2015, visiting researchers at the University of Stuttgart read parts of the book and provided helpful comments. This includes Jorge Almeida (Universidade do Porto, Porto), Murray Elder (The University of Newcastle, Australia), Théo Pierron (LaBRI, Bordeaux), M. Hossein Shahzamanian (Universidade do Porto, Porto), and Marc Zeitoun (LaBRI, Bordeaux). Those mathematical, stylistic, and orthographic errors that undoubtedly remain shall be charged to the authors. Last but not least, we thank DeGruyter for publishing our book.

Stuttgart and Hamburg, January 2016

VD, MK, GR, UH

# Contents

[Preface](#Preface.xhtml_Preface_1)

[1Algebraic structures](#chapter01_1.xhtml_chapter01_1_1)

[1.1Groups](#chapter01_1.xhtml_chapter01_1_6)

[1.2Regular polygons](#chapter01_1.xhtml_chapter01_1_28)

[1.3Symmetric groups](#chapter01_1.xhtml_chapter01_1_31)

[1.4Rings](#chapter01_2.xhtml_chapter01_2_2)

[1.5Modular arithmetic](#chapter01_2.xhtml_chapter01_2_12)

[1.5.1Euclidean algorithm](#chapter01_2.xhtml_chapter01_2_13)

[1.5.2Ideals in the integers](#chapter01_2.xhtml_chapter01_2_18)

[1.5.3Chinese remainder theorem](#chapter01_2.xhtml_chapter01_2_21)

[1.5.4Euler’s totient function](#chapter01_2.xhtml_chapter01_2_24)

[1.6Polynomials and formal power series](#chapter01_2.xhtml_chapter01_2_27)

[1.7Hilbert’s basis theorem](#chapter01_3.xhtml_chapter01_3_18)

[1.8Fields](#chapter01_3.xhtml_chapter01_3_20)

[1.9Finite fields](#chapter01_3.xhtml_chapter01_3_26)

[1.10Units modulo n](#chapter01_3.xhtml_chapter01_3_31)

[1.11Quadratic reciprocity](#chapter01_4.xhtml_chapter01_4_4)

[Exercises](#chapter01_4.xhtml_chapter01_4_16)

[Summary](#chapter01_4.xhtml_chapter01_4_30)

[2Cryptography](#chapter02_1.xhtml_chapter02_1_1)

[2.1Symmetric encryption methods](#chapter02_1.xhtml_chapter02_1_4)

[2.2Monoalphabetic cipher](#chapter02_1.xhtml_chapter02_1_9)

[2.3Polyalphabetic cipher](#chapter02_1.xhtml_chapter02_1_11)

[2.4Frequency analysis and coincidence index](#chapter02_1.xhtml_chapter02_1_14)

[2.5Perfect security and the Vernam one-time pad](#chapter02_1.xhtml_chapter02_1_16)

[2.6Asymmetric encryption methods](#chapter02_1.xhtml_chapter02_1_22)

[2.7RSA cryptosystem](#chapter02_1.xhtml_chapter02_1_24)

[2.8Rabin cryptosystem](#chapter02_1.xhtml_chapter02_1_27)

[2.9Diffie–Hellman key exchange](#chapter02_1.xhtml_chapter02_1_30)

[2.10ElGamal cryptosystem](#chapter02_1.xhtml_chapter02_1_32)

[2.11Cryptographic hash functions](#chapter02_1.xhtml_chapter02_1_36)

[2.12Digital signatures](#chapter02_2.xhtml_chapter02_2_2)

[2.13Secret sharing](#chapter02_2.xhtml_chapter02_2_5)

[2.14Digital commitment](#chapter02_2.xhtml_chapter02_2_9)

[2.15Shamir’s attack on the Merkle–Hellman cryptosystem](#chapter02_2.xhtml_chapter02_2_13)

[Exercises](#chapter02_2.xhtml_chapter02_2_25)

[Summary](#chapter02_3.xhtml_chapter02_3_4)

[3Number theoretic algorithms](#chapter03_1.xhtml_chapter03_1_1)

[3.1Runtime analysis of algorithms](#chapter03_1.xhtml_chapter03_1_2)

[3.2Fast exponentiation](#chapter03_1.xhtml_chapter03_1_8)

[3.3Binary GCD](#chapter03_1.xhtml_chapter03_1_11)

[3.4Probabilistic recognition of primes](#chapter03_1.xhtml_chapter03_1_13)

[3.4.1Fermat primality test and Carmichael numbers](#chapter03_1.xhtml_chapter03_1_14)

[3.4.2Solovay–Strassen primality test](#chapter03_1.xhtml_chapter03_1_18)

[3.4.3Miller–Rabin primality test](#chapter03_1.xhtml_chapter03_1_20)

[3.4.4Applications of the Miller–Rabin scheme](#chapter03_1.xhtml_chapter03_1_29)

[3.4.5Miller–Rabin versus Solovay–Strassen](#chapter03_1.xhtml_chapter03_1_31)

[3.5Extracting roots in finite fields](#chapter03_2.xhtml_chapter03_2_2)

[3.5.1Tonelli’s algorithm](#chapter03_2.xhtml_chapter03_2_4)

[3.5.2Cipolla’s algorithm](#chapter03_2.xhtml_chapter03_2_6)

[3.6Integer factorization](#chapter03_2.xhtml_chapter03_2_10)

[3.6.1Pollard’s p − 1 algorithm](#chapter03_2.xhtml_chapter03_2_11)

[3.6.2Pollard’s rho algorithm for factorization](#chapter03_2.xhtml_chapter03_2_12)

[3.6.3Quadratic sieve](#chapter03_2.xhtml_chapter03_2_14)

[3.7Discrete logarithm](#chapter03_2.xhtml_chapter03_2_17)

[3.7.1Shanks’ baby-step giant-step algorithm](#chapter03_2.xhtml_chapter03_2_19)

[3.7.2Pollard’s rho algorithm for the discrete logarithm](#chapter03_2.xhtml_chapter03_2_21)

[3.7.3Pohlig–Hellman algorithm for group order reduction](#chapter03_2.xhtml_chapter03_2_23)

[3.7.4Index calculus](#chapter03_2.xhtml_chapter03_2_26)

[3.8Multiplication and division](#chapter03_3.xhtml_chapter03_3_1)

[3.9Discrete fourier transform](#chapter03_3.xhtml_chapter03_3_3)

[3.10Primitive roots of unity](#chapter03_3.xhtml_chapter03_3_8)

[3.11Schönhage–Strassen integer multiplication](#chapter03_3.xhtml_chapter03_3_11)

[Exercises](#chapter03_3.xhtml_chapter03_3_18)

[Summary](#chapter03_3.xhtml_chapter03_3_25)

[4Polynomial time primality test](#chapter04.xhtml_chapter04_1)

[4.1Basic idea](#chapter04.xhtml_chapter04_6)

[4.2Combinatorial tools](#chapter04.xhtml_chapter04_9)

[4.3Growth of the least common multiple](#chapter04.xhtml_chapter04_13)

[4.4Of small numbers and large orders](#chapter04.xhtml_chapter04_19)

[4.5Agrawal–Kayal–Saxena primality test](#chapter04.xhtml_chapter04_22)

[Summary](#chapter04.xhtml_chapter04_32)

[5Elliptic curves](#chapter05_1.xhtml_chapter05_1_1)

[5.1Group law](#chapter05_1.xhtml_chapter05_1_11)

[5.1.1Lines](#chapter05_1.xhtml_chapter05_1_12)

[5.1.2Polynomials over elliptic curves](#chapter05_1.xhtml_chapter05_1_16)

[5.1.3Divisors](#chapter05_1.xhtml_chapter05_1_23)

[5.1.4Picard group](#chapter05_1.xhtml_chapter05_1_26)

[5.2Applications of elliptic curves](#chapter05_2.xhtml_chapter05_2_3)

[5.2.1Diffie–Hellman key exchange with elliptic curves](#chapter05_2.xhtml_chapter05_2_5)

[5.2.2Pseudocurves](#chapter05_2.xhtml_chapter05_2_7)

[5.2.3Factorization using elliptic curves](#chapter05_2.xhtml_chapter05_2_11)

[5.2.4Goldwasser–Kilian primality certificates](#chapter05_2.xhtml_chapter05_2_14)

[5.3Endomorphisms of elliptic curves](#chapter05_2.xhtml_chapter05_2_19)

[Exercises](#chapter05_3.xhtml_chapter05_3_17)

[Summary](#chapter05_3.xhtml_chapter05_3_28)

[6Combinatorics on words](#chapter06.xhtml_chapter06_1)

[6.1Commutation, transposition and conjugacy](#chapter06.xhtml_chapter06_7)

[6.2Fine and Wilf’s periodicity lemma](#chapter06.xhtml_chapter06_12)

[6.3Kruskal’s tree theorem](#chapter06.xhtml_chapter06_16)

[Exercises](#chapter06.xhtml_chapter06_32)

[Summary](#chapter06.xhtml_chapter06_40)

[7Automata](#chapter07_1.xhtml_chapter07_1_1)

[7.1Recognizable sets](#chapter07_1.xhtml_chapter07_1_2)

[7.2Rational sets](#chapter07_1.xhtml_chapter07_1_19)

[7.3Regular languages](#chapter07_2.xhtml_chapter07_2_7)

[7.4Star-free languages](#chapter07_2.xhtml_chapter07_2_16)

[7.5Krohn–Rhodes theorem](#chapter07_2.xhtml_chapter07_2_30)

[7.6Green’s relations](#chapter07_3.xhtml_chapter07_3_23)

[7.7Automata over infinite words](#chapter07_4.xhtml_chapter07_4_11)

[7.7.1Deterministic Büchi automata](#chapter07_4.xhtml_chapter07_4_17)

[7.7.2Union and intersection](#chapter07_4.xhtml_chapter07_4_20)

[7.7.3Omega-rational languages](#chapter07_4.xhtml_chapter07_4_23)

[7.7.4Recognizability of omega-regular languages](#chapter07_4.xhtml_chapter07_4_30)

[7.7.5Monadic second-order logic over infinite words](#chapter07_5.xhtml_chapter07_5_4)

[7.8Presburger arithmetic](#chapter07_5.xhtml_chapter07_5_13)

[7.9Solutions of linear Diophantine systems](#chapter07_5.xhtml_chapter07_5_24)

[Exercises](#chapter07_6.xhtml_chapter07_6_5)

[Summary](#chapter07_6.xhtml_chapter07_6_14)

[8Discrete infinite groups](#chapter08_1.xhtml_chapter08_1_1)

[8.1Classical algorithmic problems](#chapter08_1.xhtml_chapter08_1_7)

[8.2Residually finite monoids](#chapter08_1.xhtml_chapter08_1_11)

[8.3Presentations](#chapter08_1.xhtml_chapter08_1_13)

[8.4Rewriting systems](#chapter08_1.xhtml_chapter08_1_15)

[8.4.1Termination and confluence](#chapter08_1.xhtml_chapter08_1_16)

[8.4.2Semi-Thue systems](#chapter08_1.xhtml_chapter08_1_22)

[8.5Solving the word problem in finitely presented monoids](#chapter08_1.xhtml_chapter08_1_43)

[8.6Free partially commutative monoids and groups](#chapter08_1.xhtml_chapter08_1_50)

[8.7Semidirect products](#chapter08_2.xhtml_chapter08_2_14)

[8.8Amalgamated products and HNN extensions](#chapter08_2.xhtml_chapter08_2_16)

[8.9Rational sets and Benois’ theorem](#chapter08_2.xhtml_chapter08_2_33)

[8.10Free groups](#chapter08_3.xhtml_chapter08_3_7)

[8.11The automorphism group of free groups](#chapter08_3.xhtml_chapter08_3_22)

[8.12The special linear group SL(2, ℤ)](#chapter08_4.xhtml_chapter08_4_11)

[Exercises](#chapter08_4.xhtml_chapter08_4_20)

[Summary](#chapter08_5.xhtml_chapter08_5_5)

[Solutions to exercises](#chapter09_1.xhtml_chapter09_1_1)

[Chapter 1](#chapter09_1.xhtml_chapter09_1_2)

[Chapter 2](#chapter09_1.xhtml_chapter09_1_10)

[Chapter 3](#chapter09_2.xhtml_chapter09_2_3)

[Chapter 5](#chapter09_2.xhtml_chapter09_2_10)

[Chapter 6](#chapter09_3.xhtml_chapter09_3_2)

[Chapter 7](#chapter09_3.xhtml_chapter09_3_5)

[Chapter 8](#chapter09_4.xhtml_chapter09_4_4)

[Bibliography](#Bibliography.xhtml_Bibliography_1)

[Index](#Index_1.xhtml_Index_1_1)

[Footnotes](#Notes.xhtml)

# 1 Algebraic structures

Algebra is one of the oldest mathematical disciplines. Language and techniques from modern algebra are used in most areas of mathematics. Algebraic methods have their origins in the elementary theory of numbers and the study of equations. The elementary theory of numbers considers the properties of number systems such as the integers, the rationals, or the reals. The theory of equations, on the other hand, deals with solving equations and systems thereof. Both subjects date back to classical times. The Babylonians already knew how to solve linear and quadratic equations and how to compute square roots several hundred years before the Common Era. Their applications included land surveying and mapping, architecture, tax collection, and the computation of calendars. General procedures for solving cubic equations, however, were only discovered in the 16th century by Scipione del Ferro (1465–1526), rediscovered by Niccoló Fontana Tartaglia (1500–1557) and published by Gerolamo Cardano (1501–1576); this is the reason why the formulas for the solutions were named after Cardano. A bit later, Lodovico Ferrari (1522–1565), a student of Cardano, found the respective solutions for equations of degree 4.

The availability of computational methods also extended the number ranges. The discovery of complex numbers, for example, is often attributed to Cardano and Rafael Bombelli (1526–1573), whereas the (positive) rational numbers were already known in ancient Egypt. In antiquity, it was understood that ![](images/13_1.jpg) is not rational. The proof is credited to Theaitetos (about 415–369 B.C.) and its written version can be found in Book X of Euclid’s Elements. Nevertheless, ![](images/13_2.jpg) as a solution of X2 = 2 has a simple description and, more important in antiquity, the hypotenuse of a right-angled triangle with legs of length 1 gives a geometric interpretation. The first real numbers that are not solutions of polynomial equations with rational coefficients appeared in 1844 when Joseph Liouville (1809–1882) specified them. Such numbers are called transcendental in contrast to algebraic numbers, which are solutions of a system of polynomial equations with rational coefficients. The two best-known examples of transcendental numbers are Euler’s number e (named after Leonhard Euler, 1707–1783) and the number π. The proof that e is transcendental was given by Charles Hermite (1822–1901) in 1872\. The corresponding result for π from 1882 is due to Carl Louis Ferdinand von Lindemann (1852–1939). For Euler’s constant γ = 0.57772 . . . , it is open whether or not γ is transcendental.

The methods for showing “nonfeasibility” are often more abstract than the ones for feasibility. Giving an according polynomial suffices to show that some number is algebraic. But how can one show that no polynomial with rational coefficients has π as a root? How can one show that there is no general formula for the roots of polynomials of degree 5? Or how can one show that the ancient problem of trisecting an angle is not possible using only a ruler and a compass? Such questions had strong influence on the development of modern algebra.

On the one hand, people tried to get a better understanding of the structure of numbers; on the other hand, a broader appearance of vectors and matrices motivated the investigation of generalized arithmetic operations. Niels Henrik Abel (1802–1829) showed in 1824 that there is no formula for solving equations of degree 5\. This result was conjectured in 1799 by Paolo Ruffini (1765–1822), who gave an incomplete proof, which in turn influenced Abel’s work. Building on Abel’s ideas, Évariste Galois (1811–1832) investigated general equations and realized that the development of group theory was very significant. Pushed by David Hilbert (1862–1943), the so-called axiomatic approach became more and more popular among mathematicians at the end of the 19th century. The idea was to explore interesting objects (for example, numbers) not directly. Instead, investigations were based on a small set of given conditions (axioms), which are, among others, satisfied by the objects in question. This initiated the study of more abstract number systems. Ernst Steinitz (1871–1928) published the first axiomatic study of abstract fields in 1910\. As a further generalization of fields, the concept of rings was introduced during the first few years of the 20th century. Amalie Emmy Noether (1882–1935) provided the basis for the study of commutative rings in 1921.

The theory of semigroups and monoids was developed comparatively late. This is mainly due to the intuitive idea that the more structure an object has, the more properties can be derived for these objects. Many mathematicians thought that semigroups were too general to have any nontrivial structural properties. The first to disprove this view were Kenneth Bruce Krohn and John Lewis Rhodes (born 1937) in 1965\. They described a decomposition of finite semigroups into simple groups and flip–flops,[1](#Notes.xhtml_Notes_1)see [Theorem 7.26](#chapter07_2.xhtml_chapter07_2_40). This result is often considered to be the foundation of semigroup theory. The real significance of semigroups was only noticed as computer science became more and more important. In particular, the close relationship between semigroups and automata contributed to this.

A more general point of view is taken by universal algebra, sometimes also referred to as general algebra. It was established in 1935 by Garrett Birkhoff (1911–1996). Here, arbitrary algebraic structures are investigated and frequently appearing concepts – such as homomorphisms and substructures – are presented in a unified form. The idea of generalization is even pushed a little further in category theory. Samuel Eilenberg (1913–1998) and Saunders MacLane (1909–2005) developed the concept of categories and functors in 1942\. Category theory, due to its universality, appears in many forms; for example, the semantics of programming languages can be presented in a mathematical framework within this theory.

Applications of algebra are extraordinarily diverse; for example, algebraic ideas play an important role in automata theory, algebraic coding theory and codes of variable length, cryptography, symmetry considerations in chemistry and physics, computer algebra systems, and graph theory. Modern algebra is characterized by numerous notions. In fact, this is one of the contributions of these theories, as important properties and criteria can be described and investigated in a uniform way.

This chapter is devoted to a detailed study of groups; then we consider rings, polynomials, and fields, as far as they fit into this book’s framework or are needed in order to understand the other chapters. A short overview of the various algebraic structures is given by the following diagrams.

![](images/15_1.jpg)

We first give a brief overview of some elementary concepts of algebra. For binary operations ∘ : M × M → M, we often use the infix notation x ∘ y instead of ∘(x, y), and if the underlying operation is clear, then we write xy for short. An operation on M is associative if for all x, y, z ∈ M, we have (xy)z = x(yz), and it is commutative or Abelian (named after Niels Henrik Abel), if xy = yx holds for all x, y ∈ M. For instance, multiplication forms a commutative and associative operation on the set of natural numbers ℕ = {0, 1, 2, . . . }.

An element e ∈ M is called idempotent if e2 = e. It is called neutral if xe = ex = x for all x ∈ M. A neutral element is idempotent, but the converse does not hold: consider the set {0, 1} with multiplication, then both elements are idempotent, 1 is neutral, but 0 is not. A neutral element is often referred to as an identity. Similarly, an element z ∈ M is a zero element if xz = zx = z for all x ∈ M. A set M, together with an associative operation forms a semigroup. A semigroup with a neutral element is called a monoid. If in a monoid M with neutral element e each element x has an inverse y such that xy = yx = e, then M forms a group. We write (M, ⋅, e) when emphasizing the operation and the neutral element. In the case of two operations + and ⋅, the rules connecting these two operations can be formulated. This leads to the concepts of rings and fields, which we will discuss later.

Example 1.1. The set M = {0, . . . , n} with the operation xy = min{x + y, n} forms a finite commutative monoid. The element n is a zero element, and the element 0 is neutral. Since zero elements cannot have an inverse, M is not a group if n ≥ 1\. Roughly speaking, a subset Y of an algebraic structure Z forms a substructure if Y itself has the same structural properties as those claimed for Z. For example, consider the semigroup M = {1, 0} with multiplication as operation; in this case, {1} and {0} are subsemigroups of M. The semigroup M forms a monoid, but only {1} is a submonoid. Even though {0} forms a monoid, it is not a submonoid since it does not have the same identity as M. A substructure Y of Z is generated by X if it is the smallest substructure containing X.We denote this substructure by 〈X〉.

◊

A mapping between two algebraic structures which is compatible with the respective operations (such as + and ⋅) and which maps neutral elements to neutral elements is called a homomorphism. Thus, for a homomorphism φ: M → N between two monoids M and N, the two properties φ(xy) = φ(x)φ(y) and φ(1M) = 1N are required; here, 1M and 1N denote the neutral elements of M and N, respectively. A bijection φ always has an inverse map φ−1. If both mappings φ and φ−1 are homomorphisms, then φ is called an isomorphism. In most cases, a bijective homomorphism already is an isomorphism. An automorphism is an isomorphism from a structure onto itself.

For numbers k,ℓ ∈ ℤ, we write k | ℓ if there is an integer m ∈ ℤ with km = ℓ; in this case, k divides ℓ, and ℓ is a multiple of k. The greatest common divisor of two integers k, ℓ, not both equal to 0, is the largest nonnegative integer d such that d | k and d | ℓ, written as d = gcd(k, ℓ). In addition, it is natural to set gcd(0, 0) = 0. Two integers k, ℓ are coprime if gcd(k, ℓ) = 1\. We say that k is congruent to ℓ modulo n (and write k ≡ ℓ mod n) if there is m ∈ ℤ with k = ℓ + mn, that is, if n | k − ℓ. The integer n is the modulus.

## 1.1 Groups

The notion of a group goes back to Galois, who examined the solutions of polynomial equations over the rational numbers and tried to classify them into groups of solvable equations. Galois was the first to recognize the close connection between solutions of polynomial equations, the corresponding field extensions, and permutation groups. Old manuscripts indicate that he wrote a survey of his mathematical insights the night before a fatal duel, which took place early in the morning of May 30th, 1832\. He died one day later at the age of 20\. The importance of his work was recognized only posthumously in the middle of the 19th century.

We study groups from an abstract point of view. A group G is a set with a binary operation (g, h) ↦ g ⋅ h which is associative and thus satisfies (x ⋅ y) ⋅ z = x ⋅ (y ⋅ z). Furthermore, there is a neutral element 1 ∈ G such that 1 ⋅ x = x ⋅ 1 = x, and for each x ∈ G there is an inverse y with x ⋅ y = y ⋅ x = 1\. In fact, it is sufficient to require the existence of left inverses since these are automatically also right inverses, see [Exercise 1.13 (a)](#chapter01_4.xhtml_chapter01_4_23). Moreover, the inverses are uniquely determined and we write x−1 for the inverse y of x. If the operation is written additively (i.e., using + instead of ⋅), then the inverse is denote by −x and the neutral element is 0\. For example, the integers ℤ, with addition, form a group. A subset H of a group G is a subgroup if H contains the neutral element of G and if H with the operation of G forms a group; see [Exercise 1.14](#chapter01_4.xhtml_chapter01_4_24) for other characterizations of subgroups. For any subset X ⊆ G, the subgroup of G generated by X is 〈X〉. Thus, 〈X〉 contains exactly those group elements that can be written as a product of elements x and x−1 with x ∈ X. The empty product yields the neutral element. For X = {x1, . . . , xn}, we also write 〈x1, . . . , xn〉 instead of 〈{x1, . . . , xn}〉.

In the following, let G be a group, g, g1, g2 ∈ G be the arbitrary group elements and H be a subgroup of G. We call the set gH = { gh | h ∈ H } the (left) coset of H with respect to g. Analogously, Hg is the right coset with respect to g. The set of cosets is denoted by G/H, that is

![](images/17_9.jpg)

Analogously, H \ G = { Hg | g ∈ G } is the set of right cosets.

Lemma 1.2. For cosets and right cosets the following properties hold:

(a)|H| = |gH| = |Hg|

(b)g1H ∩ g2H ≠ 0 ⇔ g1 ∈ g2H ⇔ g1H ⊆ g2H ⇔ g1H = g2H

(c)|G/H| = |H \ G|

□

Proof: (a) The mapping g⋅ : H → gH, x ↦ gx is a bijection with inverse map g−1⋅ : gH → H, x ↦ g−1x. Thus, |H| = |gH|, and by symmetry also |H| = |Hg|. (b) Let g1h1 = g2h2 with h1, h2 ∈ H. Then, ![](images/17_6.jpg) From g1 ∈ g2H, we obtain g1H ⊆ g2H ⋅ H = g2H. Now, g1H ⊆ g2H immediately implies g1H ∩ g2H ≠ 0, and by symmetry g2H ⊆ g1H. Thus, all four statements in (b) are equivalent. (c) g1 ∈ g2H is true if and only if ![](images/17_8.jpg) holds. Thus, using (b), we obtain a bijection gH ↦ Hg−1 from the set G/H to H \ G.

□

[Lemma 1.2 (b)](#chapter01_1.xhtml_chapter01_1_9) shows that different cosets of H are disjoint. Each element g ∈ G belongs to the coset gH. These two facts together show that the cosets induce a partition of G, where by (a) all classes are of the same size.

![](images/17_2.jpg)

Fig. 1.1. The group G as a disjoint union of cosets.

The index of H in G is [G : H] = |G/H|. [Lemma 1.2 (c)](#chapter01_1.xhtml_chapter01_1_10) yields [G : H] = |H \ G|. The order of G is its size |G|. The order of an element g ∈ G is the order of 〈g〉. If 〈g〉 is finite, then the order of g is the smallest positive integer n such that gn = 1\. The following fundamental theorem is named after Joseph Louis Lagrange, 1736–1813.

Theorem 1.3 (Lagrange). |G| = [G : H]⋅ |H|

Proof: By [Lemma 1.2](#chapter01_1.xhtml_chapter01_1_8), the group G is the disjoint union of [G : H] cosets of H, each of size |H|; see [Figure 1.1](#chapter01_1.xhtml_chapter01_1_11).

□

For finite groups G, Lagrange’s theorem has the following consequences: the order of a subgroup H divides the order of G. If H = 〈g〉 for g ∈ G, this means that the order of any group element g ∈ G divides the order of G. If K is a subgroup of H and H is a subgroup of G, then we obtain [G : K] = [G : H][H : K].

Theorem 1.4. Let g be a group element of order d. Then gn = 1 ⇔ d | n.

Proof: If n = kd, then gn = (gd)k = 1k = 1\. For the converse, let gn = 1 and n = kd + r with 0 ≤ r < d. Then, 1 = gn = (gd)kgr = 1 ⋅ gr = gr and therefore r = 0\. So, n = kd + 0 = kd is a multiple of d.

□

Corollary 1.5. Let G be a finite group. For all g ∈ G, we have g|G| = 1.

Proof: Let d be the order of g ∈ G. Then, d divides |G| by Lagrange’s theorem, and thus g|G| = 1 by [Theorem 1.4](#chapter01_1.xhtml_chapter01_1_13).

□

A group G is called cyclic if G is generated by a single element x, that is, G = 〈x〉. In this case, x is called a generator of G. Cyclic groups are either finite or isomorphic to (ℤ, +, 0). If | 〈x〉| = |〈y〉| holds for cyclic groups 〈x〉 and 〈y〉, then the mapping xi ↦ yi is a group isomorphism. Therefore, cyclic groups are uniquely determined (up to isomorphism) by the group order. For all n ≥ 1, the set {1, x, x2, . . . , xn−1} with the operation xi ⋅xj = x(i+j) mod n is a cyclic group with n elements, generated by x. The operation in this group is illustrated in [Figure 1.2](#chapter01_1.xhtml_chapter01_1_15).

![](images/18_2.jpg)

Fig. 1.2. Group of order n generated by x.

Theorem 1.6. Groups of prime order are cyclic.

Proof: Let |G| be prime. We can choose g ∈ G \ {1} because |G| ≥ 2\. Now, |〈g〉| divides |G| by Lagrange’s theorem. Since |G| is prime and |〈g〉| ≥ 2, we obtain |〈g〉| = |G| and 〈g〉 = G.

□

Theorem 1.7. Subgroups of cyclic groups are cyclic.

Proof: Let G = 〈g〉 and U be a subgroup of G. Since the trivial subgroup {1} is cyclic, in the following we may assume that U ≠ {1}. There exists n > 0 with gn ∈ U. Let n be minimal with this property. Consider an arbitrary element gk ∈ U, then gk mod n ∈ U. Since n was chosen to be minimal, we conclude k ≡ 0 mod n and therefore U is generated by gn.

□

Theorem 1.8. Let G be an Abelian group and let g, h ∈ G be elements with coprime orders m, n ∈ ℕ. Then, gh has order mn.

Proof: Let d be the order of gh. From (gh)mn = (gm)n(hn)m = 1 ⋅ 1 = 1, together with [Theorem 1.4](#chapter01_1.xhtml_chapter01_1_13), we see that d is a divisor of mn. If d ≠ mn, then mn has a prime divisor p satisfying d | ![](images/19_1.jpg) . But gcd(m, n) = 1, and thus either p | m or p | n, but not both. Assume that p | m and p ∤ n. Then, ![](images/19_2.jpg) since ![](images/19_5.jpg) is not a multiple of m. This contradicts d | ![](images/19_3.jpg) thus we have d = mn.

□

The following theorem is named after Augustin Louis Cauchy (1789–1857). The proof presented here was given by McKay (1923–2012) in [[73](#Bibliography.xhtml_Bibliography_73)].

Theorem 1.9 (Cauchy). Let G be a finite group and p be a prime divisor of | G|. Then, G contains an element of order p.

Proof: Let n = |G| and S = {(g1, . . . , gp) ∈ Gp | g1 ⋅⋅ ⋅ gp = 1 in G }. In each p-tuple (g1, . . . , gp)∈ S, the elements g1, . . . , gp−1 ∈ G can be chosen arbitrarily and gp is then uniquely determined by gp = (g1 ⋅⋅ ⋅ gp−1)−1. Hence, |S| = np−1. Define f : S → S by f(g1, . . . , gp) = (gp , g1, . . . , gp−1), that is, f cyclically shifts the elements. Note that, indeed (gp , g1, . . . , gp−1)∈ S. For every s ∈ S one can consider the restriction of f to Fs = {f(s), f 2(s), . . . , f p(s)}. This restriction is a bijection, and since f p is the identity, the order of f (as a bijection on F s) is a divisor of p, that is, it is either 1 or p. In particular, |Fs| is either 1 or p. The sets { Fs | s ∈ S } form a partition of S. Let k be the number of partition classes with one element and ℓ be the number of partition classes with p elements. We obtain np−1 = |S| = k + pℓ, and p | n yields k ≡ 0 mod p. From (1, . . . ,1) ∈ S, we obtain k ≥ 1 and therefore k ≥ p. Hence, there exists s ∈ S \ {(1, . . . ,1)} with f(s) = s, that is, for s = (g1, . . . , gp), we have (g1, . . . , gp) = f(s) = (gp , g1, . . . , gp−1). We conclude g1 = g2 = ⋅⋅ ⋅ = gp ≠1 and the definition of S yields ![](images/19_4.jpg) . Therefore, g1 ∈ G has order p by [Theorem 1.4](#chapter01_1.xhtml_chapter01_1_13).

□

The rest of this section is devoted to the homomorphism theorem for groups. As we shall see later, this is the basis for an analogous result in ring theory. Let φ: G → K bea group homomorphism, that is, φ(g1 g2) = φ(g1) φ(g2) for all g1, g2 ∈ G. We define the following sets:

![](images/20_4.jpg)

We call ker(φ) the kernel of φ and im(φ) the image of φ. A subgroup H of G is normal if the left cosets of H are equal to the right cosets of H, that is, if gH = Hg for all g ∈ G. This is equivalent to saying that the left and the right cosets define the same partitions of G. If G is commutative, then obviously all subgroups are normal.

Theorem 1.10. For every subset H of a group G, the following properties are equivalent:

(a)H is a normal subgroup of G.

(b)H is a subgroup such that G /H forms a group with respect to the operation g1H ⋅ g2H = g1g2H; its neutral element is H.

(c)H is the kernel of a group homomorphism φ: G → K.

(d)H is a subgroup and for all g ∈ G, we have gHg−1 ⊆ H.

Proof: (a) ⇒ (b): We have g1H g2H = g1(Hg2)H = g1(g2H)H = g1g2H. This shows that the operation on G/H is well defined and associative and that H is the neutral element. Being well defined means that the operation is independent of the chosen representatives g1 and g2. The inverse of gH is g−1H ∈ G/H.

(b)⇒ (c): Consider the mapping φ: G → G/H, g ↦ gH. Then, φ(g1g2) = g1g2H = g1Hg2H = φ(g1) φ(g2). This shows that φ is a homomorphism. The kernel of φ is ker(φ) = { g ∈ G | gH = H } = H.

(c)⇒(d): Let φ: G → K be a group homomorphism with ker(φ) = H. Then, φ(1) = 1 yields 1 ∈ H. For all g1, g2 ∈ H, we have ![](images/20_2.jpg) , and thus ![](images/20_3.jpg) ∈ ker(φ) = H. Therefore, H is a subgroup; see [Exercise 1.14 (a)](#chapter01_4.xhtml_chapter01_4_25). For all g ∈ G and all h ∈ H, we have φ(ghg−1) = φ(g)φ(h)φ(g)−1 = φ(g)φ(g)−1 = 1 and thus gHg−1 ⊆ H = ker(φ).

(d)⇒(a): From gHg−1 ⊆ H, we obtain gH ⊆ Hg and Hg−1 ⊆ g−1H for all g ∈ G. Since all group elements in G can be represented as inverses, the latter implies Hg ⊆ gH for all g ∈ G. Both relations together yield gH = Hg for all g ∈ G.

□

If H is a normal subgroup, then the group of [Theorem 1.10 (b)](#chapter01_1.xhtml_chapter01_1_22) is called the quotient group of G modulo H. The mapping G → G/H, g ↦ gH is a homomorphism with kernel H. In the case of cyclic groups, quotient groups can be interpreted as “spooling.” Consider the finite cyclic group C6 = {0, 1, 2, 3, 4, 5} with the operation given by addition modulo 6\. Then, {0, 3} is a subgroup. Since cyclic groups are commutative, {0, 3} is normal and we can form the quotient group C6/{0, 3}; see [Figure 1.3](#chapter01_1.xhtml_chapter01_1_23). For the infinite cyclic group (ℤ, +, 0) and its normal subgroup 4ℤ a similar picture arises; see [Figure 1.4](#chapter01_1.xhtml_chapter01_1_24). Here, we identify ℤ/4ℤ with the representatives 0, 1, 2, 3\. Each element of this set corresponds to the coset in which it occurs; for example, 3 corresponds to the coset 3 + 4ℤ = {. . . , −1, 3, 7, . . . }. The same interpretation works quite analogously

![](images/21_1.jpg)

Fig. 1.3. Illustration of C6/{0, 3}.

![](images/21_2.jpg)

Fig. 1.4. Illustration of ℤ/4ℤ.

for the infinite, noncyclic group (ℝ, +, 0) and its subgroup 4ℤ. Thus, we obtain an illustration of the infinite group ℝ/4ℤ as a circle of length 4.

Theorem 1.11. Subgroups of index 2 are normal.

Proof: Let [G : H] = 2\. Then,

□

![](images/21_3.jpg)

and therefore, H is normal.

![](images/22_1.jpg)

Fig. 1.5. Illustration of the homomorphism theorem for groups.

Theorem 1.12 (Homomorphism theorem for groups). Let φ: G → K be a group homomorphism. Then, φ induces an isomorphism:

![](images/22_2.jpg)![](images/22_3.jpg)

Proof: Let H = ker(φ). The mapping φ̄ is well defined: if g1H = g2H, then g1 = g2h for a suitable h ∈ H. This yields φ̄(g1H) = φ(g1) = φ(g2h) = φ(g2)φ(h) = φ(g2) = φ̄(g2H) since φ(h) = 1\. But if φ̄ is well defined, it is obviously a homomorphism and by construction it is surjective. It remains to show that φ̄ is injective. Let φ̄(g1H) = φ̄(g2H). Then, φ(g1) = φ(g2) and ![](images/22_4.jpg) Finally, this yields ![](images/22_5.jpg) and therefore ![](images/22_6.jpg) .

□

[Figure 1.5](#chapter01_1.xhtml_chapter01_1_26) gives an illustration of the induced isomorphism φ̄ in [Theorem 1.12](#chapter01_1.xhtml_chapter01_1_27).

Remark 1.13. The homomorphism theorem for groups together with [Theorem 1.10](#chapter01_1.xhtml_chapter01_1_21) shows that it is equivalent to consider quotient groups or homomorphic images of groups. Furthermore, we see that a group homomorphism φ is injective if and only if ker(φ) = {1} holds.

◊

## 1.2 Regular polygons

In this section, we want to demonstrate the concepts introduced so far by looking at mappings on regular polygons. A regular n-gon is an undirected graph Cn = (V, E) with vertices V = ℤ/nℤ and edges E = {{i, i + 1} | i ∈ ℤ/nℤ}. The cases n = 0, n = 1 and n = 2 degenerate and we thus assume that n ≥ 3 in the remainder of this section. An n-gon always has n edges.

![](images/23_1.jpg)

An automorphism of a graph G = (V, E) is a bijective mapping φ: V → V satisfying

![](images/23_2.jpg)

The set of automorphisms Aut(G) ⊆ VV of a graph G = (V, E) forms a group with the composition of mappings as operation; the neutral element is idV. The group Aut(G) is called the automorphism group or the symmetry group of G. In this section, we investigate the groups Dn = Aut(Cn), the automorphism groups of regular n-gons; they are called dihedral groups.

If φ ∈ Dn, then φ is uniquely determined by the values φ(0) and φ(1). Let φ(0) = i with i ∈ ℤ/nℤ. Then, for φ(1) the only possible values are φ(1) = i +1 or φ(1) = i − 1, because vertex i only has edges to vertices i−1and i +1.Sincewe areonly interested in the case n ≥ 3, the vertices i −1 and i + 1 are different. If φ(1) = i + 1, then φ(2) = i + 2 follows: i and i + 2 are the only neighbors of i + 1 and φ(2) ≠ i = φ(0) because φ is bijective. Continuing this way, we obtain φ(j) = φ(0)+j. In the other case, φ(1) = i −1, we symmetrically get φ(j) = φ(0) − j for all j ∈ ℤ/nℤ. This means |Dn| = 2n for n ≥ 3, because for φ(0), we have n values to choose and two orientations are possible. The six elements of D3 can be illustrated as follows:

![](images/23_3.jpg)

Because of 6 = 3!, all permutations of the vertices 0, 1, and 2 are contained in D3. Define the rotation δ ∈ Dn and the reflection σ ∈ Dn by

![](images/23_6.jpg)

for j ∈ ℤ/nℤ. The k-fold application of δ is δk(j) = j + k and its inverse is (δk)−1 = δ−k = δn−k. The order of δ is n and of σ is 2\. We can visualize σ as the reflection over the line through the vertex 0 and the center of the polygon. If φ ∈ Dn satisfies φ(0) = i and φ(1) = i + 1, then φ = δi. And if φ(0) = i and φ(1) = i − 1, then φ = δiσ. It follows that

![](images/23_5.jpg)

Next, we give some identities for Dn

![](images/24_1.jpg)

The subgroup S = 〈σ〉 = {id, σ} of Dn = 〈δ, σ〉 contains two elements and, by Lagrange’s theorem, it has n cosets. We obtain G/S = {S, δS, . . . , δn−1S}. From δσ = σδ−1 ∉ Sδ for n ≥ 3, we conclude δS ≠ Sδ. So, the subgroup S is not normal. In the case n = 3, dividing D3 into left cosets and right cosets of S yields the following partitions:

![](images/24_2.jpg)

Next, we consider the subgroup N = 〈δ〉 = {id, δ, δ2, . . . , δn−1} of order n. This group has index 2 in Dn; its cosets are N and σN = {σ, σδ, σδ2, . . . , σδn−1}. By [Theorem 1.11](#chapter01_1.xhtml_chapter01_1_25), the subgroup N is normal. This also follows from σδi = δ−iσ.

For n ≥ 2, consider D2n. The subgroup E = 〈δ2〉 = {id, δ2, δ4, . . . , δ2n−2} contains n elements. Therefore, the index of E in D2n is 4\. Its four cosets are E, δE, σE and σδE. We have σδ2i = δ2n−2iσ; in particular, 2n − 2i is even. This implies σE = Eσ. From this, together with δE = Eδ, we conclude that E is normal. Therefore, D2n/E is a group with four elements. We choose {id, δ, σ, σδ} as representatives of the four cosets of E. In addition to the relations within D2n, we obtain δ2 = id. Instead of dealing with the cosets, we define the group structure directly on the set of representatives, using the following multiplication table.

![](images/24_3.jpg)

The table is symmetric and all diagonal entries are id. In other words, the group is Abelian and all nontrivial elements are of order 2. Therefore, the group cannot be cyclic. This group is known as the Klein four-group named after Felix Christian Klein (1849–1925). It is isomorphic to the direct product ℤ/2ℤ ×ℤ/2ℤ and to the automorphism group of the following graph with four vertices:

![](images/24_4.jpg)

## 1.3 Symmetric groups

Let Sn be the set of all permutations on {1, . . . , n}, called the symmetric group on n elements. It indeed forms a group with the operation given by the composition of mappings, where πσ is defined by (πσ)(i) = π(σ(i)) for 1 ≤ i ≤ n. If G is a group with at most n elements and g ∈ G, then x ↦ gx defines a permutation on G. Therefore, every group of order at most n is isomorphic to a subgroup of Sn. In this section, we have a closer look at the elements of Sn. Let π be a permutation on {1, . . . , n}. Then a pair (i, j) ∈ {1, . . . , n}2 with i < j is called an inversion of π if π(i) > π(j). If we think of (π(1), . . . , π(n)) as a sequence, then (i, j) is an inversion if the elements at positions i and j are in the wrong order. By I (π), we denote the number of inversions of π.

Example 1.14. Consider the permutation π ∈ S9 given by (π(1), . . . , π(9)) = (3, 1, 7, 2, 4, 6, 9, 5, 8). Then the inversions of π are (1, 2), (1, 4), (3, 4), (3, 5), (3, 6), (3, 8), (6, 8), (7, 8), and (7, 9). One way of illustrating the inversions is by writing (1, . . . ,9) twice, one above the other. Then, we draw a line from each number i in the first line to π(i) in the second line:

![](images/25_1.jpg)

Every crossing of two lines corresponds to an inversion.

◊

A permutation in Sn has at most ![](images/25_2.jpg) inversions and the permutation π = (n, . . . ,1) with π(i) = n − i + 1 matches this upper bound. The identity mapping is the only permutation without inversions. The sign of π is sgn(π) = (−1)I(π); it is an element of the multiplicative group {1, −1}.

Lemma 1.15. Let π : {1, . . . , n} → {1, . . . , n} be a permutation. Then, we have

![](images/25_3.jpg)

Proof: Let ![](images/f.jpg) ⊆ {1, . . . , n}2 be the set of inversions of π and ![](images/g.jpg) = {(i, j) | 1 ≤ i < j ≤ n}\![](images/f.jpg) be its complement, that is, ![](images/g.jpg) = {(i, j) | 1 ≤ i < j ≤ n, π(i) < π(j) }. Then, we obtain

![](images/25_4.jpg)

Here, ![](images/25_5.jpg) because each pair (i, j) with 1 ≤ i < j ≤ n contributes the factor j−i exactly once in both the numerator and the denominator.

□

Theorem 1.16. The mapping sgn: Sn → {1, −1} is a homomorphism.

Proof: Let ![](images/26_1.jpg) be the set of all two-element subsets of {1, . . . , n}. For all π ∈ Sn and all i ≠ j, clearly ![](images/26_2.jpg) . Thus, the product ![](images/26_3.jpg) is well defined, because the value of the fraction does not depend on the order of i and j. But then, this product coincides with sgn(π) and for π, σ ∈ Sn, we obtain

![](images/26_4.jpg)

where the third equality uses { {σ(i), σ(j)} | {i, j} ∈ T } = T.

□

A transposition is a permutation that swaps two elements leaving all other elements’ positions unchanged. For the transposition σ, which swaps i and j (i < j), the number of inversions is 2(j − i) − 1\. If we write σ as the tuple (σ(1), . . . , σ(n)), we obtain the following representation:

![](images/26_5.jpg)

The j − i − 1 elements between i and j each have an inversion with i as well as with j; and there is one inversion between i and j themselves. Therefore, the sign of a transposition is always −1.

Corollary 1.17. If a permutation π on {1, . . . , n} can be written as a product of m transpositions, then the sign of π is sgn(π) = (−1)m.

Proof: Each transposition has sign −1\. By [Theorem 1.16](#chapter01_1.xhtml_chapter01_1_34), the mapping sgn: Sn → {−1, 1} is a homomorphism and thus sgn(π) = (−1)m.

□

Next, we prove that the group Sn is generated by transpositions. More precisely, we show that those transpositions, swapping only adjacent elements i and i + 1, are sufficient to generate the whole group.

Theorem 1.18. Each element of the symmetric group Sn can be written as a product of at most ![](images/26_6.jpg) transpositions such that each of these transpositions only swaps adjacent elements.

Proof: Let π ∈ Sn. We use induction on the number of inversions I (π). If π has no inversions, then π(i) = i for all i, that is, π is the identity permutation. In particular, then π is the product of 0 transpositions. If π contains an inversion, then there is an index i with π(i) > π(i + 1). Let σ be the transposition that swaps i and i + 1, then πσ has one inversion less than π. By the inductive hypothesis, πσ can be written as a product of transpositions σ1 ⋅⋅ ⋅ σm, where m = I (πσ) and each of the σi only swaps adjacent elements. Now, π = σ1 ⋅⋅ ⋅ σmσ.

□

By [Corollary 1.17](#chapter01_1.xhtml_chapter01_1_35), we see that the definition of sgn is independent of the chosen order of elements in {1, . . . , n}, because the definition of a transposition is independent of this order. So, if X is a finite set and π a permutation of X, we can define sgn(π). In particular, considering a finite group G, we can start with any order of G’s elements and every order defines the same sign sgn(g) ∈ {1, −1} for g ∈ G; to see this, consider the permutation x ↦ gx on G induced by g.

Remark 1.19. The kernel of sgn: Sn → {1, −1} is the alternating group An on n elements. These are the permutations with sign 1\. The elements of An are also called even permutations, while permutations of sign −1 are called odd permutations. [Corollary 1.17](#chapter01_1.xhtml_chapter01_1_35) shows that the even permutations are those generated by an even number of transpositions. It is also noteworthy that all groups An for n ≥ 5 have no nontrivial normal subgroups. This property led to the insight that polynomial equations of degree 5 or higher generally cannot be resolved with so-called root expressions. The theorem is accordingly named after Ruffini and Abel and its discovery was the beginning of Galois theory.

◊

## 1.4 Rings

Historically, the common properties of different number systems such as the integers and the complex numbers were the main motivation for algebraic structures. Each of these structures has two operations, addition and multiplication, and there are certain connections between them. This led to the notion of a ring. Formally, a ring is given by a tuple (R, +, ⋅, 0, 1), where (R, +, 0) is an Abelian group and (R, ⋅, 1) a monoid such that multiplication distributes over addition

![](images/27_3.jpg)

The latter is called the distributivity property. Weusuallywrite R instead of (R,+,⋅,0,1). Note that

![](images/27_2.jpg)

and symmetrically r0 = 0, that is, 0 is a zero element for multiplication. The ring R is commutative if multiplication is commutative. The zero ring R = {0} is the only ring with 0 = 1\. An element having a multiplicative inverse is a unit and R∗ = { r ∈ R | ∃s : rs = sr = 1 } is called the group of units or the multiplicative group of R. Note that 1 ∈ R∗. A skew field is a ring R with R∗ = R \ {0}, that is, all elements have a multiplicative inverse except for 0\. A commutative skew field is called a field. The integers ℤ form a commutative ring and we have ℤ∗ = {1, −1}, that is, ℤ is not a field. For n > 1, the n × n matrices over ℤ form a noncommutative ring. The rationals ℚ, the reals ℝ, and the complex numbers ℂ are the fields.

Example 1.20. If R is a ring, then RR = { f : R → R | f is a mapping } forms a ring with pointwise addition and multiplication. Formally, for f, g ∈ RR the mappings f +g ∈ RR and f ⋅ g ∈ RR are defined by

![](images/28_5.jpg)

Even if R is a field, RR is not a field.

◊

A subset I ⊆ R is an additive subgroup of R if (I, +, 0) is a subgroup of (R, +, 0). Multiplicative submonoids are defined similarly. A subset S of a ring R is a subring if it is both an additive subgroup and a multiplicative submonoid. In particular, every subring is a ring with the same 0 and 1\. A subring S of a field R is called subfield if S itself is a field. An additive subgroup I ⊆ R satisfying R ⋅ I ⋅ R ⊆ I is called an ideal. An ideal can only be a subring if 1 belongs to I, but then we have I = R. The subsets {0} and R are the trivial ideals of R. We will see in [Theorem 1.32](#chapter01_2.xhtml_chapter01_2_19) that all ideals in ℤ are of the form nℤ.

The set of additive cosets of I is R/I = {r + I | r ∈ R }. Since addition in R is commutative, R /I forms an Abelian group with addition

![](images/28_6.jpg)

Let us define multiplication on R /I by

![](images/28_7.jpg)

As the following computation shows, this definition is well defined:

![](images/28_8.jpg)

The associativity of multiplication and the distributive property for R /I now follow from the corresponding properties in R. We call R/I the quotient ring of R modulo I. The elements of R /I are called residue classes or residues. We say r is congruent to s modulo I if r + I = s + I. In computations modulo I, we can switch back and forth between representatives and classes. Let X ⊆ I. If every element r ∈ I can be written as r = Σx∈X rxxsx with rx , sx ∈ R such that rx ≠ 0 ≠ sx for only finitely many x, then X generates I. If a finite generating set exists, then the ideal is called finitely generated. An ideal I is principal if it is generated by a single element, that is, if I = RrR for some r ∈ R. In ℤ, every ideal is principal because it is generated by the greatest common divisor of all its elements; see [Theorem 1.32](#chapter01_2.xhtml_chapter01_2_19).

A mapping φ: R → S between rings R and S is called a (ring) homomorphism if the following conditions hold for all x, y ∈ R:

(a)φ(x + y) = φ(x) + φ(y)

(b)φ(x ⋅ y) = φ(x) ⋅ φ(y)

(c)φ(1) = 1.

The first property means that φ is a group homomorphism with respect to addition. This also implies φ(0) = 0\. The last two properties guarantee that φ is a monoid homomorphism with respect to multiplication. In particular, (c) does not follow from(b). A bijective ring homomorphism is a ring isomorphism because, due to bijectivity, the inverse mapping is a homomorphism, too. If I ⊆ R is an ideal, then R → R /I, r ↦ r + I defines a ring homomorphism.

Let φ: R → S be a ring homomorphism. Its kernel is the ideal ker(φ) = { r ∈ R | φ(r) = 0 }. The image of φ is the subring im(φ) = { φ(r) | r ∈ R } of S. Unlike im(φ), the ideal ker(φ) is not a subring unless im(φ) = {0}. In analogy to [Theorem 1.10](#chapter01_1.xhtml_chapter01_1_21), one can show that I is an ideal if and only if I is the kernel of a ring homomorphism φ: R → S; see [Exercise 1.24](#chapter01_4.xhtml_chapter01_4_26).

Example 1.21. Let R be a ring and r ∈ R. Then the mapping φ: RR → R, f ↦ f(r) is a ring homomorphism. Its kernel is ker(φ) = { f : R → R | f(r) = 0 }. The mappings with a zero at r form an ideal in RR.

◊

Example 1.22. Consider the derivative operator

![](images/29_4.jpg)

We have (f +g)' = f ' +g, that is, D is a group homomorphism with respect to addition. On the other hand, ker(D) = {f | f is a constant mapping } is not an ideal. Therefore, D is not a ring homomorphism.

◊

The following theorem is analogous to the homomorphism theorem for groups.

Theorem 1.23 (Homomorphism theorem for rings). Let φ: R → S be a ring homomorphism. Then, φ induces the ring isomorphism

![](images/29_3.jpg)

Proof: The set φ(r+ker(φ)) has only one element, namely φ(r). Therefore, r+ker(φ) ↦ φ(r) defines a ring homomorphism. From [Theorem1.12](#chapter01_1.xhtml_chapter01_1_27), it follows that it is a bijection, and bijective ring homomorphisms are isomorphisms.

□

An easy consequence of the homomorphism theorem for rings is that homomorphisms of finite fields into themselves are bijective. We show a more general statement.

Corollary 1.24. Ring homomorphisms from a field into a ring with 0 ≠ 1 are injective. In particular, all homomorphisms between fields are injective.

Proof: Let φ be a homomorphism and suppose that φ(z) = 0 for z ≠ 0\. Then, 1 = φ(1) = φ(z−1z) = φ(z−1) ⋅ φ(z) = φ(z−1) ⋅ 0 = 0, contradicting the assumption. Thus ker(φ) = {0}, and the homomorphism theorem for rings 1.23 yields injectivity.

□

An ideal M ⊆ R is maximal if M ≠ R and there is no ideal I with M ⊊ I ⊊ R. Note that R itself is an ideal. Thus, the “largest” ideal R is not maximal in R.

Theorem 1.25. An ideal M ⊆ R in a commutative ring R is maximal if and only if R/M is a field.

Proof: Let M ⊆ R be maximal and x + M ∈ R/M a residue class with x ∉ M. We show that x +M is invertible in R /M. Note that M + xR is an ideal. Since M is maximal and x ∉ M, it follows that M + xR = R. Then, 1 can be written as 1 = m + xy for m ∈ M and y ∈ R. The product xy is congruent to 1 modulo M and thus y + M is the multiplicative inverse. This shows that each class x + M in R /M, except the zero element M, is invertible. Consequently, R /M is a field.

Now for the converse, let R/M be a field. Then 1 ∉ M, because 0 ≠ 1 in all fields. Let I ⊆ R be an ideal with M ⊊ I, and consider x ∈ I \M. Then x +M ≠ 0 + M and since R/M is a field, there is r ∈ R such that (x + M) ⋅ (r + M) = 1 + M. Then 1 + M = xr + M; therefore R = R + M = xR + M ⊆ I because I is an ideal containing both xR and M. This shows I = R, so M is maximal.

□

An element r of a ring R is a zero divisor if there exists s ∈ R \ {0} with rs = 0 or sr = 0\. For example, in the ring ℤ/6ℤthenumbers 2 and 3 are zero divisors. Invertible elements cannot be zero divisors. A ring is a domain if 0 is the only zero divisor. By this definition, in domains we always have 0 ≠ 1\. An integral domain is a commutative domain.

For an integer k ∈ ℤand a ring (R, +, ⋅, 0R, 1R), we define

![](images/30_1.jpg)

We therefore write k ∈ R, meaning the element k ⋅1R. In this notation, for 0, 1 ∈ ℤ, we have 0 = 0R ∈ R and 1 = 1R ∈ R. Two cases are possible. Either all positive integers in R are different from zero or there is a smallest positive number n with n = 0 in R. In the first case, we say that R has characteristic 0; in the second case, the characteristic is n with n > 0\. In any case, we denote the characteristic of R by char(R). The ideal char(R)⋅ℤ is the kernel of the homomorphism ℤ→ R, k ↦ k⋅1R. The homomorphism theorem for rings 1.23 shows that ℤ/char(R)ℤ is isomorphic to a subring of R. Every subring S of R has the same characteristic as R.

Lemma 1.26. Let R be a domain. Then, either char(R) = 0 or char(R) is prime.

Proof: Suppose that char(R) = mn with m, n > 1\. Since mn = 0 and m ≠ 0 ≠ n in R, both m and n are zero divisors in R.

□

Fields have no zero divisors and therefore their characteristic is either zero or a prime number. Fields of characteristic zero contain ℤ as a subring, and since all s ≠ 0 are invertible, fractions ![](images/30_2.jpg) are elements of the field for all r, s ∈ ℤ with s ≠ 0\. Thus, these fields contain the rational numbers ℚ as uniquely determined subfield. Other examples for fields of characteristic zero are ℝ, ℂ or ![](images/30_3.jpg) . All fields of characteristic p for prime number p contain ℤ/pℤ. Therefore, the fields ℚ and ℤ/pℤ are minimal with respect to set inclusion; they are called prime fields.

The binomial coefficient ![](images/31_1.jpg) for x ∈ ℂand k ∈ ℤis defined as follows:

![](images/31_2.jpg)

For k ≥ 0, we have exactly k factors in both the numerator and the denominator; in particular, for k = 0 both products are empty and thus evaluate to the neutral element 1. For n, k ∈ ℕ, we obtain ![](images/31_3.jpg) . For all x ∈ ℂ and k ∈ ℤ, the following addition theorem holds:

![](images/31_4.jpg)

This can be seen as follows. For k < 0, both sides are 0, whereas for k = 0, both sides evaluate to 1\. Now let k > 0\. Then, ![](images/31_6.jpg) For n ∈ ℕ, we have ![](images/31_5.jpg) Now by induction, using the addition theorem, we see that the binomial coefficient ![](images/31_7.jpg) is an integer for all n, k ∈ ℕ. In particular, the binomial coefficients for n ∈ ℕ and k ∈ ℤ can be interpreted as multiples of the neutral element 1R in any ring R.

Theorem 1.27 (Binomial theorem). Let R be a commutative ring. For all x, y ∈ R andall n ∈ ℕ, we have ![](images/31_8.jpg)

Proof: The sum on the right-hand side runs over all k ∈ ℤ, but almost all of these summands are zero. This convention is often helpful, because index shifts are made much easier. The proof is by induction on n. For n = 0, both sides reduce to the neutral element 1R. Now let n > 0\. Then

![](images/31_9.jpg)

□

The binomial theorem is an important tool for the consideration of mappings r ↦ rp in commutative rings.

Theorem 1.28. Let R be a commutative ring with prime characteristic p. Then, r → rp defines a ring homomorphism.

Proof: Clearly, 1p = 1 and(rs)p = rp sp. It remains to show that (r+s)p = rp+sp. Bythe binomial theorem![](images/31_10.jpg) All binomial coefficients ![](images/31_11.jpg) for 1 ≤ k ≤ p−1 are divisible by p. Since the characteristic of R is p, all these binomial coefficients are zero in R and thus ![](images/32_1.jpg)

□

The homomorphism in [Theorem 1.28](#chapter01_2.xhtml_chapter01_2_9) is usually referred to as the Frobenius homomorphism named after Ferdinand Georg Frobenius (1849–1917). It is especially interesting for fields, because in this case it is, by [Corollary 1.24](#chapter01_2.xhtml_chapter01_2_5), injective and thus, for finite fields, necessarily also bijective. As an application of [Theorem 1.28](#chapter01_2.xhtml_chapter01_2_9) for R = ℤ/pℤ, we prove Fermat’s little theorem (named after Pierre de Fermat, 160?–1665). In particular, on prime fields ℤ/pℤ the Frobenius homomorphism is the identity.

Theorem 1.29 (Fermat’s little theorem). Let p be prime. Then, ap ≡ a mod p for all a ∈ ℤ.

Proof: It suffices to prove the claim for a ∈ ℕ. We proceed by induction on a. For a = 0, the statement is true. Now, (a + 1)p ≡ ap + 1p ≡ a + 1 mod p. The first congruence follows from [Theorem 1.28](#chapter01_2.xhtml_chapter01_2_9) and the second from the induction hypothesis.

□

In particular, under the assumptions of [Theorem 1.29](#chapter01_2.xhtml_chapter01_2_11), for all a ∈ ℤ which are invertible in ℤ/pℤ, we obtain ap−1 ≡ 1 mod p.

## 1.5 Modular arithmetic

Let us start with a quick repetition of the most basic terms. The greatest common divisor of two integers k and ℓ is denoted by gcd(k, ℓ); it is the largest natural number that divides both k and ℓ. The greatest common divisor of k and 0 is defined as the number |k|. Two numbers are coprime if their greatest common divisor is 1\. For computations in the quotient ring ℤ/nℤ, for integers k, ℓ, and n the following notation is used:

![](images/32_2.jpg)

It means that k + nℤ = ℓ + nℤ, that is, k and ℓ differ by a multiple of n. If this holds, we say that k is congruent to ℓ modulo n; the integer n is called modulus. By k mod n, we denote the unique number r ∈ {0, . . . , |n| − 1} satisfying k ≡ r mod n. Frequently, k mod n is taken as representative of the residue class k + nℤ. By (ℤ/nℤ)∗, we denote the group of units of the ring ℤ/nℤ. These are the residue classes that have a multiplicative inverse.

### 1.5.1 Euclidean algorithm

The Euclidean algorithm (Euclid of Alexandria, around 300 BC) is an efficient method for computing the greatest common divisor. Since gcd(k, ℓ) = gcd(−k, ℓ) = gcd(ℓ, k), it suffices to consider natural numbers 0 < k ≤ ℓ. Let ℓ = qk + r for 0 ≤ r < k. The integer r is called the remainder and we have r = ℓ mod k. Each number dividing k and the remainder r also divides the sum ℓ = qk + r. Each number dividing k and ℓ also divides the difference r = ℓ − qk. This yields a recursive version of the Euclidean algorithm

![](images/33_4.jpg)

If k ≤ ℓ, then after two recursive calls, the smaller parameter is less than k/2\. In particular, the recursion depth is in ![](images/o.jpg)(log k).

The next theorem is often named after Étienne Bézout (1730–1783) who showed a corresponding statement for polynomials.

Theorem 1.30 (Bézout’s lemma). Let k, ℓ ∈ ℤ. Then there exist a, b ∈ ℤ such that:

![](images/33_7.jpg)

Proof: We may assume that ℓ > k > 0, all other cases are either trivial or can be reduced to this case. Let r0 = ℓ and r1 = k. The Euclidean algorithm successively computes remainders r0 > r1 > r2 ⋅⋅ ⋅ > rn > rn+1 = 0 satisfying

![](images/33_2.jpg)

for appropriate qi ∈ ℕ. It follows gcd(k, ℓ) = gcd(ri+1, ri) = gcd(0, rn) = rn. We now show that for all i ∈ {0, . . . , n} there are integers ai and bi such that ai ri+1 + bi ri = rn. For i = n, we can set an = 0 and bn = 1\. Let now i < n and ai+1 and bi+1 already defined, that is ai+1ri+2 + bi+1ri+1 = rn. With ri+2 = ri − qi+1ri+1, we obtain (bi+1 − ai+1qi+1)ri+1 + ai+1ri = rn. Thus, ai = bi+1 − ai+1qi+1 and bi = ai+1 have the desired property.

□

The proof presented above yields the following procedure: the extended Euclidean algorithm computes gcd(k, ℓ) and, additionally, two numbers a and b with the property ak + bℓ = gcd(k, ℓ).

![](images/33_6.jpg)

Let n ∈ ℕ. For each number k that is coprime to n, the extended Euclidean algorithmprovides two integers a, b with ak +bn = 1. Modulo n, we obtain ak ≡ 1 mod n. Thus, a is a multiplicative inverse of k. We have a closer look at (ℤ/nℤ)∗, the invertible elements of ℤ/nℤ, in the following theorem:

Theorem 1.31. Let n ∈ ℕ. Then the following statements hold:

(a)(ℤ/nℤ)∗ = { k + nℤ | gcd(k, n) = 1 }

(b)The number n is prime if and only if ℤ/nℤ is a field.

(c)For every k ∈ ℤ, the mapping ℤ/nℤ → ℤ/nℤ, x ↦ kx is bijective if and only if gcd(k, n) = 1.

Proof: (a) We have k ∈ (ℤ/nℤ)∗ if and only if 1 can be written in the form 1 = kℓ+mn. By [Theorem 1.30](#chapter01_2.xhtml_chapter01_2_15), this is equivalent to gcd(k, n) = 1.

(b)The ring ℤ/nℤ is a field if and only if all nonzero elements are invertible. By (a) this means that all numbers from 1 to n −1 are coprime to n. This in turn is equivalent to primality.

(c)If gcd(k, n) = 1, then k is invertible in (ℤ/nℤ)∗. Hence, the multiplication with k has an inverse mapping, thereby showing that it is a bijective function. For the converse, suppose that x ↦ kx is surjective. Then, the element 1 has a preimage, and thus there exists x ∈ ℤ with kx ≡ 1 mod n. It follows kx + ℓn = 1 for some ℓ ∈ ℤ. This shows gcd(k, n) = 1.

□

### 1.5.2 Ideals in the integers

Ideals are a concept from algebra which also plays an important role in modular arithmetic. The interest in ideals of ℤ comes from the fact that divisibility in ℤ can be formulated in terms of subset relations of ideals. We have

![](images/34_3.jpg)

From the following theorem, we obtain a converse of this statement: each subset relation of ideals in ℤ represents some divisibility of numbers.

Theorem 1.32. Let I be an ideal of ℤ. Then, there is a unique number n ∈ ℕsuch that I = nℤ. Here, n is the greatest common divisor of all numbers in I. Particularly,

![](images/34_4.jpg)

Proof: If I = {0}, then n = 0 satisfies the assertion. Let now I ≠ {0}. For all a, b ∈ I, we can find p, q ∈ ℤwith gcd(a, b) = ap + bq. So, gcd(a, b) ∈ I if and only if a, b ∈ I. The claim now follows from the observation that the greatest common divisor of all numbers in I is the uniquely determined smallest positive number in I.

□

Actually, the proof of [Theorem 1.32](#chapter01_2.xhtml_chapter01_2_19) shows that all ideals in a ring are generated by a single element as soon as division with the remainder is available. This, for example, is also the case in polynomial rings over fields; see [Section 1.6](#chapter01_2.xhtml_chapter01_2_27). Another advantage of the algebraic point of view on modular arithmetic is that by using algebraic concepts one might find simpler formulations and new interpretations for certain interrelations and contexts.

If I and J are ideals of a ring R, then I ∩ J is an ideal, too. For k,ℓ ∈ ℤ by lcm(k, ℓ) ∈ ℕ, we denote the least common multiple of k and ℓ. A tight relation between lcm and gcd is given by lcm(k, ℓ) ⋅ gcd(k, ℓ) = |k| ⋅ |ℓ|.

Theorem 1.33.

![](images/35_6.jpg)

Proof: Since kℤ ∩ ℓℤ is an ideal of ℤ, by [Theorem 1.32](#chapter01_2.xhtml_chapter01_2_19), there exists n ∈ ℕ with kℤ∩ ℓℤ = nℤ. From nℤ ⊆ kℤ and nℤ ⊆ ℓℤ, we obtain k | n and ℓ | n. So, n is a common multiple of k and ℓ and thus n ≥ lcm(k, ℓ). Let t be any common multiple of k and ℓ. Then, tℤ ⊆ kℤ ∩ ℓℤ = nℤ and consequently n | t. This shows n ≤ lcm(k, ℓ) and therefore n is the least common multiple of k and ℓ.

□

### 1.5.3 Chinese remainder theorem

For coprime numbers k and ℓ, the quotient ring ℤ/kℓℤ can be decomposed into the components ℤ/kℤ and ℤ/ℓℤ. This is exactly what is stated by the Chinese remainder theorem. The most important part of the statement is the following lemma.

Lemma 1.34. For coprime numbers k, ℓ ∈ ℤ, the following mapping is surjective:

![](images/35_4.jpg)

Furthermore, π induces a bijection between ℤ/kℓℤ and ℤ/kℤ×ℤ/ℓℤ by the mapping (x mod kℓ) ↦ (x mod k, x mod ℓ).

Proof: Consider (x+kℤ, y+ℓℤ). Since k and ℓ are coprime, there are numbers a, b ∈ ℤ with ak + bℓ = 1\. Thus, bℓ ≡ 1 mod k and ak ≡ 1 mod ℓ. For x, y ∈ ℤ, we obtain the following properties of yak + xbℓ:

![](images/35_5.jpg)

But then π(yak + xbℓ) = (x + kℤ, y + ℓℤ) and π is surjective. We have π(x) = π(x) for all x' ∈ x + kℓℤ, so (x mod kℓ) ↦ (x mod k, x mod ℓ) is well defined. Therefore, π induces a surjection of Z /kℓℤ onto ℤ/kℤ×ℤ/ℓℤ. Finally, we observe that both Z /kℓℤ and ℤ/kℤ×ℤ/ℓℤ have kℓ elements. Thus, the induced mapping is bijective.

□

If R1 and R 2 are rings, we can define a ring structure on the Cartesian product R1 × R 2 by component-wise addition and multiplication. More specifically, addition is defined by (x1, y1) + (x2, y2) = (x1 + x2, y1 + y2). The zero element is given by the pair (0, 0) ∈ R1 × R2. Similarly, multiplication is defined by (x1, y1) ⋅ (x2, y2) = (x1 ⋅ x2, y1 ⋅ y2) and the neutral element is (1, 1). This ring is called the direct product of R1 and R2.

In a somewhat more elementary form, the following theorem is originally due to Sun Tzu in the 3rd century. However, it was only published in 1247 by Qin Jiushao (ca. 1202–1261).

Theorem 1.35 (Chinese remainder theorem). Let k, ℓ ∈ ℤ be coprime. Then the following mapping defines an isomorphism of rings:

![](images/36_4.jpg)

Proof: The mapping is compatible with addition and multiplication and corresponds to the bijective mapping from [Lemma 1.34](#chapter01_2.xhtml_chapter01_2_22).

□

A consequence of the Chinese remainder theorem is that, for the coprime numbers k and ℓ, the multiplicative group (ℤ/kℓ)∗ is isomorphic to (ℤ/kℤ)∗ × (ℤ/ℓℤ)∗.

### 1.5.4 Euler’s totient function

In this section, we deal with the number of elements in (ℤ/nℤ)∗. To this end, we define Euler’s totient function φ(n) as

![](images/36_5.jpg)

By [Theorem 1.31](#chapter01_2.xhtml_chapter01_2_17), the function φ(n) counts the integers in the range from 1 to n which are coprime to n. Thus φ(1) = 1\. The Chinese remainder theorem yields

![](images/36_6.jpg)

for the coprime numbers k and ℓ. This is due to the fact that x + kℓℤ is invertible if and only if both x + kℤ and x + ℓℤ are invertible. To determine the value of the totient function for arbitrary numbers, we only have to find the value of φ(n) for the cases where n is a prime power pk. So, let p be prime and k ≥ 1.From the numbers1, . . . , pk exactly the pk−1 numbers p, 2p, . . . , pk are divisible by p and therefore not coprime to pk. The remaining pk − pk−1 numbers are coprime to pk. This shows

![](images/36_7.jpg)

Hence, we can compute φ(n) for any number n as soon as we know its prime factorization. An important property of Euler’s totient function is due to the following generalization of Fermat’s little theorem.

Theorem 1.36 (Euler). If gcd(a, n) = 1, then aφ(n) ≡ 1 mod n.

Proof: This is an immediate consequence of [Corollary 1.5](#chapter01_1.xhtml_chapter01_1_14) since a ∈ (ℤ/nℤ)∗ and φ(n) is the order of the group (ℤ/nℤ)∗.

In particular, we can determine the inverse of any element a ∈ (ℤ/nℤ)∗ by computing aφ(n)−1. We write Σd|n φ(d) for the sum over all φ(d) such that d is a positive divisor of n.

Theorem 1.37.

![](images/37_1.jpg)

Proof: Consider the following set of n fractions:

![](images/37_2.jpg)

By cancellation, we can write every fraction ![](images/37_9.jpg) as ![](images/37_10.jpg) for the coprime numbers k and d such that d | n. Hence, we obtain

![](images/37_3.jpg)

Grouping the fractions by their denominator yields the following partition of N into disjoint sets:

![](images/37_4.jpg)

Finally, |{ k/d | 0 ≤ k < d, gcd(k, d) = 1 }| = |{ k | 0 ≤ k < d, gcd(k, d) = 1 }| = φ(d) completes the proof.

□

The following theorem gives an important connection between group theory and modular arithmetic.

Theorem 1.38. Let G be a cyclic group of order n and d be a positive divisor of n. Then, G has φ(d) elements of order d.

Proof: Let g ∈ G be a generator. By ψ(d), we denote the number of elements of order d. Since the order of every element in G divides n, we have Σd|n ψ(d) = n. By [Theorem 1.37](#chapter01_2.xhtml_chapter01_2_26), it suffices to show that ψ(d) ≥ φ(d) for every divisor d of n. Consider k ∈ {1, . . . , d − 1} with gcd(k, d) = 1. Let

![](images/37_5.jpg)

We have ![](images/37_7.jpg) Since n does not divide ![](images/37_8.jpg) for i ∈ {1, . . . , d − 1}, we have ![](images/37_6.jpg) for all i ∈ {1, . . . , d − 1}. Thus, the order of h is d. Every number k ∈ (ℤ/dℤ)∗ defines an element of order d such that different numbers define different group elements. This completes the proof of ψ(d) ≥ φ(d).

□

## 1.6 Polynomials and formal power series

Throughout this section, R is a commutative ring. A formal power series with coefficients in R is an infinite sequence (a0, a1, . . . ) where all ai are from R. A polynomial is a formal power series with ai = 0 for almost all i ∈ ℕ. As usual by almost all, we mean “all but finitely many.” The degree of a polynomial f = (a0, a1, . . . ) is denoted by deg(f) and it is the maximum index d ∈ ℕ with ad ≠ 0\. The polynomial f with ai = 0 for all i ∈ ℕ is called the zero polynomial and we define its degree to be −∞. Polynomials of degree at most 0 are called constants; they are identified with the elements of R.We usually write a formal power series (a0, a1, . . . ) as a formal sum

![](images/38_1.jpg)

Here, we read X as a formal symbol or as a variable. A polynomial can be written as a finite formal sum

![](images/38_2.jpg)

If f is not the zero polynomial, wemay require that d = deg(f) and ad ≠ 0\. In this case, we call ad the leading coefficient of the polynomial f(X). The leading coefficient of the zero polynomial is zero by definition. A formal power series (a0, a1, . . . ) can also be interpreted as a mapping ℕ → R with i ↦ ai. We denote the set of formal power series by R![](images/open.jpg)X![](images/close.jpg) and the set of polynomials by R[X]. The latter is called the polynomial ring over R. The set of formal power series R![](images/open.jpg)X![](images/close.jpg) is a ring

![](images/38_3.jpg)

In this ring, the polynomials form a subring but not an ideal. A polynomial f ∈ R[X] can also be interpreted as a polynomial mapping f ̃ : R → R by substituting values for the variable X

![](images/38_4.jpg)

The mapping f ↦ f ̃ is called the evaluation homomorphism. To simplify notation, we write f(r) instead of f ̃(r). The notation f(r) is extended to formal power series, provided that the value of the infinite series Σi≥0 ai ri is well defined in the ring R. This depends on the notion of convergence in R. In any case, for power series we have f(0) = a0. The mappings R![](images/open.jpg)X![](images/close.jpg) → R with f ↦ f(0) and R[X] → RR with f ↦ f̃ are ring homomorphisms, which in general, however, are not injective. If R is finite, then RR is also finite, whereas R[X] for R ≠ {0} is infinite.

If R is an infinite field, for example, R = ℚ or R = ℝ, then the polynomial mapping f ̃ corresponding to f can only be the constant zero function if all the coefficients of f are zero. In this case, we can therefore identify polynomials and polynomial mappings. Since very often polynomials are only considered over ℚ or ℝ, the distinction between polynomials and polynomial mappings might look artificial and unnecessary. But for finite fields it is necessary, as the following example shows.

Example 1.39. Let R = ℤ/2ℤ and f(X) = X2 + X ∈ R[X]. Then, f(X) has degree 2 and it is not the zero polynomial. But if f(X) is interpreted as the mapping f ̃ : ℤ/2ℤ → ℤ/2ℤ, r ↦ r2 + r, we find that f ̃ is the zero function since f(0) = f(1) = 0 for 0, 1 ∈ ℤ/2ℤ.

◊

An advantage of this purely formal point of view is that invertibility of formal power series does not depend on convergence. Moreover, certain properties of the ring R can directly be transferred to the ring of formal power series R![](images/open.jpg)X![](images/close.jpg).

Theorem 1.40. The following properties transfer from R to R![](images/open.jpg)X![](images/close.jpg):

(a)R![](images/open.jpg)X![](images/close.jpg) is an integral domain if and only if the ring R is.

(b)f ∈ R![](images/open.jpg)X![](images/close.jpg) is invertible if and only if f(0) ∈ R is.

Proof: (a) If R has a zero divisor, then so does R![](images/open.jpg)X![](images/close.jpg) because R is a subring. Nowlet R be an integral domain and f = (a0, a1, . . . ) and g = (b0, b1, . . . ) be two elements of R ![](images/open.jpg)X![](images/close.jpg)\{0}. Let ai be the first nonzero coefficient of f and b j the first nonzero coefficient of g. Then, f ⋅ g = (c0, c1, . . . ) with

![](images/39_1.jpg)

In particular, f ⋅ g is not the zero polynomial. Thus, R![](images/open.jpg)X![](images/close.jpg) is an integral domain.

(b)If f is invertible, so must be f(0) since (f ⋅ g)(0) = f(0) ⋅ g(0). For the converse, let f = (a0, a1, . . . ) and assume that f(0) = a0 ∈ R is invertible. Define b0 by a0 ⋅ b0 = 1\. Now, let k ≥ 1 and (b0, . . . , bk−1) be already defined. Then define bk by

![](images/39_2.jpg)

Then, we obtain a formal power series g = (b0, b1, . . . ) in the ring R![](images/open.jpg)X![](images/close.jpg) with the property (f ⋅ g) = 1 = (1, 0, 0, . . . ).

□

Example 1.41. The inverse of the formal power series Σi≥0 X i is 1 − X.

◊

Theorem 1.42 (Degree formula). Let f, g ∈ R[X]. Then, we have

(a)deg(f + g) ≤ max(deg(f), deg(g))

(b)deg(fg) ≤ deg(f) + deg(g)

(c)If the leading coefficient of at least one of the polynomials f and g is not a zero divisor, then deg(fg) = deg(f) + deg(g).

Proof: These statements are true if f = 0 or g = 0\. Thus, we can assume that

![](images/39_3.jpg)

The first statement follows from ![](images/40_1.jpg) The product of f and g has the form ![](images/40_2.jpg) Thus, deg(fg) ≤ deg(f) + deg(g). If an or bm is not a zero divisor, then anbm ≠ 0 and thus deg(fg) = deg(f) + deg(g).

□

Remember that each integer i can be interpreted as an element of R by i-fold summation of 1 ∈ R. The derivative of a formal power series f(X) = Σi≥0 aiXi is defined by

![](images/40_3.jpg)

Theorem 1.43. For derivatives, the following rules hold:

(a)(f + g)'(X) = f' (X) + g'(X)

(b)(f ⋅ g)'(X) = f' (X) ⋅ g(X) + f(X) ⋅ g'(X).

Proof: Let f = Σi≥0 aiXi and g = Σi≥0 biXi. Then:

![](images/40_4.jpg)

□

Similar to [Theorem 1.43](#chapter01_3.xhtml_chapter01_3_4), one can give an abstract proof for the derivation rules of ![](images/40_9.jpg) and f(g(X)), provided that the expressions are defined over the formal power series.

Theorem 1.44. Let g ∈ R[X] \ {0} such that its leading coefficient is invertible in the ring R. For every f ∈ R[X], there are unique polynomials q, r ∈ R[X] with

![](images/40_12.jpg)

Proof: We show the existence and uniqueness of q and r by induction on deg(f). If deg(f) < deg(g), then q = 0 and r = f is necessary and sufficient. Now let f(X) = ![](images/40_10.jpg) and deg(f) = n ≥ m = deg(g). Consider the polynomial ![](images/40_5.jpg) , where bm is the leading coefficient of g. Its degree is n and the coefficient of X n is an. Therefore, the degree of ![](images/40_6.jpg) is less than n. For all polynomials q and r, the following two equations are equivalent:

![](images/40_11.jpg)![](images/40_7.jpg)

By the induction hypothesis, there are unique polynomials q̂ and r̂ with f̂ = q̂g + r̂ and deg(r̂ ) < m. The identity f(X) = q(X) ⋅ g(X) + r(X) with deg(r) < m holds if and only if ![](images/40_8.jpg) and r(X) = r(̂ X).

□

The proof of [Theorem 1.44](#chapter01_3.xhtml_chapter01_3_5) provides an algorithm for the division of polynomials with remainder, called polynomial division. In the following example, let R = ℤ/4ℤ. Similar to the classical method for integer division, we demonstrate the method on polynomials f(X) = X5 + 2X3 + 3X and g(X) = 3X2 + 2X + 1 from R[X]

![](images/41_1.jpg)

For arbitrary rings R – including polynomial rings – we write s | t if the element s ∈ R divides the element t ∈ R, that is, if r ∈ R exists with rs = t. For f, g, r ∈ R[X], we write f mod g = r if deg(r) < deg(g) and there is a polynomial q ∈ R[X] satisfying f = qg + r. In fields, using this notation we can apply the (extended) Euclidean algorithm on two polynomials f and g. Analogous to [Theorem 1.32](#chapter01_2.xhtml_chapter01_2_19), we obtain the following statement.

Theorem 1.45. Let F be a field. Then every ideal in F[X] is principal. If t, t' ∈ F[X] generate the same ideal, then there exists a ∈ F ∗ with t' = at.

Proof: Let I ⊆ F[X] be an ideal different from {0}, and t ∈ I a polynomial of minimum degree in I \{0}. For each f ∈ I, by [Theorem 1.44](#chapter01_3.xhtml_chapter01_3_5) there is a representation f = qt+r with deg(r) < deg(t). From r = f − qt ∈ I, we obtain r = 0, and thus any polynomial f ∈ I belongs to the principal ideal generated by t. Now let t, t' ∈ F[X] be two polynomials generating the same principal ideal I. If t = 0, then necessarily t' = 0 also holds. So, let t ≠ 0 ≠ t. After a scalar multiplication with an appropriate a ∈ F ∗, we can assume that t and t' have the same leading coefficient. Then, t − t' ∈ I on the one hand has a smaller degree than t, and on the other hand t − t' = qt for a polynomial q ∈ F[X]. This yields t = t' and the claim follows.

□

Corollary 1.46. Let F be a field and f, g ∈ F[X] with f ≠ 0. Then there exists a unique polynomial t ∈ F[X] having the following three properties:

(a)There are a, b ∈ F[X] with t = af + bg.

(b)For all a, b ∈ F[X] holds t | af + bg.

(c)The leading coefficient of t is 1.

Proof: From [Theorem 1.45](#chapter01_3.xhtml_chapter01_3_7), we see that the ideal generated by f and g is a principal ideal and is generated by a polynomial t. Because of f ≠ 0, also t ≠ 0; and using a scalar multiplication we can assume that the leading coefficient of t is 1 ∈ F. This implies (a), since t is generated by f and g. Property (b) holds, since f and g are generated by t. The condition (c) is guaranteed by assumption, which also shows the uniqueness of t.

□

The polynomial t from [Corollary 1.46](#chapter01_3.xhtml_chapter01_3_8) is a polynomial of maximum degree dividing f and g. Therefore, t is called the greatest common divisor gcd(f, g) of the polynomials f and g. Two polynomials are called coprime if their greatest common divisor is the polynomial 1\. The next corollary shows that coprime polynomials f and g have no common roots, that is, there is no s ∈ R with f(s) = 0 = g(s).

Corollary 1.47. Let s ∈ R and f ∈ R[X]. Then

(a)f(s) = 0 ⇔ (X − s) | f(X)

(b)f(s) = a ⇔ f(X) = q(X)(X − s) + a for a polynomial q(X) ∈ R[X].

Proof: It is sufficient to show (b). Suppose that f(X) = q(X)(X − s) + a. Then, f(s) = q(s) ⋅ (s − s) + a = 0 + a = a. Now let f(s) = a. By [Theorem 1.44](#chapter01_3.xhtml_chapter01_3_5) there are q, r ∈ R[X] with f(X) = q(X)(X − s)+ r(X) and deg(r) < deg(X − s) = 1\. So, r ∈ R follows. Moreover, we obtain a = f(s) = q(s)(s − s) + r = 0 + r = r.

□

An element s ∈ R is called a root (or a zero) of the polynomial f ∈ R[X] if f(s) = 0\. The multiplicity of a root s ∈ R of a polynomial f ∈ R[X] \ {0} is the maximum n ∈ ℕ such that (X − s)n | f . [Corollary 1.47](#chapter01_3.xhtml_chapter01_3_10) states that the multiplicity of a root is always at least 1\. A root is called simple if its multiplicity is 1; otherwise a root is called multiple.

The following theorem shows that, for integral domains, the degree of a polynomials is an upper bound for the number of roots. In general, this is not true. Consider the polynomial f(X) = X2 + X of degree 2 over the ring ℤ/6ℤ. The four roots of this polynomial are 0, 2, 3 and 5\. This results in two factorizations f(X) = X(X + 1) and f(X) = X2 + X = X2 − 5X + 6 = (X − 2)(X − 3). All elements of ℤ/6ℤ are roots of the polynomial g(X) = X 3 − X. In particular, for arbitrary rings the degree does not give a bound on the number of roots.

Theorem 1.48. Let R be an integral domain. The number of roots of a polynomial f ∈ R[X] with f ≠ 0 is at most deg(f). This is still true if multiple roots are counted according to their multiplicity.

Proof: If s1 ∈ R is a root of f , then by [Corollary 1.47](#chapter01_3.xhtml_chapter01_3_10), we first have f(X) = (X − s1)q1(X) for a polynomial q1(X) ∈ R[X] with deg(q1) = deg(f)−1\. If s2 ∈ R is a root of q1(X), we obtain f(X) = (X − s1)(X − s2)q2(X) for q2(X) ∈ R[X] with deg(q2) = deg(f) − 2\. Here, s1 = s2 can possibly hold. We continue this decomposition procedure for f until

![](images/42_1.jpg)

for qm(X) ∈ R[X] with deg(qm) = deg(f) − m ≥ 0 such that qm has no roots in R. If f(s) = 0 for some arbitrary root s ∈ R, then, because R has no zero divisors, at least one of the factors (s − si) has to be zero. This shows that the elements s1, . . . , sm with m ≤ deg(f) are the only roots of f .

□

The following lemma provides a relationship between the derivative of a polynomial and the simplicity of roots.

Proposition 1.49. Let R be an integral domain and f ∈ R[X] with f ≠ 0. A root s ∈ R of f is simple if and only if f (s) ≠ 0.

Proof: If s has at least a multiplicity of 2, then (X − s)2 divides f . By the rule for the derivatives of products given in [Theorem 1.43](#chapter01_3.xhtml_chapter01_3_4), the polynomial (X − s) divides f' (X) and therefore f' (s) = 0\. Suppose that s is a simple root. Then, f can be written as f(X) = (X − s) ⋅ g(X). Now g(s) ≠ 0 because otherwise (X − s) would divide g and thus (X − s)2 would divide f. The derivative of f is f' (X) = g(X) + (X − s) ⋅ g'(X). Thus, we have f' (s) = g(s) + 0 ⋅ g'(s) = g(s) ≠ 0.

□

From [Corollary 1.47](#chapter01_3.xhtml_chapter01_3_10) and [Proposition 1.49](#chapter01_3.xhtml_chapter01_3_13), we obtain the following statement:

Corollary 1.50. Let F be a field and f ∈ F[X]. If f and f' are coprime, then all roots of f are simple roots.

□

Let f ∈ R[X] and 〈f〉, the ideal f ⋅ R[X] generated by f . For the quotient ring R[X]/〈f〉, we write R[X]/f for short. If we write a ≡ b mod f , this means a + 〈f〉 = b + 〈f〉 in R[X]/f .

Let F be a field. A nonconstant polynomial f ∈ F[X] is called irreducible if f cannot be written as the product of two polynomials of strictly lower degree. In particular, any linear polynomial X −a is irreducible. From [Theorem 1.42 (c)](#chapter01_3.xhtml_chapter01_3_2) and [Corollary 1.47](#chapter01_3.xhtml_chapter01_3_10) ,we can directly conclude that a polynomial of degree 2 or 3 is irreducible if and only if it has no roots.

Theorem 1.51. Let F be a field and f ∈ F[X]. Then, F[X]/f is a field if and only if f is irreducible.

Proof: First, let f be irreducible and let g ∈ F[X] \ 〈f〉. Then f and g are coprime. By [Corollary 1.46](#chapter01_3.xhtml_chapter01_3_8), there exist polynomials a, b ∈ F[X] such that af + bg = 1\. Now bg ≡ 1 mod f . Therefore, in F[X]/f every nonzero residue class is invertible, which means that F[X]/f is a field. Note that since deg(f) > 0, the ring F[X]/f is not zero.

For the converse, let f be not irreducible, that is, f is constant or a product of polynomials of smaller degree. First, suppose that f is constant. In the case of f = 0, the quotient F[X]/0 is isomorphic to F[X] and the latter is not a field since polynomials having roots cannot be inverted. If f is a nonzero constant, then F[X]/f is the zero ring and thus not a field. If the polynomial f can be written as a product of two polynomials of strictly smaller degree, f = gh, then g ≢ 0 mod f and h ≢ 0 mod f but gh ≡ 0 mod f . Thus F[X]/f contains zero divisors and therefore is not a field.

□

Next, we examine the size of F[X]/f .

Theorem 1.52. Let F be a field and f ∈ F[X] \ {0}. Then, F[X]/f as an additive group is isomorphic to F deg(f).

Proof: Let d = deg(f) and Fd = { g ∈ F[X] | deg(g) < d }. As an additive group Fd is isomorphic to F d since a polynomial of degree less than d is defined by the sequence of coefficients (a0, . . . , ad−1) ∈ Fd. The homomorphism g ↦ g mod f from Fd to F[X]/f is surjective because, by [Theorem 1.44](#chapter01_3.xhtml_chapter01_3_5), the residue classes of F[X]/f have representatives of degree less than d. It is injective since g = g mod f for all g ∈ F d. This proves the theorem.

□

Example 1.53. Let F = ℤ/2ℤand f = X3+X+1 ∈ F[X]. In F[X]/f, we have f ≡ 0 mod f . Since −1 = +1 holds in F, this is equivalent to X3 ≡ X + 1 mod f . This allows us to reduce exponents i ≥ 3 in Xi. For example, we obtain

![](images/44_1.jpg)

Since deg(f) = 3 and f(r) ≠ 0 for all r ∈ F, f is irreducible in F[X]. Using [Theorems 1.51](#chapter01_3.xhtml_chapter01_3_15) and 1.52, we finally see that F[X]/f is a field with eight elements.

◊

Example 1.54. The Advanced Encryption Standard (AES) works with the irreducible polynomial X8 + X4 + X3 + X +1 of degree 8 over F = ℤ/2ℤ. Here, all computations are done in the field F[X]/(X8 + X 4 + X3 + X +1). This field contains 256 elements that can be represented by 1 byte each, the ith bit being the coefficient of Xi for 0 ≤ i ≤ 7\. The addition operation is the bitwise exclusive-or of 2 bytes and the multiplication rule follows directly from the polynomial representation given above.

◊

## 1.7 Hilbert’s basis theorem

A commutative ring R is called Noetherian if each ideal is generated by a finite set. The term refers to Emmy Noether who was a student of Hilbert and the first female university professor for mathematics in Germany. Hilbert’s basis theorem states that polynomial rings over Noetherian rings are Noetherian themselves. It formed the basis for the rapid development of algebraic geometry in the 20th century. We will restrict our considerations to commutative rings throughout this section.

Every field F is a Noetherian ring since the only two ideals {0} and F require at most one generating element. The ring ℤ is Noetherian since, according to [Theorem 1.32](#chapter01_2.xhtml_chapter01_2_19), every ideal is principal. By [Theorem 1.45](#chapter01_3.xhtml_chapter01_3_7), also every ideal of the polynomial ring F[X] in one variable X over a field F is principal; therefore F[X] is Noetherian, too. In the polynomial ring ℂ[X, Y] in two variables, the ideal 〈X, Y〉 is not principal because if f(X, Y) is supposed to generate the polynomial X, then Y must not occur in f(X, Y). But then the polynomial Y cannot be generated by f(X, Y). As we shall see, ℂ[X, Y] is Noetherian. Generally, the polynomial ring R[X1, . . . , Xn] in n variables is defined inductively as R[X1, . . . , Xn] = R[Xn] for R' = R[X1, . . . , Xn−1].

Theorem 1.55 (Hilbert’s basis theorem). Let n ∈ ℕand R be aNoetherian commutative ring. Then the polynomial ring R[X1, . . . , Xn] is Noetherian.

Proof: Since R[X1, . . . , Xn] = R[Xn] for R' = R[X1, . . . , Xn−1], it suffices to show the theorem for the polynomial ring R[X] in one variable. Let I ⊆ R[X] be an ideal. For f ∈ I, let ℓf be the leading coefficient of f. For f, g ∈ I, both ℓf + ℓg and ℓf − ℓg are the leading coefficients of polynomials of degree at most max{deg(f), deg(g)} in I. The set { ℓf | f ∈ I } is an ideal in R. So, there is a finite set of polynomials B' ⊆ I such that

![](images/45_4.jpg)

Let d = max{ deg(b) | b ∈ B' }. For every, e < d the set { ℓf | f ∈ I, deg(f) ≤ e } is an ideal in R. Thus there is a finite set Be ⊆ I satisfying

![](images/45_5.jpg)

We let B = B' ∪⋃e<d Be. For each f ∈ I, there exists g ∈ 〈B〉 with deg(f) = deg(g) and ℓf = ℓg. By induction on the degree, we have f − g ∈ 〈B〉. This yields f ∈ 〈B〉 and I is generated by the finite set B.

□

A typical application of Hilbert’s basis theorem is the following situation. Let F be a field and N ⊆ Fn be the set of roots of polynomials ![](images/f.jpg) ⊆ F[X1, . . . , Xn]. That is

![](images/45_6.jpg)

Then, N is already the set of roots of a finite subset B ⊆ ![](images/f.jpg) because N is the set of roots of 〈![](images/f.jpg)〉. According to Hilbert’s basis theorem, it is sufficient to have a finite “basis” B' ⊆ 〈![](images/f.jpg)〉. If each element of B' is generated by elements from ![](images/f.jpg), these generators from F provide the desired subset B.

## 1.8 Fields

Throughout this section, F is a field and char(F) its characteristic. If char(F) = 0, then F contains the rational numbers ℚas its prime field. For char(F) ≠ 0, the characteristic is a prime number p and F contains the finite field ℤ/pℤ as its prime field, which we also denote by ![](images/f_d.jpg)p. One also frequently runs across the expression GF(p) for p. Here, GF stands for Galois field. The multiplicative group of finite fields is always cyclic. The same holds for all finite multiplicative subgroups of the complex numbers. This follows from the [next theorem](#chapter01_3.xhtml_chapter01_3_21).

Theorem 1.56. Every finite subgroup of the multiplicative group F ∗ is cyclic.

Proof: Let U be a finite subgroup of F ∗ with order n. Let d1, . . . , dn be the orders of the elements of U and d = lcm(d1, . . . , dn). Each of the n elements of U is a root of the polynomial X d − 1\. From [Theorem 1.48](#chapter01_3.xhtml_chapter01_3_11), we obtain d ≥ n because a polynomial of degree d cannot have more than d roots. Since di | n for all i, we have d | n and thus d = n. In U, there exists an element α of order d. This can be seen as follows. Let u1 and u2 be elements of orders d1 and d2, respectively. There exist powers ![](images/46_3.jpg) and ![](images/46_4.jpg) of u1 and u2, respectively, such that their orders ![](images/46_1.jpg) and ![](images/46_2.jpg) are coprime and satisfy lcm![](images/46_5.jpg) By [Theorem 1.8](#chapter01_1.xhtml_chapter01_1_17), the order of ![](images/46_6.jpg) is lcm(d1, d2). From d = n we now obtain 〈α〉 = U.

□

Corollary 1.57. Let U ⊆ F ∗ be a finite multiplicative subgroup with at least two elements. Then, Σu∈U u = 0.

Proof: Let n be the order of U and g be a generating element. Since n ≥ 2, we have g ≠ 1\. Moreover

![](images/46_13.jpg)

and therefore ![](images/46_8.jpg) The result follows since { gi | 0 ≤ i < n} = U.

□

A field extension E of F is a field that contains F as a subfield. We want to show that, to each polynomial f ∈ F[X], there is a field extension E such that f can be decomposed into linear factors in E [X], that is, E contains (not necessarily different) elements β, α1, . . . , αd such that d = deg(f) and ![](images/46_9.jpg) in E[X]. Here, β ∈ F is the leading coefficient of f . In particular, for finite fields F, the field extension E and the elements αi ∈ E can effectively be determined. We call the field E a splitting field of f over F.

Theorem 1.58. Let f ∈ F[X] with leading coefficient β. Then there is a field extension E and α1, . . . , αd ∈ E with d = deg(f) such that ![](images/46_10.jpg) din E[X]. If F is finite, then we can assume E to be finite.

Proof: If d ≤ 1, there is nothing to do since f already has the desired form. So, let d > 1\. If f is not irreducible, then f can be decomposed into a product f = gh with deg(g) < d and deg(h) < d. The statement is now obtained by induction. First, let E' be the splitting field of g over F. We then construct the splitting field E of h over E' .

□

Finally, let f be irreducible. Then, E' = F[X]/f is a field by [Theorem 1.51](#chapter01_3.xhtml_chapter01_3_15). From the finiteness of F, together with [Theorem 1.52](#chapter01_3.xhtml_chapter01_3_16), we conclude that E ' is finite, too. After renaming the variable X to α, we can write E' ' = F [α]/f(α) and use X again as the name of a variable. In E', by construction we have f(α) = 0\. Thus, α is a root and f ∈ E'[X] can be decomposed into f(X) = (X − α)g(X), where deg(g) < d. Note that the leading coefficient of g is β. Inductively, for g and E' there is a field extension E where g splits into linear factors. Thus, over E [X] we obtain

![](images/46_11.jpg)

where the leading coefficient of f is still β ∈ F. Substituting αd = α, we obtain the desired result

![](images/46_12.jpg)

□

A field E is algebraically closed if every nonzero polynomial f(X) ∈ E [X] admits a factorization ![](images/47_1.jpg) for β, αi ∈ E. Applying [Theorem 1.58](#chapter01_3.xhtml_chapter01_3_24) “infinitely often” to a field F and all polynomials over this field leads to the so-called algebraic closure of F. By construction, the algebraic closure of F is algebraically closed. The formal proof for the existence of the algebraic closure is based on the axiom of choice. Furthermore, one can show that the algebraic closure of a field is unique up to isomorphism; this means that all minimal field extensions of F where every polynomial splits into linear factors are isomorphic. The algebraic closure of a field F is always infinite, even if F itself is finite. The complex numbers ℂ are the algebraic closure of the field of real numbers ℝ but not of the rational numbers ℚ because, among others, the number π is not in the algebraic closure of ℚ.

Let n ≥ 1 and G ⊆ ℂ be the set of roots of the polynomial X n − 1 over the complex numbers ℂ. Since the polynomial X n − 1 and its derivative nXn−1 are coprime, Xn − 1 has n different roots. These roots form a finite subgroup of ℂ∗. By [Theorem 1.56](#chapter01_3.xhtml_chapter01_3_21), the group G is cyclic of order n. This shows that every cyclic group can be found as a subgroup of ℂ∗. We now want to examine the situation in arbitrary fields.

Theorem 1.59. Let n ≥ 1 be an integer with char(F) ∤ n. Then there is a field extension E of F and an element α ∈ E ∗ of order n such that

![](images/47_2.jpg)

We call α a primitive root of unity of order n.

Proof: We already know that f(X) = Xn − 1 splits into linear factors in an appropriate field extension E. The roots of f(X) form a finite subgroup of E ∗ consisting of at most n elements. By [Theorem 1.56](#chapter01_3.xhtml_chapter01_3_21), this subgroup is cyclic. Furthermore, we have f' (X) = nXn−1. Since char(F) does not divide n, we have f' (α) ≠ 0 for all α ∈ E∗. Since f(0) ≠ 0, all roots of X n − 1 are simple. Thus, they are pairwise distinct and the cyclic subgroup is generated by an element α of order n.

□

## 1.9 Finite fields

A special case of [Theorem 1.56](#chapter01_3.xhtml_chapter01_3_21) shows that the multiplicative group of finite fields is always cyclic. This fact is of central importance for the study of finite fields.

Every field is a vector space over its prime field. In particular, a finite field F is a finite-dimensional vector space over its prime field ![](images/f_d.jpg)p for a prime number p. If the dimension is n, then F contains exactly pn elements. We state this property in the following theorem and give an alternative proof that does not require linear algebra, but uses Cauchy’s theorem instead.

Theorem 1.60. Let F be a finite field of characteristic p. Then there exists n ≥ 1 with |F| = pn.

Proof: By [Lemma 1.26](#chapter01_2.xhtml_chapter01_2_7), the number p is prime. Then, in the additive group of F, all nonzero elements have order p. By Cauchy’s theorem ([Theorem 1.9](#chapter01_1.xhtml_chapter01_1_19)), for every prime divisor q of |F|, there is an element of order q. Thus, p is the only prime divisor of |F| and hence, |F| = pn for an appropriate exponent n ≥ 1.

□

Theorem 1.61. Let p be a prime number and n ≥ 1. Then there exists a field with pn elements.

Proof: Let q = pn and let E be a finite splitting field of f(X) = Xq − X over p. The field E exists by [Theorem 1.58](#chapter01_3.xhtml_chapter01_3_24). The derivative of f is f' (X) = −1\. Thus, f and f' ' are coprime and, by [Corollary 1.50](#chapter01_3.xhtml_chapter01_3_14), all roots of f are simple. This shows that Xq − X has exactly q different roots in E. By [Theorem 1.28](#chapter01_2.xhtml_chapter01_2_9), the n-fold application of the Frobenius automorphism yields an automorphism φ: E → E, x ↦ xq. The roots of f are those elements x which satisfy φ(x) = x. These elements form a field with pn elements.

□

Theorem 1.62. Let F and K be finite fields and |K| a power of |F|. Then, F is isomorphic to a subfield of K.

Proof: Let |F| = q = pn for a prime number p and n ≥ 1\. By [Theorem 1.56](#chapter01_3.xhtml_chapter01_3_21), both F ∗ and K ∗ are cyclic. First, let α be a generator of F ∗. Then, α is a root of the polynomial Xq−1−1 ∈ p[X]. Let f be a factor of Xq−1−1 with f(α) = 0 in F such that f is irreducible in p[X]. By [Theorem 1.51](#chapter01_3.xhtml_chapter01_3_15), the quotient ring ![](images/f_d.jpg)p[X]/f is a field. The homomorphism φ: ![](images/f_d.jpg)p[X]/f → F, g(X) ↦ g(α) is well defined and thus surjective. Therefore, φ is an isomorphism by [Corollary 1.24](#chapter01_2.xhtml_chapter01_2_5). Without loss of generality, we assume that F = ![](images/f_d.jpg)p[X]/f in the remainder of the proof.

Since K contains qk elements for some k ≥ 1, its prime field is ![](images/f_d.jpg)p. The cyclic group K ∗ contains qk−1 elements and thus it contains a cyclic subgroup of order q −1\. Therefore, Xq−1 − 1 can be decomposed into linear factors over K, and f as a divisor of Xq−1 − 1 has a root β ∈ K. We now define a homomorphism ψ: Fp[X]/f → K, g(X) ↦ g(β). As a homomorphism of fields it is injective and thus F appears as an isomorphic subfield of K.

□

An immediate consequence of the [previous theorem](#chapter01_3.xhtml_chapter01_3_28) is that, up to isomorphism, every finite field is uniquely determined by its number of elements. This justifies the notation q or GF(q), respectively, for the field with q elements. By combining the results in this section, we obtain the following classification of finite fields.

Corollary 1.63. For every prime power q > 1, up to isomorphism there is a unique field q with q elements. Moreover, all finite fields are of this form.

Proof: By [Theorem 1.61](#chapter01_3.xhtml_chapter01_3_28), there exists a field ![](images/f_d.jpg)q with q elements. By [Theorem 1.62](#chapter01_3.xhtml_chapter01_3_29), this field is unique up to isomorphism. Finally, by Theorem 1.60, there are no other finite fields.

□

Example 1.64. Let n ≥ 1\. By [Theorem 1.61](#chapter01_3.xhtml_chapter01_3_28), there is a field extension E over ![](images/f_d.jpg)2 with 2n elements and it can be written as E = ![](images/f_d.jpg)2[X]/f for an irreducible polynomial f(X) ∈ ![](images/f_d.jpg)2[X] of degree n. If we regard E as a vector space over ![](images/f_d.jpg)2, then the elements 1, X, . . . , Xn−1 from E are linearly independent. If we define αi = (0 ⋅⋅ ⋅ 010 ⋅⋅ ⋅ 0) with 1 at the (n − i)th position from the left, then Xi ↦ αi induces a bijection between E and the set ![](images/b.jpg)n of 0 − 1 sequences of length n. Here, any polynomial of degree less than n is represented by the sequence of its coefficients. In particular, this yields the structure of a field on ![](images/b.jpg)n.

Now let f(X) = X3 + X2 + 1 ∈ ![](images/f_d.jpg)2[X]. This polynomial has no roots in ![](images/f_d.jpg)2. Its degree is 3, so f is irreducible and E = ![](images/f_d.jpg)2[X]/f is a field with eight elements. The elements of E are the linear combinations of 1, X, X2 with coefficients from ![](images/f_d.jpg)2. The sequences of these coefficients result in a representation of E by 0 − 1 sequences of length 3\. Multiplying such sequences, for example, we obtain

![](images/49_5.jpg)

because (X2 + 1)(X2 + X + 1) ≡ 1 mod f in ![](images/f_d.jpg)2[X].

◊

## 1.10 Units modulo n

We have seen that the group of units (ℤ/nℤ)∗ is cyclic if n is prime. In this section, we want to describe the structure of the multiplicative group (ℤ/nℤ)∗ for prime powers n. The structure of (ℤ/nℤ)∗ for arbitrary numbers n can then be obtained using the Chinese remainder theorem. Considering the group G = (ℤ/8ℤ)∗, we can identify G with the odd numbers 1, 3, 5, 7\. We have a2 = 1 for all a ∈ G. Particularly G, being of order 4, is not a cyclic group. We start with two technical lemmas.

Lemma 1.65. Let p be an odd prime and e ≥ 2. For all a ∈ ℤ, we have

![](images/49_6.jpg)

Proof: For e = 2, the statement is trivial. So, let e > 2\. Inductively, we have ![](images/49_7.jpg) ≡ 1 + ape−2 mod pe−1. Hence, there is a number b ∈ ℤ such that ![](images/49_8.jpg) + ape−2 + bpe−1. Using ![](images/49_3.jpg) for 1 ≤ k < p, we obtain

![](images/49_4.jpg)

Now, ![](images/49_10.jpg) because p > 2, and thus ![](images/49_9.jpg) mod pe follows.

□

Lemma 1.66. Let e ≥ 3. Then for all a ∈ ℤ, we have (1 + 4a)2e−3 ≡ 1 + 2e−1a mod 2e.Proof: The statement is trivial for e = 3\. Let e > 3\. Then by inductive hypothesis, we may assume that (1+4a)2e−4 = 1+2e−2a+ 2e−1b for b ∈ ℤ. Using e ≤ 2e−4,we obtain

![](images/50_3.jpg)

We now use these two lemmas to show that certain elements in (ℤ/peℤ)∗ have a large order.

Theorem 1.67. Let p be an odd prime. Then, for all e ≥ 1 the group (ℤ/peℤ)∗ is cyclic. For e ∈ {1, 2}, the group (ℤ/2eℤ)∗ is cyclic, too. If e > 2, then (ℤ/2eℤ)∗ is isomorphic to the additive group ℤ/2ℤ×ℤ/2e−2ℤ and therefore not cyclic.

Proof: The multiplicative group of a finite field is cyclic. This shows the assertion for all cases where e = 1\. Now let p be odd and e ≥ 2. We choose a generator g of (ℤ/pℤ)∗. Then, gp−1 = 1 + ap and (p + g)p−1 = 1 + bp for suitable integers a and b. Suppose that p | a and p | b. Then, gp ≡ g mod p2 and (p + g)p ≡ p + g mod p2, which leads to a contradiction as follows:

![](images/50_2.jpg)

Thus, without loss of generality, we may assume that gcd(a, p) = 1; otherwise we could take p + g as generating element of (ℤ/pℤ)∗. [Lemma 1.65](#chapter01_4.xhtml_chapter01_4_1) yields (1 + ap)pe−1 ≡ 1 + ape mod pe+1 and therefore (1 + ap)pe−1 ≡ 1 mod pe. In particular, the order of 1+ap in (ℤ/peℤ)∗ divides pe−1.Again from [Lemma1.65](#chapter01_4.xhtml_chapter01_4_1), we conclude that (1+ap)pe−2 ≡ 1 + ape−1 ≢ 1 mod pe. Therefore, the order of gp−1 in (ℤ/peℤ)∗ is pe−1 and, thus, the order of g is (p − 1)pe−1. Consequently, (ℤ/peℤ)∗ is cyclic.

The group (ℤ/4ℤ)∗ is cyclic because it is of order 2\. We now come to the case p = 2 and e > 2\. [Lemma 1.66](#chapter01_4.xhtml_chapter01_4_2) implies 52e−2 = (1 + 4)2e−2 ≡ 1 + 2e mod 2e+1 and thus 52e−2 ≡ 1 mod 2e. Quite similarly, one can show that 52e−3 ≡ 1 + 2e−1≢ 1 mod 2e. Therefore, the order of the number 5 in (ℤ/2eℤ)∗ is 2e−2. Let G be the subgroup of (ℤ/2eℤ)∗ generated by 5\. Suppose that −1 ∈ G; in other words, we have 5n ≡ −1 mod 2e for some n ∈ ℕ. Then, −1 ≡ 5n ≡ 1 mod 4, a contradiction. This shows G ∩ −G = 0\. From |G ∪ −G| = 2e−1 = |(ℤ/2eℤ)∗| we obtain G ∪ −G = (ℤ/2eℤ)∗. In particular, the group homomorphism ℤ/2ℤ × ℤ/2e−2ℤ → (ℤ/2eℤ)∗, (a, b) ↦ (−1)a5b is surjective and hence bijective.

□

## 1.11 Quadratic reciprocity

Let ![](images/f_d.jpg)q be a finite field. An element a ∈ ![](images/f_d.jpg)q is a square or a quadratic residue if there exists b ∈ ![](images/f_d.jpg)q with b2 = a. In this case, we call b a square root of a. If b is a square root of a, then so is −b. Since quadratic equations over fields have at most two solutions, b and −b are the only square roots of a. In general, not all elements of a field are squares. As a simple example, consider 3 = {0, 1, −1}, where −1 is not a square. The following theorem, named after Euler, gives an effective criterion to test whether a ∈ q is a square.

Theorem 1.68 (Euler’s criterion). Let q be a finite field and q ∈ ℕ be odd. Then the mapping ![](images/51_1.jpg) is a surjective homomorphism of (multiplicative) groups. Moreover

![](images/51_2.jpg)

Proof: If a is a square, then there exists ![](images/51_3.jpg) with b2 = a. From [Corollary 1.5](#chapter01_1.xhtml_chapter01_1_14), we obtain ![](images/51_4.jpg) Now, let a not be a square. By [Theorem 1.56](#chapter01_3.xhtml_chapter01_3_21), the multiplicative group ![](images/51_19.jpg) is cyclic. Let g be a generator of this group and choose k ∈ ℕ such that a = g2k+1. From gq−1 = 1, we conclude ![](images/51_5.jpg) because the polynomial X2 − 1 has no other roots. Since the order of g is q − 1, we obtain ![](images/51_6.jpg) and thus

![](images/51_7.jpg)

Now we have shown that in all cases ![](images/51_8.jpg) and 1 occurs if and only if a is a square. This also shows that the mapping is a homomorphism. For surjectivity, we note that ![](images/51_9.jpg) and ![](images/51_10.jpg) for all generators g of ![](images/51_11.jpg)

□

Euler’s criterion implies that there are as many squares as nonsquares in ![](images/51_12.jpg) if q is odd. We take a look at squares in prime fields ℤ/pℤ. At first glance, the fields ℤ/pℤ and ℤ/qℤ for different primes p and q do not seem to have very much in common. But, surprisingly, both structures are tightly connected by their quadratic residues. This is what the law of quadratic reciprocity is about.

Let n be an arbitrary odd number and a ∈ ℤ coprime to n. The mapping x ↦ ax mod n defines a permutation on the set {0, . . . , n − 1}. We let

![](images/51_13.jpg)

and call ![](images/51_14.jpg) the Jacobi symbol (named after Carl Gustav Jacob Jacobi, 1804–1851); it is the sign of the permutation x ↦ ax mod n. The connection between quadratic residues and signs of permutations is given by the following result of Yegor Ivanovich Zolotarev (1847–1878).

Theorem 1.69 (Zolotarev’s lemma). Let p be an odd prime and a ∈ ℤ such that p ∤ a. Then, a is a square modulo p if and only if ![](images/51_15.jpg)

Proof: [Lemma 1.15](#chapter01_1.xhtml_chapter01_1_33) shows

![](images/51_16.jpg)

The last congruence follows from Fermat’s little theorem. Euler’s criterion yields the result.

□

By Zolotarev’s lemma, also the commonly used Legendre symbol (named after Adrien-Marie Legendre, 1752–1833) can be defined using the Jacobi symbol. Usually, the same notation is used. However, only odd primes p are considered. Moreover, the domain of ![](images/52_4.jpg) is extended to all a ∈ ℤ by having ![](images/52_2.jpg) for p | a. From Euler’s criterion, we obtain for the Legendre symbol ![](images/52_1.jpg) the property ![](images/52_3.jpg) mod p for all a ∈ ℤ.

Now, we formulate the law of quadratic reciprocity in [Theorem 1.70 (a)](#chapter01_4.xhtml_chapter01_4_9), along with its two supplements [(b)](#chapter01_4.xhtml_chapter01_4_10) and [(c)](#chapter01_4.xhtml_chapter01_4_11) and the two multiplication rules ([d)](#chapter01_4.xhtml_chapter01_4_12) and ([e)](#chapter01_4.xhtml_chapter01_4_13) for the Jacobi symbol.

Theorem 1.70 (Law of quadratic reciprocity). Let m ∈ ℤ, and let n ∈ ℕ be odd with gcd(m, n) = 1. Then the following statements hold:

![](images/52_5.jpg)![](images/52_6.jpg)![](images/52_7.jpg)![](images/52_8.jpg)![](images/52_9.jpg)

Proof: (a) We first assume that m, n ≥ 1 and that m is odd. The permutation x ↦ x+1 mod m has the sign 1 because the elements 0, . . . , m−2 all have an inversion with m − 1 and there are no other inversions. By sequential application of the mappings, we see that sgn(x ↦ x + y0 mod m) = 1 holds for all y0 ∈ ℤ. Let P = {0, . . . , m − 1} × {0, . . . , n − 1}.We define mappings μ and ν on P by

□

![](images/52_16.jpg)

For every fixed y', the mapping νy' : (x, y') → (nx + y'  mod m, y') is a permutation on the set {0, . . . , m − 1} × {y'} and its sign is ![](images/52_10.jpg) The mapping νy' also defines a permutation of the same sign on the set P if every value (x, y) with y ≠ y' is mapped to itself. Now ν is the sequential application of all ' νyfor 0 ≤ y'  < n. This yields sgn![](images/52_12.jpg) Analogously, μ is a permutation with sgn![](images/52_11.jpg) Thus

![](images/52_13.jpg)

By the Chinese remainder theorem, we can regard μ∘ ν−1 as a permutation π on the set {0, . . . , mn − 1}. For (x, y) ∈ P, it maps nx + y to x + my. We now count the inversions of π. These are the pairs ((x, y), (x' , y')) ∈ P2 satisfying nx + y < nx'  + y' and x + my > x'  + my. The last two requirements are equivalent to x < x' and y > y'. Therefore, π has ![](images/52_14.jpg) inversions. This shows

![](images/52_15.jpg)

Now, we have shown (a) for positive numbers because ![](images/53_1.jpg)

(b)Using [Lemma 1.15](#chapter01_1.xhtml_chapter01_1_32), we obtain

![](images/53_2.jpg)

(d)This property holds according to [Theorem 1.16](#chapter01_1.xhtml_chapter01_1_34) because sgn is a homomorphism. In particular, the law of quadratic reciprocity (a) holds for all odd numbers m ∈ ℤwith gcd(m, n) = 1.

(c)From what we have already shown, we conclude

![](images/53_3.jpg)

The assertion follows by induction on n.

(e)By the Chinese remainder theorem, there exists r ∈ ℕ with r ≡ 1 mod 4 and r ≡ m mod n. Thus

![](images/53_4.jpg)

This completes the proof.

□

The proof of the law of quadratic reciprocity, we presented here goes back to George Rousseau [[89](#Bibliography.xhtml_Bibliography_90)]. The law of quadratic reciprocity yields the following algorithm for computing the Jacobi symbol:

![](images/53_6.jpg)

Note that, in this algorithm, only the four least significant bits of the numbers m and n are used to find out whether powers of −1 evaluate to 1 or −1.

Exercises

1.1. Show that every semigroup has at most one neutral element.

1.2. Show that in a monoid every element has at most one inverse.

1.3. Show that in a finite monoid M each left inverse is also right inverse, that is, ba = 1 implies ab = 1 for all a, b ∈ M.

1.4. Show that for infinite monoids, the claim of [Exercise 1.3](#chapter01_4.xhtml_chapter01_4_17) does not hold in general.

1.5. Let S be a semigroup. An element a ∈ S is called regular if there exists b ∈ S such that aba = a. Show that for every regular element a ∈ S, there is an element c ∈ S with both aca = a and cac = c.

1.6. Let S be a finite semigroup. Recall that an element e ∈ S is idempotent if it satisfies e2 = e. Show:

(a)For each x ∈ S, the set { xk | k ≥ 1} ⊆ S contains a unique idempotent element. This element is some power xℓ with 1 ≤ ℓ ≤ |S|.

(b)The element x|S|! is idempotent for all x ∈ S.

1.7. Let φ: M → G be a homomorphism from a finite semigroup M onto a group G and H be a smallest subsemigroup of M such that φ(H) = G. Show that H is a group.

1.8. A semigroup S is inverse if for every x ∈ S there exists a unique element ![](images/54_1.jpg) such that ![](images/54_2.jpg) and ![](images/54_3.jpg)

(a)Show ![](images/54_4.jpg) for idempotents e, f of an inverse semigroup.

(b)Show that the idempotents in an inverse semigroup forma commutative subsemigroup.

1.9. Let S be a finite semigroup with n elements and a1, . . . , an ∈ S be arbitrary. Show that there exists an index i ∈ {1, . . . , n} and an element b ∈ S with a1 ⋅⋅ ⋅ ai = a1 ⋅⋅ ⋅ aib.

1.10. Specify a finite monoid M and a submonoid U of M such that | U| does not divide |M|.

1.11. Let X and Y be nonempty sets, S a semigroup, and φ: Y × X → S a mapping. Show that the operation ∘ with (x, s, y) ∘ (x' , s' , y) = (x, s ⋅ φ(y, x) ⋅ s' , y) defines a semigroup on the set X × S × Y, the so-called Rees sandwich semigroup named after David Rees (1918–2013).

1.12. Show that, in a group, only the neutral element is idempotent. Moreover, a finite monoid is a group if and only if it has exactly one idempotent.

1.13. Let G be a semigroup. Prove the following assertions:

(a)Suppose there is an element e ∈ G with the following properties:

–For all g ∈ G, we have eg = g (left neutral element).

–For all g ∈ G, there exists h ∈ G with hg = e (left inverse elements). Then, G is a group.

(b)Suppose there is an element e ∈ G with the following properties:

–For all g ∈ G, we have ge = g (right neutral element).

–For all g, ∈ G there exists h ∈ G with hg = e (left inverse elements). Then, G is not necessarily a group.

(c)If for all a, b ∈ G the equations ax = b and ya = b have solutions x, y ∈ G, then G is a group.

1.14. Let G be a group and S ⊆ G a subset.

(a)Show that the following properties are equivalent:

(i)S is a subgroup of G.

(ii) S ≠ 0 and xy−1 ∈ S for all x, y ∈ S.

(b)Let S be finite. Show that the following properties are equivalent:

(i)S is a subgroup of G.

(ii) S ≠ 0 and xy ∈ S for all x, y ∈ S.

(c)Specify a group G and an infinite subset S ⊆ G such that S is not a subgroup of G, but it has the property xy ∈ S for all x, y ∈ S.

1.15. Let G and H be groups and φ: G → H be a mapping. Show that the following properties are equivalent:

(i)φ is a group homomorphism, that is, for all x, y ∈ G, we have φ(1G) = 1H, φ(x−1) = φ(x)−1, and φ(xy) = φ(x)φ(y).

(ii) For all x, y ∈ G, we have φ(xy) = φ(x)φ(y).

1.16. LetMbe a monoid satisfying m2 = 1 for all m ∈ M. Show that M is a commutative group.

1.17. Show that in a commutative group G the elements of odd order form a subgroup.

1.18. Let G be a group and H be a subgroup of G. Show that the implication xH = yH ⇒ xHx−1 = yHy−1 holds for all x, y ∈ G.

1.19. Let G be a (possibly infinite) group and H a subgroup satisfying [G : H] = n < ∞, that is, H has finite index. Prove the following assertions:

(a)For all g ∈ G there exists i ∈ {1, . . . , n} such that gi ∈ H.

(b)N = ⋂x∈G xHx−1 is the largest normal subgroup of G contained in H. Furthermore, G/N is finite.

1.20. Show that the relation given by the normal subgroup property is not transitive.

1.21. Let G be a group. Show that the bijective function f : G → G with f(a) = a−1 is a group homomorphism if and only if G is commutative.

1.22. Let G and H be groups, let f : G → H be a group homomorphism and let a ∈ G be an element of finite order. Show that the order of f(a) divides the order of a.

1.23. Show that every finite domain R is a skew field.

1.24. Let R be a commutative ring. Show that for a subset I ⊆ R, the following statements are equivalent:

(i)I is an ideal.

(ii) I is an additive subgroup such that R /I with the operations

![](images/56_2.jpg)

forms a ring, where I is the neutral element with respect to addition and 1 + I is the neutral element with respect to multiplication.

(iii) I is the kernel of a ring homomorphism.

1.25. Let R be a ring and I and J be ideals in R with I ⊆ J. Show that R/J and (R/I)/(J/I) are isomorphic.

1.26. Let R be a ring and I and J be ideals of R. Which of the following sets are ideals of R?

| (i)I + J | (ii) I ⋅ J | (iii) I ∪ J | (iv) I ∩ J |

1.27. Show that in the ring ℤ[X], the ideal 〈6, X2 − 2〉 = 6ℤ[X]+(X2−2)ℤ[X] is neither a principal ideal nor maximal.

1.28. Determine the order of the element 3 in the multiplicative group (ℤ/16ℤ)∗.

1.29. Count the elements in (ℤ/60ℤ)∗ with even order.

1.30. Let m, n > 1 be natural numbers with gcd(m, n) > 1\. Show that the additive groups (ℤ/mℤ) × (ℤ/nℤ) and ℤ/mnℤ are not isomorphic.

1.31. Find s ∈ ℕwith 51 ⋅ s ≡ 1 mod 98.

1.32. Find the two smallest numbers n1, n2 ∈ ℕsuch that the following congruences for i = 1, 2 are satisfied: ni ≡ 2 mod 3, ni ≡ 3 mod 4 and ni ≡ 6 mod 7.

1.33. Show that ![](images/56_3.jpg)mod 60 for all n ∈ ℕ.

1.34. Show that 5 is the only prime number of the form z4 +4 with z ∈ ℤ. Hint: Use polynomial division to determine a polynomial p such that z4 + 4 = (z2 − 2z + 2) ⋅ p(z).

1.35. Compute gcd(X6 + X5 + X3 + X, X8 + X7 + X6 + X4 + X3 + X + 1) in the polynomial ring ![](images/f_d.jpg)2[X] over the two-element field ![](images/f_d.jpg)2.

1.36. Let f(X) = X5+X2 +1 ∈ ![](images/f_d.jpg)2[X]. Show that f(X) is irreducible over the two-element field ![](images/f_d.jpg)2.

1.37. Let t ≥ 1\. The polynomial f(X) ∈ ℝ[X] is called t-thin if it is the sum of at most t terms of the form aiXi. Then, f(X) =Σi≥0 aiXi and ai ≠ 0 for at most t indices i. Show that the number of positive real roots of f(X) ≠ 0 is bounded by t − 1.

1.38. Let 0 ≠ f (X) = Σi aiXi ∈ ℝ[X] be a polynomial of degree d. The number of sign changes of f(X) is the number of sign changes in the sequence (a0, . . . , ad); and this is defined as the number of sign changes in the subsequence that remains if all aj with aj = 0 are omitted. The number of sign changes in the sequence (0, 1, 0, −3, 4, 0, 2, −1) thus is that of (1, −3, 4, 2, −1), which is 3.

(a)Let 0 < λ ∈ ℝ be a positive real number. Show that the number of sign changes of g(X) = (X − λ)f(X) is strictly greater than the number of sign changes of f(X).

(b)(Descartes’ rule of signs; named after René Descartes, 1596–1650) The number of positive real roots (with multiplicities) of f(X) is bounded by the number of sign changes in the sequence (a0, . . . , ad).

1.39. Let f(X) = Xn + an−1Xn−1 + ⋅⋅ ⋅ + a0 ∈ ℤ[X]. Show that if r ∈ ℚ is a root of f(X), then r ∈ ℤ and r divides a0.

1.40. (Eisenstein’s criterion; named after F. Gotthold M. Eisenstein, 1823–1852) Let f(X) = anXn + ⋅⋅ ⋅ + a0X0 ∈ ℤ[X] with n ≥ 1 and an ≠ 0\. Suppose there exists a prime number p such that p ∤ an and p | an−1, ..., p | a0, but p2 ∤ a0. Show that f(X) is irreducible over ℚ.

1.41. Prove the following statements using Eisenstein’s criterion from the previous exercise:

(a)Let p be a prime number and f(X) = Xn − p for n ≥ 1\. Then, f(X) is irreducible over ℚ and thus in particular ![](images/57_1.jpg)

(b)Let p be a prime number and f(X) = Xp−1 + Xp−2 +⋅ ⋅⋅ +1\. Then, f(X) is irreducible over ℚ.

Hint: f(X) can be written as ![](images/57_2.jpg) and f(X) is irreducible over ℚ if and only if f(X + 1) is.

1.42. We extend formal power series to series of the form

![](images/57_3.jpg)

Claim: The series ![](images/57_4.jpg) satisfies S(X) = 0.

Proof: X ⋅ S(X) = S(X) and therefore S(X) ⋅ (1 − X) = 0\. On the other hand, (1 − X) ⋅ Σi≥0 X i = 1\. From these facts, we obtain

![](images/57_5.jpg)

Where is the error in this proof?

1.43. Consider the set ![](images/58_1.jpg) with addition defined by (a + ![](images/58_3.jpg) and multiplication by ![](images/58_2.jpg) ![](images/58_6.jpg) Show that, with these operations, ![](images/58_4.jpg) is a field.

1.44. Let F be a field, E a field extension of F and α ∈ E a root of the polynomial p(X) ∈ F[X] with deg(p) ≥ 1\. Prove that there is a unique polynomial m(X) ∈ F[X] with the leading coefficient 1 and the property

![](images/58_7.jpg)

The polynomial m(X) is called the minimal polynomial of α.

1.45. Let a ∈ ℤand p an odd prime with p ∤ a. Let m be the order of a in (ℤ/pℤ)∗ and n the order of a in (ℤ/peℤ)∗ for e ≥ 1\. Show that m | n and ![](images/58_5.jpg)

1.46. Let ![](images/f_d.jpg) be a field with q elements for an odd number q. Show that a ∈ is a square if and only if X − a ∈ [X] divides the polynomial X(q−1)/2 − 1.

## Summary

Notions

–semigroup, monoid

–Abelian, commutative

–homomorphism

–isomorphism

–group, inverse element

–generated substruct. 〈X〉

–coset

–order of a group

–order of an element

–index [G : H]

–cyclic group

–generating element

–kernel ker(φ), image im(φ)

–normal subgroup

–quotient group G /H

–symmetry group

–symmetric group

–inversion

–sign sgn(π)

–transposition

–(commutative) ring

–zero ring

–skew field

–field

–subring, subfield

–ring homomorphism

–ideal, quotientring

–principal ideal

–maximal ideal

–zero divisor

–(integral) domain

–characteristic char(R)

–prime field

–Frobenius homomorphism

–formal power series

–polynomials R [X]

–zero polynomial

–degree deg(f)

–leading coefficient

–derivative f '

–root, multiplicity

–irreducible

–Noetherian ring

–field extension

–splitting field

–algebraic closure

–finite field q

–Jacobi symbol

–Legendre symbol

Methods and results

–partitioning into cosets

–Lagrange’s theorem: |G| = [G : H]⋅ |H|

–g|G| = 1\. Moreover: gn = 1 ⇔ order of g divides n

–groups of prime order are cyclic

–subgroups of cyclic groups are cyclic

–G Abelian group, g, h ∈ G with coprime orders m, n ⇒ gh is of order mn

–Cauchy’s theorem: p prime divisor of |G| ⇒ G has an element of order p

–normal subgroups are exactly the kernels of group homomorphisms

–subgroups of index 2 are normal subgroups

–homomorphism theorem for groups: φ: G → H homomorphism ⇒ G/ ker(φ) ≅ im(φ)

–structure of the symmetry group of a regular polygon

–π permutation on {1, . . . , n}. Then, sgn(π) = (−1)# of inversions ![](images/59_1.jpg)

–sgn: Sn → {−1, 1} is a homomorphism

–π is product of m transpositions ⇒ sgn(π) = (−1)m

–each permutation is the product of transpositions

–homomorphism theorem for rings: φ: R → S homomorphism ⇒ R/ ker(φ) ≅ im(φ)

–ring homomorphisms φ: F → R with F a field and R ≠ {0} are injective

–R commutative. Then: I ⊆ R maximal ideal ⇔ R/I field

–R domain ⇒ char(R) = 0 or char(R) = p prime

–binomial theorem: ![](images/59_2.jpg)

–R commutative, char(R) = p prime ⇒ x ↦ xp is a homomorphism on R

–Fermat’s little theorem: R commutative, char(R) = p prime ⇒ ∀a ∈ R: ap = a

–Bézout’s lemma: For all k,ℓ ∈ ℤ there exist a, b ∈ ℤ with gcd(k, ℓ) = ak + bℓ.

–extended Euclidean algorithm

–k ∈ (ℤ/nℤ)∗ ⇔ gcd(k, n) = 1 ⇔ the mapping x ↦ kx on ℤ/nℤ is bijective

–n is prime ⇔ ℤ/nℤ is a field

–ideals in ℤ are generated by a single element

–k | ℓ ⇔ ℓℤ ⊆ kℤ; kℤ + ℓℤ = gcd(k, ℓ)ℤ; kℤ ∩ ℓℤ = lcm(k, ℓ)ℤ

–Chinese remainder theorem: For gcd(k, ℓ) = 1, the mapping ℤ/kℓℤ → ℤ/kℤ × ℤ/ℓℤ defined by x mod kℓ ↦ (x mod k, x mod ℓ) is a homomorphism of rings.

–computing Euler’s totient function: φ(pk) = (p − 1)pk−1 for p prime, φ(kℓ) = φ(k)φ(ℓ) for gcd(k, ℓ) = 1

–Euler’s theorem: gcd(a, n) = 1 ⇒ aφ(n) ≡ 1 mod n

–Σd|n φ(d) = n

–G cyclic group of order n, d | n ⇒ G has φ(d) elements of order d

–R![](images/open.jpg)X![](images/close.jpg) integral domain ⇔ R integral domain

–f ∈ R![](images/open.jpg)X![](images/close.jpg) invertible ⇔ f(0) ∈ R invertible

–deg(f + g) ≤ max(deg(f), deg(g))

–deg(f ⋅ g) ≤ deg(f) + deg(g) with equality in the case of integral domains

–(f + g)' = f ' + g; (f ⋅ g)' = f ' ⋅ g + f ⋅ g'

–polynomial division

–F field⇒every ideal in K [X] is principal

–gcd of polynomials over a field

–f(s) = 0 ⇔ (X − s) divides f(X)

–R integral domain, f ≠ 0 ⇒ f(X) ∈ R[X] has at most deg(f) roots

–Let R be an integral domain, f ≠ 0\. Then: root s of f is a simple root ⇔ f (s) ≠ 0

–F field, f ∈ F[X], f and f ' coprime ⇒ all roots of f are simple

–F field, f ∈ F[X]. Then: F[X]/f field ⇔ f irreducible

–F field, 0 ≠ f ∈ F[X] ⇒ F[X]/f as additive group is isomorphic to Fdeg(f)

–Hilbert’s basis theorem: R Noetherian and commutative ⇒ R [X1, . . . , Xk] Noetherian

–finite subgroups of the multiplicative group of a field are cyclic

–the multiplicative groups of finite fields are cyclic

–U finite subgroup of F∗, |U| ≥ 2 ⇒ Σu∈U u = 0

–∀f ∈ F[X] there is a splitting field E. And: F finite ⇒ E finite

–existence of primitive roots of unity in fields

–F finite field ⇒ |F| = pn for prime p

–For all n ≥ 1 and primes p there is a field F with |F| = pn.

–finite fields with the same number of elements are isomorphic

–p ≥ 3 prime ⇒ (ℤ/peℤ)∗ cyclic

–Fore ≥ 2, the group (ℤ/2eℤ)∗ is isomorphic to the additive group ℤ/2ℤ×ℤ/2e−2ℤ.

–Euler’s criterion: Let q be odd. Then: ![](images/60_2.jpg) is a square ⇔ ![](images/60_1.jpg)

–If q is odd, then exactly half of the elements in ![](images/60_3.jpg) are squares.

–Zolotarev’s lemma: Let p ≥ 3 be prime. Then: a ∈ (ℤ/pℤ)∗ is a square ⇔ ![](images/60_5.jpg)

–Law of quadratic reciprocity: m, n ∈ ℕodd and coprime, m = m1m2, n = n1n2. Then: ![](images/60_6.jpg) ![](images/60_7.jpg) and ![](images/60_4.jpg)

–computing the Jacobi symbol

# 2 Cryptography

Historically, cryptography was placed in the realm of espionage, diplomacy, and warfare. Etymologically, the name goes back to the Greek words kryptos (κρυπτoζ , hidden) and graphein (γραφϵιν,writing). Although some people considered the mathematics of devising and breaking codes, for a long time it remained a discipline on the fringe of mathematics. Several things changed this view. During the Second World War, sophisticated mathematical techniques were developed to break the Enigma code of the German forces. The following Cold War and the widespread usage of computers and the advent of the Internet led to the need of sending financial and other sensitive information over public channels. This sparked an intensive development in mathematical cryptography, both symmetric and public key. Besides the classical intention of protecting messages and data against unauthorized reading, cryptography has nowadays a much wider range of applications. These include digital signatures and electronic obligations. A digital signature is to be thought of as an analog of a written signature but for electronic or digital messages. Digital commitments are a common component in many cryptographic protocols. They allow a decision to be fixed, but it is only revealed at some later time; however, changing your mind is impossible.

Applications of cryptography include the protection of privacy in e-mail conversations, secure online banking, Internet shopping, electronic voting, digital money remittance, dated stamps, and secret sharings among several people. The study of cryptography also includes methods to attack and to break encrypted systems (cryptanalysis) as well as (more or less) open codes. The latter has no sharp borderline with slang or jargon. The typical example for this is French argot, originally spoken by thieves to prevent outsiders from understanding their conversations. Nowadays, argot plays a role of jargon without a primary intention of secrecy.

Cryptography also provides mental exercises, often in the form of puzzles; for example, the following correspondence between Frederick the Great (1712–1786) and Voltaire (1694–1778) has been handed down. Frederick the Great sent the following message to Voltaire:[2](#Notes.xhtml_Notes_2)

![](images/61_1.jpg)

Voltaire answered as follows:

![](images/61_2.jpg)

To solve this puzzle, one needs a little French (see [Exercise 2.1](#chapter02_2.xhtml_chapter02_2_26)).

But the basic task of cryptography is still to make secure communication possible via an insecure channel so that an attacker cannot understand or read the message.

![](images/62_1.jpg)

Fig. 2.1. Scheme of an encrypted communication.

The scheme is described in [Figure 2.1](#chapter02_1.xhtml_chapter02_1_3). We note that, in the context of cryptography, source encoding (i.e., data compression) does not have the aim of data compaction but rather the removal of redundancies. In order to not leak any information about the original text (for instance whether or not it is highly compressible), one can append some random data before encryption; this has the additional good property that the same message is never encrypted in the same way.

## 2.1 Symmetric encryption methods

A classical symmetric cryptographic system (or symmetric cryptosystem for short) uses the same keys for encryption and decryption. It consists of the following components:

–AfinitesetX of plaintexts (or texts for short).

–AfinitesetY of ciphertexts (ciphers, respectively).

–AfinitesetK of keys.

–Anencoding function c : X × K → Y and a decoding function d : Y × K → X such that d(c(x, k), k) = x for each x ∈ X. For a fixed key k, we also write ck(x) instead of c(x, k); analogously, we use the notation dk(y).

It is also common to use the term encryption function for the encoding function and, similarly, decryption function for the decoding function. For the purpose of illustration, we usually consider a communication between two persons A and B, named Alice and Bob. One reason for these names is that “she” always refers to the person A while “he” always refers to B. Sometimes we need more people in the examples, for example, the opponent Oscar. Whenever Alice and Bob use a symmetric cryptosystem, they must agree on a secret key k. Typically, the length of k ∈ K is much smaller than that of the transmitted message, so we can put some effort into transferring k. Even more important, the transfer of k can be separated in space and time from the encrypted transmission of the message. In the following, we discuss some basic aspects of symmetric cryptosystems; for a more detailed exposition we refer to [[4](#Bibliography.xhtml_Bibliography_5), [14](#Bibliography.xhtml_Bibliography_15)]. In our investigation of symmetric cryptosystems, we generally assume that initially only Alice and Bob know the key k. We should realize that there are several ways to compromise a cryptographic communication:

–The attacker Oscar can break the key. That is, Oscar gets knowledge of the secret key. Once Oscar has broken the key, he can decrypt and read messages, but he can also encrypt and send fake messages without Alice’s and Bob’s knowledge.

–On the other hand, even without knowing the key Oscar might be able to develop a working decryption scheme. This kind of compromise is called the global solution since Oscar now has the ability to decrypt all messages without a key. However, he still is not able to encrypt texts himself. In contrast to the global case, we speak of a local solution if Oscar can only decrypt certain messages instead of all of them.

–If Oscar is only able to get partial information about the key or the plaintext, he still has obtained some gain of information. In some cases, an attacker might not even be interested in reading an entire message. He could be content to get some partial information: for example, in the case of a credit card transaction, he might be interested solely in the credit card number.

Generally, when investigating the possible types of attack, our conservative assumption is that the attacker at least knows the cryptographic systems being used. This assumption is known as Kerckhoffs’ principle (named after Auguste Kerckhoffs, 1835–1903). In the following, we will distinguish between different cases with respect to

Oscar’s knowledge and abilities:

Ciphertext-Only: Oscar only knows ciphertexts.

Known-Plaintext: Oscar knows pairs of plain and ciphertexts.

Chosen-Plaintext: Oscar is able to have selected texts encrypted.

Chosen-Ciphertext: Oscar is able to have ciphertexts decrypted.

Since attack and defense are usually closely related, we can similarly characterize the levels of security against attacks by opponents with mere knowledge of the encrypted message:

Perfect or absolute security: Decryption is provably impossible regardless of the applied effort.

Computational security: Decryption requires efforts that are provably infeasible in practice.

Relative computational security: Decryption is not easier than the solution of a problem which is generally considered to be hard.

Pragmatic security: Despite intensive efforts, no efficient method for decryption is known. In short, the encryption method “appears to be secure.”

In practice, classic cryptography is based on pragmatic security. The problem with this approach, however, is that the encryption methods are often easier to break than expected.Moreover, security depends on the honesty of the creator, but the creator might hide some “trapdoor” within the cryptosystem. This trapdoor might be not obvious, but it might be included intentionally to allow a restricted possibility of breaking the code.

## 2.2 Monoalphabetic cipher

Monoalphabetic substitutions belong to the earliest and simplest cryptographic methods. The set of letters is identified with the elements of the ring ℤ/26ℤ. For simplicity, we omit special and capital letters.

![](images/64_1.jpg)

Now, symbols can be added and subtracted modulo 26\. So let X = Y = K = {a, . . . , z}. Then the shift cipher is given by c(x, k) = x + k mod 26 and d(y, k) = y − k mod 26.

The special case k = 3 is known as Caesar’s cipher because it reportedly was used by Julius Caesar (100–44 BC). Here is an example

![](images/64_2.jpg) wlphrgdqdrvhwgrqdihuhqwhv timeodanaosetdonaferentes

The encoding is given in the upper line and the plaintext is in the lower one. The plaintext refers to a Latin phrase in which Laocoön warns the Trojans not to accept the gift from the Greek: the Trojan Horse. Due to the linear number of keys (here 26), a bruteforce attack on a shift cipher is simple. This type of coding is a special case of permuting the alphabet. The general idea is to allow all permutations of the alphabet as keys. These are the monoalphabetic substitutions and there is an enormous number of them: 26! ≈ 4 × 1026. If one was able to test a million keys per second, an exhaustive search would take more than 1013 years. This is much longer than the age of the Universe which is currently estimated to be about 13.8 × 109 years old, dating from the Big Bang. Exhaustively searching for the key of a monoalphabetic substitution is impossible, so other methods are used, like frequency analysis, which use the fact that, in natural language, letters have a characteristic frequency.

A nice presentation of a substitution encryption can be found in the short story The Gold-Bug by Edgar Allan Poe (1809–1849), published in 1843\. The story is about Legrand’s search for the treasure of Captain Kidd where the following coded message plays a central role:

![](images/65_4.jpg)

The chief character Legrand infers from the name “Kidd” that the plaintext is written in English. Then, he identifies the following frequencies of the occurring symbols:

![](images/65_2.jpg)

He correctly conjectures that 8 codes the most common letter e. Then, Legrand looks for a possible encoding of the word “the” for which “;48 ” looks promising. After the last “;48” one finds “;(88.” From“;(88” he reconstructs the word “tree.” By further considerations, one can eventually reconstruct the full table of the decoding function.

![](images/65_3.jpg)

This yields the following plaintext in a readable form with spacing and special characters:

![](images/65_5.jpg)

With a telescope (here good glass) you can see the place almost before your eyes when sitting in the Bishop’s hostel.

## 2.3 Polyalphabetic cipher

As mentioned above, monoalphabetic substitution can be broken by frequency analysis. That is, one can exploit the frequency of individual symbols in order to decode the text. One idea to prevent such an attack is to periodically use different shifts of the alphabet.

This is the so-called Vigenère cipher (Blaise de Vigenère, 1523–1596). Keys in this method are words over the alphabet ℤ/26ℤ. For encryption, we first choose a fixed word k = k0 ⋅⋅ ⋅ kd−1 with ki ∈ ℤ/26ℤ. Then, we encrypt our plaintext x = x0 ⋅⋅ ⋅ xn−1 by c0(x0) ⋅⋅ ⋅ cn−1(xn−1) using the encryption function:

![](images/66_1.jpg) cj(a) ≡ a + kj mod d mod 26

Poe’s text from The Gold-Bug encrypted with the Vigenère cipher using the key k = gold then becomes

![](images/66_3.jpg)

Counting the frequencies of the symbols in the ciphertext yields:

![](images/66_2.jpg)

In comparison to monoalphabetic substitutions, we see a much more uniform distribution of the symbols and, moreover, there are no longer any telltale combinations like “th.”

For a long time, this method was considered invulnerable because a frequency analysis is not (directly) applicable. But the problem arises that repeatedly appearing pieces in the text are encrypted equally, whenever the distance between them is a multiple of the key length d. Let us once again have a look at the above example in order to illustrate the problem.

![](images/66_4.jpg)

Here, we see that the word “the” in the fourth line is encrypted by “hsh” twice.

Under the assumption that the key length or a multiple of it is known, we can break the Vigenère cipher as follows. Let the known key length (or multiple of it) be denoted by d. We perform frequency analysis by column, that is, we record d columns in such away that column i includes all encoded symbols whose position is congruent to i modulo d. Now, all characters in a column are encoded by the same symbol, and we can attack the encryption of each column via brute force, frequency analysis, or the like.

As a first step to protect against this kind of attack, we should keep the key length d secret. In fact, there are more relatively simple methods to hamper attacks by frequency analysis. One such possibility is lossless data compression (often referred to as source encoding). Because of the included elimination of redundancy, a compressed text appears as a random string; all symbols have roughly the same frequency. In order to not leak any information due to the compression ratio, augmenting a sufficient amount of random bits after compression is recommended.

## 2.4 Frequency analysis and coincidence index

We have already seen the frequency analysis method, whichwe used to break monoalphabetic substitutions. Now we extend this method. We have seen how to break the Vigenère cipher using frequency analysis if the key length, or a multiple thereof, is known. The attack by the coincidence index now just tries to determine a multiple of the key length. Let x = x1 ⋅⋅ ⋅ xn and ![](images/67_1.jpg) be two texts of length n over the alphabet Σ. The according coincidence index κ(x, x) is defined to be

![](images/67_2.jpg)

Here, δ is the so-called Kronecker delta (Leopold Kronecker, 1823–1891), defined as follows:

![](images/67_3.jpg)

The coincidence index measures the relative frequency of coincidence of the same symbol in the same position in the texts x and x. If we assume x and x'  to be chosen from a uniform distribution, then we obtain ![](images/67_4.jpg) where E denotes the expected value and N = |Σ| the alphabet size. If the symbols are not distributed uniformly, then the probability for a match increases. Thus, for random texts on an arbitrary distribution of symbols, we obtain

![](images/67_5.jpg)

In the concrete case of an alphabet with N = 26 uniformly distributed symbols, we obtain the value E [κ] = 3.8%. In experiments with natural language texts from the same language, an expectation of E [κ] ≈ 7% is obtained, a significantly higher value than in the random case above. An important fact for substitution ciphers, however, is that the coincidence index of two texts does not change when both are encoded with the same encryption key

![](images/67_6.jpg)

Now we want to take advantage of this fact to determine d. Let the ciphertext y be given. Then, at first for ℓ ∈ ℕ, we determine the value κℓ = κ(y, σℓ(y)), where σℓ(y) is the cyclic shift of y by ℓ symbols to the left. If the value ℓ is a multiple of d, then κℓ measures the coincidence of two natural texts encrypted with the same key. Thus, we expect κℓ to be in the range of 7%; otherwise, the value will be less. Here is an example to illustrate this technique.

The text from “The Gold-Bug” has length n = 203\. If y is the Vigenère encryption of this text with the secret key gold, then

![](images/68_1.jpg)

As described above, the local maxima are probably the key length or multiples thereof; here, peaks at ℓ = 4, 8, 12 give strong hints on d = 4.

An attack using the coincidence criterion is also feasible for more general polyalphabetic substitutions. Thus, a polyalphabetic substitution is easy to attack. Nevertheless, this encryption method is still relevant today. For example, commercial software with this method is still available, and for cell phones in the United States, this method with a key length of 160 bits is the only approved one.

## 2.5 Perfect security and the Vernam one-time pad

Perfectly secure encryption methods have been known at least since 1918, and shortly thereafter they were in use. Nevertheless, the term perfect security was only precisely defined mathematically by Claude Elwood Shannon (1916–2001) [[96](#Bibliography.xhtml_Bibliography_97)]. Following his definition, an encryption is perfectly secure if the probability for the occurrence of a ciphertext y is independent of the plaintext x. In other words, the conditional probability Pr[y | x] has to be equal to Pr[y]. In this case, the occurrence of a ciphertext does not provide any information about the plaintext x. It should be noted that certain aspects of information are not covered by this model; for example, some facts about the message cannot be hidden from Oscar, such as when the message was sent, how big the message is, or who sent and who received the message.

In principle, it is very easy to design an abstract cryptosystem which is perfectly secure. Let X be a set of texts and let texts x ∈ X occurwith probability Pr [x] > 0\. Alice and Bob choose a finite group G to be the set of ciphers Y as well as the set of keys K. The group G is public, but it has to be large enough that we can embed X as a subset in G. Bob chooses a secret key k ∈ G uniformly at random. Then he communicates the key k to Alice over a secure channel. For example, Alice and Bob meet personally before the decision about the text x is taken. WhenBob intends to inform Alice about x, he sends the product y = xk over a public channel. Alice recovers x by computing x = yk−1. The probability for each ciphertext y is now Pr[y] = Σx Pr[x−1y] Pr[x] = 1/|G| and thus independent of x ∈ X. The problem is that an observer Oscar knows y and perhaps later, for example, from Alice’s reaction, he might know x as well. Knowing x and y reveals k. So, the key k is good for one time, only. (Even if Oscar does not know x, he could detect that the same message was sent again unless k is changed.)

An advantage is that the method is valid in any group that is large enough, so we are free to choose the group structure. A reasonable simplification is to demand k = k−1 for all k ∈ G because then no inverses have to be computed and encryption and decryption methods are identical. Now k = k−1 is equivalent to k2 = 1\. So we can, for example, choose G = (ℤ/2ℤ)n for n ∈ ℕ with log2 |X| < n. The elements of G are then the bit strings y ∈ ![](images/b.jpg)n = {0, 1}n and the group operation is the bitwise exclusive-or ⊕. Therefore, encryption and decryption in this case can be performed very efficiently. For this special case, we obtain the cryptosystem using the so-called Vernam one-time pad by Gilbert Vernam (1890–1960) who published it in 1918 and had it patented shortly thereafter. It is an encryption scheme with a “one-time key” because, for each message x, a new key must be chosen to guarantee the security. One can view the Vernam one-time pad as a generalization of the Vigenère cipher. The subjects of encryption are bit sequences of length n. Here, X ⊆ ![](images/b.jpg)n = Y = K. Encryption and decryption using the key k ∈ ![](images/b.jpg)n then work as follows:

![](images/69_2.jpg)

From the above discussion, it is clear that one-time encryption with the Vernam one-time pad is perfectly secure. But this guarantee is lost if the key is used twice. This is why the scheme is called a one-time pad. As noted above, an attacker can determine the key in a known-plaintext scenario: knowing a plaintext x and its corresponding ciphertext c(x, k) the attacker can compute the key k by x ⊕ c(x, k) = x ⊕ x ⊕ k = k.

A Vernam one-time pad is used whenever perfect security is required so that the efforts of key generation and transmission become secondary issues.[3](#Notes.xhtml_Notes_3)A major problem is that the number of different keys is not smaller than that of the plaintexts. So, if we can transmit the key secretly, why can we not simply use this transmission for x instead? The point is that the key generation is completely decoupled from the text: Alice and Bob can agree on k in advance, before x is fixed. The difficulty due to the large number of keys cannot be avoided by the [next theorem](#chapter02_1.xhtml_chapter02_1_20).

Theorem 2.1. Let X denote a set of texts with Pr[x] > 0 for all x ∈ X, let K be a set of keys, and suppose that the ciphertexts Y satisfy Pr[y] > 0 for all y ∈ Y. If the underlying cryptosystem is perfectly secure, then |X| ≤ |Y| ≤ |K|.

Proof: First, for each key k ∈ K, the encoding function x ↦ c(x, k) is an injective mapping from X to Y, which implies |X| ≤ |Y|. Then, because of the perfect security property, for a fixed x0 ∈ X and each y ∈ Y, there has to be a key k ∈ K with y = c(x0, k). Otherwise, we have Pr[y | x0] = 0 ≠ Pr[y], contradicting the perfect security property. Therefore, k ↦ c(x0, k) is a surjective mapping from K to Y and thus |K| ≥ |Y|.

□

With a large number of keys, a design for a uniformly distributed random key selection is not obvious. [Theorem 2.1](#chapter02_1.xhtml_chapter02_1_20) shows that the key length cannot be reduced without sacrificing perfect security. Nowwe can show that the uniform distribution is also essential if the key generation is independent of the text. Therefore, we must not rely on the so-called pseudo-random generators in the key generation for the Vernamone-time pad, or the system is not perfectly secure anymore.

Theorem 2.2. Let |X| = |Y| = |K| such that Pr[x] > 0 for all x ∈ X. If keys are chosen independently of plaintexts, then the following statements are equivalent:

(a)The cryptosystem is perfectly secure.

(b)For every k ∈ K, we have Pr[k] = 1/|K|, and for all x ∈ X and y ∈ Y there is a key kxy ∈ K with c(x, kxy) = y.

Proof: From Pr[k] = 1/|K|, we obtain Pr[y | x] = Pr[kxy | x] = Pr[kxy] = 1/|K|, and then Pr[y] = ΣxPr[x] Pr[y | x] = (ΣxPr[x])/|K| = 1/|K|. Thus, the cryptosystem is perfectly secure. Conversely, let Pr[y] = Pr[y | x]. Suppose that c(x, k1) = y = c(x, k2) for two different keys k1, k2 ∈ K. Then, since |K| = |Y|, there exists some ciphertext y' ∈ Y such that there is no k ∈ K with c(x, k) = y'. Thus, Pr[y'] = Pr[y' | x] = 0, a contradiction to |X| = |Y|. Therefore, for every x and every y there exists a unique key kxy ∈ K with c(x, kxy) = y. Similarly, for every key k ∈ K and every cipher y ∈ Y, there exists a unique x ∈ X with k = kxy. This yields Pr[k] = Pr[kxy] = Pr[y | x] = Pr[y]. In particular, we have Pr[k1] = Pr[y] = Pr[k2] for all k1, k2 ∈ K. Consequently, Pr[k] = 1/|K| for all k ∈ K.

□

## 2.6 Asymmetric encryption methods

The cryptosystems considered so far are symmetric, as they use the same key for encryption and decryption. Therefore, before the communication, Alice and Bob need to agree on a key which is unknown to an attacker. For a key exchange, Alice andBob can, for example, meet in a café and exchange the key personally. Back home again, they can exchange messages over an insecure channel with the help of the key. But what is to be done when no café is available at the right time?

The problem can be solved by using different keys for encryption and decryption, which leads to the concept of asymmetric cryptosystems. The idea was first published in 1976 by Diffie and Hellman. Alice uses two keys for the communication. The first one is a public key that is made visible to anyone. However, the second key is private and secret, known solely to Alice. If Bob wants to send a message to Alice, he uses her public key for encryption. Alice in turn uses her private key to decrypt Bob’s message. This scheme elegantly solves the problem of key exchange because the communicated key is Alice’s public key, but nothing else. This is why the method is also called a public-key cryptosystem. Even if Oscar eavesdrops on the conversation, his only possibility is to decode Bob’s message based on the public key and the ciphertext. Therefore, methods of this kind have to be designed in such a way that this attack by Oscar cannot be performed efficiently. The problem is that we hardly know any way to prove such a statement rigorously. In public-key cryptography, you have to be content with relative computational security or even with pragmatic security.

There is another danger: Oscar pretends to be Alice by exchanging his public key with hers. Then he may receive and decrypt messages that were meant for Alice. This scenario is often referred to as man-in-the-middle attack. In [Section 2.12](#chapter02_2.xhtml_chapter02_2_2), we present a method for Alice to label her key with some kind of signature to prevent these attacks.

The main goal in public-key cryptography is to ensure that Oscar is not able to determine the original message from the ciphertext along with the public key. One relies on relative computational security for this, meaning that Oscar could decrypt messages in principle, but his resources in time or energy, according to our current knowledge, are not sufficient to do so. Therefore, public-key systems are based on a computational problem which is believed to be not efficiently solvable from a practical point of view. We consider the following asymmetric encryption methods:

RSA: This is probably the best known and most successful asymmetric method. It is based on the factorization of large integers.

Rabin: This is related to the Rivest–Shamir–Adleman (RSA) system and it also relies on integer factorization.

Diffie-Hellman: The method is not directly designed for encryption, but it is a method of exchanging keys for symmetric cryptosystems. Its security is based on the computation of discrete logarithms.

ElGamal: This cryptosystem is related to the Diffie–Hellman key exchange. Its security is also based on the discrete logarithm.

Merkle–Hellman: It is based on the NP-complete knapsack problem. However, Shamir was able to show that it is not secure. We present Shamir’s attack at the end of this chapter.

Even though it is widely believed that the factorization of large numbers and the discrete logarithm problem cannot be solved efficiently, no proof is known for these conjectures. Therefore, we are always interested in new cryptosystems based on different computational problems: for instance, group-based cryptography uses non-commutative groups as a platform and algebraic operations like conjugacy to design cryptographic schemes. So far, theses schemes have not fulfilled initial promises and, at present, practical applications are rare. This might drastically change if simple schemes like RSA become insecure due to more efficient factorizations algorithms.

## 2.7 RSA cryptosystem

The best-known public-key encryption method is RSA. It is named after the last names of its inventors Ronald Linn Rivest (born 1947), Adi Shamir (born 1952), and Leonard Adleman (born 1945). In RSA, Alice chooses two distinct primes p and q and computes the product n = pq. Next, Alice computes two numbers e, s ≥ 3 such that es ≡ 1 mod (p−1)(q−1). Typically, Alice chooses e, say e = 17 in case that 17 ∤ φ(n), and then she computes s using the extended Euclidean algorithm. A small number e, like e = 17, is not a problem as long as we take care that no message x is encrypted with xe ≤ n. However, the number s should be large; otherwise, the private key (n, s) is insecure due to an attack of Michael J.Wiener [[110](#Bibliography.xhtml_Bibliography_111)]. If s has less than one-quarter as many bits as the modulus n, then, in typical cases, this attack may discover the secret s. The public key is the pair (n, e); and encryption is done by x ↦ xe mod n. Alice decrypts by y ↦ ys mod n. Let y = xe mod n. If es = 1 + (p − 1)k, then

![](images/72_1.jpg)

by Fermat’s little theorem. Analogously, one can show that ys ≡ x mod q. In other words, both p and q divide ys − x. Since p and q are coprime, n = pq divides ys − x and, hence, we have ys ≡ x mod n. If x ∈ {0, . . . , n − 1}, then we obtain ys mod n = x. Thus, every encrypted message is decrypted correctly.

In [Chapter 3](#chapter03_1.xhtml_chapter03_1_1), we show how to find large primes p and q ([Section 3.4](#chapter03_1.xhtml_chapter03_1_13)), what properties p and q should have in order to ensure that n cannot be factorized easily ([Section 3.6](#chapter03_2.xhtml_chapter03_2_10)), how xe mod n can be computed efficiently ([Section 3.2](#chapter03_1.xhtml_chapter03_1_8)), and that the number n can easily be factorized as soon as one knows the secret key s (end of [Section 3.4.4](#chapter03_1.xhtml_chapter03_1_29)). Since we assume that factorization cannot be done efficiently, this implies that the secret key is secure. However, it is not known whether the decryption of the RSA method is secure. It is conceivable that, even without the knowledge of s, an attacker could decrypt the ciphertext. It is not possible to unambiguously assign a secret key s to the decryption function. So one can determine s' by knowing the rule es' ≡ 1 mod lcm(p −1, q−1); since p −1 and q−1 are even, clearly lcm(p−1, q−1) < (p − 1)(q − 1). Consequently, y ↦ ys mod n and y ↦ ys' mod n define the same mappings on {0, . . . , n − 1}. But in general, s ≠ s. For example, y ↦ y23 mod 55 and y ↦ y3 mod 55 define the same mappings on {0, . . . ,54}; they satisfy 7 ⋅ 23 ≡ 1 mod 20 and 7 ⋅ 3 ≡ 1 mod 20.

One of the problems in RSA, and in many similar cryptosystems, occurswhen only a few messages are likely to be sent. Then Oscar simply encrypts all these messages with the public key (n, e). For each of these messages, he stores the pair consisting of plaintext and corresponding ciphertext. Later, if Oscar eavesdrops on a message encrypted by (n, e), he compares it to his list of messages. If the ciphertext occurs in his list, then he knows the corresponding plaintext. To prevent this type of attack, a sufficient amount of random bits is usually appended to each message. In practice, 128–256 random bits are considered to be secure. It can be useful to insert the random bits at various (fixed) positions of each message.

## 2.8 Rabin cryptosystem

In the Rabin cryptosystem (developed by Michael Oser Rabin, born 1931), a message is encrypted by squaring it in the quotient ring modulo n = pq for two large prime numbers p and q. The method was published in 1979\. It should be noted that the decryption is ambiguous: indeed, if Bob sends the value y ∈ {0, . . . , n−1} to Alice, where x2 ≡ y mod n, then Alice finds four different square roots of y and she has to decide which is the correct one for x. The number of choices can be reduced to 2 by requiring the selection of x in the set ![](images/73_1.jpg) because x2 ≡ (n − x)2 mod n. But this does not resolve ambiguity completely. This disadvantage is partly compensated by the fact that the decryption can be proved to be essentially as hard as the factorization of n. No such statement is known for RSA.

It is easy to put more assumptions on x so that the encryption is very likely to be unique. As a typical example, you can require the first k bits of a message to match the last k bits. However, with additional assumptions about the encrypted messages, the connection between the hardness of decryption and that of integer factorization may become more and more incoherent. It seems to be a principle dilemma with Rabin’smethod. Still, the mathematical and philosophical consequences are interesting enough to justify discussing the Rabin cryptosystem. The system works as follows:

(a)Alice chooses two distinct primes p and q with p ≡ q ≡ −1 mod 4 and computes n = pq.

(b)The public key is n, and the private key is (p, q).

(c)If Bob wants to send a message x ∈ ℤ/nℤto Alice, he computes y = x2 mod n and sends y.

(d)In order to decrypt y, Alice computes the values

![](images/73_3.jpg)

and then, using the Chinese remainder theorem, obtains up to four different values of z ∈ ℤ/nℤ with z ≡ ±zp mod p and z ≡ ±zq mod q.

To prove the correctness of the method, we have to show that one of the four possible values of z equals x. From x2 ≡ y mod n, we can conclude x2 ≡ y mod p and x2 ≡ y mod q. Since p and q are prime, each of the equations X2 ≡ y mod p and X2 ≡ y mod q has at most two solutions ±xp ∈ ℤ/pℤ and ±xq ∈ ℤ/qℤ, respectively. In particular, x satisfies x ≡ ±xp mod p and x ≡ ±xq mod q. By symmetry, it suffices to show that ![](images/73_4.jpg) mod p, because then {−zp , +zp} = {−xp, +xp}. For p | y, nothing has to be shown. So let x, y ∈ (ℤ/pℤ)∗. From Fermat’s little theorem, we have![](images/74_1.jpg) mod p. This yields

![](images/74_2.jpg)

and thus the correctness of the Rabin method.

As mentioned before, Alice has to be able to identify the original message x out of the four possible values for z. For this purpose, it is customary to limit the space of plaintexts in order to make it possible for Alice to choose the right one with high probability. Therefore, the first and the last k bits of a message x are often required to coincide; say k = 20 or k = 64.

If n can be factorized, then it becomes easy to decrypt a message y by performing the same steps as Alice does. However, an attacker does not have to proceed this way to decrypt y, but might be able to determine the original message x in an entirely different way. Suppose there is an efficient algorithm R such that, on input y ∈ { x2 | x ∈ ℤ/nℤ}, it computes R(y) with R(y)2 ≡ y mod n. The idea is that a potential attacker will use R for deciphering. We show that R can be used to factorize n. First, we choose x ∈ {2, . . . , n − 1} at random. If gcd(x, n) ≠ 1, then we have factorized n. So let gcd(x, n) = 1 and z = R(x2 mod n). There are four possibilities which are equally likely:

(a)x ≡ z mod p and x ≡ z mod q

(b)x ≡ z mod p and x ≡ −z mod q

(c)x ≡ −z mod p and x ≡ z mod q

(d)x ≡ −z mod p and x ≡ −z mod q.

In each of the cases (b) and (c), the computation of gcd(x + z, n) yields a nontrivial factor of n, and gcd(x − z, n) gives the other factor of n. Therefore, we factorized n with a success probability of 1/2\. The success probability can be increased arbitrarily by repeating this algorithm for several rounds. Therefore, if we can compute square roots modulo n, then we can factorize n. So, under the assumption that factorizing n is not possible, no attacker can have an algorithm for deciphering messages in the Rabin cryptosystem.

If we are using the variant where the first and the last k bits of x coincide, then an attacker only needs to have an algorithm R which, on input

![](images/74_4.jpg)

computes R(y) with R(y)2 ≡ y mod n. In this setting, you still choose x ∈ {2, . . . , n − 1} at random (choosing x such that the first and the last k bits coincide is pointless since the result will be z = x); and you can assume that gcd(x, n) = 1\. The element y = x2 mod n is in the domain of R with a probability in the order of magnitude of 2−k. Therefore, after expectedly 2k rounds, we find y in the domain of R and we can proceed with z = R(y) as before. Therefore, with increasing k, this reduction becomes increasingly loose. So, from a practical point of view, the reduction still works fork = 20, but it fails for k = 64\. Some other reduction might work even for k = 64, but to date no such approach is known.

## 2.9 Diffie–Hellman key exchange

Consider the following scenario where Alice and Bob wish to establish an encrypted communication over the Internet. For efficiency reasons, they want to use a symmetric encryption method and thus they need a common secret key. Agreement on such a key can be performed securely and efficiently using the Diffie–Hellman key exchange (Bailey Whitfield Diffie, born 1944; Martin Edward Hellman, born 1945).

Alice and Bob agree on a prime number p and a number g mod p generating a sufficiently large subgroup of ![](images/75_2.jpg) Since ![](images/75_3.jpg) is cyclic, there are φ(p − 1) generators of ![](images/75_1.jpg) Therefore, it is often required for g to generate the whole group ![](images/75_4.jpg) For practical applications, however, a weaker assumption is sufficient. You can choose p such that p − 1 is divided by a large prime number q. For a randomly chosen value of g, we have g(p−1)/q ≢ 1 mod p with probability 1 − 1 /q. Thus, a random element g almost surely passes the test g(p−1)/q ≢ 1 mod p,where q is a divisor of the order of g. If g ∈ (ℤ/pℤ)∗ passes the test, then q divides the order of g.

Alice and Bob agree on the values of p and g. These need not be kept secret. So they may communicate via e-mail. Then Alice and Bob produce secret random numbers a and b in {2, . . . , p − 1}, respectively. Alice computes A = ga mod p and Bob B = gb mod p.NowAlicepubliclysends A to Bob, and Bob publicly sends B back to Alice. Since Ab ≡ gab ≡ Ba mod p, they can use the key K = (Ab mod p) = (Ba mod p) ∈ {1, . . . , p − 1} for their subsequent communication. For instance, they could use K as a secret key in some symmetric cryptosystem.

The following example uses very small numbers, in particular q = 11\. In realistic applications, numbers with several hundred decimals are used.

Example 2.3. Alice and Bob agree on p = 23 and g = 5. Then, g2 ≡ 2 mod 23\. Therefore, the order of g in (ℤ/23ℤ)∗ is at least 11\. In fact, g generates (ℤ/23ℤ)∗ and thus its order is 22\. Alice chooses (randomly) a = 6, Bob chooses b = 13\. Alice computes A ≡ 56 ≡ 8 mod 23 andsends A = 8 to Bob. Bob in turn computes B ≡ 513 ≡ 21 mod 23 and sends B = 21 to Alice. Alice computes K = 216 mod 23 = 18\. Bob computes K = 813 mod 23 = 18\. Everyone may see the numbers 23, 5, 8, and 21, but the secret key K = 18 remains hidden.

◊

The security of this method depends on the difficulty of computing the discrete logarithm. In practice, very large primes are used. The prime number q is maximal with respect to p if q = (p−1)/2 is also a prime. In this case, q is called a Sophie Germain prime (Sophie Germain, 1776–1831), and g can be chosen to be 2\. The values of p, g, A, B are known to any eavesdropper, but the Diffie–Hellman problem is to compute K. The Diffie–Hellman problem is solvable if the discrete logarithm a of A ≡ ga mod p or b ofB ≡ gb mod p can be computed. So far, no efficient algorithm for the Diffie–Hellman problem is known.

However, a third party Oscar could try to get between Alice and Bob, and then pretend to be Alice communicating with Bob, and to be Bob communicating with Alice, without them realizing that. To prevent this man-in-the-middle attack, Alice and Bob can provide signatures for all messages sent. Digital signatures are discussed in [Section 2.12](#chapter02_2.xhtml_chapter02_2_2).

## 2.10 ElGamal cryptosystem

The ElGamal method was developed in 1985 by Taher ElGamal (born 1955) and is used for both digital signatures and encryption [[40](#Bibliography.xhtml_Bibliography_40)]. Like RSA, the ElGamal method is an asymmetric encryption algorithm using a public and a private key. While the security of the RSA algorithm is based on the fact that no efficient factorization algorithm is known, ElGamal uses the discrete logarithm problem. The basic idea is simple: multiply a message with the key obtained from the Diffie–Hellman key exchange. Again, a prime number p with a large prime factor q of p − 1 is needed. Typically, one first chooses q, a sufficiently large prime, and then checks primality of p = kq + 1 for some relatively small even number k.

If gk ≢ 1 mod p for g ∈ (ℤ/pℤ)∗, then q divides the order of g. A random element satisfies this property with a probability of 1 − 1 /q. Alice chooses a random number a ∈ {2, . . . , p − 2} as secret key and computes

![](images/76_4.jpg)

The public key consists of the triple (p, g, A). The encryption of a message m by Bob to Alice is performed blockwise, so we can assume that the plaintext m is from the set {0, . . . , p − 1}. Bob chooses a random number b ∈ {2, . . . , p − 2} and computes

![](images/76_5.jpg)

The ciphertext consists of the pair (B, c). Alice decrypts the text by multiplying c by Bp−1−a in p∗. This leads to the correct result

![](images/76_6.jpg)

Example 2.4. Let p be the Sophie Germain prime 11 and g = 2\. Let the secret key be a = 4\. Alice publishes the triple (p, g, A) = (11, 2, 5). Bob wants to send the message m = 7 and has chosen b = 3 and thus B = 8. He computes c ≡ 53 ⋅ 7 ≡ 6 mod 11 and sends the pair (8, 6) to Alice. She obtains 86 ⋅ 6 ≡ 7 mod 11, which is the correct plaintext.

◊

A disadvantage of the ElGamal method is that the ciphertext is twice as long as the plaintext. Moreover, Bob needs to use a new random number b for each message m. Otherwise, Oscar can easily decrypt all messages as soon as he knows at least one pair of a plaintext and a ciphertext. If (B, c) and (B, c') are ciphertexts corresponding to messages m and m', respectively, and if Oscar knows (B, c) and (B, c') as well as m, he obtains m' ≡ mc−1c' mod p. Typically, secret messages do not remain secret very long. For example, Oscar may simply assume that the first message is Hello Alice.

In an analogous manner, ElGamal encryption can be done over any finite cyclic group. In particular, this can be done over a cyclic subgroup of an elliptic curve. Thus, it serves as the basis for elliptic curve cryptography (see, e.g., [[5](#Bibliography.xhtml_Bibliography_6)]). We discuss elliptic curves and their groups in [Section 5](#chapter05_1.xhtml_chapter05_1_1).

## 2.11 Cryptographic hash functions

One of the applications of cryptographic hash functions is digital signatures, as described in the next section. In general, the alphabet in this section is' = {0, 1}; however, the concepts introduced here can be adapted to arbitrary finite alphabets. A hash function is a mapping

![](images/77_3.jpg)

for n ∈ ℕ. A compression function is a mapping

![](images/77_4.jpg)

for natural numbers m > n; so a hash function maps words of arbitrary length to words of fixed length n. A compression function is a function that maps words of a given length to words of a fixed smaller length. Neither hash functions nor compression functions are injective. To be able to efficiently use hash functions in cryptography, we require h(x) to be easily computable for all x. However, it is crucial that one cannot efficiently find an x for a given s ∈ ![](images/b.jpg)n with h(x) = s. A mapping having these two properties is called a one-way function. From the current state of research it is not known whether one-way functions exist at all. Based on the principle of relative computational security, however, there are many mappings for which it is generally assumed that finding preimages is hard. A function where no efficient method for finding preimages is currently known, is the exponentiation in finite groups. Here, computing preimages means just solving the discrete logarithm problem; see [Section 3.7](#chapter03_2.xhtml_chapter03_2_17).

A collision is a pair (x, x') such that h(x) = h(x') and x ≠ x'. A function h is called collision resistant if it is computationally hard to find a collision (x, x'). All hash and compression functions have collisions since they are not injective. Collision-resistant hash functions are one-way functions: if an algorithm can compute the preimage x of an image y, then one can randomly choose an x' and compute y = h(x') and some preimage x ∈ h−1(y). Now, (x, x') is a collision if x ≠ x'. The probability for this is high enough since f is far from being injective. Thus, if collisions cannot be computed efficiently, then preimages also cannot be determined efficiently.

An encryption function ck : ![](images/b.jpg)n →![](images/b.jpg)n with key k ∈ ![](images/b.jpg)n yields the following canonical compression functions g : ![](images/b.jpg)2n →![](images/b.jpg)n:

(a)g(k, x) = ck(x) ⊕ x

(b)g(k, x) = ck(x) ⊕ x ⊕ k

(c)g(k, x) = ck(x ⊕ k) ⊕ x

(d)g(k, x) = ck(x ⊕ k) ⊕ x ⊕ k.

Here, ⊕ is the bitwise exclusive-or. All these mappings can easily be computed (assuming that this is the case for ck), but they are difficult to invert if we have a good encryption function. More robust statements are usually not available. On the one hand, this is because such statements about the security of encryption functions are not known; however on the other hand, it is also important how ⊕ and ck behave relative to each other. If, for example, ck(x) = x ⊕ k, then all of the above compression functions are easy to invert.

Merkle–Damgård construction

We now assume that we have a collision resistant compression function g : ![](images/b.jpg)2n →![](images/b.jpg)n; for example, we may use one of the functions defined above, if we have a sufficiently good encryption function. Using g, we intend to construct a collision resistant hash function h : ![](images/b.jpg)∗ → ![](images/b.jpg)n. For this purpose, we use the Merkle–Damgård-construction designed by Ralph C. Merkle (born 1952) and Ivan Bjerre Damgård (born 1956). To simplify the presentation, we assume that we only compute hash values of messages with less than 2n bits. For the typical value of n = 128, this number is greater than the estimated number of atoms in the universe. Collisions with more than 2128 bits could not be written down anyway.

So let x ∈ ![](images/b.jpg)∗ be any word with less than 2n bits. We add as few zeros as possible on the right of x in order to obtain a word x' whose length is divisible by n. Let ℓx ∈ n be the binary encoding of the length of x; we allow leading zeros such that ℓx has length n. The length of the word x̄ = xℓx is divisible by n. We can therefore write x̄ = x1 ⋅⋅ ⋅ xs with xi ∈ ![](images/b.jpg)n and s ≥ 1\. Note that xs = ℓx. Now, we let H0 = 0n ∈ ![](images/b.jpg)n and Hi = g(Hi−1 ⋅ xi) for i ≥ 1; here, ⋅ denotes the concatenation operation. The hash value of x is defined as

![](images/78_2.jpg)

Suppose, we know two different words x, y ∈ ![](images/b.jpg)∗ of length less than 2n satisfying h(x) = h(y). We show that, under this assumption, we are able to find a collision for g; to do that, we define x̄ = x1 ⋅⋅ ⋅ xs and ȳ = y1 ⋅⋅ ⋅ yt as extensions of x and y as defined above, with xi , yi ∈ ![](images/b.jpg)n. Let H 0, . . . , H s be the intermediate values in the computation of the hash value of x, and G0, . . . , Gt those for y. Without loss of generality, let s ≤ t. If Hs−i−1 ≠ Gt−i−1 and Hs−i = Gt−i, then

![](images/79_10.jpg)

is a collision of g, as both words are mapped by g to Hs−i. If this situation does not occur, then, since Hs = h(x) = h(y) = Gt, the property Hs−i = Gt−i holds for all i ∈ {0, . . . , s}. Under this assumption, we show that there is an index i ∈ {0, . . . , s−1} with xs−i ≠ yt−i. If, on the contrary, we have xs−i = yt−i for all 0 ≤ i < s, then in particular ℓx = xs = yt = ℓy. Consequently, x and y have the same length, resulting in s = t and x = y; this is a contradiction. Thus, an index i ∈ {0, . . . , s−1} with xs−i ≠ yt−i exists. Then, (Hs−i−1 ⋅ xs−i, Gs−i−1 ⋅ ys−i) is a collision of g. Therefore, if g is collision resistant, then h is collision resistant.

## 2.12 Digital signatures

In 1991, the Digital Signature Algorithm (DSA) was proposed by the US National Institute of Standards and Technology (NIST). To send an appropriately signed message, a random number generator and an efficient primality test are required. Additionally, one relies on well-known secure hash functions, like the ones described in the previous section. A hash function computes a small fixed-length value from an arbitrarily long bit string. In the scenario of DSA, hash values with bit length 160 are needed.

We now describe the nine steps Alice has to perform in order to sign a message according to the DSA standard. The first five steps are independent of the message content:

(1)Alice chooses a prime number q with about 160 bits.

(2)She selects some even number k such that p = kq + 1 is a prime number with 512–1024 bits.

(3)She searches for ![](images/79_2.jpg) satisfying ![](images/79_3.jpg) mod p 0 and computes ![](images/79_4.jpg) mod p.

(4)Alice randomly chooses x ∈ {1, . . . , q − 1} and computes y = gx mod p.

(5)Alice publishes (q, p, g, y) and specifies the hash function. So far, Alice’s only secret is the number x.

It might be unclear what ![](images/79_5.jpg) mod p means and why Alice succeeds in finding such an element g. We know that the multiplicative group ![](images/79_6.jpg) is cyclic, and since q | p − 1, it has a unique subset U of order q. In fact, Alice needs a generator g of U. For each ![](images/79_8.jpg) the element ![](images/79_7.jpg) is in U, which is guaranteed by Fermat’s little theorem. If g ≢ 1 mod p, then g is a generator because q is prime. The chance of finding a generator of U is very high: the homomorphism ![](images/79_9.jpg) with f ↦ f k is surjective and all elements of U aremet equally often. Therefore, the probability for g to generate the group U is 1 − 1/q.

The method’s security depends on the fact that no efficient algorithm is known for computing x ∈ {1, . . . , q − 1} from y ∈ {1, . . . , p − 1}. The only known method is to compute the discrete logarithm of y to base g. The order q has a binary length of 160 bits and should thus be too large to do that.

After these general preliminaries, we now describe the steps that Alice needs to perform when sending a signed message m to Bob.

(6)Alice computes the hash value h ∈ {1, . . . , q − 1} of the message m.

(7)She randomly chooses a sufficiently large number ℓ ∈ {1, . . . , q − 1}.

(8)She computes the remainder r = ((gℓ mod p) mod q) ∈ {0, . . . , q − 1}.

(9)Finally, she determines s = (ℓ−1(h + xr) mod q) ∈ {0, . . . , q − 1}. If s = 0, then Alice restarts the procedure at step (7).

The last step is possible because ℓ ∈ (ℤ/qℤ)∗. The signature of the message m is the pair (r, s), and Alice sends (m, r, s) to Bob. The signature is a bit string of length 320, that is 40 bytes.

If Bob receives a message m with signature (r, s), he verifies the signature as follows. He computes the hash value h and then u = s−1h mod q and υ = s−1r mod q. Then, he checks whether the following congruence holds:

![](images/80_1.jpg)

If the congruence is satisfied, he accepts the signature. In order to see that all correctly built signatures are accepted, we consider the following lines. From Alice’s computations, we know that sℓ ≡ h + xr mod q. This yields

![](images/80_3.jpg)

and consequently r ≡ (guyυ mod p) mod q, as desired. Note that the signature (r, s) only fits to one single hash value h. Thus, it is not possible to eavesdrop on a signature (r, s) and use it for a different message m' with the hash value h' ≠ h.

Suppose that Oscar tries to fake a signature. We may assume that he is using the correct hash value h for the message m. The problem for Oscar is that, after the values (h, r, s) have been chosen, the values of ℓ mod q and x mod q directly determine each other. So, Oscar can then compute ℓ if and only if he can compute x. If he has no information about x at all, then for him all elements gℓ ∈ U are equally likely. For solving the congruence r ≡ (gℓ mod p) mod q, nothing better is known than computing the discrete logarithm of y to base g. In order to prevent the public key (q, p, g, y) from being compromised, one can use certification agencies for signing the public key.

As a second method for digital signatures, let us mention RSA signatures. The idea here is to reverse the order of encryption and decryption in a cryptosystem. The RSA algorithm works correctly, because the encryption function c and the decryption function d aremutually inverse functions. Bob knows Alice’s public RSA key and can compute the encryption function c, but only Alice knows the decryption function d. If Alice wants to send a signed message m to Bob, then she computes the hash value h(m) and sends the pair (m, d(h(m))) to Bob. Bob, receiving a message (m, s) from Alice, computes h(m) and accepts if h(m) = c(s). If the message indeed originates from Alice, then c(s) = c(d(h(m))) = h(m).

## 2.13 Secret sharing

Secret sharing is about the following situation: Alice wants to distribute a secret s among n people in such a way that t of these people together are able to reconstruct s; however, if less than t people meet, it must not be possible for them to gain any information about s. Mechanisms like this are often used in access controls for systems or information: for instance, one can imagine a company with twenty employees to have a very important customer data base. This data base is encrypted with a key s. The owner, Alice, does not want any single employee to gain access to the data base because he could steal the file and sell it to a competitor. But if three or more employees meet, they should be able to work with the customer data base. It should not matter at all which three of the twenty employees are trying to access entries of the customer file. Another useful property is the ability to add another person with access to the secret s. In the above example, Alice could hire more employees.

We first consider a mechanical solution of this problem. Suppose that the secret is hidden behind some door. Alice could build a door with several locks such that each lock has to be unlocked before the door opens. For every lock, she can produce arbitrarily many keys. Let {1, . . . , n} be the set of employees, and let A1, . . . , Am be the subsets of {1, . . . , n} with t − 1 elements. We note that ![](images/81_1.jpg) Alice builds m locks, each one labeled by a subset Aj.

![](images/81_2.jpg)

An employee i ∈ {1, . . . , n} gets the key to lock Aj if and only if i ∉ Aj. Therefore, if B = Aj is a meeting of t − 1 employees, then none of the employees in B has the key to the lock Aj. In particular, no subset of less than t employees can open the door. On the other hand, if B is a subset of at least t employees, then B \ Aj ≠ 0 for all j ∈ {1, . . . , m}. This shows that every key is in the possession of some member in B and thus, the group B can open the door.

In order to implement this method without physical locks, Alice could fix a large finite commutative group G, for instance, Alice could use G = ℤ/nℤ. We assume that the secret is an element s ∈ G. Every key to the virtual lock Aj is a pair (j, gj) where gj is a random element in G, except for gm, which is chosen as ![](images/82_1.jpg) Then, all keys together can recover ![](images/82_2.jpg) On the other hand, if some key is missing, then all elements in G could be the secret key (with the same probability if the elements gj are chosen independently and uniformly at random). The purpose of the first component in the keys is to (easily) allow gj = gk for j =k.

If Alice hires a new employee n + 1, she has to install ![](images/82_3.jpg) new locks. The labels of these locks are subsets Bj of {1, . . . , n + 1} with n + 1 ∈ Bj and |Bj| = t − 1\. Thus, in the physical setting, the new employee n + 1 gets the keys to all the old locks, and the keys to the new locks are distributed accordingly among the old employees. In the virtual implementation, Alice has to choose a new element gj ∈ G for every lock but one, including the old locks. The remaining key is chosen such that the sum yields s. If Alice keeps the old keys for the locks A1, . . . , Am, then the new employee can recover the secret s all on his own by summing up his keys.

The large number of keys and the difficulties when adding participants are serious drawbacks. These problems are solved by an approach developed by Shamir [[94](#Bibliography.xhtml_Bibliography_95)].

Shamir’s secret sharing scheme

We assume that the secret s is a natural number: for instance, s could encode a password in decimal. Alice first chooses a prime number p which should be much larger than n and s. The prime number p is published. Now, Alice constructs a random polynomial a(X) by choosing coefficients a1, . . . , at−1 ∈ p independently and uniformly at random. These coefficients together with the secret s define the polynomial

![](images/82_4.jpg)

The degree of a is smaller than t, and at 0, the polynomial a evaluates to a(0) = s. Next, Alice communicates the information (i, a(i)) to person i using a secure channel. If t or more of these people work together, they can reconstruct the coefficients of the polynomial a with their t values and, thus, the secret s. For instance, they may use Lagrange interpolation. For t pairwise different elements x1, . . . , xt ∈ ![](images/f_d.jpg)p, the ith Lagrange polynomial ℓi(X) is defined by

![](images/82_5.jpg)

Thus, ℓi is a polynomial of degree t − 1, and

![](images/83_1.jpg)

If a(x1), . . . , a(xt ) are known, we can determine ã (X) = Σ1≤i≤t a(xi)ℓi(X). The polynomial a(X)−ã(X) has zeros in each of x1, . . . , xt. Since the degree of a(X)−ã(X) is at most t − 1, it has to be the zero polynomial. We conclude a(X) = ã(X). This shows that t or more people can reconstruct the secret s. It is also easy to see that further people can be added easily.

We still have to show that less than t people are not able to obtain information about the secret s. For this, let t − 1 different points (xi , a(xi)) ∈ (![](images/f_d.jpg)p \ {0}) × ![](images/f_d.jpg)p for i ∈ {1, . . . , t−1} be known. If less than t−1 points are known, even less information is available. By Lagrange interpolation, there are p polynomials ã(X) ∈ ![](images/f_d.jpg)p[X] of degree less than t satisfying ã(xi) = a(xi) for all i ∈ {1, . . . , t − 1}. Each of these polynomials would result in a different secret s̃ = ã(0). Since each such polynomial ã(X) is equally likely, every secret s̃ is equally likely. We note that if we had used ℤ or ℚ instead of ![](images/f_d.jpg)p, then the possible elements s̃ could not all have the same probability; in addition, the coefficients ai could not be chosen uniformly at random.

## 2.14 Digital commitment

The following conversation between Alice, an employee of the investment advisory company Ruin Invest, and a potential customer Bob was intercepted.[4](#Notes.xhtml_Notes_4)

Bob: Tell me five shares you recommend for purchase. If they all rise during the next month, then I will be your customer.

Alice: If I told you the shares, then you could invest without paying us. I suggest you look at our recommendations of the last month. You will be amazed what gains you would have made on a purchase.

Bob: How can I be sure that you really recommended these shares? You could just pick five winners. If you now tell me ongoing shares, I know you cannot change your choice. I would not cheat and invest in the shares you recommended.

Alice: We do not cheat either, and we will tell you the recommended shares of the last month.

The mutual distrust leads to a problem here. As a mechanical solution, the current recommendation could be deposited in a sealed envelope at a safe place. Then the choice could be checked afterward. An electronic version to solve this problem is referred to as digital commitment. Alice commits herself to an information t (here just 1 bit). Using a symmetric encryption method, the following steps are performed:

(1)Alice randomly chooses an (initially secret) key k.

(2)Bob randomly generates a string x and sends it to Alice.

(3)Alice encrypts xt using the key k by computing y = ck(xt).

(4)Alice sends y to Bob.

Thus, Alice has committed herself to xt. Later on, Bob can verify Alice’s choice:

(5)Alice sends the key k to Bob.

(6)Bob decrypts the message y using the key k and verifies that dk(y) = xt for a bit t. Then, Bob is convinced that Alice had committed herself to t.

How can Alice cheat? She could try to find a key k' resulting in a desired t. But then also dk' (y) = xt' has to hold for the random string x. With a randomly selected key k, this corresponds to a known plaintext attack, which a good cryptosystem should be able to withstand. Bob is in an even worse position because, besides the secret text y, he only knows a prefix of the plaintext (namely, x).

A public collision resistant hash function f can also be used to make a commitment. The protocol for this is as follows:

(1)Alice randomly chooses two bit strings x1, x2.

(2)Alice sends f(x1x2t) and x1 to Bob.

Now again Alice has committed herself to t. Later, Bob can verify Alice’s information t:

(3)Alice sends x1x2t to Bob.

(4)Bob compares f(x1x2t) and x1 with those values he previously obtained from Alice.

Since f is difficult to invert, Bob cannot determine the bit t before he receives x1x2t (especially because several preimages of f(x1x2t) could have the prefix x1). Disclosing a part of the random information makes it possible to check whether Alice chose special strings that would make it easier to find a collision. So Alice has to disclose the “true” value of t. The main advantage of this protocol is that Bob does not have to send any messages: for instance, Alice could use a radio station, newspaper ads, a web page or her Twitter account.

Example 2.5. Alice and Bob have a telephone conversation. They want to decide who has to attend the cryptography course the next day to take notes. For this purpose, each of them flips a coin. If both have the same result (both have heads or both have tails), then Alice has to attend the course; otherwise Bob has to go. If Alice tells Bob the result of her coin toss, he could choose his result such that Alice has to go; conversely, the same situation occurs if Bob is the first to tell the result of his coin toss. Therefore, they agree on the following protocol. Alice commits to a bit t, then Bob tells Alice his coin toss result in form of a bit t. Finally, Alice reveals her bit t, and both of them know who will attend the course.

◊

## 2.15 Shamir’s attack on the Merkle–Hellman cryptosystem

The Merkle–Hellman cryptosystem is based on the knapsack problem, which is one of the classical NP-complete problems [[44](#Bibliography.xhtml_Bibliography_44)]. The cryptosystem was developed by Merkle and Hellman and published in 1978 [[75](#Bibliography.xhtml_Bibliography_75)]. Their hope was to have designed a secure cryptosystem that is based on a provably hard problem (unless P = NP). This hope did not last long: soon after its presentation, it was destroyed by Shamir.

In the following, we describe the Merkle–Hellman scheme in its original form and, after that, we explain Shamir’s method for breaking it. The presentation essentially follows [[95](#Bibliography.xhtml_Bibliography_96)], but in a somewhat less technical (and less general) way.

The input to the knapsack problem is a sequence (s1, . . . , sn , c) of natural numbers in binary, and the question is whether there is a subset I ⊆ {1, . . . , n} such that

![](images/85_1.jpg)

We understand c to be the capacity of a knapsack and si the size of the i th piece. Then, we want to know whether it is possible to fill the knapsack completely. The algorithmic difficulty arises from the binary encoding of the numbers, because when the numbers are given in unary, then the problem is solvable in polynomial time; see [Exercise 2.18](#chapter02_3.xhtml_chapter02_3_2). On the other hand, the problem becomes very simple in some special cases, even if the inputs are in binary.

We call a sequence of positive real numbers (s1, . . . , sn) superincreasing if sj > ![](images/85_2.jpg) for all 1 ≤ j ≤ n. The sequence si = 2i for i ∈ ℕ is superincreasing, whereas the Fibonacci sequence F i is not. The knapsack problem for superincreasing sequences is solvable in linear time: when considering si in the order from n down to 1, one has to include i in I if and only if the remaining capacity suffices. In particular, solutions are unique.

The Merkle–Hellman cryptosystem

The cryptographic idea is to hide the property of being superincreasing by a modulo computation. The Merkle–Hellman cryptosystem consists of two parts: one private and one public. Alice secretly chooses a superincreasing sequence (s1, . . . , sn) and a modulus m. This number has to satisfy ![](images/85_3.jpg) Preferably, m should be prime because Alice needs two more secret numbers u, w ∈ {2, . . . , m − 1} such that uw ≡ 1 mod m. Concretely, it was suggested to have n = 100 and the numbers si having n+i−1 bitswhilemshould have 2n bits. In order to hide the order of the numbers si ,Alice chooses a permutation π on {1, . . . , n}. She publishes a sequence (a1, . . . , an) with values 0 < ai < m and![](images/86_1.jpg) aπ(i) = siu mod m

Then, ai is a number with 2n bits. Bob encrypts a bit string (x1, . . . , xn) ∈ ![](images/b.jpg)n of length n by the sum

![](images/86_2.jpg)

Bob sends y to Alice on a public channel. It follows y < n22n, so y consists of about 2n + log n bits. Alice receives y and computes c = yw mod m. She knows

![](images/86_3.jpg)

and by the choice of m this yields c = Σi≤n xπ(i)si. Since (s1, . . . , sn) is superincreasing, she can reconstruct the sequence (xπ(1), . . . , xπ(n)) ∈ ![](images/b.jpg)n and therefore she knows all the xi for 1 ≤ i ≤ n.

Shamir’s attack

We will show that the Merkle–Hellman system in the form just described is insecure and can be broken. The crucial observation is that it is neither necessary to compute the permutation π nor the sequence (s1, . . . , sn) nor the numbers m, or w. The attacker aims for a permutation σ, a superincreasing sequence of positive rational numbers (r1, . . . , rn, 1), and a number V with 0 < V < 1 such that

![](images/86_4.jpg) ri ≡ aσ(i)V mod 1

Here, a ≡ b mod 1 means that the difference a − b is an integer. If the aim is achieved, it follows that

![](images/86_5.jpg)

Since ![](images/86_6.jpg) and because the sequence of the ri is superincreasing, an attacker obtains all xσ(i) efficiently. We may have π ≠ σ, but the interest is in the sequence (x1, . . . , xn), only. Since σ and the xσ(i) are known, the xi can be computed.

It is not clear how an attacker can achieve this task, but there is a very important aid: the attacker knows that σ, the sequence (r1, . . . , rn), and the number V exist: consider σ = π, ri = si/m, and V = w/m. We fix the unknown value υ = w/m and we try to approach υ with our value V.

For each index i ∈ {1, . . . , n}, we consider the function fi : [0, 1) → [0, 1) with fi(V) = aiV mod 1\. As usual, we have [0, 1) = { x ∈ ℝ| 0 ≤ x < 1 }. The graph of this function is a sawtooth wave. There are exactly ai zeros 0, 1/ai, . . . , (ai − 1)/ai; and, except for the jumps, the slope is always ai. In the following, numbers of the form q /ai with 0 ≤ q < ai are called positions.

![](images/87_1.jpg)

At the point υ, the function fπ(i) evaluates to

![](images/87_6.jpg)

Since (s1, . . . , sn, 1) is superincreasing, this means that the permutation π is determined by the order of the values fi (υ).This is the crucial observation that makes breaking the Merkle–Hellman method possible. The problem is now reduced to finding a sufficiently good approximation of the value υ.

There are less than n4 possibilities for the initial sequence (π(1), . . . , π(4)). Without loss of generality, we can assume to be in a phase of the attack where the values π(1), . . . , π(4) are correct. If the initial sequence is not correct, it is not clear whether the aim will be achieved. If the aim is not achieved, then we try the next possibility for π(1), . . . , π(4). If the aim is achieved with an incorrect hypothesis for π(1), . . . , π(4), this does not matter. Thus, after a maximum of four exchanges in the sequence (a1, . . . , an),we can assume that we have π(j) = j for 1 ≤ j ≤ 4; and, without restriction, a1, . . . , a4 correspond to the smallest values s1, . . . , s4.

Let J = {1, 2, 3, 4}. We choose λ ≥ 0 with aj > 22n+j−λ for all j ∈ J. The attack is easier if λ is small. If a1, . . . , a4 were uniformly distributed, then we would expect λ ≤ 8\. From a practical viewpoint, this justifies assuming that λ is a small constant. Actually, a weaker assumption suffices in the mathematical analysis. Later, we see that the attack is successful with high probability as long as λ is sublinear.

Next, we consider for each j ∈ J a natural number cj with 0 < cj < aj and

![](images/87_3.jpg)

where 0 ≤ εj < 1/aj. We have ajυ = cj + ajεj and thus ajυ mod 1 = sj/m = ajεj < 1 for all j ∈ J (because π(j) = j for j ∈ J). From the estimations m > 22n − 1, aj > 22n+j−λ and sj < 2n+j−1 (from the bit length of sj), we conclude 22n−1+2n+j−λεj < 2n+j−1 and thus

![](images/87_4.jpg)Let ℓ ∈ J be such that ![](images/87_5.jpg) for all j ∈ J. In the following, we assume that cℓ ≠ 0\. We discuss this again later and provide a justification for the assumption. For the time being, we can consider the case cℓ ≠ 0 as the case to treat first. From ([2.1](#chapter02_2.xhtml_chapter02_2_19)) and ([2.2](#chapter02_2.xhtml_chapter02_2_20)), we obtain ![](images/88_1.jpg)

Because of cℓ ≠ 0, the following system of Diophantine inequalities in the four unknowns cj with j ∈ J has an integer solution:

![](images/88_2.jpg)

By υ, we know that at least one solution of the system ([2.3](#chapter02_2.xhtml_chapter02_2_22)) is guaranteed. For the following,weonlyneedthevalue cℓ and the index ℓ ∈ J. However, we need to compute all possible solutions for each ℓ ∈ J and thus, a priori, we obtain a list cℓ,1, cℓ,2, cℓ,3, . . . . The number of ℓ ∈ J is only 4, but the respective lists could become too long and thus cause the attack to fail. But the following heuristic shows that one does not have to be afraid of the lists becoming too long. On the contrary, we can assume that we will find exactly one ℓ and only one cℓ ≠ 0, and even this only if we investigate the correct set {π(1), . . . , π(4)}. In all other cases, it is likely that no solution will be found (which then also shows that {π(1), . . . , π(4)} was not chosen correctly).

To explain the heuristic, we assume for the moment that the numbers aj for j ∈ J are independently and uniformly distributed random variables. If we fix a position 0 < p/aℓ < 1, then the probability for the interval

![](images/88_5.jpg)

to have a nonempty intersection with each set of positions ℕ/aj for j ∈ J\{ℓ}, is at most (2−n+λ)3 = 2−3n+3λ. Summing up over all positions, we obtain the result that there exists a solution with a probability which is at most 2−n+3λ. If λ is sublinear, then this probability converges to zero. (For λ ∈ O(1), the probability approaches zero exponentially fast.) A problem with the estimation is that the values aj are not independent and, for the right choices of {π(1), . . . , π(4)} and ℓ, there exists some solution. However, in many cases there is only one (or very few) solutions. Moreover, from the user perspective, wemust deal with the case where the solution (cj)j∈J ∈ ℕ4 is unique. This solution can be found by standard methods in polynomial time as there is only a constant number of inequalities.

Should there be, contrary to expectations, several solutions, an attacker might find all solutions by checking them one by one. For simplicity, we may assume that {π(1), . . . , π(4)} is correct and for this choice exactly one solution cℓ of the system ([2.3](#chapter02_2.xhtml_chapter02_2_22)) with ℓ ∈ J exists and that cℓ and ℓ ∈ J are known.

Defining α = cℓ/aℓ and ε = 2−3n+λ, from Equation ([2.1](#chapter02_2.xhtml_chapter02_2_19)), we obtain the property υ ∈ [α, α + ε]. For each index 1 ≤ i ≤ n, at most one position p/ai can be within the interval [α, α+ε] because the distance ![](images/88_4.jpg) between p/ai and (p+1)/ai is too large for ε. The graph of the function fi with fi(V) = aiV mod 1 within the interval [α, α+ε] therefore consists of at most two segments, which can easily be computed. There are at most ![](images/o.jpg)(n2) intersections, and we partition the interval [α, α + ε] in at most ![](images/o.jpg)(n2) subintervals such that no intersections and no positions are in the interior of the subintervals. Since (0, s1/ m, . . . , sn/ m, 1) is superincreasing, υ has to be in the interior of such a subinterval. This is a good occasion to reintegrate the previously excluded case cℓ = 0, which leads to the special case α = 0\. Within the interval [0, ε], there are no intersections at all, and we only get one additional interval (0, ε) with the possibility υ ∈ (0, ε). Now, let (β, β+δ) be the interior of a subinterval (where now we allow β = 0 and δ = ε). The graph of each function fi yields a unique segment within (β, β + δ). Thus, the segments are linearly ordered from bottom to top and this defines a permutation σ.

![](images/89_1.jpg)

For every V ∈ (β, β + δ), the corresponding permutation σ has the property

![](images/89_4.jpg)

Only very few of these sequences (aσ(1)V mod 1, . . . , aσ(n)V mod 1, 1) will be superincreasing. However, at the latest during the attack phase, in which the guess of {π(1), . . . , π(4)} and cℓ is correct, the existence of such a sequence in one of the subintervals is guaranteed. In this phase, it is the interval (β, β + δ) with υ ∈ (β, β + δ). Here, σ coincides with π. Of course, we do not know at all whether we are in the right phase or at the right β. But we know that this is possible and we just want to check whether (aσ(1)V mod 1, . . . , aσ(n)V mod 1, 1) is superincreasing.

First, for 1 ≤ i ≤ n, we define natural numbers ci by ⌊aiβ⌋. Then, for V ∈ (β, β+δ), we have aiV mod 1 = ai − ci.

For each interval (β, β + δ) with associated permutation σ we obtain the following n + 3 linear inequalities in the indeterminate V:

![](images/89_3.jpg)

Writing this in a clearer form, we obtain

![](images/90_1.jpg)

For any choice of β, this yields two rational numbers 0 ≤ L, R ≤ 1 with the solution set V ∈ (L, R). In the correct phase and if υ ∈ (β, β + δ) is true, then υ lies inside such an interval (L, R). Thus, it is guaranteed to find an interval with L < R.

We take ![](images/90_2.jpg) and define rσ(i) = aσ(i)V − cσ(i). Then the aim of the attack is reached because the sequence (0, r1, . . . , rn, 1) is superincreasing. We can now decrypt all messages.

We have a look again at the complexity of the attack. In the worst case, we have to test ![](images/o.jpg)(n4) cases to find π(1), . . . , π(4). For each of these possibilities, solutions (cj)j∈J ∈ ℕ4 are found in polynomial time, provided they exist. One can assume that once solutions exist, they are unique. But even a very generous estimate, a polynomial number of solutions would not detract from the fundamental strength of the attack. Next, for each choice of π(1), . . . , π(4) and each solution (cj)j∈J ∈ ℕ4 only ![](images/o.jpg)(n2) intervals are considered. Each of these intervals defines a system of linear inequalities in one variable V. These are only polynomially many. At least one of these systems of equations defines a superincreasing sequence (rσ(1), . . . , rσ(n), 1). The Merkle–Hellman encryption is ineffective.

As noted by Shamir, there is another weak point of the Merkle–Hellman cryptosystem: the attack can start long before the transmission of the first message, because the calculations can start as soon as Alice publishes the parameters. We might have days or weeks to find σ and a superincreasing sequence (rσ(1), . . . , rσ(n)). The selected parameters can be verified by encrypting self-chosen plaintexts.

## Exercises

2.1. Decrypt the communication between Frederick the Great and Voltaire on page 49.

2.2. Is it true that every encryption function with a finite set of ciphertexts (for fixed key k) has to be surjective?

2.3. Let n = 7 ⋅ 11 = 77 and e = 43.

(a)How many elements does the multiplicative group (ℤ/77ℤ)∗ contain?

(b)Determine s ∈ ℕ satisfying es ≡ 1 mod φ(n).

(c)The message y = 5 was encrypted via RSA using the public key (77, 43). What is the plaintext x?

2.4. (Multiple exponent attack) A message x was encrypted using the two RSA keys (551, 5) and (551, 13). The resulting ciphers are 514 and 438, respectively. Determine the plaintext x.

2.5. (Multi-prime RSA) Let p1, . . . , pm be m different prime numbers, let n = p1 ⋅⋅ ⋅ pm, and let s ⋅ e ≡ 1 mod φ(n). Messages x, y ∈ {0, . . . , n − 1} are encrypted by c(x) = xe mod n and decrypted by d(y) = ys mod n. Show that the method is correct, that is, d(c(x)) = x holds for all x ∈ {0, . . . , n − 1}.

## 2.6. Let n = 11 ⋅ 23 = 253.

(a)Encrypt the message 17 using the Rabin cryptosystem with public key n.

(b)Decrypt the ciphertext 36 using the Rabin cryptosystem with secret key (11, 23).

(c)Bob wants to encrypt 8-bit messages x ∈ 00{0, 1}400 using the Rabin cryptosystem with public key n and send them to Alice. Will Alice be able to decrypt these messages unambiguously?

## 2.7. Let n = 2 ⋅ 23 + 1 = 47 and g = 5.

(a)What is the order of g in (ℤ/nℤ)∗?

(b)Let a = 16 and b = 9 be the secret keys of Alice and Bob, respectively. Which are their public keys A and B and the shared secret k in the Diffie–Hellman key exchange protocol?

(c)Bob wants to send x = 33 with the public key (n, g, A) and the secret key b using the ElGamal encryptionmethod (with A, b as above). What is the ciphertext (y, B)?

2.8. Let h : X→Y be a compression function. For y ∈Y, we define ‖y‖=|{ x | h(x)=y }|. Furthermore, let N be the number of collisions of h and m = Σy∈Y ‖y‖/|Y| the average size of ‖y‖. Show the following relationships:

![](images/91_1.jpg)

2.9. Let h1 : {0, 1}2m → {0, 1}m be a collision resistant compression function. The functions hi : {0, 1}2im→{0, 1}m for i>1aredefinedby hi(x1x2)=h1(hi−1(x1)hi−1(x2)) for x1, x2 ∈ {0, 1}2i−1m. Show that the hi are collision resistant, too.

2.10. Let n = pq for two secret primes p and q of the form p = 2p' +1 and q = 2q' + 1, respectively, where p' and q' are the prime numbers, too. Let a ∈ (ℤ/nℤ)∗ be an element of order 2pq. Define the compression function h : {1, . . . , n2}→ (ℤ/nℤ)∗ by h(x) = ax mod n. We use the values n = 603 241 and a = 11 to fix such a compression function. Use the collision h(1 294 755) = h(80 115 359) to factorize n.

2.11. (ElGamal signatures) Let p be a prime number and α be a generator of (ℤ/pℤ)∗. The plaintext space is defined as T = (ℤ/pℤ)∗ and the signature space as S =(ℤ/pℤ)∗ × ℤ/(p − 1)ℤ. Keys are of the form k = (p, α, β, m, s) ∈ ℕ5 where β = αm mod p and s ∈ (ℤ/(p − 1)ℤ)∗. The signature function uk : *J* → S is defined by uk(x) = (γ, δ) where γ = αs mod p and δ = (x − mγ)s−1 mod (p − 1). The verification function is

![](images/92_1.jpg)

(a)Show that υk(x, γ, δ) = true if and only if uk(x) = (γ, δ) is a valid signature. For the direction from left to right you can assume that γ is a generator of (ℤ/pℤ)∗.

(b)Create signed texts from the knowledge of (p, α, β).

(c)Let (γ, δ) be a valid signature for x. Let h, i, j be integers such that 0 ≤ h, i, j ≤ p−2 and gcd(hγ − jδ, p − 1) = 1\. Then the following values are computed:

![](images/92_3.jpg)

Show that (λ, μ) is a valid signature for x'.

2.12. We want to share the secret s = 7 among four people such that any three of them are able to recover s. Use the subset scheme over G = ℤ/12ℤ.

2.13. Using Shamir’s secret sharing scheme, distribute the secret 42 among three persons such that only at least two of them working together can reconstruct the secret.

2.14. The company RUIN INVEST has two directors, seven heads of department and 87 other employees. The valuable customer file is protected by a secret key. Develop a method for distributing the key such that the following groups are able to access the file: (i) Both directors together, (ii) at least one director and all seven heads of department, (iii) at least one director, at least four heads of department and at least 11 employees.

2.15. A group of at least three employees of a company wants to compute their average income, in order to compare it with each one’s personal salary. They all are honest but no one wants to reveal his or her income to the others. Specify a protocol that solves this problem.

2.16. Alice and Bob want to decide who has the higher salary. This shall be accomplished without anyone of them getting to know the salary of the other. Design a protocol for this task assuming that there is a known finite set of possible salaries.

2.17. Specify a fair protocol for an electronic roulette game. You need not describe in detail how the bids are made.

2.18. Show that the knapsack problem (s1, . . . , sn, c) with the si coded in binary and c coded in unary can be solved in ![](images/o.jpg)(n ⋅ c) steps.

2.19. The ciphertext 90 has been encrypted via the Merkle–Hellman cryptosystem using the list (43, 72, 16, 46, 50) with the multiplier u = 57 and the prime number 71\. What is the plaintext?

2.20. Show that sequences (si)i∈ℕ satisfying si+1 ≥ 2si > 0 are superincreasing.

## Summary

Notions

–symmetric cryptosystem

–plaintext

–ciphertext

–key

–global solution

–local solution

–Kerckhoffs’ principle

–ciphertext-only attack

–known-plaintext attack

–chosen-plaintext attack

–chosen-ciphertext attack

–perfect security

–computational security

–relative computational security

–pragmatic security

–Caesar’s cipher

–shift cipher

–monoalphabetic cipher

–frequency analysis

–polyalphabetic cipher

–Vigenère cipher

–coincidence index

–Kronecker delta

–Vernam one-time pad

–asymmetric cryptosystem

–public-key encryption

–man-in-the-middle attack

–RSA cryptosystem

–Rabin cryptosystem

–Diffie–Hellman key exchange

–ElGamal cryptosystem

–hash function

–compression function

–one-way function

–collision

–collision resistant

–Merkle–Damgård construction

–digital signature

–Digital Signature Algorithm (DSA)

–RSA signature

–secret sharing

–digital commitment

–Merkle–Hellman cryptosystem

–knapsack problem

–superincreasing sequence

Methods and results

–scheme of an encrypted communication

–frequency of characters in the plaintext space unevenly distributed and known frequency distribution ⇒ frequency analysis in monoalphabetic substitution possible

–The knowledge of diphthongs like “th” and frequently appearing words like “the” in English is very useful in frequency analysis.

–In the polyalphabetic substitution with a key of length d every dth character is encrypted with the same monoalphabetic substitution.

–The coincidence index can be used to compute the key length d for polyalphabetic substitutions; then, a frequency analysis can be applied.

–The Vernam one-time pad ensures perfect security.

–The key length of the Vernam one-time pad is optimal.

–Under the assumption that chosen keys are independent of the plaintext, the keys for the Vernam one-time pad have to be chosen uniformly at random.

–RSA cryptosystem: encryption and decryption by exponentiation in ℤ/nℤ; n is the product of two large prime numbers; security is based on the hardness of factorization

–Rabin cryptosystem: encryption by squaring in ℤ/nℤ; n is the product of two large prime numbers; security is based on hardness of factorization

–The decryption used in the Rabin procedure provides up to four possible plaintexts if the plaintext space ℤ/nℤ is not restricted.

–Diffie–Hellman key exchange: key gab for group element g, where only ga and gb are sent; security is based on hardness of the discrete logarithm

–ElGamal cryptosystem: encryption by multiplication with the Diffie–Hellman key; security is based on hardness of the discrete logarithm

–Compression functions obtained from encryption functions

–The Merkle–Damgård construction transforms a collision resistant compression function into a collision resistant hash function.

–Generation of signatures using the Digital Signature Algorithm (DSA)

–Construction of RSA signatures

–Sharing secrets by subsets of keys

–Shamir’s secret sharing

–Lagrange polynomials and Lagrange interpolation

–Digital commitments by means of a symmetric cryptosystem

–Digital commitments by means of a collision resistant hash function

–Merkle–Hellman cryptosystem: messages are encrypted as capacity of a given knapsack problem; the cryptosystem is not secure

–Shamir’s attack on the Merkle–Hellman cryptosystem

# 3 Number theoretic algorithms

Many cryptosystems rely on fast arithmetic in various algebraic structures. For instance, when creating the private and the public key for Rivest–Shamir–Adleman (RSA), you have to find large prime numbers p and q, as well as to invert modulo (p − 1)(q − 1); then, a fast algorithm for exponentiation is required for encryption and decryption. In addition, we want fast algorithms for multiplication and division for the elementary operations of computing the product of two numbers modulo n. On the other hand, the security of many cryptosystems relies on the difficulty of some number theoretic problems. For instance, RSA is secure only as long as there is no efficient algorithm for integer factorization. It is therefore important to know how factorization algorithms work and to be aware of the cases when factorization is easy. Similarly, the ElGamal cryptosystem relies on the difficulty of the discrete logarithm. When solving equations in finite fields, it is important to extract roots; this is a recurring subproblem in various other settings. Before we consider some algorithms for the above problems, we will start with two basic tools for estimating the (worst-case or the expected) running time of an algorithm.

## 3.1 Runtime analysis of algorithms

Throughout this chapter, let ℝ≥0 be the set of nonnegative real numbers. We start with some techniques concerning the runtime analysis of algorithms. To this end, for any function f : ℝ≥0 →ℝ≥0, we define the function class

![](images/95_4.jpg)

as the set of functions growing at most as fast as f. The O-notation was popularized by Edmund Georg Hermann Landau (1877–1938).

Master theorem

In the runtime estimation of recursive algorithms, you often have to deal with recurrences. We present asymptotic estimates for a large class of such recurrences.

Lemma 3.1. Let a ≥ 0, b > 1, and f, g : ℝ≥0 →ℝ≥0 with f(1) ≤ g(1). If f(n) ≤ a⋅ f(n/b)+ g(n) for all n ≥ b, then ![](images/95_2.jpg) for all k ∈ ℕ.

Proof: For k = 0, the claim is true. Now, let k > 0. By definition, we have f(bk) ≤ a ⋅ f(bk−1) + g(bk). The inductive hypothesis for k − 1 yields

![](images/95_3.jpg)

□

Distinguishing different cases depending on the specific values of the parameters a and b and the specific function g, we obtain the following theorem. Here, log n = max(1, log2 n).

Theorem 3.2 (Master theorem). Let a, b, c ∈ ℝ≥0 with b > 1 and let f : ℝ≥0 → ℝ≥0 be nondecreasing with f(n) ≤ a ⋅ f(n/b) + ![](images/o.jpg)(nc). Then

![](images/96_1.jpg)

Proof: Suppose that f(1) ≤ d and f(n) ≤ a ⋅ f(n/b) + dnc for some d > 0\. The function h(n) = f(n)/d satisfies h(1) ≤ 1 and h(n) ≤ a ⋅ h(n/b) + nc. If h satisfies the claim of the theorem, so does f . It therefore suffices to deal with the case f(1) ≤ 1 and f(n) ≤ a ⋅ f(n/b) + nc. Furthermore, it is enough to consider n = bk with k ∈ ℕ: the function f is nondecreasing and since p(bn) ∈ ![](images/o.jpg)(p(n)) for the functions p on the right-hand side, we can bound the value on n by the value on the next b-power. With g(n) = nc, [Lemma 3.1](#chapter03_1.xhtml_chapter03_1_3) yields

![](images/96_2.jpg)

If a < bc, the limit of the geometric series yields a constant factor

![](images/96_3.jpg)

For a = bc, we have f(n) ≤ nc ⋅ (k + 1) ∈ ![](images/o.jpg)(nc log n). The remaining case is a > bc:

![](images/96_4.jpg)

Thus, the proof is complete for all cases.

The following example gives another typical approach for solving recurrences. The idea is to verify an educated guess.

□

Example 3.3. Let f : ℝ≥0 → ℝ≥0 be a nondecreasing function such that f(n) ≤ ![](images/96_5.jpg) for some d ≥ 1\. If we had ![](images/96_6.jpg) then f(n) ∈ ![](images/o.jpg)(n log n) by the master theorem. The “+4” should not change the asymptotics, and we therefore conjecture that for some sufficiently large constant k ≥ 4d we have f(n) ≤ kn log2 n for all n ≥ 1\. Here, “sufficiently large” means that the conjecture holds for all n between 1 and 256d, that is, the base case is true. Let now n > 256d and suppose the conjecture holds for values smaller than n. Then

![](images/97_1.jpg)

Thus, f(n) ≤ kn log2 n as desired.

◊

Birthday paradox

The birthday paradox can be quite helpful in the consideration of randomized algorithms. The idea is that, in a random sequence of elements from an n-element set, there is a high probability of two identical elements occurring within the first ![](images/97_2.jpg) elements. Taking as basic set the 366 possible birthdays, it can be shown that the probability of two people having the same birthday in a group of 23 people is greater than 1/2\. Since the number 23 seems surprisingly small, this situation is usually described by the name birthday paradox.

Let N be an n-element set. We consider a random sequence of length m consisting of elements of N. The probability that the first i + 1 items in the sequence are all different is

![](images/97_3.jpg)

Thus, the probability that all m items are different can also be written as

![](images/97_4.jpg)

Here, a uniform distribution of the elements is assumed; however, if certain elements are more likely than others, then the probability of a match is even greater. With the inequality (1 + x) ≤ ex, we can estimate the probability to have no duplicates as follows:

![](images/97_5.jpg)

With increasing m, the term ![](images/97_6.jpg) approaches 0\. For ![](images/97_7.jpg) a probability below 1/2 will be reached. The birthday paradox is the basis for runtime estimations in so-called ρ algorithms.

## 3.2 Fast exponentiation

Let M be a monoid. Fast exponentiation means: on input a ∈ M and n ∈ ℕ find the element an applying as few monoid operations as possible. Naively, one could determine an by the recursive rule an = a ⋅ an−1 with n − 1 operations. But if n is given in binary, this leads to an exponential algorithm. If n is an even number, one can determine an from an/2 by squaring. The fast exponentiation method now tries to square as often as possible. Moreover, it should not be necessary to store more than constantly many monoid elements. This is achieved by the following algorithm:

![](images/98_1.jpg)

If n is odd, then an = a ⋅ an−1, and n − 1 is even. Therefore, n can be halved in each iteration. If â and n̂ are the initial values of a and n, respectively, then the loop invariant is e ⋅ an = ân̂ . In each execution of the while loop at most two monoid operations are performed, so this algorithm requires at most 2 ⌊log2 n⌋ + 2 operations. The maximum number of operations is reached on numbers of the form n = 2k − 1\. In the case of M = ℤ/mℤ, with modular multiplication as the operation, the above algorithm is also called fast modular exponentiation. This is meant to emphasize that you do not compute the number an ∈ ℤ first and then reduce modulo m, but that all intermediate results are computed modulo m. Therefore, these numbers are limited by m, whereas an can already become very large for rather small numbers a and n.

We note that for cryptographic applications, in order to make sure that you cannot deduce any information about the input by measuring the execution time or the energy consumption, it is often desirable for the running time not to depend on n but only on the number of digits of n. For this purpose, the first line of the while loop could be replaced by

![](images/98_3.jpg)

Remark 3.4. The above approach is not always optimal. Consider the computation of a15. Using fast exponentiation, we need six operations: squaring three times yields the elements a2, a4, a8; and with three further multiplications,we obtain a15 = a ⋅a2 ⋅ a4 ⋅ a8. If, on the other hand, we compute the five elements a2, a3 = a ⋅ a2, a6 = (a3)2, a12 = (a6)2 and a15 = a12 ⋅a3 with one operation each, then these five multiplications lead to the desired result. The general approach of this kind is usually referred to as addition chains. An addition chain for n ∈ ℕ\{0} is a sequence (a0, . . . , ak) of natural numbers with the properties a0 = 1, ak = n, and each number ai (for i ≥ 1) is the sum of two (not necessarily different) preceding numbers. Here, the length k is the number of monoid operations required to compute an by this addition chain. The addition chain for 15 that results from fast exponentiation, is (1, 2, 3, 4, 7, 8, 15). The alternate computation with five multiplications uses the addition chain (1, 2, 3, 6, 12, 15). The main algorithmic disadvantage (except that one has to construct optimal addition chains, which, however, does not require monoid operations) is that, in general, all intermediate results need to be stored. At best, nearly half of the required monoid operations can be saved using addition chains; see Section 4.6.3 in [[55](#Bibliography.xhtml_Bibliography_55)].

◊

## 3.3 Binary GCD

We have seen, in [Section 1.5.1](#chapter01_2.xhtml_chapter01_2_13), how to compute the greatest common divisor with a logarithmic number of recursive calls. The algorithm presented there can be applied to arbitrary rings which admit a Euclidean division, so-called Euclidean domains. This includes polynomial rings over fields; see [Theorem 1.44](#chapter01_3.xhtml_chapter01_3_5). However, in many settings, the operation “ℓ mod k” is considered to be expensive in the sense that it uses significantly more time and energy than, for instance, addition and subtraction. The binary gcd (the procedure bgcd below) efficiently computes the greatest common divisor of two natural numbers such that all divisions and multiplications are by the number 2\. Assuming that we represent natural numbers in binary, these are nothing but bitwise shifts.

![](images/99_2.jpg)

The number of recursive calls is in O(log k +log ℓ) since, after at most two calls, at least one of the arguments is divided by 2\. Note that 2 is a common divisor of k and ℓ if and only if both of them are even. Since gcd(k, ℓ) = gcd(k − ℓ, ℓ), the correctness of the algorithm follows. It is possible to extend the binary gcd such that, on input k and ℓ, it additionally computes numbers a and b with ak + bℓ = gcd(k, ℓ). Moreover, this extension also does not use arbitrary division and multiplication; see [Exercise 3.3](#chapter03_3.xhtml_chapter03_3_19).

## 3.4 Probabilistic recognition of primes

For many applications, such as the RSA cryptosystem, very large prime numbers are needed. This leads to the question of how to rapidly check a given (large) number n for primality. In the [next chapter](#chapter04.xhtml_chapter04_1), we will present a deterministic polynomial time algorithm for this problem. However, its running time cannot compete with the probabilistic methods presented here. The two main procedures in this section – the Solovay–Strassen and the Miller–Rabin primality test – work in rounds. In each round, a number a ∈ {1, . . . , n − 1} is selected at random and, depending on a, the output is either that n is composite or that n is probably prime. If the output is that n is composite, then n is actually composite. But whenever the output says that n is probably prime, then n could still be composite. However, both methods have the property that, for a composite number n, with probability at least 1/2, the chosen a reveals n as composite. Therefore, after k independent rounds, a composite number is discovered with a probability of at least 1 − 2−k. If after 100 rounds each time the output claimed that n may be prime, then the error probability is less than

![](images/100_2.jpg)

### 3.4.1 Fermat primality test and Carmichael numbers

On input n, the Fermat test consists of two steps. First, it randomly chooses a ∈ {1, . . . , n − 1}. Then, it computes b = an−1 mod n. If n is prime, then Fermat’s little theorem yields b = 1\. Thus, if b ≠ 1, then n is composite. Otherwise, if b = 1, then n might be prime, but we do not know for sure. It could therefore be helpful to repeat the procedure in order to possibly reveal n as composite.

Carmichael numbers are named after Robert Daniel Carmichael (1879–1967). A Carmichael number is a composite number n satisfying an−1 ≡ 1 mod n for all a ∈ (ℤ/nℤ)∗. This means that the Fermat test fails for such numbers because there is no real chance to find a suitable a which proves that n is composite (of course, there is always the tiny chance to choose a ∉ (ℤ/nℤ)∗ and find a divisor of n). There are infinitely many Carmichael numbers [[2](#Bibliography.xhtml_Bibliography_3)]. The first three Carmichael numbers are 561, 1105, and 1729\. The Carmichael numbers are the Knödel numbers K1. They are named after Walter Knödel (born 1926) who was the founding Dean of the Department of Computer Science at the University of Stuttgart. A number n belongs to Krif an−r ≡ 1 mod n for all a ∈ (ℤ/nℤ)∗. The following theorem collects some basic properties of Carmichael numbers. A natural number n is square-free if m2 ∤ n for all integers m ≥ 2, that is, no prime power of exponent greater than 1 appears in the prime factorization of n.

Theorem 3.5. Let n be a Carmichael number. Then the following properties hold:

(a)n is odd

(b)n is square-free, and

(c)n has at least three different prime factors.

Proof: (a) Note that n ≥ 4\. If n is even, then ![](images/101_1.jpg) mod n, a contradiction. (b) Suppose that n = pdu for some prime number p such that p ∤ u and d ≥ 2\. Then wee have

![](images/101_2.jpg)

This yields (pd−1 + 1)n ≡ 1 mod pd and (pd−1 + 1)n−1 ≢ 1 mod pd. Let b ≡ pd−1 + 1 mod pd and b ≡ 1 mod u. Then, b is an element in (ℤ/nℤ)∗ satisfying bn−1 ≢ 1 mod n, a contradiction.

(c)Assume that n = pq for two prime numbers p ≠ q. Let g ∈ ℤ/nℤ be a generator modulo p and congruent 1 modulo q. The order of g is p − 1\. On the other hand, gn−1 = 1 since n is a Carmichael number. This yields

![](images/101_8.jpg)

and thus p − 1 | q − 1. Symmetrically, we have q − 1 | p − 1 and thus p = q, a contradiction. Therefore, n has at least three different prime factors.

### 3.4.2 Solovay–Strassen primality test

Robert Martin Solovay (born 1938) and Volker Strassen (born 1936) combined Euler’s criterion and the law of quadratic reciprocity to obtain a probabilistic primality test, the Solovay–Strassen test. The basic idea is the following. To assure the primality of a given odd number n ≥ 3, in each round you verify that ![](images/101_4.jpg) mod ![](images/101_5.jpg) for a randomly chosen a ∈ (ℤ/nℤ)∗. More precisely, one round of the Solovay–Strassen test works as follows:

(1)Select a ∈ {1, . . . , n − 1} at random.

(2)Compute ![](images/101_6.jpg) mod n. If b ∉ {1, −1}, halt and output “n is composite.”

(3)Compute ![](images/101_7.jpg) If b = c, halt and output “n is probably prime.” Otherwise, output “n is composite.”

For the computation of b, we use fast exponentiation and c is computed using the algorithm for the Jacobi symbol. Note that b ∈ {1, −1} implies a ∈ (ℤ/nℤ)∗. If n is prime,then the output is “n is probably prime” by Euler’s criterion and Zolotarev’s lemma. We now show that, in every round, composite numbers are detected with probability greater than 1/2\. If n survived k rounds of this procedure, then the probability that n is prime is at least 1 − 2−k. There are no exceptions for this test such as Carmichael numbers for the Fermat test.

Theorem 3.6. Let ![](images/102_1.jpg) mod n } for an odd number n ≥ 3. Then, E (n) is a subgroup of (ℤ/nℤ)∗ and we have

![](images/102_2.jpg)

Proof: E (n) contains the element 1; so it is not empty and, by [Theorem 1.70 (d)](#chapter01_4.xhtml_chapter01_4_12), E (n) is a group. The direction from right to left follows from Euler’s criterion ([Theorem 1.68](#chapter01_4.xhtml_chapter01_4_6)) and Zolotarev’s lemma ([Theorem 1.69](#chapter01_4.xhtml_chapter01_4_7)). For the remaining direction, suppose that E (n) = (ℤ/nℤ)∗ for a composite number n. In particular, n is a Carmichael number. From [Theorem 3.5](#chapter03_1.xhtml_chapter03_1_17), n is square-free. We can write n = pu for a prime number p ≥ 3 with p ∤ u. Let a be not a square modulo p and congruent 1 modulo u. In particular, a ∈ (ℤ/nℤ)∗. Then, we have

![](images/102_3.jpg)

From E(n) = (ℤ/nℤ)∗, we obtain ![](images/102_4.jpg) mod n and therefore ![](images/102_5.jpg) mod u. This is a contradiction to a ≡ 1 mod u.

□

If n is an odd and composite number, then the index of the subgroup E (n) in (ℤ/nℤ)∗ is at least 2\. Thus, more than half of the elements of {1, . . . , n − 1} are not in E(n). All such elements lead to a round of the Solovay–Strassen test in which n is detected as composite.

### 3.4.3 Miller–Rabin primality test

The initial situation is as follows: let n ≥ 3 be an odd number. After a certain number of trial divisions, we suspect that n could be prime. The Miller–Rabin test is named after Gary Lee Miller and Michael Oser Rabin. In every round, it either refutes the primality or it yields the result that n is prime with a probability of at least 3/4\. The Miller–Rabin test refines the Fermat test and it can also handle Carmichael numbers. It can even be efficiently performed for large numbers and, by repeating it independently, it can be made sufficiently reliable for all practical purposes, such as cryptographic applications.

Given an odd number n ≥ 3, the Miller–Rabin test works as follows:

(1)Write n − 1 = 2ℓu for an odd number u.

(2)Select a ∈ {1, . . . , n − 1} at random and let b = au mod n.

(3)If b = 1, halt and output “n is probably prime.”

(4)For b ≠ 1, construct the following sequence by successive squaring in ℤ/nℤ:

![](images/103_8.jpg)

(5)If −1 occurs in this sequence, halt and output “n is probably prime”; otherwise output “n is composite.”

First, let n be prime. Then by Fermat’s little theorem, we have an−1 ≡ 1 mod n for all a ∈ {1, . . . , n − 1}. If b ≡ 1 mod n, the output is “n is probably prime.” So let b ≢ 1 mod n. Since ![](images/103_4.jpg) mod n, the sequence (![](images/103_5.jpg) ) contains an element c whose square in ℤ/nℤ is equal to 1, and c itself is not 1\. But ℤ/nℤ is a field in which the polynomial X2 − 1 only has the two roots 1 and −1\. Therefore, −1 occurs in the list. This shows that in any case the output is “n is probably prime” whenever n is actually prime.

It remains to consider the case where n is composite. In [Theorem 3.11](#chapter03_1.xhtml_chapter03_1_28), we show that then in at most 1/4 of all cases the output is “n is probably prime.”

Proposition 3.7. Let n = rst ∈ ℕ for pairwise coprime numbers r, s, t ≥ 1 such that r, s ≥ 3 are odd. Let u be odd, ℓ ≥ 1 and

![](images/103_6.jpg)

for k = min{ 2ℓ−1u | ∀a ∈ G: a2ℓ' u ≡ 1 mod rs }. Then, H ≠ G.

Proof: Since ℓ ≥ 1, we have −1 ∈ G and thus k ∈ ℕ. By construction of k there exists a ∈ G with a2k ≡ 1 mod rs and ak ≢ 1 mod rs. Without loss of generality, let ak ≢ 1 mod r. From the Chinese remainder theorem, there exists b with b ≡ a mod r and b ≡ 1 mod st. We have b2k ≡ 1 mod rs and hence b ∈ G. On the other hand, b ∉ H because bk ≢ ±1 mod rs. This shows H ≠ G.

□

Using [Proposition 3.7](#chapter03_1.xhtml_chapter03_1_22), one can easily prove an error probability of at most 1/2 for the Miller–Rabin test: for any odd composite number n, we can consider the groups

![](images/103_7.jpg)

for k = min{ 2ℓ−1u | ∀a ∈ G: a2ℓ' u ≡ 1 mod n }. Remember that n − 1 = 2ℓu for an odd number u. All elements a ∈ (ℤ/nℤ)∗ \ H lead to the output “n is composite.” If G ≠ (ℤ/nℤ)∗, then we also have H ≠ (ℤ/nℤ)∗. Otherwise, n is a Carmichael number and by [Theorem 3.5](#chapter03_1.xhtml_chapter03_1_17), we can write n = rs for odd coprime numbers r, s ≥ 3\. [Proposition 3.7](#chapter03_1.xhtml_chapter03_1_22) yields H ≠ G. Therefore, in any case, the index of H in (ℤ/nℤ)∗ is at least 2\. This gives an error probability of 1/2\. Proving the error probability 1/4 is slightly more involved.

Lemma 3.8. Let n = pd ≠ 9 for some odd prime p. At most 1/5 of all elements a ∈ (ℤ/nℤ)∗ yield the output “n is probably prime” in the Miller–Rabin test.

Proof: The group (ℤ/nℤ)∗ is cyclic of order (p − 1)pd−1. Let g be a generator of (ℤ/nℤ)∗. We have gcd((p − 1)pd−1, n − 1) = p − 1\. Therefore, we have (gk)n−1 ≡ 1 mod n if and only if pd−1 | k. Hence, exactly p − 1 elements a ∈ (ℤ/nℤ)∗ satisfy an−1 ≡ 1 mod n. If an−1 ≢ 1 mod n, then

![](images/104_11.jpg)

and the output is “n is composite.” Unless p = 3 and d = 2, we have ![](images/104_2.jpg) 1/pd−1 ≤ 1/5.

□

Lemma 3.9. Let n = rs for odd coprime numbers r, s ≥ 3 and suppose that n is not a Carmichael number. At most 1/4 of all elements a ∈ (ℤ/nℤ)∗ yield the output “n is probably prime” in the Miller–Rabin test.

Proof: Let

![](images/104_9.jpg)

for ![](images/104_4.jpg) Note that H is a subgroup of G which, in turn, is a subgroup of (ℤ/nℤ)∗. Since n is not a Carmichael number, we have G ≠ (ℤ/nℤ)∗, and [Proposition 3.7](#chapter03_1.xhtml_chapter03_1_22) shows H ≠ G. Therefore, the index of H in (ℤ/nℤ)∗ is at least 4.

Next, we show that the output “n is probably prime” implies a ∈ H. If b = 1, then a ∈ H. Let now b2i ≡ −1 mod n for i < ℓ. Then, ![](images/104_5.jpg) mod rs and thus a ∈ G. In particular, the element a is considered in the definition of k and thus, 2iu divides k. This shows a ∈ H. Therefore, all elements a ∈ (ℤ/nℤ)∗ \ H lead to the output “n is composite.”

□

In the case of n being a Carmichael number, we use the property that n has at least three different prime factors for applying [Proposition 3.7](#chapter03_1.xhtml_chapter03_1_22) twice.

Lemma 3.10. Let n be a Carmichael number. At most 1/4 of all elements a ∈ (ℤ/nℤ)∗ yield the output “n is probably prime” in the Miller–Rabin test.

Proof: By [Theorem 3.5](#chapter03_1.xhtml_chapter03_1_17), we have n = rst for coprime numbers r, s, t ≥ 3\. Let G = (ℤ/nℤ)∗ and ℓ' ∈ ℕ minimal such that

![](images/104_12.jpg)

Since −1 ∈ G, we have ℓ' ≥ 1\. We define ![](images/104_7.jpg) Let

![](images/104_10.jpg)

Note that J is a subgroup of H and H is a subgroup of G. [Proposition 3.7](#chapter03_1.xhtml_chapter03_1_22) shows H ≠ G. If J ≠ H, then the index of J in G is at least 4, and we are done, since all a ∈ G\ J yield the output “n is composite.” So let J = H, that is, ah ≡ ±1 mod rs implies ah ≡ ±1 mod n for all a ∈ G. If ah ≡ −1 mod n, then ah ≡ −1 mod rs; now, the element â defined by â ≡ a mod rs and â ≡ 1 mod t is in H \ J, a contradiction. This shows J = { a ∈ (ℤ/nℤ)∗ | ah ≡ 1 mod n }. Let m ∈ ℕ be minimal with J = {a ∈ (ℤ/nℤ)∗ | a2mu ≡ 1 mod n }. We set k = 2m−1u. By [Proposition 3.7](#chapter03_1.xhtml_chapter03_1_22)

![](images/105_8.jpg)

is a proper subgroup of J. Hence, the index of K in G is at least 4.

It remains to show that the output “n is probably prime” implies a ∈ K. If b = 1, then a ∈ K. Let now b2i ≡ −1 mod n for i < ℓ. Then, b2i ≡ −1 mod rs and thus i < ℓ. It follows that a ∈ H = J. In particular, a is considered in the definition of m. We conclude i < m and a ∈ K. Therefore, all a ∈ G \ K yield the output “n is composite.”

□

Theorem 3.11. Let n ≥ 3 be odd and composite. At most 1/4 of all elements a ∈ {1, . . . , n − 1} yield the output “n is probably prime” in the Miller–Rabin test.

Proof: All elements a ∈ {1, . . . , n − 1} with a ∉ (ℤ/nℤ)∗ yield the output “n is composite.” For n ≠ 9, the claim therefore follows from the [Lemmas 3.8](#chapter03_1.xhtml_chapter03_1_23), [3.9](#chapter03_1.xhtml_chapter03_1_25) and [3.10](#chapter03_1.xhtml_chapter03_1_26). For n = 9, the Miller–Rabin test considers eight possible choices for a, but only a = 1 and a = −1 lead to the output “n is possibly prime.”

□

This shows that the Miller–Rabin test yields a given level of certainty with half as many rounds as the Solovay–Strassen test.

### 3.4.4 Applications of the Miller–Rabin scheme

[Proposition 3.7](#chapter03_1.xhtml_chapter03_1_22) does not require that 2ℓu = n − 1\. This allows us to extend the Miller–Rabin scheme to other settings. Let n ≥ 3 be odd. Suppose that ℓ ≥ 1 and that u is odd. We can arbitrarily choose a ∈ {1, . . . , n − 1}, set b = au mod n, and then consider the sequence ![](images/105_2.jpg) Let

![](images/105_3.jpg)

![](images/105_7.jpg)

for ![](images/105_4.jpg) [Proposition 3.7](#chapter03_1.xhtml_chapter03_1_22) shows H ≠ G. For every element a ∉ H one of the following properties holds:

(a)![](images/105_5.jpg) mod n, or

(b)![](images/105_6.jpg)

Thus, for a random element a ∈ {1, . . . , n − 1} one of these two conditions is satisfied in at least half of the cases. If condition (a) is satisfied because a is not invertible modulo n, then we find a nontrivial divisor of n, namely gcd(a, n). If, in contrast, condition (a) is satisfied for a ∈ (ℤ/nℤ)∗, then G =(ℤ/nℤ)∗. If ![](images/106_1.jpg) mod n and condition (b) holds, then there is an element ![](images/106_2.jpg) such that c2 ≡ 1 mod n and c ≢ ±1 mod n. But then (c − 1)(c + 1) ≡ 0 mod n, and gcd(c − 1, n) is a nontrivial divisor of n. In particular, half of all elements a ∈ {1, . . . , n − 1} yield either a divisor of n or the result G ≠ (ℤ/nℤ)∗. If φ(n) divides 2ℓu, then G = (ℤ/nℤ)∗ and we can use the Miller–Rabin scheme as a probabilistic method for factorizing n. For example, if all prime factors of φ(n) are elements of the set {p1, . . . , pm}, then n can be factored by choosing ℓ and u such that ![](images/106_3.jpg) holds.

Security of the secret key in RSA

Using the Miller–Rabin scheme, we will show that the secret key for the RSA cryptosystem is secure. For the RSA algorithm, two sufficiently large primes p and q are determined and n = pq is computed. Then numbers e, s ≥ 3 with es ≡ 1 mod φ(n) are computed. The public key is the pair (n, e), and the secret key is s. Encryption is done by x ↦ xe mod n; decryption can be accomplished by y ↦ ys mod n. If it is possible to factorize n, then it is possible, from the knowledge of e, to determine the secret key s efficiently. However, it is generally believed that there is no efficient method for factorizing large numbers, and that it is therefore not feasible to factorize n. We want to show that with the knowledge of the secret key s, it is easily possible to determine the factors of n. Since it is assumed that the latter cannot be performed efficiently, there can be no efficient method to determine s with the knowledge of the public key (n, e).

Let s ∈ ℕ be a number with (xe)s = xes ≡ x mod n for all x ∈ ℤ. Then, aes−1 ≡ 1 mod n for all a ∈ (ℤ/nℤ)∗. Wewrite es−1 = 2ℓu with an odd u. From [Proposition 3.7](#chapter03_1.xhtml_chapter03_1_22), using the same notation, we obtain H ⊊ G = (ℤ/nℤ)∗. In particular, the following procedure yields a factor of n with high probability:

(1)Choose a ∈ {2, . . . , n − 1} at random.

(2)If gcd(a, n) ≠ 1, then we have a divisor of n.

(3)Let b = au mod n.

(4)If b ≠ 1, then consider the sequence ![](images/106_4.jpg) modulo n. If −1 does not occur in this sequence, then, because of b2ℓ ≡ 1 mod n, the sequence contains an element c ≢ ±1 mod n with c2 ≡ 1 mod n. Thus, computing gcd(c − 1, n), we obtain a divisor of n.

(5)If no divisor has been found so far, repeat the process with a new value of a.

As we saw above, this procedure finds a divisor of n with a probability of at least 1/2 in each iteration. Under the assumption that one cannot factorize n efficiently, this shows that it is not possible for an attacker to derive the secret key from the public key in the RSA cryptosystem.

### 3.4.5 Miller–Rabin versus Solovay–Strassen

The Solovay–Strassen test plays a minor role in practice and it cannot compete with the Miller–Rabin test, the latter being conceptually and algorithmically simpler. The Solovay–Strassen test loses because, for a fixed choice of a, whenever the Solovay–Strassen test deduces that n is composite, then so does the Miller–Rabin test. We show this in [Theorem 3.12](#chapter03_1.xhtml_chapter03_1_32).

Let n ≥ 3 be odd and a ∈ ℤ with gcd(a, n) = 1\. The number n is a pseudoprime to base a if an−1 ≡ 1 mod n (and so, n with the choice of a passes the Fermat test); n is an Eulerian pseudoprime to base a if ![](images/107_1.jpg) mod n is true (and so, n with the choice of a passes the Solovay–Strassen test); finally, n is a strong pseudoprime to base a if n − 1 = 2ℓu for an odd u and one of the following conditions is satisfied:

–au ≡ 1 mod n, or

–thereexists0 ≤ k < ℓ such that ![](images/107_2.jpg) mod n

On this choice of a, strong pseudoprimes pass the Miller–Rabin test. The less bases there are such that a composite number n is an (Eulerian or strong, respectively) pseudoprime, the more likely the respective primality test will detect that n is composite. Carmichael numbers are pseudoprimes to all bases.

If n is an Eulerian pseudoprime to base a, then a(n−1)/2 mod n ∈ {1, −1} and therefore an−1 = (a(n−1)/2)2 ≡ 1 mod n. So n is a pseudoprime to base a. Thus, the Solovay–Strassen test on composite numbers never performs worse (and on Carmichael numbers it always performs better) than the Fermat test. The next theorem shows that the Miller–Rabin test performs even better; see also [Exercise 3.4](#chapter03_3.xhtml_chapter03_3_20).

Theorem 3.12. Every strong pseudoprime n to base a is also an Eulerian pseudoprime to base a.

Proof: Let a ∈ (ℤ/nℤ)∗ such that the output of the Miller–Rabin test is “n is probably prime.” We need to show that the Solovay–Strassen test gives the same output. We write n − 1 = 2ℓu with u odd. Note that ℓ ≥ 1 since n is odd. Let b = au mod n. Since ![](images/107_3.jpg) and u is odd, we have

![](images/107_4.jpg)

![](images/107_5.jpg)

It therefore remains to show that ![](images/107_6.jpg) mod n. If b = 1, then this is true. Let now b2k−1 ≡ −1 mod n for some k ∈ {1, . . . , ℓ}. In particular, the order of b modulo n is 2k.

We let n = p1 ⋅⋅ ⋅ pt for not necessarily distinct primes pi. Let pi − 1 = 2ℓi ui for ui odd. By reordering, we can assume that ℓ1 ≤ ⋅⋅ ⋅ ≤ ℓt. We have b2k ≡ 1 ≢ −1 ≡ b2k−1 mod pi for all i. Therefore, the order of b modulo pi is 2k, and we obtaink ≤ ℓ1. Let s be the number of exponents ℓi with k = ℓi. For i ≤ s we have pi − 1 = 2kui = 2k(1 + 2zi) = 2k + 2k+1zi ≡ 2k mod 2k+1, and if i > s, then 2k+1 | pi − 1 and thus pi ≡ 1 mod 2k+1. This yields

![](images/108_1.jpg)

If s is even, then 2k+1 | n−1and![](images/108_2.jpg) mod n. Otherwise, if s is odd, then 2k+1 ∤ n−1 and ![](images/108_3.jpg) mod n. Euler’s criterion and Zolotarev’s lemma yield

![](images/108_4.jpg)

Thus, ![](images/108_5.jpg) We conclude ![](images/108_6.jpg) mod n, as desired.

□

The proof of [Theorem 3.12](#chapter03_1.xhtml_chapter03_1_32) is adapted from Carl Bernard Pomerance (born 1944), John Lewis Selfridge (1927–2010), and Samuel Standfield Wagstaff, Jr. (born 1945) [[85](#Bibliography.xhtml_Bibliography_86)].

## 3.5 Extracting roots in finite fields

Extracting roots in a group G is the following problem. Let an element a ∈ G be given, which is known to be a square, that is, an element b ∈ G with a = b2 exists. The goal is to determine such an element b satisfying a = b2. In general, the solution is not unique. It is often difficult to extract roots modulo n. In this section, we show that in finite fields, this problem is efficiently solvable using probabilistic algorithms. Let ![](images/f_d.jpg) be a finite field. On input a ∈ ![](images/f_d.jpg),wewant to compute b ∈ ![](images/f_d.jpg) with b2 = a. We call b a square root of a and say that a is a square or a quadratic residue. If b is a root of a, then so is −b. Since quadratic equations over fields have at most two solutions, we conclude that b and −b are the only roots of a. There are some special cases where extracting roots is particularly simple. Before we examine a general method, let us first consider two such special cases.

Let G be a finite group of odd order and a ∈ G. We let b = a(|G|+1)/2. The crucial point here is that (|G| + 1)/2 is an integer. From [Corollary 1.5](#chapter01_1.xhtml_chapter01_1_14), we have a|G| = 1\. Thus, b2 = a|G|a = a. So b is a square root of a. This covers the case![](images/f_d.jpg) = ![](images/f_d.jpg)2n because here the order of the multiplicative group ![](images/f_d.jpg)∗ = ![](images/f_d.jpg) \ {0} is odd. In particular, each element in 2n is a square.

Before we proceed to the second special case, we want to remark that, in general, not every element of a field is a square. A simple example for that is ![](images/f_d.jpg)3 = {0, 1, −1}. In this field, −1 is not a square. We can use Euler’s criterion to check whether an element a of a field ' with an odd number of elements is a square: we have a(|![](images/f_d.jpg)|−1)/2 = 1 if and only if a is a square. We now investigate the case || ≡ −1 mod 4 separately since, in this case, extracting roots is simple. The reason is that exactly one of the elements a and −a in ![](images/f_d.jpg)∗ is a square: since |![](images/f_d.jpg)| + 1 is divisible by 4, the element b = a(|![](images/f_d.jpg)|+1)/4 is well defined and we have

![](images/109_1.jpg)

Thus, if a is a square, then b is one of its square roots. Next, we consider two algorithms to extract roots in arbitrary finite fields ' for which || is odd.

### 3.5.1 Tonelli’s algorithm

Let ![](images/f_d.jpg) be a finite field with an odd number q = || of elements. We present the probabilistic method for extracting roots, as developed by Alberto Tonelli (1849–1921) in 1891\. To this end, we write q − 1 = 2ℓu with u odd. Let

![](images/109_2.jpg)

Each set Gi−1 is a subgroup of Gi, and Gℓ = ![](images/f_d.jpg)∗. Since ∗ is cyclic, all groups Gi are cyclic, too. Let x be a generator of ![](images/f_d.jpg)∗. Then, x2ℓ−i is a generator of Gi. In particular, we can see that the index of Gi−1 in Gi is 2.

Let g ∈ ![](images/f_d.jpg)∗ be not a square. With Euler’s criterion, we obtain ![](images/109_3.jpg) ![](images/109_11.jpg)Thus, ![](images/109_4.jpg) and, moreover, Gℓ−i−1 and g2i Gℓ−i−1 are the two cosets of Gℓ−i−1 in Gℓ−i; that is, you can alternate between these two cosets by multiplication with g2i. Each quotient Gi/Gi−1 is generated by a power of g. Thus, also ![](images/f_d.jpg)∗/ G0 is generated by g. In particular, each element a ∈ ![](images/f_d.jpg)∗ can be written as a = gkh with h ∈ G0. The idea now is to extract the roots of gk and h separately. For h, this is easy because G0 is of odd order. If a is a square, then k is even: Euler’s criterion yields

![](images/109_10.jpg)

and, because of ![](images/109_12.jpg)we see that k must be even, showing that gk/2 is a root of gk. Therefore, it only remains to determine the exponent k. Let k = Σj≥0 kj2j be the binary representation of k. For the first i bits k0, . . . , ki−1 of k, using ![](images/109_6.jpg) we obtain

![](images/109_7.jpg)

This shows that ![](images/109_8.jpg) If k0, . . . , ki−2 are known already, then the bit ki−1 is uniquely determined, because ![](images/109_9.jpg) Finally, this yields the following algorithm:

(1)Choose a random element g ∈ ∗ until g is not a square.

(2)Determine k0, . . . , kℓ−1 successively such that ![](images/110_2.jpg) for all i.

(3)Let ![](images/110_1.jpg) and h = ag−k.

(4)Return b = gk/2 h(u+1)/2 as a root of a.

In each iteration of the first step, g is not a square with probability 1/2\. Therefore, a suitable g is found after only a few rounds with high probability. To check whether c ∈ Gℓ−i, we compute c2ℓ−iu. Using fast exponentiation, this takes O(log q) operations in . The test has to be carried out ℓ times, so ![](images/o.jpg)(ℓ log q) operations in ' suffice for this part. Since ℓ ≤ log q, the worst case here is O(log2 q) operations. The remaining steps are in O(log q).

This can be slightly improved using a trick of Daniel Shanks (1917–1996). For this purpose, we compute c = au. The element gu is not a square since

![](images/110_10.jpg)

Replacing g by gu, after step (1) of Tonelli’s algorithm, we may assume that ![](images/110_4.jpg) The condition ![](images/110_9.jpg) now is equivalent to ![](images/110_6.jpg) This can be checked using ![](images/o.jpg)(ℓ) field operations. Thus, the complexity of the algorithm is improved to ![](images/o.jpg)(ℓ2 + log q) operations in .

### 3.5.2 Cipolla’s algorithm

Let ![](images/f_d.jpg) be a finite field with an odd number of elements. We now present and investigate the randomized algorithm of Michele Cipolla (1880–1947) for finding a square root. This algorithm works with polynomials in [X]. On input a ∈ , the idea is to construct a field extension in which it is easy to compute a square root of a. In the following, let the input a ∈ ![](images/f_d.jpg)∗ be a square:

(1)Repeatedly choose elements t ∈ ' at random until t2 − 4a is not a square.

(2)Let f = X2 − tX + a.

(3)Compute b = X(||+1)/2 mod f . This is the desired square root of a.

We first show that, with high probability, a suitable element t is chosen in the first step.

Theorem 3.13. Let a ∈ ![](images/f_d.jpg)∗ be a square. If t ∈ ' is randomly chosen, then t2 − 4a is not a square with probability (|![](images/f_d.jpg)| − 1)/(2|![](images/f_d.jpg)|).

Proof: By completing the square, we see that t2 − 4a is a square if and only if the polynomial X2 − tX + a splits into linear factors over . The number of polynomials X2 − tX + a with t ∈ ' that split into linear factors over ' is equal to the number of polynomials (X−α)(X−β) with αβ = a. If you choose α, then β is uniquely determined (since a ≠ 0). We have α = β if and only if α is one of the two square roots of a. There are |![](images/f_d.jpg)|−3 different ways to choose α such that α ≠ β and αβ = a. Due to the symmetry in α and β, this yields (|![](images/f_d.jpg)| − 3)/2 polynomials. Additionally, there are the two possibilities for α = β being a square root of a. The remaining (|![](images/f_d.jpg)| − 1)/2 polynomials do not split into linear factors. This proves the statement of the theorem.

□

If t2 − 4a is not a square, then the polynomial f = X2 − tX + a ∈ ![](images/f_d.jpg)[X] is irreducible. Using [Theorem 1.51](#chapter01_3.xhtml_chapter01_3_15), we see that ![](images/k.jpg) = ![](images/f_d.jpg)[X]/f is a field that contains . The field ' contains X as an element. An important property of the element X ∈ is provided by the following theorem.

Theorem 3.14. In , we have X|![](images/f_d.jpg)|+1 = a.

Proof: If |![](images/f_d.jpg)| = pq for some prime p, then the mapping φ: ![](images/k.jpg) → ![](images/k.jpg) with φ(x) = x|![](images/f_d.jpg)| is the q-fold application of the Frobenius homomorphism x ↦ xp; see Theorem 1.28\. In particular, φ is a homomorphism. Since the roots of the polynomial Y|![](images/f_d.jpg)| − Y ∈ ![](images/k.jpg)[Y] are exactly the elements of ![](images/f_d.jpg), we see that φ(x) = x if and only if x ∈ ![](images/f_d.jpg).

Consider the polynomial h = Y2 − tY + a ∈ ![](images/k.jpg)[Y]. The roots of this polynomial are X and t−X. Since the coefficients of h are in, the elements φ(X) and φ(t−X) are roots of h, too. For instance, we have 0 = φ(0) = φ(h(X)) = φ(X)2 − tφ(X) + a. We conclude {X, t − X} = {φ(X), φ(t − X)}. Now, X ∉ ![](images/f_d.jpg) yields φ(X) ≠ X and thus X|![](images/f_d.jpg)| = φ(X) = t − X. Finally, we obtain X|![](images/f_d.jpg)|+1 = XX|![](images/f_d.jpg)| = X(t − X) = a.

From [Theorem3.13](#chapter03_2.xhtml_chapter03_2_7), it follows that, with high probability after a few runs, the algorithm will find a suitable element t ∈ ![](images/f_d.jpg). Therefore, Cipolla’s algorithm can be performed efficiently. Once t is found, the algorithm executes O(log |![](images/f_d.jpg)|) field operations. From [Theorem 3.14](#chapter03_2.xhtml_chapter03_2_9), we see that b ∈ is a square root of a. Now a, by assumption, has two square roots in . But since the equation Y2 = a has only two solutions, it follows that b ∈ ![](images/f_d.jpg). This shows the validity of Cipolla’s algorithm.

□

If a ∈ ![](images/f_d.jpg)∗ is not a square, then Cipolla’s algorithm still computes a square root b of a, but in this case we have b ∈ \ ![](images/f_d.jpg). Also, note that if a is not a square, then the success probability for finding an appropriate t is (|![](images/f_d.jpg)|+1)/(2|![](images/f_d.jpg)|); this is slightly better than in the case of a being a square.

## 3.6 Integer factorization

The security of many cryptosystems is based on the assumption that it is impossible to factorize large numbers efficiently. In this chapter, we will introduce some methods to demonstrate that the factorization of certain numbers is easy; from that we immediately obtain criteria for poorly chosen keys in certain cryptosystems. To factorize a number n one needs to find a factor m of n with 1 < m < n. To completely decompose n into its prime factors, one can go on by factorizing m and n /m. Before starting to factorize a number n, one can use a primality test like the Miller–Rabin test to check whether n is composite at all.

### 3.6.1 Pollard’s p − 1 algorithm

An idea of John Michael Pollard for factorization is the following. Let p be a prime divisor of n. With Fermat’s little theorem, we obtain ak ≡ 1 mod p for all multiples k of p −1\. If p −1 contains only prime factors of a set B, then we can use ![](images/112_1.jpg) Frequently, B is chosen to be the set of all primes up to a certain size. If ak ≢ 1 mod n, we obtain a nontrivial divisor of n by computing gcd(ak − 1, n). This leads to the following algorithm to find a divisor of n:

(1)Let ![](images/112_2.jpg)

(2)Compute gcd(ak − 1, n) for a randomly chosen a ∈ {2, . . . , n − 1}.

(3)If this does not yield a proper divisor of n, then try a new value of a or a larger base B of prime numbers.

Of course, in step(2),we first compute b = ak mod n with fast modular exponentiation and then gcd(b−1, n). The problem with Pollard’s p −1 algorithm is that the structure of the group (ℤ/nℤ)∗ is fixed. If no prime divisor p of n has the property that p −1 has only small prime factors, then this method does not work. Using an overlarge base B makes k huge, and thus the algorithm becomes inefficient.

### 3.6.2 Pollard’s rho algorithm for factorization

Another idea of Pollard’s for integer factorization uses the birthday paradox. The basic idea behind so-called ρ algorithms is as follows. From the birthday paradox, there is a high probability that in a sequence of ![](images/112_3.jpg) random elements from a finite set M two chosen elements are the same. Instead of a random sequence, you determine a pseudo-random sequence m0, m1, . . . with the property that mi+1 can be uniquely determined from mi. Then, if mi = mj, we obtain mi+k = m j+k for all k ≥ 0\. Moreover, from the viewpoint of an observer m0, m1, . . . , should behave like a random sequence. In particular, the probability of finding two indices i < j with mi = m j after ![](images/112_4.jpg) steps is high. The shape of the image below motivates the term “ρ algorithm.”

![](images/112_5.jpg)

Assume that n has a prime divisor p, and let f : ℤ/pℤ → ℤ/pℤ be an arbitrary mapping. The target set of f being finite, there exist integers j > i ≥ 0 with f j(x0) = f i(x0). If f behaves sufficiently randomly, then, with high probability, this phenomenon will already occur after the first ![](images/113_1.jpg) steps. The function f(x) = x2 + a mod p with a ∉ {−2, −1, 0} is often used; f(x) = x2 + 1 mod p is a typical example. As, unfortunately, we do not know p yet, we compute F (x) = x2 + a mod n instead of f. This yields

![](images/113_2.jpg) Fi(x0)≡ f i(x0) mod p

Now, we hope to find two elements that are the same in the f -sequence, but different in the F-sequence. For the corresponding indices i ≠ j, we have

![](images/113_8.jpg)

Using this pair (i, j), we now obtain a nontrivial factor of n by computing gcd(Fj(x0)−F i(x0), n). The problem is that storing each of the F i(x0) is too expensive, as is the comparison of all F i(x0) with each other. The solution is to continually increase the distance which we suspect is between i and j. Let xi = Fi(x0) and yi = F2i(x0). If xi ≡ xi+k mod p, then we obtainxj ≡ xj+k mod p for all j ≥ i. In particular, for j = kℓ ≥ i we have xj ≡ x2j = yj mod p. This leads to the following algorithm:

(1)Choose x0 ∈ {0, . . . , n − 1} at random, and let y0 = x0.

(2)For all i ≥ 1, successively consider the pairs

![](images/113_4.jpg) (xi , yi) = (F(xi−1), F2(yi−1))

and check whether gcd(yi − xi , n) yields a nontrivial divisor of n.

(3)Once gcd(yi − xi , n) = n holds, the procedure is stopped and restarted with a new initial value x0 or a different function F.

If gcd(yi−xi , n) = n holds, then we have found a cycle for the F-sequence. The problem is that the ρ algorithm for factorization is only efficient if n has a sufficiently small prime factor p. The expected number of arithmetic operations of the procedure to find a divisor of n is ![](images/113_5.jpg) If the smallest prime divisor is of order ![](images/113_6.jpg) then ![](images/113_7.jpg) operations have to be carried out. This is not feasible for large integers.

### 3.6.3 Quadratic sieve

The quadratic sieve is a factorization algorithm which does not require the input n to have some special structure. The basic idea is to find integers x and y such that x2 ≡ y2 mod n and x ≢ ±y mod n. In this case, both gcd(x − y, n) and gcd(x + y, n) yield a nontrivial factor of n.

We first fix a factor base B consisting of −1 together with a list of prime numbers. A typical choice is

![](images/114_9.jpg)

for some bound b depending on n. An integer is B-smooth if it can be written as a product of elements in B. In the first phase, we compute a large set of numbers S such that r2 mod n is B-smooth for all r ∈ S. Then, in the second phase, we choose a subset T of S such that all prime exponents in Πr∈T(t2 mod n) are even. Finally, we set x = Πr∈T r and y is computed from Πr∈T(r2 mod n) by halving all prime exponents. By construction, we have x2 ≡ y2 mod n. However, if x ≡ ±y mod n, then we either have to try a different choice for T, compute an even larger set S, or start all over again with a bigger bound b.

Let us consider the first phase in more detail. Let ![](images/114_2.jpg) and

![](images/114_10.jpg)

for some bound c significantly smaller than m /2\. We define f(r) = r2 −n for r ∈ R. Note that |f(r)| is in the order of magnitude of 2cm < n. We want to compute

![](images/114_11.jpg)

For every element r ∈ S, there is a factorization

![](images/114_5.jpg)

The computation of S starts with the vector (f(−c + m), . . . , f(c + m)). For every prime p ∈ B, if some entry in this vector is divisible by p, we divide it by p as often as possible. If we end up with an entry 1 or −1, then the initial integer at this position is B-smooth. Note that this computation also gives the prime exponents ep,s. It is too costly to check for every entry whether it is divisible by p. Here, the sieving comes into play. The entry f(r) is divisible by p if and only if f(r) = r2 − n ≡ 0 mod p. We compute solutions r1 and r2 of the quadratic equation r2 ≡ n mod p; this can be achieved with Tonelli’s or Cipolla’s algorithm from [Section 3.5](#chapter03_2.xhtml_chapter03_2_2). We have ![](images/114_6.jpg) mod p, and f(r) is divisible by p if and only if r ∈ {r1, r2} + pℕ. By construction of the vector, it suffices to consider c/p entries.

In the second phase, we want to compute a subset T ⊆ S such that in the product

![](images/114_7.jpg)

all exponents Σr∈T ep,r for p ∈ B are even (including the exponent of −1). To this end, we need to find a nontrivial solution of the following system of linear equations modulo 2 with variables Xr ∈ {1, 0}:

![](images/114_8.jpg)

In particular, we want to have |S| ≥ |B|. The set T is given by

![](images/115_4.jpg)

Finally, we set x = Πr∈T r and y = Πp∈B p(Σr∈T ep,r)/2.

If B is too small, we have to choose a huge c in order to have |S| ≥ |B|. On the other hand, if B is large, the sieving takes a lot of time and we have to solve a large system of linear equations. Typically, you start with rather “small” values of b and c in the order of magnitude of ![](images/115_2.jpg) and then increases them if the algorithm does not succeed with the factorization of n.

There are many optimizations of the quadratic sieve. For instance, it suffices to only consider primes p in the factor base such that n modulo p is a square; otherwise the quadratic equation r2 ≡ n mod p has no solution.

Example 3.15. Let n = 91\. We consider the factor base B = {−1, 2, 3, 5}. With m = 9 and c = 2, we obtain R = {7, 8, 9, 10, 11}. For r ∈ R , we compute f(r) = r2 − 91\. This yields the initial vector (f(7), . . . , f(11)) = (−42, −27, −10, 9, 30). The following table summarizes the sieving stage.

![](images/115_3.jpg)

The B-smooth numbers are −27 = (−1) ⋅ 33 and −10 = (−1) ⋅ 2 ⋅ 5 and 9 = 32 and 30 = 2 ⋅ 3 ⋅ 5\. Possible choices for T are T1 = {8, 9, 10, 11} and T2 = {8, 9, 11} and T3 = {10}. For T1, we obtain x1 = 8⋅9⋅10⋅11 = 7920 and y1 = 2⋅33 ⋅5 = 270; we can omit the sign of y1 since both +y1 and −y1 are considered. We have gcd(x1−y1, 91) = 1 and gcd(x1 + y1, 91) = 91\. Therefore, T1 does not yield a factorization of 91\. For T2, we obtain x2 = 8 ⋅ 9 ⋅ 11 = 792 and y2 = 2 ⋅ 32 ⋅ 5 = 90\. This yields the factorization 91 = 13 ⋅ 7 since gcd(x2 − y2, 91) = 13 and gcd(x2 + y2, 91) = 7\. Finally, for T3, we obtain x3 = 10 and y3 = 3\. This immediately yields the factors x3 − y3 = 7 and x3 + y3 = 13.

◊

## 3.7 Discrete logarithm

Currently, no efficient methods for integer factorization are known, and it is widely believed that no such methods exist. The security of many cryptosystems depends heavily on this assumption. However, you cannot completely rule out the possibility that one day factorizing can be done sufficiently fast. Therefore, we are interested in cryptosystems whose security is based on the hardness of other computational problems. One such problem is the discrete logarithm.

Let G be a group and g ∈ G an element of order q. Let U be the subgroup of G generated by g, so |U| = q. Then, x ↦ gx defines an isomorphism ℤ/qℤ → U which can be computed using fast exponentiation in many applications. The discrete logarithm problem is the task of determining the element x mod q from the knowledge of the elements g and gx in G. If G is the additive group (ℤ/nℤ, +, 0), this is easy using the extended Euclidean algorithm. But what should be done when the Euclidean algorithm is not available? It seems that, then, the inverse mapping of x ↦ gx cannot be computed efficiently. In applications, it is therefore sufficient to work with the multiplicative group of a finite field or a finite group of points on an elliptic curve. With elliptic curves, you can apparently reach the same level of security with fewer bits, but since we have not yet dealt with elliptic curves, wewill restrict ourselves to the case ∗p for a prime number p.

We fix the prime number p and the element ![](images/116_2.jpg) Let the order of g in ![](images/116_4.jpg) be q. Then, in particular, q is a divisor of p − 1\. Suppose we are given ![](images/116_3.jpg) The task is to determine x' ≤ p − 1 with ![](images/116_1.jpg) The naive method is to exhaustively try out all possible values for x. The expected search time is approximately q/2\. This is hopeless if q,written in binary, has a length of 80 bits or more. In typical applications, q and p have a bit size of about 160 to 1000 bits each. The computation of xy mod z is very efficient when using fast modular exponentiation, even for numbers x, y, z with more than 1000 bits. Therefore, the mapping ℤ/qℤ → U with x ↦ gx can, in fact, be computed efficiently. The currently known algorithms for the discrete logarithm problem on inputs of bit size log n achieve a runtime of ![](images/116_5.jpg) on elliptic curves. This is considered to be subexponential and is significantly better than ![](images/o.jpg)(n), but still too slow to treat 160-digit numbers reasonably. Note that a 160-digit number has an order of magnitude of 2160.

### 3.7.1 Shanks’ baby-step giant-step algorithm

Let G be a finite group of order n, let g ∈ G be an element of order q, and let y be a power of g. We search for a number x with gx = y, the discrete logarithm of y to base g. A classical algorithm to compute the discrete logarithm is the baby-step giant-step algorithm by Shanks. Here, a number m ∈ ℕ is chosen, which should be of approximate size ![](images/116_6.jpg) If q is unknown, you can instead choose m to have approximate size ![](images/116_7.jpg) and substitute q by n in the following. For all r ∈ {m−1, . . . ,0} in the baby steps, one computes the values g−r = gq−r ∈ G and stores the pairs (r, yg−r ) in a table B. In practical implementations, you should use hash tables for efficiency reasons.

Note that for exactly one r with 0 ≤ r < m there is a number s with x = sm + r. Substituting z = yg−r, the pair (r, z) is in the table and z = gsm. The giant steps are as follows. We compute h = gm, and then for all s with 0 ≤ s < ⌈q/m⌉, we check whether a table entry (r, hs) exists. If we find such numbers r and s, then x = sm + r is the desired value.

The running time is dominated by m, that is, approximately ![](images/117_1.jpg) or ![](images/117_2.jpg) respectively. This is not particularly pleasing, but no faster methods are known. A bigger problem with this method is the huge amount of memory needed to store the m pairs (r, z). Even if you can reduce the table size by hashing and other elaborate methods, an enormous amount of data still have to be maintained and stored. For realistic sizes like q ≥ 2100, the baby-step giant-step algorithm is not feasible.

### 3.7.2 Pollard’s rho algorithm for the discrete logarithm

As before, let G be a finite group of order n, let g ∈ G be an element of order q, and y a power of g. We search for a number x with gx = y. The runtime of Pollard’s ρ algorithm to compute x is similar to that of Shanks’ baby-step giant-step algorithm; however, it requires only a constant amount of storage space. The price for this advantage is that the ρ algorithm yields no worst-case time bound, but rather a bound that is based on the birthday paradox. It only provides an expected time complexity of ![](images/117_3.jpg)

First, we decompose G into three disjoint sets, P1, P2 and P3. In ![](images/117_4.jpg) for example, you could define the Pi by residues modulo 3\. In principle, the exact decomposition is irrelevant, but it should be easy to compute and ensure that the following scheme yields something like a random walk through the subgroup of G generated by g. We think of a pair (r, s) ∈ ℤ/qℤ×ℤ/qℤ as a representation of grys ∈ G. The above partition defines a mapping f : ℤ/qℤ×ℤ/qℤ→ℤ/qℤ×ℤ/qℤ as follows:

![](images/117_5.jpg)

Let f(r, s) = (r' , s) and h = grys and ![](images/117_10.jpg)then h' = gh for h ∈ P1, h' = h2 for h ∈ P2 and h' = hy for h ∈ P3. The ρ algorithm starts with a random pair (r1, s1) and iterates the computation by

![](images/117_8.jpg)

for i ≥ 1\. We define ![](images/117_7.jpg) and observe that hi+1 can uniquely be determined from hi. Therefore, the sequence (h1, h2, . . . ) in G encounters a cycle after a finite initial segment and, therefore, it looks like the Greek letter ρ, again explaining the name of the algorithm.

There exist t and r with ht = ht+r. Now hℓ = hℓ+r holds for all ℓ ≥ t. We use this fact to keep the required storage space bounded by a constant. We could proceed as we did in [Section 3.6.2](#chapter03_2.xhtml_chapter03_2_12) to find different indices i, j with hi = hj. However, we want to use an alternative approach, which could also be used in the ρ algorithm for factorization. We work in phases: at the beginning of each phase, a value hℓ is stored. In the first phase, we let ℓ = 1\. Then, for k ∈ {1, . . . , ℓ}, we successively compute the value hℓ+k and compare it with hℓ.We stop the procedure if ℓ is found such that hℓ = hℓ+k. Otherwise, we replace hℓ by h2ℓ and ℓ by 2ℓ and start a new phase. Note that, at the latest, we will stop if ℓ is greater than or equal to t + r because then, with k = r, we reach the situation hℓ = hℓ+k.

Thus, we stop with the pairs (r, s) = (rℓ , sℓ) and (r' , s) = (rℓ+k , sℓ+k), for which ![](images/118_10.jpg) This implies ![](images/118_1.jpg) and therefore r + xs ≡ r' + xs' mod q. Now, x(s−s) ≡ r−r mod q. The probability for s = s' is small and if q is prime, we can solve the congruence uniquely. This method, however, can also be applied to more general situations and we might possibly obtain different x to solve the last congruence. If possible, we check for all these solutions x whether gx = y holds. Otherwise, we restart the procedure, using another random pair (r1, s1).

The analysis of the running time depends on the expected minimal value t + r, yielding ht = ht+r. If the sequence (h1, h2, . . . ) behaves randomly, then we look for k such that the probability for the existence of ht = ht+r with 1 ≤ t < t + r ≤ k is greater than 1/2\. The birthday paradox leads to an expected running time of ![](images/118_2.jpg) for Pollard’s ρ algorithm.

### 3.7.3 Pohlig–Hellman algorithm for group order reduction

If the prime factorization of the order of a cyclic group G is known, then the discrete logarithm problem can be reduced to the prime divisors. The according method was published by Stephen Pohlig and Martin Hellman. Let |G| = n with

![](images/118_3.jpg)

where the product runs over all prime divisors p of n. Let y, g ∈ G be given such that y is a power of g. We look for a number x with y = gx. We define

![](images/118_11.jpg)

The elements Gp = {hnp | h ∈ G } form a subgroup of G. If h generates G, then hnp generates Gp. In particular, Gp contains exactly pe(p) elements. The following theorem shows that it is sufficient to solve the discrete logarithm problem in the groups Gp.

Theorem 3.16. For all primes p with p | n let xp ∈ ℕ be given such that ![](images/118_7.jpg) If x ≡ xp mod pe(p) for all primes p | n, then y = gx.

Proof: We have ![](images/118_8.jpg) Thus, the order of g−xy is a divisor of np for all p | n. The greatest common divisor of all np is 1, so the order of g−xy also must be 1\. This shows y = gx.

□

With the Chinese remainder theorem from [Theorem 3.16](#chapter03_2.xhtml_chapter03_2_24), we can compute a solution in G from the solutions in the groups Gp. We further simplify the problem for Gp by reducing the discrete logarithm to groups of order p. Without loss of generality let now |G| = pe for a prime number p. Since x < pe, there exists a unique representation

![](images/119_1.jpg)

with 0 ≤ xi < p. We successively compute x0, . . . , xe−1 as follows. Let x0, . . . , xi−1 be known already for i ≥ 0\. For ![](images/119_13.jpg) we have

![](images/119_2.jpg)

Raising both sides to the pe−i−1th power yields

![](images/119_14.jpg)(3.1)

since ![](images/119_5.jpg) for e' ≥ e. The element ![](images/119_6.jpg) generates a group of order at most p, and the number xi is obtained by solving the discrete logarithm problem of equation (3.1) within this group. This can, for example, be done using Shanks’ baby-step giant-step

algorithm or Pollard’s ρ algorithm with ![](images/119_7.jpg) group operations.

For arbitrary cyclic groups G with |G| = n, we thus have a method for computing the discrete logarithm which requires

![](images/119_8.jpg)

group operations. Here, the rough estimate e(p) ⋅ log n covers the computation of gp, yp, and zi.

### 3.7.4 Index calculus

Index calculus is an algorithm for computing discrete logarithms in (ℤ/qℤ)∗ for some prime q. Given g ∈ (ℤ/qℤ)∗ and a ∈ 〈g〉, we want to compute an integer x with a = gx. We choose some bound b and we let

![](images/119_9.jpg)

be a factor base. Remember that an integer is B-smooth if and only if it can be written as a product of numbers in B. The index calculus algorithm consists of two stages. First, for every p ∈ B we compute yp with

![](images/119_10.jpg)

Second, we try to find y such that agy mod q is B-smooth; this is done by randomly choosing y until this condition holds. Then, we can write agy mod q = Πp∈B pep and obtain

![](images/119_11.jpg) mod q

and thus x = −y + Σp∈B epyp mod q − 1 satisfies a ≡ gx mod q.

It remains to describe the computation of the yp. To this end, we randomly choose many different z such that gz mod q is B-smooth, that is, we can write gz mod q = Πp∈B pf(p,z). We stop if we have found a large set Z of such numbers z, at least |B| + 1. Then the yp’s are obtained as solutions of the system of linear equations

![](images/120_1.jpg)

The expected running time of the index calculus algorithm is similar to that of the quadratic sieve. The main ingredient in the algorithm is the notion of B-smoothness. It is not easy to (efficiently) generalize this notion to groups other than (ℤ/qℤ)∗. This is one of the main reasons for considering elliptic curves over finite fields ![](images/f_d.jpg)q with q odd; in this setting, it is widely believed that such a generalization does not exist. This is one of the main reasons for the popularity of cryptosystems based on elliptic curves: the same level of security can be achieved with smaller keys than for cryptosystems based on (ℤ/qℤ)∗.

## 3.8 Multiplication and division

The classical method of multiplying two binary numbers of length n requires Θ(n2) operations. Let the two numbers r and s of 2k bits each be of the following form:

![](images/120_6.jpg)

Here, A represents the k most significant bits of r and B the k least significant bits. Similar for C and D with respect to s. In other words, we can write r = A 2k + B and s = C 2k + D. From that we obtain

![](images/120_3.jpg) k

Instead of following this approach, Karatsuba’s algorithm (Anatoly Alexeyevich Karatsuba, 1937–2008) recursively computes the three products AC, (A + B)(C + D), and BD. Then, rs can be computed performing only three multiplications of numbers with bit length at most k

![](images/120_4.jpg)

Let tmult(n) be the time which this recursive method takes to multiply numbers of n bits. Since n-bit numbers can be added in time ![](images/o.jpg)(n), the master theorem yields the following estimate for tmult(n):

![](images/120_5.jpg)

Thus, by a divide-and-conquer approach, we have reduced the exponent of the classical method from 2 to approximately 1.58496.

Another important arithmetic operation is the computation of a mod m. Because of

![](images/121_1.jpg)

this operation can be reduced to subtraction, multiplication and integer division. For subtraction, the complexity of the classical method is linear in the number of digits. For multiplication, we have just seen an algorithm with subquadratic running time. So, now division remains to be investigated. To this end, we sketch in the following a method, which, using only subtractions and multiplications, is able to compute sufficiently many decimal places of the reciprocal of a given integer. Once we know enough bits of ![](images/121_2.jpg) after the decimal point, we can compute ![](images/121_3.jpg) by multiplying a and ![](images/121_4.jpg) . Those bit values of ![](images/121_5.jpg) contributing merely to the fractions part of this product need not be computed.

To approximate ![](images/121_6.jpg) , we can use the Newton method (Sir Isaac Newton, 1643–1727) to find the root of ![](images/121_7.jpg) For this purpose, we compute better and better approximations xi to this root by the rule

![](images/121_8.jpg)

In our particular case, this results in the rule

![](images/121_9.jpg)

If we begin with an initial value x0 between 0 and ![](images/121_11.jpg) , the sequence (xi)i∈ℕ very quickly converges to ![](images/121_10.jpg) . A good initial value is, for example, x0 = 2−⌊log2 m⌋−1. The value ⌊log2 m⌋ + 1 can be found easily by counting the number of binary digits of m. Without further computation, the initial value x0 can be specified in binary by a sequence of zeros after the decimal point, followed by a 1. The problem that we have to work with noninteger numbers can be eliminated by previously multiplying by a sufficiently large power of 2; this can be achieved by a simple shift operation.

## 3.9 Discrete fourier transform

The goal of the discrete Fourier transform (named after Jean Baptiste Joseph Fourier, 1768–1830) is to multiply polynomials very efficiently. Let R be a commutative ring and b ≥ 1 a natural number with an inverse in R. That is, the multiplicative inverse b−1 ∈ R exists. This is always the case if R is a field of characteristic zero, like ℂ. It also holds in fields of characteristic p such that gcd(b, p) = 1\. And it is also true if b = 2r is a power of two and R = ℤ/nℤ for odd n. Note that ℤ/nℤ may have various zero divisors.

The b-fold direct product Rb of R consists of all vectors (u0, . . . , ub−1) with ui ∈ R. For Rb, we can consider two different multiplications to be defined in a natural way. First, we can perform a componentwise multiplication:

![](images/122_1.jpg)

Or we interpret a vector (u0, . . . , ub−1) as a polynomial Σi uiXi and multiply polynomials in the quotient ring R [X]/(Xb −1). To distinguish these two kinds of multiplication, we denote the product of the polynomials f and g as f ∗ g (it is called the convolution product). By convention ui = 0 for all i < 0 and all i ≥ b. This eases notation because we need no explicit summation limits. In this quotient ring, the identity X b = 1 holds, and we obtain

![](images/122_2.jpg)

Let now ω ∈ R be a bth root of unity, that is, an element satisfying ωb = 1\. Then, we can evaluate f(X) ∈ R[X]/(Xb − 1) at powers ωi and

![](images/122_11.jpg)

defines a ring homomorphism from R[X]/(Xb − 1) into Rb. A primitive bth root of unity is an element ω ∈ R \ {1} satisfying the following conditions:

(a)ωb = 1,

(b)![](images/122_4.jpg) for all 1 ≤ k < b.

If ω is a primitive bth root of unity, then ω−1 is as well, since the equation in condition (b) can be multiplied by ω−k(b−1). If c ≥ 1 divides b, then ωc is a primitive (b/c)th root of unity in R because we have

![](images/122_5.jpg)

with k' = kc < b. Note that, in the third term of the equation above, each power ![](images/122_10.jpg) is counted exactly c times. From [Corollary 1.57](#chapter01_3.xhtml_chapter01_3_23), the complex number ![](images/122_6.jpg) is a primitive bth root of unity in ℂ. The discrete Fourier transform is possible in each ring R in which b has a multiplicative inverse b−1 and where a primitive bth root of unity ω exists. For such rings R, the polynomial ring R[X]/(Xb − 1) with the identity Xb = 1 and the direct product Rb are isomorphic. The isomorphism can be explained by matrix multiplications. The {0, . . . , b − 1}×{0, . . . , b − 1} matrices F = (ωij)i,j and ![](images/122_7.jpg) satisfy

![](images/122_8.jpg)

Here, (aij)i,j denotes the matrix with entry aij at the (i, j)-position. For i ≠ j we have ![](images/123_1.jpg) and for i = j this sum equals b. Thus, F ⋅ F̄ is a diagonal matrix with value b on the diagonal. In particular, the matrices F and F̄ are invertible and F ⋅F̄ ⋅b−1 is the unit matrix. Now, ![](images/123_9.jpg) and we obtain the following ring isomorphism F : R[X]/(Xb − 1) → Rb, mapping each element f(X) = Σi aiXi to

![](images/123_10.jpg)

In particular, multiplicationwith the matrix F can be interpreted as evaluating a polynomial f at points 1, ω, ω2, . . . , ωb−1. The mapping F : R[X]/(Xb − 1) → Rb is called discrete Fourier transform. For the inverse mapping, the matrix F is replaced by ![](images/123_3.jpg) and in the end the result is multiplied by the scalar b−1.

![](images/123_4.jpg)

Fig. 3.1. Computing f ∗ g using the discrete Fourier transform.

To compute the coefficients zi in f(X) ∗ g(X) = Σi ziXi according to [Figure 3.1](#chapter03_3.xhtml_chapter03_3_6), we use the following strategy:

(1)Compute F(f(X)) and F(g(X)), that is, f(ωi) and g(ωi ) for 0 ≤ i < b.

(2)Evaluate the products hi = f(ωi)⋅ g(ωi) in R for 0 ≤ i < b.

(3)Compute ![](images/123_5.jpg)

Since F is a ring isomorphism, we have

![](images/123_6.jpg)

Next, let us consider the special case that b is a power of 2, that is, b = 2r for r ≥ 1\. Then, the computation of F (f(X)) can efficiently be performed using a divide-and-conquer strategy. This leads to the fast Fourier transform (abbreviated FFT) as follows. We write polynomials f(X) of degree less than b in the form

![](images/123_12.jpg)

The polynomials fj have degree less than b/2 and ω2 is a primitive (b/2)th root of unity. If f = (a0, . . . , ab−1), then f0 = (a0, a2, . . . , ab−2) and f1 = (a1, a3, . . . , ab−1).

This yields

![](images/124_9.jpg)

Let F' : R[X]/(Xb/2 − 1) → Rb/2 be the Fourier transform of dimension b/2 with the root of unity ω2. If we have computed F'(f0) = (u0, . . . , ub/2−1) and F'(f1) = (υ0, . . . , υb/2−1), then we can determine F (f) as follows. With vectors

![](images/124_8.jpg)

of length b, we determine by componentwise computation

![](images/124_10.jpg)

The transformed F(f0) and F(f1) can be recursively computed with the same procedure. The additions in R and multiplications with ωi and b−1 are called elementary arithmetic operations. Let t(b) be the number of elementary arithmetic operations necessary in this scheme for computing F (f). Then, t(b) satisfies the recurrence t(b) ≤ 2 t(b/2) + ![](images/o.jpg)(b) since to determine the Fourier transform two recursive calls for f0 and f1 of half the size are needed. The results of these two recursive calls will be combined to obtain the transform f using a linear number of operations. The master theorem, [Theorem 3.2](#chapter03_1.xhtml_chapter03_1_5), then yields t(b) ∈ ![](images/o.jpg)(b log b).

If we want to compute the product f(X) ∗ g(X) of two polynomials of degree less than d in R[X], then we can choose b as the smallest power of 2 with b ≥ 2d. If a primitive bth root of unity ω is known, then using the FFT according to the scheme in [Figure 3.1](#chapter03_3.xhtml_chapter03_3_6), the product of f(X) and g(X) can be computed with only ![](images/o.jpg)(d log d) elementary arithmetic operations. The naive approach, in contrast, requires ![](images/o.jpg)(d2) elementary arithmetic operations.

## 3.10 Primitive roots of unity

Let b ∈ ℕ and ' be a field of characteristic zero or characteristic p with gcd(b, p) = 1. Then, b is invertible in ![](images/f_d.jpg). Moreover, the formal derivative of the polynomial Xb − 1 is bXb−1. Therefore, the polynomial Xb−1 has no multiple roots. In a field extension of , the polynomial Xb − 1 splits into linear factors and the bth roots in the field extension are pairwise distinct. The group of bth roots of unity thus has b elements. It is cyclic and generated by an element ω. Then, ωb = 1 and ωk ≠ 1 for all 1 ≤ k < b. This implies ![](images/124_4.jpg) for all 1 ≤ k < b. Since fields have no zero divisors, ![](images/124_5.jpg) follows; and the generator ω is a primitive bth root of unity. If ![](images/f_d.jpg) = ℂ, for example, we may choose ![](images/124_6.jpg)

In general, however, a ring has zero divisors, and therefore the properties ωb = 1 and ωk ≠ 1 for all 1 ≤ k < b are not sufficient to ensure ![](images/124_7.jpg) The remaining part of this section is dedicated to the following theorem which is crucial for Schönhage and Strassen’s algorithm for the fast multiplication of large numbers.

Theorem 3.17. Let b = 2r and let m be a multiple of b, and let n = 2m + 1. We define ψ = 2m/b and ω = ψ2. Then the following properties hold in ℤ/nℤ:

(a)b−1 = −2m−r

(b)ψb = −1

(c)ω is a primitive bth root of unity.

Proof: In ℤ/nℤ we have 2m = −1\. The claims b−1 = −2m−r and ψb = −1, as well as ωb = 1, are therefore trivial. We have to show ![](images/125_1.jpg) for all 1 ≤ k < b. Since b = 2r is a power of 2, an induction on r yields

![](images/125_2.jpg)

Now let k = 2ℓu with an odd number u. Using 0 ≤ ℓ < r, we have a factor of the form ![](images/125_8.jpg) in the above product. Now, ![](images/125_10.jpg) Since u is odd, we obtain ![](images/125_4.jpg)

□

## 3.11 Schönhage–Strassen integer multiplication

Multiplying two n-bit numbers requires n2-bit operations when using the classical method. In 1960, Karatsuba noticed that it can be done much faster with a surprisingly simple divide-and-conquer approach; he showed that asymptotically less than n1.6 operations are sufficient; see [Section 3.8](#chapter03_3.xhtml_chapter03_3_1). A major breakthrough came when Arnold Schönhage (born 1934) and Volker Strassen were able to present a method with a nearly linear number of arithmetic operations in 1971 [[91](#Bibliography.xhtml_Bibliography_92)]. More specifically, they showed that the multiplication of two n-bit numbers can be done in time ![](images/o.jpg)(n log n log log n) on a multitape Turing machine. It took 35 more years, until Martin Fürer (born 1947) could further improve this time bound to ![](images/o.jpg)(n log n 2log∗ n); see [[43](#Bibliography.xhtml_Bibliography_43)]. Here, log∗ n denotes the number of applications of the logarithm needed to have a result less than 1\. The function 2log∗ n asymptotically grows much slower than log log n; however, on all realistic inputs, log log n is smaller.

![](images/125_3.jpg)

In the remainder of this section, we prove the result of Schönhage–Strassen.

Theorem 3.18. The multiplication of two natural numbers of bit size n can be done with ![](images/o.jpg)(n log n log log n) bit operations.

The input consists of two natural numbers u and υ. We may assume that the binary representation of the product uυ requires at most n bits and that n = 2s is a power of 2. It is sufficient to compute uυ modulo 2n + 1\. In the according quotient ring, 2n = −1 holds. We define b = 2⌈s/2⌉ and ℓ = 2⌊s/2⌋. As a rule of thumb, we note

–2n + 1 is large and odd.

–n = 2s is the input size and a power of 2.

–s ∈ ℕ is a small number.

–![](images/126_1.jpg)

We decompose the input into b blocks of length ℓ and write u = Σi ui2ℓi and υ = Σi υi2ℓi, where 0 ≤ ui , υi < 2ℓ for all i. By convention, ui = υi = 0 holds for all i < 0 and for all i ≥ b. Let yi = Σj ujυi−j; then yi ≠ 0 can only hold for 0 ≤ i < 2b − 1\. For 0 ≤ i < b at most i + 1 summands ujυi−j in yi are nonzero, which yields yi < (i + 1)22ℓ; and in yb+i at most b − i −1 summands do not vanish, resulting in yb+i < (b − i −1)22ℓ. With 2bℓ = −1, we obtain

![](images/126_2.jpg)

in ℤ/(2n + 1)ℤ. Since −(b − i − 1)22ℓ < wi < (i + 1)22ℓ, it is sufficient to determine the values wi modulo b(22ℓ + 1). Since b is a power of 2 and 22ℓ + 1 is odd, according to the Chinese remainder theorem we can first compute the wi modulo b, then modulo 22ℓ + 1, and finally combine these two intermediate steps for the result modulo b(22ℓ + 1). Letting ![](images/126_3.jpg) mod b and ![](images/126_4.jpg) mod 22ℓ + 1, we obtain wi from ![](images/126_5.jpg) and ![](images/126_6.jpg) by the computation

![](images/126_7.jpg)

since 22ℓ ≡ 0 mod b. The resulting values wi with −(b − i − 1)22ℓ < wi < (i + 1)22ℓ each have ![](images/126_8.jpg) bits. From w0, . . . , wb−1 we compute

![](images/126_9.jpg)

This requires ![](images/126_10.jpg) additions or subtractions, respectively, each on operands of length ![](images/126_11.jpg) These can be performed by the classical methods in linear time. It remains to show how to find the values ![](images/126_12.jpg) and ![](images/126_13.jpg)

We first describe how the values wiare computed. First, we let ![](images/126_14.jpg) mod b and ![](images/126_15.jpg) mod b for 0 ≤ i < b. This is easy because b is a power of 2 and ui and υi are given in binary. Since ![](images/126_16.jpg) we have ![](images/126_17.jpg) mod b. Therefore, it is sufficient to determine the ![](images/126_18.jpg) for 0 ≤ i < 2b. We know that ![](images/126_20.jpg) and therefore 1 + 3 log b < 4 log b bits for each ![](images/126_19.jpg) are sufficient. Let ![](images/126_22.jpg) and ![](images/126_21.jpg) This means that u' can be obtained from the ![](images/126_24.jpg) by inserting sufficiently long blocks of zeros between them; υ' can be constructed in the same way. Then, we have

![](images/127_1.jpg)

The binary lengths of u' and υ' are bounded by 4b log b, so with the method of Karatsuba, we can compute the product u' ⋅ υ' in time ![](images/o.jpg)((b log b)1.6)⊆ ![](images/o.jpg)(b2) = ![](images/o.jpg)(n). From the result, one can directly extract the values yi since the corresponding blocks do not overlap.

Next, wewant to determine the![](images/127_2.jpg) We let N = 22ℓ+1 andR = ℤ/Nℤ. In particular, 22ℓ = −1 in R. Note that N is approximately ![](images/127_3.jpg) The number N is large, but it is much smaller than 2n. The subsequent calculations are performed in the polynomial ring R[X]/(Xb − 1). The elements ψ = 22ℓ/b and ω = ψ2 have the properties given by [Theorem 3.17](#chapter03_3.xhtml_chapter03_3_10). Thus, this polynomial ring is isomorphic to the direct product Rb, and multiplication of polynomials can be reduced to multiplications in R as shown in [Section 3.9](#chapter03_3.xhtml_chapter03_3_3). We consider the following two polynomials:

![](images/127_11.jpg)

Since ψb = −1 and Xb = 1, we have the following:

![](images/127_6.jpg)

By the factor ψi in the definition of f and g it is ensured that yb+i has the desired negative sign. Let h(X) = f(X)∗g(X) ∈ R[X]/(Xb −1) and write ![](images/127_7.jpg) Then, we obtain the ![](images/127_8.jpg) as follows:

![](images/127_9.jpg)

We compute the zi using the fast discrete Fourier transform, in which we recursively use the same algorithm for multiplication in R. It remains to show how to compute the number ziψ−i mod 22ℓ + 1 efficiently. The time bound ![](images/o.jpg)(ℓ) is sufficient. Elements of R are represented by numbers z in {0, . . . ,22ℓ}. Numbers z ∈ R can efficiently be multiplied with −1 by computing 22ℓ + 1 − z with the classical method. Because of ψ−i = −ψb−i in R, it suffices to compute elements zψj mod N for 0 < j < b. Now, ψj ≡ 2k mod N for k = 2ℓj/b ∈ {1, . . . ,2ℓ − 1}. The value z2k can be computed by left-shifting z by k bits. We can split the result of the shift operation into two 2ℓ-bit blocks z' , z' ∈ {0, . . . ,22ℓ − 1} such that z2k = z' + z22ℓ. Subtracting z' from z' modulo N now yields the desired result since z' − z' ≡ z' + z22ℓ = z2k ≡ ψj mod N.

Overview of the algorithm

In the following, we give a sketch of how the algorithm works. Here, x ∈ R means that the element x from the ring R is given or was computed. Arrows stand for a causal connection. In order to give a better insight into the proportions, b and ℓ are replaced by ![](images/128_1.jpg)

![](images/128_2.jpg)

The individual steps of the algorithm can be summarized as follows:

(1)The numbers u and υ each are decomposed in ![](images/128_3.jpg) blocks of ![](images/128_4.jpg) bits. Each block is computed modulo ![](images/128_5.jpg) then u' and υ' are compiled from the blocks with sufficiently many zeros inserted.

(2)The numbers u' and υ' are multiplied using the Karatsuba multiplication algorithm.

(3)Due to the shielding by sufficiently many zeros, the blocks ![](images/128_6.jpg) can be reconstructed from the product uυ.

(4)The ![](images/128_8.jpg) blocks are viewed as numbers modulo ![](images/128_7.jpg) and interpreted as coefficients of polynomials f and g.

(5)The Fourier transforms F (f) and F (g) of f and g are computed.

(6)In the computation of F(f) ⋅ F(g) for each of the![](images/128_9.jpg) multiplications in the ring ![](images/128_10.jpg) the algorithm is called recursively.

(7)Using the inverse Fourier transform the product of the polynomials f and g is determined.

(8)The values ![](images/128_11.jpg) appear as coefficients of the polynomial f(X) ∗ g(X).

(9)With the Chinese remainder theorem the numbers ![](images/128_15.jpg) mod ![](images/128_16.jpg) and ![](images/128_13.jpg) mod ![](images/128_14.jpg) can be combined to wi mod ![](images/128_12.jpg)

(10)The product uυ is computed from the numbers wi.

Runtime analysis

Computing F(f(X)), F(g(X)), and ![](images/129_1.jpg) takes ![](images/o.jpg)(b log b) elementary arithmetic operations, each of which can be performed with ![](images/o.jpg)(ℓ)-bit operations. This results in ![](images/o.jpg)(ℓ ⋅ b log b) = ![](images/o.jpg)(n log n) operations. Furthermore, b products hi = f(ωi)⋅ g(ωi ) modulo 22ℓ + 1 have to be computed recursively. Let M (n) be the number of bit operations needed to multiply two n-bit numbers using the Schönhage–Strassen algorithm. Then, we obtain the following recurrence:

![](images/129_7.jpg)

Thus, M(n)/n ≤ 2M(2ℓ)/2ℓ + O(log n). For n = 2s and t(s) = M(2s)/2s, we obtain

![](images/129_8.jpg)

This yields t(s) ∈ ![](images/o.jpg)(s log s) by the master theorem (see [Theorem 3.2](#chapter03_1.xhtml_chapter03_1_5) and [Example 3.3](#chapter03_1.xhtml_chapter03_1_6)).

Thus, we finally have M(n) ∈ ![](images/o.jpg)(n log n log log n).

## Exercises

3.1. (Master theorem II) Let ![](images/129_4.jpg) and ![](images/129_5.jpg) Show that f(n) ∈ ![](images/o.jpg)(n).

3.2. Show that on input two binary numbers a, b ∈ ℕ, one can decide in polynomial time whether there exists c ∈ ℚ with c2 = a/b.

3.3. Give an extension of the binary gcd algorithm such that, on input k,ℓ ∈ ℕ, it computes a, b, t with ak + bℓ = t = gcd(k, ℓ). The algorithm should not use division and multiplications by numbers other than 2.

3.4. Show that 1729 is an Eulerian pseudoprime to base 2, but not a strong pseudoprime to base 2\. In addition, use the Miller–Rabin scheme to find a nontrivial divisor of 1729.

3.5. (Lucas test; named after Édouard Lucas, 1842–1891) Let n ≥ 1 and a ∈ ℤ. Show that n is prime if the following two conditions are satisfied:

(i)an−1 ≡ 1 mod n and

(ii) a(n−1)/q ≢ 1 mod n for all prime divisors q of n − 1.

3.6. (Pépin test; named after Théophile Pépin, 1826–1904) Let n ≥ 1\. Show that the Fermat number ![](images/129_6.jpg) is prime if and only if 3(fn−1)/2 ≡ −1 mod fn.

3.7. Let p > 2 be a prime number and consider the Mersenne number n = 2p − 1 (named after Marin Mersenne, 1588–1648).

(a)Show that if n is prime, then f(X) = X2 − 4X + 1 ∈ n[X] is irreducible.

(b)Suppose that n is prime and let K = ![](images/f_d.jpg)n[X]/f . Show that Xn = 4 − X and (X − 1)n+1 = −2 in K.

(c)Suppose that n is prime and let K = ![](images/f_d.jpg)n[X]/f . Show that (X − 1)n+1 = 2X(n+1)/2 in K.

(d)Show that n is prime if and only if X(n+1)/2 ≡ −1 mod X2 − 4X + 1 in (ℤ/nℤ)[X].

3.8. (Lucas–Lehmer test; named after É. Lucas and Derrick Lehmer, 1905–1991) Let p > 2 be a prime number and n = 2p − 1 the corresponding Mersenne number. The sequence (ℓj)j∈ℕ is defined by ℓ0 = 4 and ![](images/130_1.jpg) mod n. Show that n is prime if and only if ℓp−2 = 0.

Hint: Show that ![](images/130_4.jpg)mod X2 − 4X + 1 in (ℤ/nℤ)[X].

3.9. A linear Diophantine equation has the form a1X1 +⋅ ⋅ ⋅+anXn = an+1 with ai ∈ ℤ. Explain how to check whether a solution (x1, . . . , xn)∈ ℤn exists and how to compute it.

3.10. Compute the square root of 2 in the field ![](images/f_d.jpg)41 = ℤ/41ℤ. Use Tonelli’s algorithm and choose g = 3 in the first step.

3.11. Let p be prime with p ≡ 5 mod 8\. We consider the field ![](images/f_d.jpg)p and a square a ∈ ![](images/f_d.jpg)p. Show that if a(p−1)/4 = 1, then a(p+3)/8 is a square root of a; and if a(p−1)/4 = −1, then 2−1(4a)(p+3)/8 is a square root of a.

3.12. Let p be a prime number with p ≡ −1 mod 4 and let f(X) = X2 + 1.

(a)Show that the polynomial f(X) is irreducible in ![](images/f_d.jpg)p[X].

(b)Show how to efficiently find an element a with 1 ≤ a < p − 1 such that ![](images/130_3.jpg) and ![](images/130_2.jpg)

(c)Show that in p2 = p[X]/f it is possible to extract roots in deterministic polynomial time.

3.13. Compute the square root of 2 in the field ![](images/f_d.jpg)23 = ℤ/23ℤ. Use Cipolla’s algorithm and choose t = 0 in the first step.

3.14. Use Pollard’s p − 1 algorithm to find a nontrivial divisor of n = 253\. In the first step, let B = {2, 3} and a = 2, in the second step B = {2, 3, 5} and a = 2.

3.15. Find a nontrivial divisor of n = 689 with Pollard’s ρ algorithm. Use F (x) = x2 + 1 mod n and the initial value x0 = 12.

3.16. Compute the discrete logarithm of 3 to base 2 in the multiplicative group (ℤ/19ℤ)∗ using Shanks’ baby-step giant-step algorithm.

3.17. Let G be a finite group and g ∈ G. Show how to determine the order of g using Shanks’ baby-step giant-step algorithm.

3.18. Let G = (ℤ/23ℤ)∗ and g = 3.

(a)Determine the order of g in G.

(b)Use Pollard’s ρ algorithm to compute the discrete logarithm of 18 to base 3 in G. Decompose G with respect to the residue classes modulo 3 and use r1 = s1 = 1 as initial values.

3.19. Compute the discrete logarithm of 5 to base 2 in the multiplicative group (ℤ/19ℤ)∗. Reduce the problem with the Pohlig–Hellman method to discrete logarithms in groups of smaller order.

3.20. Let ![](images/131_4.jpg) be a Fermat prime. Show that discrete logarithms in (ℤ/pℤ)∗ can be computed in deterministic polynomial time.

3.21. Let q = 97, b = 4 and ω = −22.

(a)Show that ω is a primitive bth root of unity in ![](images/f_d.jpg)q.

(b)Specify the Fourier matrices F, ![](images/131_1.jpg) with respect to ω.

(c)Compute the product f ∗ g of the polynomials f(X) = 1 + X + X2 and g(X) = 2 + 3X using the FFT.

3.22. Let p1, p2, p3 ∈ 256ℤ + 1 be distinct primes of at most 64 bits, let ωi be a primitive 256th root of unity in the field Ki = ℤ/piℤ, and let Fi be the Fourier transform in Ki with respect to ωi. On input two numbers u = Σj≥0 uj264j and υ = Σj≥0 υj264j with 0 ≤ uj , υj < 264 we determine Ui(X) = Σj≥0(uj mod pi)Xj and Vi(X) = Σj≥0(υj mod pi)Xj. Then, in Ki we compute the coefficients of

![](images/131_2.jpg)

using the FFT. Finally, we determine the polynomial W(X) = Σj≥0wjXj with wj ≡ wi,j mod pi by means of the Chinese remainder theorem. At last, we return the number w = W(264). What is the running time of this algorithm? What are the maximum values for u and υ to ensure that w = uυ holds?

## Summary

Notions

–addition chain

–Carmichael number

–square-free

–pseudoprime

–Eulerian pseudoprime

–strong pseudoprime

–square, quadratic residue

–square root

–root extraction in groups

–factorization

–pseudo-random sequence

–B-smooth

–discrete logarithm

–primitive root of unity

–elementary arithmetic operation

Methods and results

–master theorem for estimation of recurrence equations

–birthday paradox: For random sequences of m events from Ω with ![](images/132_1.jpg)the probability to have two identical elements in the sequence is greater than 1/2.

–fast exponentiation for computing an with O(log n) multiplications

–binary gcd

–Fermat test

–properties of Carmichael numbers

–The error probability of the Solovay–Strassen primality test is at most 1/2.

–description of the Miller–Rabin primality test

–The error probability of the Miller–Rabin primality test is at most 1/4.

–Miller–Rabin scheme yields an algorithm for factorization of n if a multiple of φ(n) is known or if φ(n) has only small prime divisors

–Miller–Rabin scheme as evidence for the secret RSA key to be secure

–n Eulerian pseudoprime to base a ⇒ n pseudoprime to base a

–n strong pseudoprime to base a⇒ n Eulerian pseudoprime to base a

–root extraction in groups of odd order

–root extraction in ![](images/f_d.jpg)q with q ≡ −1 mod 4

–Tonelli’s algorithm for extracting roots in ![](images/f_d.jpg)q with odd number q

–Cipolla’s algorithm for extracting roots in ![](images/f_d.jpg)q with odd q

–Pollard’s p − 1 algorithm

–Pollard’s ρ algorithm for integer factorization

–quadratic sieve

–Shanks’ baby-step giant-step algorithm for discrete logarithm

–Pollard’s ρ algorithm for discrete logarithm

–Pohlig–Hellman algorithm for discrete logarithm: step 1 reduction to prime powers, step 2 reduction to prime divisors

–index calculus algorithm

–Karatsuba integer multiplication in ![](images/o.jpg)(n1,58496⋅⋅⋅ )

–division using Newton method

–discrete Fourier transform: ring isomorphism R[X]/(Xb − 1) → Rb

–fast Fourier transform: computing the discrete Fourier transform with ![](images/o.jpg)(b log b) elementary arithmetic operations

–primitive roots of unity in ℤ/(2m + 1)ℤ

–Schönhage–Strassen integer multiplication in ![](images/o.jpg)(n log n log log n)

# 4 Polynomial time primality test

In August 2002, a message rapidly spread out, reaching all mathematically interested people throughout the world within hours: “PRIMES is in P.” The scientists Manindra Agrawal, Neeraj Kayal, and Nitin Saxena from India had found a polynomial-time primality test. Composed of the initials of their last names, this method is called the AKS test. It is neither based on unproven hypotheses like, for example, the generalized Riemann hypothesis (Georg Friedrich Bernhard Riemann, 1826–1866), nor does it provide any probabilistic claims like the Miller–Rabin test from [Section 3.4.3](#chapter03_1.xhtml_chapter03_1_20). The problem called PRIMES, that is, “check whether an integer, given in binary, is prime,” is thus in the complexity class P of problems decidable in deterministic polynomial time.

The simplicity of the method is sensational. We are able to treat all aspects of the proof in full detail here. No specialized number theoretical insight that would go beyond the scope of this book is required. The work of Agrawal, Kayal, and Saxena was awarded the Gödel-Prize (Kurt Gödel, 1906–1978)[5](#Notes.xhtml_Notes_5)in 2006.

By now, a number of textbooks have presented the AKS test; see, for example [[19](#Bibliography.xhtml_Bibliography_20), [32](#Bibliography.xhtml_Bibliography_32), [41](#Bibliography.xhtml_Bibliography_41)]. Our presentation becomes a little easier due to the use of field extensions instead of cyclotomic polynomials. The necessary prerequisites for understanding the AKS test are modest: only parts of [Sections 1.1](#chapter01_1.xhtml_chapter01_1_6), [1.4](#chapter01_2.xhtml_chapter01_2_2), [1.5](#chapter01_2.xhtml_chapter01_2_12), [1.6](#chapter01_2.xhtml_chapter01_2_27), and [1.8](#chapter01_3.xhtml_chapter01_3_20) are required.

## 4.1 Basic idea

The following lemma is the main idea behind the AKS primality test. The proof is similar to Fermat’s little theorem.

Lemma 4.1. Let a, n ∈ ℕ with gcd(a, n) = 1. The number n is prime if and only if the following polynomial congruence holds in ℤ[X]:

![](images/133_1.jpg) (X + a)n ≡ Xn + a mod n

Proof: First, suppose that n is prime. We have (X + a)n ≡ Xn + an ≡ Xn + a mod n. The first congruence follows from [Theorem 1.28](#chapter01_2.xhtml_chapter01_2_9) and the second from Fermat’s little [Theorem 1.29](#chapter01_2.xhtml_chapter01_2_11).

For the converse, consider a prime number p which is a proper divisor of n and let pk be the largest power of p dividing n. Then, pk is also the largest power of p dividing n(n − 1) ⋅⋅ ⋅ (n − p + 1). It follows that pk−1 is the largest power of p dividing ![](images/133_2.jpg) Thus, the term ![](images/133_3.jpg) does not vanish modulo n.

□

The implication from right to left is not required in the following; as a primality test, it cannot be used in this form, anyway, because if we multiply out (X + a)n, in principle all the n + 1 coefficients have to be computed, and the number of coefficients is exponential in the input size ⌊log2 n⌋ + 1.

The congruence (X + a)n ≡ Xn + a mod n is weakened to (X + a)n ≡ Xn + a mod (Xr−1, n) for a small number r ∈ ℕ. This simplified congruence has to be checked for all a with a ≤ ℓ for some sufficiently large ℓ. The idea is to show that r and ℓ can be chosen to be small, that is, polylogarithmic in n. We first note that the congruence (X + a)n ≡ Xn + a mod (Xr − 1, n) can also be seen as an equality (X + a)n = Xn + a in the quotient ring ℤ[X]/(Xr − 1, n), where (Xr − 1, n) is the ideal generated by the polynomials X r − 1 and n. Put another way: a congruence

![](images/134_7.jpg)

means that there are polynomials g(X), h(X) ∈ℤ[X] satisfying

![](images/134_8.jpg)

From this description, it is obvious that congruence modulo n implies congruence modulo (Xr − 1, n). The computation of (X + a)n mod (Xr − 1, n) can be done by fast exponentiation and we may replace each power Xr by 1 and compute coefficients modulo n. The polynomials then have at most r coefficients, each of which is smaller than n. Thus, if r is polylogarithmic in n, then (X + a)n ≡ Xn + a mod (Xr − 1, n) can be checked in polynomial time.

## 4.2 Combinatorial tools

In the next three sections, we provide some tools for the correctness proof of the AKS test. We start with two elementary combinatorial theorems. For a set A let ![](images/134_3.jpg) be the set of all k-element subsets of A.

Theorem 4.2. For every finite set A, we have ![](images/134_4.jpg)

Proof: Let |A| = n. The theorem is correct for k ≤ 0 or k ≥ n. For 0 < k < n there are n(n − 1) ⋅⋅ ⋅ (n − k + 1) sequences (a1, . . . , ak) of pairwise different elements ai ∈ A. Two such sequences represent the same subset of A if the sequences coincide up to a permutation of the indices. There are k! such permutations.

□

The following theorem often appears in connection with drawing balls from an urn as “unordered selection with repetition.” Note that 0 ∈ ℕ is a natural number.

Theorem 4.3. For all r, s ∈ ℕ, we have ![](images/134_5.jpg)

Proof: We imagine r + s points arranged in a horizontal row. From these, we choose s points and replace them by bars. By [Theorem 4.2](#chapter04.xhtml_chapter04_10), there are ![](images/134_6.jpg) possibilities for choosing the positions of the bars. Each such selection corresponds to one s-tuple (e1, . . . , es) ∈ℕs with ![](images/135_1.jpg)

![](images/135_2.jpg)

First, e1 points are chopped off by the first bar. After the first bar, e 2 points are chopped off by the second bar, and so on. The sth bar is followed by some remaining points in order to obtain a total of r points. This gives a bijection between the solutions of the inequality and the possible choices of points and bars.

□

For r = t − 1 and s = ℓ + 1, we have ![](images/135_3.jpg) Therefore, the previous theorem yields

![](images/135_4.jpg)

## 4.3 Growth of the least common multiple

We denote the least common multiple of the numbers 1, . . . , n by lcm(n). In the following, we derive a lower bound for the growth of lcm(n). The proof we present is based on an article by Nair [[79](#Bibliography.xhtml_Bibliography_79)].

Lemma 4.4. For all m, n ∈ ℕ with 1 ≤ m ≤ n, we have ![](images/135_5.jpg)

Proof: We investigate the integral ![](images/135_6.jpg) The evaluation is done in two different ways. First, we apply the binomial theorem to rewrite (1 − x)n−m as ![](images/135_7.jpg) Then, we obtain

![](images/135_8.jpg)

Thus, the evaluation of the integral yields

![](images/135_9.jpg)

If we multiply I with lcm(n), then I ⋅ lcm(n) becomes an alternating sum of integers since ![](images/135_10.jpg) The value of I being positive, we see that I ⋅ lcm(n) is in ℕ. By induction on n − m, we now show that ![](images/135_11.jpg) For m = n, we have

![](images/135_12.jpg)

Let now 1 ≤ m < n. We use partial integration ∫ uυ dx = uυ − ∫uυ' dx with ![](images/136_1.jpg) and u' = xm−1 and with υ = (1 − x)n−m and υ' = −(n − m)(1 − x)n−m−1. Note that u(1) ⋅ υ(1) = u(0) ⋅ υ(0) = 0\. Thus, we obtain

![](images/136_2.jpg)

This shows ![](images/136_3.jpg) and finally ![](images/136_4.jpg)

□

Since ![](images/136_5.jpg) is the largest binomial coefficient in the binomial expansion of 4n = ![](images/136_6.jpg) we see that ![](images/136_7.jpg) is greater than the average value 4n/(2n + 1). For n ≥ 3, in particular

![](images/136_8.jpg)

By [Lemma 4.4](#chapter04.xhtml_chapter04_15), this yields lcm![](images/136_9.jpg) We improve this estimate a little in the following theorem.

Theorem 4.5. For all n ≥ 7, we have lcm(n) > 2n.

Proof: [Lemma 4.4](#chapter04.xhtml_chapter04_15) yields two divisors of lcm(2n + 1)

![](images/136_10.jpg)

Since n and 2n + 1 are coprime, ![](images/136_11.jpg) is a divisor of lcm(2n + 1). With Equation ([4.2](#chapter04.xhtml_chapter04_17)), we obtain ![](images/136_12.jpg) Let n ≥ 4\. Then

![](images/136_13.jpg)

Therefore, 2n < lcm(n) for all n ≥ 9\. The only remaining cases to investigate are n = 7 and n = 8\. We directly compute 27 = 128 < 420 = lcm(7) and 28 = 256 < 840 = lcm(8).

□

## 4.4 Of small numbers and large orders

Let gcd(n, r) = 1\. Then ordr(n) denotes the order of n in the multiplicative group (ℤ/rℤ)∗, that is

![](images/137_5.jpg)

The following technical lemma states that, under certain assumptions, a small number r is guaranteed to exist such that ordr(n) is large with respect to r. For the rest of this section log, as usual, denotes the logarithm to base 2.

Lemma 4.6. Let m ≥ 2 and let n be a prime number with m2 log n < n. Then there exists a positive number r ≤ m2 log n satisfying ordr(n) > m.

Proof: Let s = ⌊m2 log n⌋. Since n is prime and n > s, the order ordr(n) is defined for all r with 1 ≤ r ≤ s. By contradiction, we assume that ordr(n) ≤ m for all such r. In particular, for each r ∈ {1, . . . , s} there exists i ∈ {1, . . . , m} such that ni ≡ 1 mod r. So r divides ni −1 and therefore also the product![](images/137_2.jpg) This implies that lcm(s) is a divisor of![](images/137_1.jpg) Since m ≥ 2, we have s ≥ 7\. Using [Theorem 4.5](#chapter04.xhtml_chapter04_18), we obtain

![](images/137_3.jpg)

It follows ![](images/137_4.jpg) and thus m ≤ 1, a contradiction.

□

Theorem 4.7. Let n ≥ 225 be a prime number. Then there exists r ∈ ℕ such that r ≤ log5 n and ordr(n) > log2 n.

Proof: For n ≥ 225 we have n > log5 n, and with m = ⌊log2 n⌋, by [Lemma 4.6](#chapter04.xhtml_chapter04_20) there is a suitable number r satisfying r ≤ log5 n.

□

## 4.5 Agrawal–Kayal–Saxena primality test

The AKS primality test on input n ∈ ℕworks as follows.

(1)If n < 225, check primality of n directly. From now on, we assume that n > log5 n.

(2)Check whether n = mk for a number m and some k ≥ 2\. In the following, we may assume that n ≠ pk for all primes p and all k ≥ 2.

(3)Search for r ∈ {⌈log2 n⌉ + 1, . . . , ⌊log5 n⌋} with gcd(r, n) = 1 and ordr(n) > log2 n. If no such number r can be found (or we find r with gcd(r, n) ≠ 1), then by [Theorem 4.7](#chapter04.xhtml_chapter04_21) the input n is composite and we halt the procedure. From now on, we assume that r ∈ ℕ with gcd(r, n) = 1 and log2 n < r ≤ log5 n, as well as ordr(n) > log2 n.

(4)For all a ∈ {2, . . . , r − 1} check whether gcd(a, n) = 1\. From now on, we additionally assume that gcd(a, n) = 1 for all 1 ≤ a ≤ r.

(5)Let ![](images/138_1.jpg) and for all a ∈ {1, . . . , ℓ} check the congruence

![](images/138_7.jpg)

If the answer is positive for all a ∈ {1, . . . , ℓ}, then n is prime, otherwise n is composite.

Theorem 4.8. The AKS primality test is correct and it runs in polynomial time (in the input size log n).

The remainder of this section is devoted to the proof of [Theorem 4.8](#chapter04.xhtml_chapter04_24). The number 225 is a constant and has no influence on the asymptotic runtime. For each exponent k ≤ log n it can be checked by binary search, whether a number m exists such that n = mk. In particular, the test, whether n = mk can be done in polynomial time. The values a, ℓ, r are bounded by log5 n. The Euclidean algorithm for testing whether gcd(a, n) = 1 has polynomial running time, and for each pair (a, r), the congruence

![](images/138_8.jpg)

can be checked in polynomial time as well. For a prime number n, the AKS test outputs that n is prime. This follows from [Lemma 4.1](#chapter04.xhtml_chapter04_7) and [Theorem 4.7](#chapter04.xhtml_chapter04_21). It remains to show that the test is able to expose composite numbers. We therefore assume, to the contrary, that the AKS algorithm claims n to be prime, even though there exists a prime number p < n which divides n. Overall, we can make the following assumptions:

–n is composite

–p is prime and p | n

–∀k ≥ 1: n ≠ pk

–r ≤ log5 n < n

–∀a ∈ {1, . . . , r}: gcd(a, n) = 1

–log2 n < ordr(n) ≤ φ(r)

–![](images/138_4.jpg)

–∀a ∈ {1, . . . , ℓ} : (X + a)n ≡ Xn + a mod (Xr − 1, n)

From these assumptions, we will derive a contradiction. Let ![](images/f_d.jpg) be the splitting field of the polynomial f(X) = Xr −1 over ![](images/f_d.jpg)p. Then, ![](images/f_d.jpg) is a finite field extension of ![](images/f_d.jpg)p, in which the polynomial f(X) splits into linear factors

![](images/138_5.jpg)

with αi ∈ ![](images/f_d.jpg). Since f (X) = rXr−1 with r ≢ 0 mod p, we have f' (αi) ≠ 0 for all roots αi. Therefore, the roots are pairwise distinct by [Proposition 1.49](#chapter01_3.xhtml_chapter01_3_13). Thus, the set

![](images/138_9.jpg)

is a subgroup of order r which, according to [Theorem 1.56](#chapter01_3.xhtml_chapter01_3_21), is cyclic. There are φ(r) possibilities for choosing a generator of U. Let

![](images/139_1.jpg) L = {0,1, . . . , ℓ}

Since neither 0 nor 1 generate U and since ℓ ≤ φ(r), some generator α of U satisfies −α ≠ a for all a ∈ L. We fix α and we note that α + a ≠ 0 in ' for all a ∈ L. We have r < p since gcd(a, n) = 1 for all a ∈ {1, . . . , r}. Because of ℓ < r < p, we can consider L as a subset of ![](images/f_d.jpg)p ⊆ ![](images/f_d.jpg).

Definition 4.9. We call a number m ∈ ℕ introspective for a polynomial g(X) ∈ ![](images/f_d.jpg)p[X] if

![](images/139_2.jpg) ∀β ∈ U: g(β)m = g(βm)

Lemma 4.10. Let m1, m2 be introspective for g(X) ∈ p[X]. Then also m1m2 is introspective for g(X).

Proof: For β ∈ U, we also have βm1 ∈ U. This yields g(β)m1m2 = g(βm1 )m2 = g(βm1m2 ).

□

Lemma 4.11. The numbers ![](images/139_3.jpg) and p are introspective for all polynomials (X + a) with a ∈ L.

Proof: The prime p is introspective for every polynomial g(X) ∈ ![](images/f_d.jpg)p[X] because in characteristic p, the mapping x ↦ xp is an automorphism of fields. Thus, g(β)p = g(βp) for all β ∈ ![](images/f_d.jpg). It remains to show ![](images/139_4.jpg) for all β ∈ U. Again, we take advantage of the fact that x ↦ xp is an automorphism of fields. Therefore, in ![](images/f_d.jpg), we obtain

![](images/139_5.jpg)

By assumption, we have (X + a)n ≡ Xn + a mod (Xr − 1, n). This yields (X + a)n ≡ Xn + a mod (Xr − 1, p). Together with βr = 1, we conclude (β + a)n = βn + a in ![](images/f_d.jpg). This shows that ![](images/139_6.jpg) is introspective.

□

Lemma 4.12. Let m be introspective for the polynomials g(X), h(X) ∈ p[X]. Then m is introspective for the polynomial (g ⋅ h)(X) = g(X) ⋅ h(X).

Proof: We have (g ⋅ h)(β)m = g(β)m ⋅ h(β)m = g(βm)⋅ h(βm) = (g ⋅ h)(βm).

□

Lemma 4.13. For all i, j ≥ 0, all a ∈ L andall ea ∈ ℕ, the number ![](images/139_7.jpg) is introspective for the polynomial g(X) =Πa∈L(X + a)ea .

Proof: By [Lemma 4.11](#chapter04.xhtml_chapter04_27) and [Lemma 4.12](#chapter04.xhtml_chapter04_28), both ![](images/139_8.jpg) and p are introspective for g(X). [Lemma 4.10](#chapter04.xhtml_chapter04_26) shows that i and j can be chosen arbitrarily.

□

In the following, let

![](images/140_1.jpg)

be the subgroup of (ℤ/rℤ)∗ generated by ![](images/140_2.jpg) and p. Define t = |G| and observe that log2 n < ordr(n) ≤ t ≤ φ(r). Let P be the set of polynomials

![](images/140_3.jpg)

Equation ([4.1](#chapter04.xhtml_chapter04_12)) shows ![](images/140_4.jpg) Let

![](images/140_14.jpg)

Then ![](images/g.jpg) ⊆ ![](images/f_d.jpg)∗ because α + a ≠ 0 holds for all a ∈ L = {0, . . . , ℓ}. We give two different estimates for |![](images/g.jpg)|, and then show that they contradict each other.

Lemma 4.14. The mapping P → ![](images/f_d.jpg)∗ with g(X) ↦ g(α) is injective.

Proof: Let g1(X), g2(X) ∈ P with g1(α) = g2(α). Consider ![](images/140_6.jpg) Then, we have

![](images/140_15.jpg)

Thus, the polynomial g1(X) − g2(X) has at least the t roots αm with m ∈ G. On the other hand, the degree of g1(X) − g2(X) is less than t, so g1(X) = g2(X) and therefore the mapping g(X) ↦ g(α) is injective.

□

As a consequence of [Lemma 4.14](#chapter04.xhtml_chapter04_30), we have ![](images/140_8.jpg) We consider a set of introspective numbers Î ⊆ ℕ defined as follows:

![](images/140_9.jpg)

At this point, we have to use the assumption that n has at least two prime divisors, thus ensuring that Î contains sufficiently many numbers. Since ![](images/140_10.jpg) has a prime divisor different from p, the set Î contains exactly ![](images/140_11.jpg) elements, and |Î| > t = |G|. The mapping Î → G: m ↦ (m mod r) thus cannot be injective, which means that there exist m1, m2 with 1 ≤ m1 < m2 and m1, m2 ∈ Î, such that m1 ≡ m2 mod r. We further remark that ![](images/140_12.jpg) Now we show that all elements g(α) ∈ G are roots of the nontrivial polynomial Ym1 − Ym2. From αr = 1, we obtain αm1 = αm2. For g(α) ∈ G it follows that g(α)m1 − g(α)m2 = g(αm1) − g(αm2) = 0\. As a consequence ![](images/140_13.jpg) because the polynomial Ym1 − Ym2 has at most m2 roots. We obtain a contradiction by the following computation:

![](images/141_1.jpg)

This proves the correctness of the AKS test and thus [Theorem 4.8](#chapter04.xhtml_chapter04_24).

We now summarize the steps of the proof. The assumptions in our proof by contradiction lead us to a field ![](images/f_d.jpg) and a choice of α ∈ ![](images/f_d.jpg). A principle used several times is the fact that in fields the zero polynomial is the only polynomial having more roots than indicated by the degree; in combinatorics, this argument is known as the polynomial method. Then, a set G of exponents is considered which applied to α lead to different elements αm from . Depending on |G|, we describe a set P of polynomials. For the set P, by construction, we know its cardinality. The set P is embedded into the multiplicative group of ' by evaluation at α. The subset of ![](images/f_d.jpg)' which corresponds to P is called ![](images/g.jpg) and we obtain |![](images/g.jpg)| = |P|. The next step shows that all elements of ![](images/g.jpg) are roots of a polynomial of small degree. This yields a second estimate of ![](images/g.jpg) which, however, contradicts the first.

## Summary

Notions

–PRIMES

–deterministic polynomial time P

–f1(X) ≡ f2(X) mod (Xr − 1, n)

–![](images/141_2.jpg) denotes the set of k-subsets of A

–lcm(n) is the least common multiple of 1, . . . , n

–orr(n) is the order of n in (ℤ/rℤ)∗

–introspective number

–polynomial method

Methods and results

–Let gcd(a, n) = 1\. Then, n is prime ⇔ (X + a)n ≡ Xn + a mod n

–For every finite set A, we have ![](images/141_3.jpg)

–![](images/141_4.jpg)

–![](images/141_5.jpg)

–lcm(n) > 2n for n ≥ 7

–If n ≥ 225 is prime, then there exists r ≤ log5 n with ordr(n) > log2 n.

–AKS primality test on input n ≥ 225:

(1)If n = mk for k ≥ 2, then output “n is composite.”

(2)Compute r ≤ log5 n with gcd(r, n) = 1 and ordr(n) > log2 n.

(3)If such an r does not exist, then output “n is composite.”

(4)If gcd(a, n) ≠ 1 for some a ∈ {2, . . . , r − 1}, then output “n is composite.”

(5)Let ![](images/142_1.jpg)

(6)If (X + a)n ≢ Xn + a mod (Xr − 1, n) for some a ∈ {1, . . . , ℓ}, then output “n is composite.”

(7)Otherwise, output “n is prime.”

–polynomial running time of the AKS test

–If n is prime, then the AKS test outputs that n is prime.

–If n is composite, then the AKS test outputs that n is composite.

# 5 Elliptic curves

Johann Carl Friedrich Gauss (1777–1855) showed that the complex numbers ℂ can be identified with the plane ℝ × ℝ. By contracting the infinitely far border of this plane to a single point, we obtain the surface of a sphere. The extra point in the drawing corresponds to the North Pole and the real numbers together with this point appear as a circle on the sphere.

![](images/143_1.jpg)

The typical shape of an elliptic curve over ℂ is more complicated and it emerges when we consider a grid. In the simplest case, this is the additive subgroup L = ℤ+ iℤ. For the grid L, we can form the quotient group ℂ/L. We can visualize this group as a three-dimensional image similar to the surface of a sphere. However, ℂ/L does not give a sphere but a torus, that is, the surface of a donut. We start with the unit square [0, 1] × [0, 1] inside ℝ×ℝ. Then, the four edges of [0, 1] × [0, 1] belong to the grid L (when identifying ℝ×ℝ with ℂ); and we obtain ℂ/L by glueing together the top and the bottom edge as well as the left and the right edge. This results in a torus as a visualization of ℂ/L. In ℂ/L, seen as an additive group, there are exactly four elements of order at most 2\. In the unit square [0, 1] × [0, 1], they correspond to the points (0, 0), (0, 1/2), (1/2, 0), and (1/2, 1/2). Thus, the Klein four-group ℤ/2ℤ×ℤ/2ℤappears as a subgroup of ℂ/L.

Consider a cubic equation of type Y2 = X 3+AX+B with constants A and B and two variables X and Y over the complex numbers ℂ; and let E = {(a, b) ∈ ℂ×ℂ| b2 = a3 + Aa +B } be its set of solutions. If the roots of the polynomial X3+AX+B are all different, then E is a smooth surface of (real) dimension 2 inside the space ℂ×ℂof dimension 4\. The set E can naturally be identified with the surface of a torus; as in the step from a plane to a sphere, one has to add some extra “point at infinity.” The connection between E and the surface of a torus is given by the following parametrization: there exist w1, w2 ∈ ℂ\ {0} with ![](images/144_1.jpg) and a total function f : ℂ → ℂ ∪ {∞} with f(z) = f(z + w) for all w in the grid L = {mw1 + nw2 |m, n ∈ ℤ} such that

![](images/144_5.jpg)

As a partial mapping from ℂtoℂ, the function f is meromorphic and f' is its derivative; we set f' (z) = ∞whenever f' (z) is undefined over ℂ. The parametrization has the additional property that the mapping ℂ/L → E ∪ {(∞, ∞)} with z ↦ (f(z), f' (z)) is bijective. This allows us to identify E ∪ {(∞, ∞)} with the torus ℂ/L. A meromorphic function f with f(z) = f(z + w) for all w ∈ L is called elliptic; and the above connection coins the term elliptic curve. For more details on parametrizations of elliptic curves, we refer to the existing literature and textbooks such as [[57](#Bibliography.xhtml_Bibliography_58)] or [[90](#Bibliography.xhtml_Bibliography_91)].

![](images/144_3.jpg)

The real solutions of Y2 = X3 + AX + B can be obtained as the intersection of a plane and the torus defined by E. For instance, taking the intersection of the torus with the equatorial plane, we obtain two circles, one positioned inside the other. If we cut the outer circle and pull the endpoints to infinity, then the standard image of an elliptic curve over the real numbers emerges (see the second plot in [Figure 5.1](#chapter05_1.xhtml_chapter05_1_5)), and the points on this curve still satisfy the cubic equation. We can imagine that, in this case, the point (∞, ∞) from the torus has become an infinitely distant point, called the point at infinity.

The three plots in [Figure 5.1](#chapter05_1.xhtml_chapter05_1_5) show the elliptic curves (over ℝ) given by the equations Y2 = X3 − X + B with B ∈ {−1, 0, 1}. The third one, for example, shows the set of points

![](images/144_6.jpg)![](images/145_1.jpg)

Fig. 5.1. Elliptic curves over ℝ.

We call such a set of points a curve. If (a, b) is a point on the curve, then (a, −b) is another one. The picture does not really look like an ellipse and, in fact, the connection between ellipses and elliptic curves can only be understood via a detour to elliptic functions.

Due to our focus on discrete methods, elliptic curves over finite fields are of particular interest. To this end, we start with an algebraic equation Y2 = X3 + AX + B with coefficients in ℤ and investigate the points satisfying this equation modulo some prime p, that is,

![](images/145_4.jpg)

where p denotes the finite field ℤ/pℤ. [Figure 5.2](#chapter05_1.xhtml_chapter05_1_7) gives two examples of such “curves” for p = 101\. There are some hidden lines and circular structures, but the exact scheme looks rather random. This “regular chaos” makes elliptic curves of significant interest for cryptographic applications.

![](images/145_3.jpg)

Fig. 5.2. Elliptic curves over ℤ/101ℤ.

In the distant future, the Rivest–Shamir–Adleman (RSA) algorithm could be broken, while cryptography using elliptic curves might remain secure. It is widely believed that techniques such as the quadratic sieve ([Section 3.6.3](#chapter03_2.xhtml_chapter03_2_14)) or the index calculus method ([Section 3.7.4](#chapter03_2.xhtml_chapter03_2_26)) cannot be efficiently adapted to elliptic curves; this approves the use of elliptic curves in cryptography and it is the main reason for smaller key sizes in elliptic curve cryptosystems. The position of the points follows a precise geometric structure, thereby forming an Abelian group. A computer is able to perform computations in this group’s structure very efficiently. The fascination of elliptic curves has influenced whole generations of mathematicians. The study of such curves lead Andrew Wiles (born 1953) and Richard Taylor (born 1962) to the proof of Fermat’s Last Theorem, which states that, for every integer n ≥ 3, the equation Xn + Yn = Z n has no positive integer solution.

In the following, let K denote a field and k an algebraically closed field containing K. Thus, k is always infinite; it is a field extension of K in which each polynomial splits into linear factors. For K = ℚ or K = ℝ, we choose k = ℂ. For K = p, we content ourselves with the knowledge that an algebraic closure exists and that it is infinite. We do not treat the subject in full generality: fields of characteristic 2 are omitted completely, and for characteristic 3, we only consider curves in Weierstrass normal form (Karl Theodor Wilhelm Weierstrass, 1815–1897). A general elliptic curve is defined by an equation of the form

![](images/146_5.jpg)

for constants A, B, C, D, and E. The equation is in Weierstrass normal form if C = D = E = 0\. If the characteristic is neither 2 nor 3, then, by affine transformations, every elliptic curve is equivalent to one in Weierstrass normal form; see [Exercise 5.1](#chapter05_3.xhtml_chapter05_3_18).

We choose coefficients A, B ∈ K and consider the polynomial s(X) = X3 +AX+B = (X − a1)(X − a2)(X − a3). We are only interested in the (generic) case where the three roots a1, a2, a3 ∈ k are pairwise distinct. This is equivalent to 4A3 + 27B2 ≠ 0; see [Exercise 5.2](#chapter05_3.xhtml_chapter05_3_21). The polynomial s(X) leads us to an equation with two variables

![](images/146_6.jpg)

The solutions of this equation can be interpreted as a curve in K × K. We call the set

![](images/146_7.jpg)

an elliptic curve over K. In particular, E (K) is a subset of E (k). As we have seen earlier, it is natural to add a so-called point at infinity, denoted by O. By abuse of notation, we also call

![](images/146_8.jpg)

an elliptic curve. In projective coordinates, the point at infinity would belong to the curve in a natural way from the very beginning.

Unlike E (K), the curve E (k) always contains infinitely many points: since k is algebraically closed, we can always extract square roots. In particular, for each of the infinitely many a ∈ k there exists b ∈ k with (a, b) ∈ E(k).

For a point P = (a, b) ∈ k×k,wedefine ![](images/147_1.jpg) and![](images/147_2.jpg) Thus, besides![](images/o.jpg), exactly the three points Pi = (ai , 0) in Ẽ(k) satisfy ![](images/147_3.jpg) As we will see later, these four points form a Klein four-group with ![](images/o.jpg) as the neutral element. If the polynomial s(X) already splits into linear factors over K, then the points Pi are in E (K).

If q is a prime power, we have |E(q)| ≤ 2q because each X-coordinate provides at most two solutions in the Y-coordinate. A deep result by Helmut Hasse (1898–1979) provides a much more precise statement:![](images/147_7.jpg)

Formula ([5.1](#chapter05_1.xhtml_chapter05_1_9)), in a way, provides a connection between chance and necessity[6](#Notes.xhtml_Notes_6). Suppose for every a ∈ q, we independently and uniformly at random chose c ∈ q and counted the pairs (a, b), (a, −b) if and only if c = b2 is a square. Then, wewould expect q pairswith a deviation of about![](images/147_6.jpg) One can think of c as a randomized equivalent of s(a). By Hasse’s theorem, this probabilistic behavior coincides rather precisely with the actual bounds.

## 5.1 Group law

The interest in elliptic curves in the context of cryptography or number theoretic algorithms is based upon a binary operation + on E ̃(K) such that (Ẽ(K), +, ![](images/o.jpg)) forms an Abelian group.We present a geometric approach, which uses lines and their intersection with E ̃(K) as an approach to define the addition. It turns out to be quite obvious that +maps two points of Ẽ(K) to a point on E ̃(K), that ![](images/o.jpg) is the neutral element, every point has an inverse, and + is commutative. The only unobvious property is associativity, which is surprisingly difficult to prove. We give a complete and self-contained proof of associativity in [Sections 5.1.2](#chapter05_1.xhtml_chapter05_1_16) and [5.1.3](#chapter05_1.xhtml_chapter05_1_23).

### 5.1.1 Lines

A line in k × k is a set of points L that can either be described by the equation X = a or by Y = μX+ν. In the first case, we speak of a vertical. We imagine the point at infinity O lying on every vertical but on no other line.

We investigate the intersection of lines with points on an elliptic curve E (k) given by Y2 = s(X) with s(X) = X3 + AX + B. If L is a vertical given by X = a, then the points P = (a, b) and ![](images/148_1.jpg) are in the intersection L ∩ E(k) whenever b2 = a3 + Aa + B. For b = 0, we have ![](images/148_2.jpg) and the point is counted twice. Together with the point at infinity ![](images/o.jpg), this gives exactly three points in the intersection of E ̃(k) and the vertical.

If L is described by the equation Y = μX + ν and if P = (a, b) belongs to the intersection of L and E (k), then a is a root of the following polynomial:

![](images/148_11.jpg)

This polynomial of degree 3 over k has exactly three (not necessarily distinct) roots, and each root uniquely defines an associated Y-coordinate via the linear equation. If we write t(X) = (X − x1)(X − x2)(X − x3), then a ∈ {x1, x2, x3} and, by comparing the coefficients of X2, we obtain x1 + x2 + x3 = μ2. Let yi = μxi + ν for i ∈ {1, 2, 3}. Then, we obtain

![](images/148_12.jpg)

If we know the two points (x1, y1) and (x2, y2), then we can determine the third point (x3, y3) using the following formulas:

![](images/148_10.jpg)

We find the parameter ν by

![](images/148_13.jpg)

To determine the parameter μ, we have to distinguish between the cases x1 ≠ x2 and x1 = x2. Assume that x1 ≠ x2. Then, μ can be computed as

![](images/148_7.jpg)

Otherwise, if x1 = x2, then x1 is a double root of t(X), and we have

![](images/148_14.jpg)

We have y1 ≠0 because otherwise s'(x1) = 0, that is, x1 would also be a double root of s(X), a case which we have excluded from our considerations. Together with the fact that 2 ≠ 0 in k, this yields 12

![](images/148_9.jpg)

The value μ is the slope of the tangent of the elliptic curve at the point (x1, y1).

Many computations can be performed in the field K without having to consider the algebraic closure k. Let x1, A, B, μ, ν ∈ K and as given earlier t(X) = s(X) − (μX + ν)2 = (X − x1)(X − x2)(X − x3). Then, x2 ∈ K if and only if x3 ∈ K. If x2 is in K, then L ∩ E(k) = {(xi , yi) | i = 1, 2, 3} ⊆ E(K). Thus, if two points of a line belong to Ẽ(K), then the third point is in E ̃(K), too. This leads to the crucial idea of how to obtain the commutative group structure on the set E ̃(K). We let the point at infinity O be the neutral element, and the sum of any three points of E ̃(K) (with multiplicities) lying on a common line is defined to be zero.

We make this explicit by giving formulas for the group operation. Several cases need to be distinguished. For all P ∈ E ̃(K), we define P + ![](images/o.jpg) = ![](images/o.jpg) + P = P. The sum of two points P = (x1, y1) and Q = (x2, y2) of E(K) is computed as follows:

(a)If x1 ≠ x2, we draw a line through P and Q. This means we compute ![](images/149_1.jpg) and x3 = μ2 − x2 − x1 and finally y3 = y1 + μ(x3 − x1). We let ![](images/149_2.jpg) and

![](images/149_3.jpg)

(b)If x1 = x2 and y1 ≠ −y2, then y1 = y2 ≠ 0 and P = Q. We determine the tangent slope ![](images/149_4.jpg) and x3 = μ2 − 2x1 as well as y3 = y1 + μ(x3 − x1). The third point on the line through P and Q is R = (x3, y3). To achieve P + Q + R = ![](images/o.jpg), we define

![](images/149_5.jpg)

(c)Finally, if x1 = x2 and y1 = −y2, then P and Q are on a vertical, and the third point on this line is ![](images/149_6.jpg) Therefore, we define

![](images/149_9.jpg)

Theorem 5.1. The aforementioned operation on E ̃(K) defines the structure of an Abelian group with ![](images/o.jpg) as its neutral element.

Proof: We have already seen that P + Q ∈ E ̃(K) for P, Q ∈ E ̃(K). From the rules given earlier it follows that

□

–O is the neutral element,

–the inverse−P of P = (a, b) ∈ E(K) is ![](images/149_7.jpg) and

–we have P + Q = Q + P for all P, Q ∈ Ẽ(K).

The only condition which is not clear and, in fact, difficult to show, is the associative law

![](images/149_8.jpg) (P + Q) + R = P + (Q + R)

In order to show associativity, we take a detour via polynomials. The presentation of this proof is the subject of the following two sections.

### 5.1.2 Polynomials over elliptic curves

We define and investigate polynomials over E (k). As given earlier, let s(X) = X3 + AX + B. Let a1, a2, a3 ∈ k be the roots of s(X); they are assumed to be pairwise different. The polynomial ring in two variables X and Y is denoted by k[X, Y]. Each polynomial f(X, Y) ∈ k[X, Y] can be evaluated at (a, b) ∈ k × k to obtain f(a, b). We restrict

ourselves to the evaluation at points of the elliptic curve. At these points, the evaluation of f(X, Y) ∈ k[X, Y] coincides with the evaluation of

![](images/150_6.jpg)

for each polynomial h(X, Y) ∈ k[X, Y]. Thus, in the ring k[X, Y] we can introduce an equation Y2 = s(X) and consider the quotient ring

![](images/150_7.jpg)

where 〈Y2 = s(X)〉 is the ideal generated by Y2 − s(X). We call k[x, y] the polynomial ring over E (k). The element x ∈ k[x, y] is the residue class of X modulo 〈Y2 = s(X)〉 and, similarly, y is the residue class of Y. For a polynomial f ∈ k[x, y] and a point P = (a, b) ∈ E (k), the value f(P) = f(a, b) ∈ k is well defined, since all polynomials g in the residue class of f satisfy g(P) = f(P) for all P ∈ E(k). In the following, we show that the ring k[x, y] behaves very similarly to the usual polynomial ring. To this end, we introduce the norm of a polynomial, which allows us to use our knowledge about polynomials in one variable. Using the norm, we introduce a notion of degree that satisfies the degree formula. The usual notion of a degree cannot be used here since, for example, y2 = s(x) would have both degree 2 and degree 3\. Then, we show that, for points on the elliptic curve, the order of a root can be defined in a reasonable manner. It is not entirely obvious how this can be achieved since, for instance, the point (a1, 0) of the elliptic curve is a root of the polynomial x + y − a1, but neither x − a1 nor y can be factored out. By k[x], we denote the image of the polynomial ring k[X] in k[x, y]. It is clear that k[X] can be identified with k[x]. Note, however, that (y3 − y2)(y + 1) is in k[x] while neither y3 − y2 nor y + 1 is in k[x].

Every polynomial f ∈ k[x, y] can be written as f = υ(x) + y ⋅ w(x) for υ(x), w(x) ∈ k[x]: Suppose that f = Σi≥0 fi(x)yi for fi(x) ∈ k[x]. Then

![](images/150_3.jpg)

and we can set υ(x) = Σi≥0 f2i(x)si (x) and w(x) =Σi≥0 f2i+1(x)si (x).

Lemma 5.2. If f ∈ k[x, y] is a polynomial with f ≠ 0, then it has only a finite number of roots in E(k).

Proof: Let f = υ(x) + y ⋅ w(x). We reduce the problem to a polynomial with only one variable. Consider

![](images/150_5.jpg)

If f(P) = 0 for infinitely many P ∈ E (k), then the polynomial g has infinitely many roots in k. Thus, it is the zero polynomial. Since the degrees in x of w2(x) and υ2(x),respectively, are even (or−∞) but the degree of s(x) is 3, it follows that υ(x) = w(x) = 0 and thus f = 0.

□

The lemma implies uniqueness of the representation f = υ(x) + yw(x). To see this, let υ(x)+yw(x) = υ̃(x)+yw̃ (x) and consider g = υ(x)−υ̃(x)+y(w(x)−w̃ (x)). Then, g(P) = 0 for all P ∈ E (k), and thus, from [Lemma 5.2](#chapter05_1.xhtml_chapter05_1_18) we obtain υ(x) = υ̃(x) and w(x) = w̃ (x).

For f = υ(x) + yw(x) ∈ k[x, y], we define ![](images/151_1.jpg) by ![](images/151_2.jpg) Since the representation f = υ(x) + yw(x) is unique, ![](images/151_3.jpg) is well defined. Implicitly, ![](images/151_4.jpg) was already used in the proof given earlier, even though we did not know (and did not use) that f it is well defined. We can now formally define the norm of f :

![](images/151_5.jpg)

Thus, the norm N (f) is a polynomial in k[x]. In particular, the norm of x is x2 and the norm of y is −s(x). One can easily check that N(f ⋅ g) = N(f) ⋅ N(g). For f ∈ k[x] let degx(f) be the degree of f as a polynomial in k[X]. Then, we have

![](images/151_6.jpg)

This holds because the degree of υ2(x) is even (or −∞) but the degree of s(x)w2(x) is odd (or −∞). Moreover, we note that N (f) = 0 implies f = 0\. We define the degree of f ∈ k[x, y] by

![](images/151_11.jpg)

Note that deg(f) can never be 1, whereas all other values −∞, 0, 2, 3, . . . are in the image of deg. In the following, we will see that this is a key idea for understanding elliptic curves. The degree mapping factors are as follows:

![](images/151_8.jpg)

These mappings are monoid homomorphisms, where the operations in k[x, y] and k[x] are multiplicative while in {−∞} ∪ ℕ it is additive. Let us keep in mind that deg(f) ≠ 1 and deg(fg) = deg(f) + deg(g) for all f, g ∈ k[x, y].

Suppose that fg = 0 in k[x, y]. Then, N(f)N(g) = 0 in k[x] and therefore N(f) = 0 or N (g) = 0\. This implies f = 0 or g = 0, thereby showing that k[x, y] is an integral domain, that is, the zero polynomial 0 is the only zero divisor.

Next, we want to define the order ordP(f) of a polynomial f ∈ k[x, y] at a point P ∈ E(k). Remember that, over an algebraically closed field k, every polynomial f ∈ k[X] can be split into linear factors

![](images/151_9.jpg)

where di is the order (or multiplicity) of the root xi ∈ k and ![](images/151_10.jpg) For polynomials f ∈ k[x, y], the situation is quite similar.

Theorem 5.3. Let f ∈ k[x, y] with f ≠ 0 and P = (a, b) ∈ E(k). For exactly one d ∈ ℕ there exist g, h ∈ k[x, y] such that g(P) ≠ 0 ≠ h(P) and

![](images/152_7.jpg)

where a1, a2, a3 are the roots of s(X).

Proof: First, we show the uniqueness of d for a ∉ {a1, a2, a3}. Consider fg = (x − a)dh and f g̃ = (x−a)eh̃ for d > e ≥ 0.We obtain (x−a)dg̃h = fgg ̃ = (x−a)eh̃g and therefore

![](images/152_8.jpg)

Since (x − a)e is not the zero polynomial, we obtain (x − a)d−eg̃h = h̃g. Using d > e we see that ((x − a)d−eg̃h)(P) = 0 and thus (h̃g)(P) = h̃(P)g(P) = 0\. This shows that g(P) = 0 or h̃(P) = 0\. Hence, for every a, there is at most one d satisfying fg = (x−a)dh and g(P) ≠ 0 ≠ h(P).

Next, we show the uniqueness of the exponent d for a ∈ {a1, a2, a3}. Note that in this situation, we have b = 0\. Let fg = ydh and f g̃ = yeh̃ for d > e ≥ 0\. As before, we obtain

![](images/152_9.jpg)

Since ye is nonzero, this yields yd−eg̃h = h̃g. Now, d > e implies yd−eg̃h(P) = 0 and thus h̃(P)g(P) = 0\. Therefore, g(P) = 0 or h̃(P) = 0.

We now prove the existence of d. By [Corollary 1.47](#chapter01_3.xhtml_chapter01_3_10), there exists an integer e ≥ 0 and polynomials υ, w ∈ k[x] with

![](images/152_10.jpg)

and υ(a) ≠ 0 or w(a) ≠ 0\. First, consider the case a ∉ {a1, a2, a3} and b ≠ 0\. If υ(a) + bw(a) ≠ 0, we can choose d = e, g = 1 and h = υ(x) + yw(x). If υ(a) + bw(a) = 0, then υ(a) − bw(a) ≠ 0 has to hold because otherwise 2υ(a) = 0 = 2bw(a) in contradiction to υ(a) ≠ 0 or w(a) ≠ 0\. Thus, the polynomial g = υ(x) − yw(x) satisfies g(P) ≠ 0 and fg = (x − a)eN(g). The polynomial (x − a)eN(g) is in k[x] and can thus be written as (x − a)dh(x) with h(a) = h(P) ≠ 0.

For the other case, without loss of generality we may assume that a = a1 and b = 0\. Then

![](images/152_11.jpg)

For υ(a) ≠ 0 we can choose d = 2e and g = (x − a2)e(x − a3)e and h = υ(x) + yw(x) since b = 0 ensures h(P) = υ(a). In the case of υ(a) = 0, we have υ(x) = (x − a)cυ̃(x) for c > 0 and υ̃(a) ≠ 0\. This yields

![](images/152_12.jpg)

with w̃ (x) = (x−a2)c(x−a3)cw(x). Note that w̃ (a) ≠ 0\. If we let h = w̃ (x)+ysc−1(x)υ̃(x), then also h(P) = w̃ (a) ≠ 0 because b = 0\. Then

![](images/153_12.jpg)

and we have reached our goal with d = 2e + 1.

□

For a polynomial f ≠ 0 and a point P ∈ E (k) let d ∈ ℕ be defined as in [Theorem 5.3](#chapter05_1.xhtml_chapter05_1_20). We call d the order of f at P and write d = ordP(f). Note that f(P) = 0 if and only if ordP(f) > 0\. If ordP(f) > 0, we also speak of the multiplicity of the root P. An important property of the order follows directly from the uniqueness in [Theorem 5.3](#chapter05_1.xhtml_chapter05_1_20):

![](images/153_13.jpg)

for all f, g ∈ k[x, y] and P ∈ E(k).

Theorem 5.4. Let f, h ∈ k[x, y] with f ≠ 0 ≠ h and ordP(f) ≤ ordP(h) for all P ∈ E(k). Then, there is a polynomial g ∈ k[x, y] satisfying fg = h.

Proof: It suffices to show the existence of g ∈ k[x, y] with ![](images/153_3.jpg) since then ![](images/153_4.jpg) and thus fg = h. Because of ![](images/153_5.jpg) for all points P, by replacing f by ![](images/153_6.jpg) we may thus assume that f ∈ k[x]. We use induction on the degree of f. If degx(f) = 0, then f ∈ k is a constant and g = f −1h satisfies the requirements of the theorem. For degx(f) = 1, it is sufficient to consider the normalized case f = x − a. Let h = υ(x) + yw(x) and let P = (a, b) be a point on the curve. From ![](images/153_7.jpg) we obtain ordP(h) ≥ 1 and ![](images/153_8.jpg) Thus υ(a) + bw(a) = 0 = υ(a) − bw(a). For b ≠ 0 this yields υ(a) = w(a) = 0 and, hence, h contains a factor x − a. The remaining case is b = 0, υ(a) = 0 and w(a) ≠ 0\. We may assume that a = a1. Since (x − a)(x − a2)(x − a3) = s(x) = y2, we have ordP(x − a) = 2\. On the other hand, ordP(h) = 1 because

□

![](images/153_11.jpg)

Here, w̃ (x) = (x − a2)(x − a3)w(x), and υ̃(x) is determined by υ(x) = (x − a)υ̃(x). This contradicts ordP(x − a) ≤ ordP(h). Therefore, the situation b = 0, υ(a) = 0 and w(a) ≠ 0 cannot occur for degx(f) = 1.

Now let degx(f) > 1\. Then, f can be written as f = f1f2, where both degx(f1) and degx(f2) are smaller than degx(f). We can apply the induction hypothesis to f1 and h. This yields the existence of g1 ∈ k[x, y] with f1 ⋅ g1 = h. Now, ordP(f2)≤ ordP(g1) for all P ∈ E(k). Again, by induction there exists g2 ∈ k[x, y] with f2g2 = g1. Thus, we obtain fg2 = f1f2g2 = f1g1 = h.

5.1.3 Divisors

A divisor (with nonnegative coefficients) in this context is a formal sum ![](images/153_10.jpg) where n P ∈ ℕfor all P and n P = 0 for almost all P. Therefore, the sum is finite. Divisors can be added:![](images/154_1.jpg)

Note that the addition of divisors is associative. The empty sum with n P = 0 for all P ∈ E (k) is the neutral element. The degree of a divisor D = ΣP∈nP n PP is given by

![](images/154_2.jpg)

Obviously, deg(D1 + D2) = deg(D1) + deg(D2). By [Lemma 5.2](#chapter05_1.xhtml_chapter05_1_18), every polynomial f ∈ k[x, y] defines a unique divisor div(f) by

![](images/154_3.jpg)

Since ordP(f ⋅ g) = ordP(f) + ordP(g), it follows that div(f ⋅ g) = div(f) + div(g). Divisors of type div(f) are called principal divisors. Let us first determine the principal divisor of f = x − a. Let P = (a, b). If a ∈ {a1, a2, a3}, say a = a1, then we have (x − a)(x − a2)(x − a3) = s(x) = y2 and hence ordP(x − a) = 2; this yields div(x − a) = 2P. For a ∉ {a1, a2, a3}, we have ![](images/154_4.jpg) and ![](images/154_5.jpg) So regardless of a, we always obtain div(x − a) = P + P.

In the next step let f = f(x) ∈ k[x]. Then, ![](images/154_6.jpg) with ![](images/154_7.jpg) If we choose elements yi ∈ k such that Pi = (xi , yi)∈ E(k), then the principal divisor of f is

![](images/154_8.jpg)

Then for f ∈ k[x], we obtain the formula

![](images/154_18.jpg)

For a divisor D = ΣP∈E(k) nPP we further define ![](images/154_9.jpg) Obviously, deg(D) = ![](images/154_10.jpg) Now let f ∈ k[x, y], then ![](images/154_11.jpg) It follows that ![](images/154_12.jpg) and therefore ![](images/154_13.jpg) We obtain

![](images/154_14.jpg)

This yields

![](images/154_15.jpg)

Therefore, a principal divisor can never have degree 1\. Since for P = (a, b) ∈ E (k) the divisor ![](images/154_16.jpg) is a principal divisor, all divisors of type ![](images/154_17.jpg) are principal divisors.

Let us examine the principal divisors of a linear polynomial f = μx + ν + γy for μ, ν, γ ∈ k. The case γ = 0 has already been treated earlier. So, without loss of generality let γ = −1\. The principal divisor can be obtained from the three points in the intersection of the line L = {(x, y) ∈ k × k | y = μx + ν } and the elliptic curve. The corresponding formulas can be found in [Section 5.1.1](#chapter05_1.xhtml_chapter05_1_12).

### 5.1.4 Picard group

In the following, all computations are performed modulo principal divisors. Formally, we define an equivalence relation by C ∼ D if there exist polynomials f, g ∈ k[x, y] such that C +div(f) = D +div(g). Then [D], as usual, denotes the equivalence class of D. If C1 ∼ D1 and C2 ∼ D2, then also C1+C2 ∼ D1+D2. Thus, the set of equivalence classes is a commutative monoid with respect to the operation [C]+[D] = [C+D]. All principal divisors are in the same class, which is the neutral element 0\. This monoid is in fact a group because ![](images/155_1.jpg) is a principal divisor, that is, ![](images/155_2.jpg) and hence ![](images/155_3.jpg) The group consisting of these classes is called the Picard group (Charles Émile Picard, 1856–1941) and it is denoted by Pic0(E(k)). We show that the Picard group Pic0(E(k)) can be identified with Ẽ(k).

Let us first consider the class of principal divisors. There is no other divisor in this class: suppose that D + div(f) = div(h) for polynomials f, h ∈ k[x, y]. Then, ordP(f) ≤ ordP(h) for all P ∈ E (k) and, by [Theorem 5.4](#chapter05_1.xhtml_chapter05_1_22), there exists a polynomial g with fg = h. Thus, D = div(g) is a principal divisor. In particular, the zero class does not contain any divisor of degree 1\. For P ∈ E(k), it then follows that [P] ≠ 0 in Pic0(E(k)) and therefore the Picard group is not trivial.

If we consider two points P, Q ∈ E(k), then [P] ≠ [Q] is equivalent to ![](images/155_4.jpg) If ![](images/155_5.jpg) the x-coordinates of P and ![](images/155_6.jpg) are different and there is a unique line through P and ![](images/155_9.jpg) This line intersects the elliptic curve in a third point R. Then, ![](images/155_8.jpg) is a principal divisor for a linear polynomial and therefore ![](images/155_7.jpg) This shows that [P] ≠ [Q]. If ![](images/155_10.jpg) then P ≠ (ai , 0) and ![](images/155_11.jpg) for the third point R in the intersection of the tangent at P with the curve E (k). Thus, for two different points P, Q ∈ E (k), we always have [P] ≠ [Q]. It remains to consider the point at infinity ![](images/o.jpg) and we define [![](images/o.jpg)] = 0.

Theorem 5.5. The mapping

![](images/155_15.jpg)

defines an isomorphism of Abelian groups.

Proof: As we have just seen, the mapping is injective. It is surjective, too. To see this, we give an equivalence preserving reduction process on the set of divisors. A divisor of the form ![](images/155_14.jpg) can be replaced by 0\. For each divisor P + Q with ![](images/155_13.jpg) we find a line and thus another point R on the curve with the property that P + Q + R is a principal divisor. Thus, P + Q can be replaced by ![](images/156_1.jpg) Each step reduces the degree of a divisor. The algorithm ends at 0 and therefore at the point at infinity or at a divisor of degree 1, that is, a point on the curve. The homomorphism property P + Q ↦ [P] + [Q] directly follows from the construction.

Since the Picard group is an Abelian group, the points of the elliptic curve E ̃(k) also form an Abelian group. Furthermore, if K is a subfield of k, the formulas in [Section 5.1.1](#chapter05_1.xhtml_chapter05_1_12) show that Ẽ(K) = { (a, b) ∈ K × K | b2 = s(a) } is a subgroup. Addition, as introduced in [Section 5.1.1](#chapter05_1.xhtml_chapter05_1_12), coincides with addition in the Picard group. The associative law, thus, is a consequence of the interpretation of the points on the curve as divisors and the interpretation of lines as principal divisors. This completes the proof of [Theorem 5.1](#chapter05_1.xhtml_chapter05_1_15).

□

## 5.2 Applications of elliptic curves

This section is mostly self-contained. We therefore repeat the most important properties of elliptic curves. Let K be a field with a characteristic different from 2 and let A, B ∈ K with 4A3 + 27B2 ≠ 0\. The set of points defined by the equation Y2 = X3 + AX2 + B is

![](images/156_6.jpg)

If we add a new point ![](images/o.jpg), called the point at infinity, then we obtain the elliptic curve E ̃(K) defined by the parameters A and B.

![](images/156_7.jpg)

There is an addition + on E ̃(K) such that (Ẽ(K), +, ![](images/o.jpg)) forms an Abelian group with neutral element O. For points P = (x1, y1) and Q = (x2, y2) in E(K), the sum P + Q is given by the following formulas.

(a)If x1 ≠ x2, then for ![](images/156_4.jpg) we define x3 = μ2 − x2 − x1 and y3 = μ(x1 − x3)− y1 and P + Q = (x3, y3).

(b)If x1 = x2 and y1 = y2 ≠ 0, we have P = Q. In this case, we use ![](images/156_5.jpg) for defining x3 = μ2 − 2x1 and y3 = μ(x1 − x3)− y1 and 2P = P + Q = (x3, y3).

(c)If x1 = x2 and y1 = −y2, we define P + Q = O.

Case (c) gives a simple formula for computing the inverse. For P = (x1, y1)∈ E (K), we have −P = (x1, −y1). Case (a) occurs if and only if P ≠ Q and P ≠ −Q. We presented a complete proof of the group laws in [Section 5.1](#chapter05_1.xhtml_chapter05_1_11). In particular, we have P + Q ∈ Ẽ(K) for all P, Q ∈ E ̃(K). The addition on E ̃(K) might look mysterious at first sight but it has a geometric motivation, which is given in [Section 5.1.1](#chapter05_1.xhtml_chapter05_1_12).

Many cryptographic protocols are based on arithmetic in cyclic groups. A typical example is the subgroup 〈g〉 of (ℤ/pℤ)∗ generated by g ∈ (ℤ/pℤ)∗. The analogon for elliptic curves is 〈P〉 where P is a point on an elliptic curve over a finite field. The general idea is to replace the operation gk in (ℤ/pℤ)∗ by

![](images/157_1.jpg)

on the elliptic curve. For the efficient computation of k ⋅ P, you can use fast exponentiation with the only difference that multiplication is replaced by addition. For the sake of security, certain requirements have to be met by the subgroup 〈P〉 generated by P: for example, this group should be large, and its order should have a large prime divisor. The advantage of elliptic curves is that the same level of security as in (ℤ/pℤ)∗ can already be achieved with smaller key lengths. This is mainly because algorithmic techniques that rely on linear algebra seem not to work over elliptic curves: for instance, to date there has been no efficient adaptation of the quadratic sieve or the index calculus algorithm.

### 5.2.1 Diffie–Hellman key exchange with elliptic curves

We use Diffie and Hellman’s key exchange protocol as an example of how to apply elliptic curves in cryptography; see [Section](#chapter02_1.xhtml_chapter02_1_30) 2.9 for the classical version. Alice and Bob wish to agree upon a common key which is not known to anybody else. The common key could then be used for a symmetric encryption method such as AES. The problem is that all communication between Alice and Bob can be intercepted.

First, Alice chooses an elliptic curve Ẽ(ℤ/pℤ) together with a point P = (x, y) on this curve. The naive approach for this is to choose the parameters A, B, and p of the curve as well as a random element x such that x3 + Ax + B is a square in ℤ/pℤ; and then Alice computes y as a square root of x3 + Ax + B modulo p. This could be done using Tonelli’s or Cipolla’s algorithm or, as in the Rabin cryptosystem, she could rely on special prime numbers p for which the extraction of roots is easy. The following procedure is much simpler: Alice first chooses a large prime number p and elements A, x, y ∈ ℤ/pℤat random, and then she computes B = y2 −x3−Ax mod p. The elliptic curve Ẽ(ℤ/pℤ) is fully defined by the parameters A, B, and p. By construction, the point P = (x, y) lies on the curve.

Alice sends the public key (p, A, B, x, y) to Bob. As a secret key, Alice chooses a ∈ ℕ. Then, she sends the coordinates of the point a ⋅ P to Bob. Bob proceeds analogously. He chooses a secret number b ∈ ℕ and sends b ⋅ P to Alice. They are now both able to compute the point

![](images/157_3.jpg)

Neither of them needs to know the other’s secret key. The point Q can be used as their common secret key (for example by taking the first n bits of the binary representation). The computation of a, when given P and a⋅P, is exactly the discrete logarithm to base Pin the group E ̃(ℤ/pℤ). One can therefore assume that intercepting the communication does not help in retrieving the secret key. The computation of Q, when given the points P, a ⋅ P and b ⋅ P, is known as the Diffie–Hellman problem, and it is believed not to be efficiently solvable.

We note that the ElGamal cryptosystem can also be adapted to elliptic curves in the very same way as the Diffie–Hellman key exchange protocol.

### 5.2.2 Pseudocurves

The proof of the group laws for E ̃(K) in [Section 5.1](#chapter05_1.xhtml_chapter05_1_11) relies on the fact that K is a field. Now, we consider elliptic curves over quotient rings ℤ/nℤ. If n is composite, then such rings are not fields. Thus, we cannot rely on validity of the group laws anymore. Even the sum of two points is not necessarily defined in all cases since the denominators in the above computations need not be invertible.

Let n ∈ ℕ be an odd number greater than 1 and let A, B ∈ ℤ such that gcd(4A3 + 27B2, n) = 1\. The pseudocurve defined by the parameters A and B is

![](images/158_4.jpg)

The name pseudocurve shall indicate that ℤ/nℤ does not need be a field. As usual, we identify ℤ/nℤ with {0, . . . , n − 1}. We transfer the addition operation from elliptic curves to pseudocurves, but with the restriction that the sum is only partially defined. The point at infinity ![](images/o.jpg) is neutral and for P = (x1, y1) and Q = (x2, y2) in Ẽ(ℤ/nℤ)\{O}, we define P + Q as follows.

(a)If gcd(x2 − x1, n) = 1, then let ![](images/158_2.jpg)

(b)If x1 = x2 and y1 = y2 with gcd(y1, n) = 1, then we define ![](images/158_3.jpg)

In both cases, we define the addition P + Q = (x3, y3) by x3 = μ2 − x2 − x1 and y3 = μ(x1 − x3)− y1. All computations are modulo n.

(a)If x1 = x2 and y1 = −y2, we define P + Q = O.

There are three possibilities for P + Q to be undefined. First, we could have x1 ≢ x2 mod n, but x2 − x1 is not in (ℤ/nℤ)∗. Second, we could have P = Q, but y1 is not in (ℤ/nℤ)∗. And the third possibility for composite numbers n is x1 ≡ x2 mod n but y1 ≢ ±y2 mod n.

Theorem 5.6. Let P, Q ∈ Ẽ(ℤ/nℤ) such that P + Q is defined. Then, P + Q ∈ Ẽ(ℤ/nℤ).

Proof: We may assume that P ≠ ![](images/o.jpg) and Q ≠ O. Let P = (x1, y1) and Q = (x2, y2). First, suppose that x2 − x1 is invertible modulo n. In this case, the claim essentially follows from the derivation (see [Section 5.1.1](#chapter05_1.xhtml_chapter05_1_12)) of the earlier given formulas. However, a few minor adjustments are necessary. Let μ ≡ (y2 − y1)⋅ (x2 − x1)−1 mod n. Then, P + Q = (x3, y3) with x3 = μ2 − x2 − x1 mod n and y3 = μ(x1 − x3)− y1 mod n. For ν ≡ y1 − μx1 mod n, we have

![](images/159_10.jpg)

Therefore, P and Q are points on the line Y = μX + ν over ℤ/nℤ. Let s(X) = X3 + AX + B and g(X) = μX + ν. Both x1 and x2 are roots of the polynomial t(X) = s(X) − g2(X) of degree 3 over ℤ/nℤ. From [Corollary 1.47](#chapter01_3.xhtml_chapter01_3_10), we obtain t(X) = (X − x1)r(X) for a polynomial r of degree 2\. Since x2 − x1 is invertible, x2 is a root of r. Together with the degree formula from [Theorem 1.42](#chapter01_3.xhtml_chapter01_3_1) this yields

![](images/159_11.jpg)

for x̂̂3 ∈ ℤ/nℤ. By comparing the coefficients at X2, we see that x̂3 ≡ x3 mod n. For ŷ3 = g(x3),we have ![](images/159_3.jpg) mod n and thus (x3, ŷ̂3) ∈ Ẽ(ℤ/nℤ). Moreover, ŷ3 = μx3 + ν ≡ −μ(x1 − x3) + y1 ≡ −y3 mod n shows P + Q = (x3, y3) ∈ Ẽ(ℤ/nℤ).

The second case is x1 ≡ x2 mod n. We can exclude the case that y1 ≡ −y2 mod n because the point at infinity belongs to Ẽ(ℤ/nℤ). Since P + Q is defined, we can conclude that y1 ≡ y2 mod n and that 2y1 is invertible modulo n; remember that n is odd. In particular, P = Q. Let P+Q = 2P = (x3, y3) in Ẽ(ℤ/nℤ).We use closure of the operation on elliptic curves over ℚ. We interpret x1, y1 ∈ {0, . . . , n −1} ⊆ℚ. Let B' = B + kn with

![](images/159_12.jpg)

Let E' be the curve defined by A and B. Then, Ẽ(ℤ/nℤ) = Ẽ(ℤ/nℤ) and P = (x1, y1)∈ Ẽ(ℚ). Due to the addition rules, there exist ![](images/159_5.jpg) with

![](images/159_6.jpg)

and ![](images/159_7.jpg) mod n as well as ![](images/159_8.jpg) mod n. Here, (2y1)−2 denotes the inverse of (2y1)2 modulo n. Now, 2P ∈ Ẽ(ℚ) yields (x3, y3) ∈ Ẽ(ℤ/nℤ).

□

Let m > 1 be a divisor of n. Then, E ̃(ℤ/mℤ) inherits the property of being a pseudocurve from Ẽ(ℤ/nℤ). By the homomorphism theorem for rings, we know that mod m: ℤ/nℤ → ℤ/mℤ: x ↦ x mod m is a ring homomorphism. We extend this mapping to points P = (x, y) ∈ Ẽ(ℤ/nℤ) by

![](images/159_9.jpg) P mod m = (x mod m, y mod m)

and define ![](images/o.jpg) mod m = O. If P is a point on the pseudocurve Ẽ(ℤ/nℤ), then P mod m is a point on the pseudocurve Ẽ(ℤ/mℤ). An important special case of this modulo operation on curve points occurs if m is prime. Then, E ̃(ℤ/mℤ) is an elliptic curve since m > 2 and 4A3 + 27B2 ≠ 0 in ℤ/mℤ. The following theorem connects the operations on the two pseudocurves. The main problem is that P + Q in E ̃(ℤ/nℤ) might a priori be obtained by different formulas than (P mod m)+(Q mod m) in Ẽ(ℤ/mℤ). We show that this cannot happen.

Theorem 5.7. Let m > 1 be a divisor of n and let P, Q ∈ Ẽ(ℤ/nℤ) be points such that P + Q is defined. Then, (P mod m) + (Q mod m) in Ẽ(ℤ/mℤ) is defined and

![](images/160_5.jpg)

Proof: We may assume that P = (x1, y1) ≠ ![](images/o.jpg) and Q = (x2, y2) ≠ O. The ring homomorphism mod m: ℤ/nℤ → ℤ/mℤ is compatible with forming inverses, that is, for gcd(x, n) = 1 we have

![](images/160_6.jpg)

On the left-hand side of the equation, (x mod n)−1 denotes the inverse of x modulo n while, on the right-hand side, the element x mod m is inverted in ℤ/mℤ. If we apply the same formulas for the addition of the points in Ẽ(ℤ/nℤ) and Ẽ(ℤ/mℤ), then the homomorphism property yields the desired result. In particular, the sum (P mod m)+ (Q mod m) is defined in this situation. The remaining cases are

(a)x1 ≢ x2 mod n and x1 ≡ x2 mod m

(b)x1 ≡ x2 mod n, y1 ≡ y2 ≢ 0 mod n and y1 ≡ −y2 mod m

(c)x1 ≡ x2 mod n and y1 ≢ ±y2 mod n

In case (a), the sum P + Q is not defined because x2 − x1 is divisible by m and therefore not invertible modulo n. Thus, the requirements of the theorem are not satisfied. In case (b), the sum P + Q is not defined either because 2y1 ≡ y1 + y2 mod n and m | y1 + y2. Thus, 2y1 is not invertible modulo n. If case (c) occurs, then again P + Q is not defined.

□

### 5.2.3 Factorization using elliptic curves

In order to factorize an integer n > 1, you try to find m ∈ {2, . . . , n − 1} with m | n. Although still unproven, the factorization of binary numbers is considered to be not solvable in polynomial time. Therefore, a factorization algorithm is only taken into account after you have checked that the number in question is composite. We already discussed several primality tests. A second typical preparatory step is to exclude small divisors by trial divisions. The idea of using elliptic curves for factorization was derived by Hendrik Willem Lenstra Jr. (born 1949). In the following, we present a probabilistic variant of this approach. The basic idea is Pollard’s p − 1 algorithm, which we repeat briefly. Let n be a composite number, p a prime factor of n and let a ∈ ℕ with gcd(a, n) = 1.We assume that k ∈ ℕ is a multiple of p − 1\. By Fermat’s little theorem, we have ap−1 ≡ 1 mod p, and thus also

![](images/160_4.jpg)

Now p | ak −1 and p | n. If ak ≢ 1 mod n then gcd(ak −1, n) yields a nontrivial divisor of n. In this method, we have some freedom in the choice of a and k. Apossible strategy for choosing k is motivated by the hope that p − 1 can be factorized into small prime divisors. Since we do not know p at this point, you could choose k as

![](images/161_1.jpg)

Here, C is an expected upper bound for the prime divisor of p − 1\. In order to keep k within a reasonable size, C must not be too large. For a, an arbitrary value from (ℤ/nℤ)∗ can be chosen. The disadvantage of the method is that the structure of ℤ/nℤ cannot be changed. If, for example, no prime factor p of n has the property that p − 1 has only small prime divisors, then Pollard’s p − 1 algorithm is not successful. This is where pseudocurves come into play because, for every n, there are numerous pseudocurves Ẽ(ℤ/nℤ).

Lenstra’s method also starts by choosing a bound C and constructing a number k as before. The greater the number C, the better the chance of finding a divisor. However, the time for the computation also grows with C. The idea is to randomly select a pseudocurve Ẽ(ℤ/nℤ) and a point P ∈ Ẽ(ℤ/nℤ). Then, you try to compute k ⋅ P with the hope that, at some point in this computation, the sum of two points is undefined. This will then yield a nontrivial divisor of n. If the computation of k ⋅ P is successful, then we repeat this step with another pseudocurve. This is not possible with Pollard’s p − 1 algorithm.

We now discuss the details of the method. The algorithm first chooses A, x, y ∈ {0, . . . , n − 1} at random. Then, B is computed by

![](images/161_3.jpg)

If gcd(4A3 + 27B2, n) ≠ 1, then we either found a nontrivial divisor of n or we repeat the process. The pseudocurve Ẽ(ℤ/nℤ) is now given by the equation Y2 = X3 + AX + B with gcd(4A3 + 27B2, n) = 1 and the point on Ẽ(ℤ/nℤ) is P = (x, y).

Remark 5.8. If we determined A and B first, then it would be harder to find a nonzero point on the curve. Note that neither Tonelli’s nor Cipolla’s algorithm can be used for the extraction of roots since ℤ/nℤ is not a field.

◊

The operation on pseudocurves need not be defined for all possible arrangements of parentheses. For example, in the computation of 5 ⋅ P, it is possible that ((P + P) + (P + P)) + P is defined whereas (P + P) + ((P + P) + P) is undefined. The difference here is that, in the second case, 3 ⋅ P = (P + P) + P occurs as an intermediate result. Moreover, for two different parentheses, where all intermediate results are defined, we cannot expect that both of them yield the same result. This problem is circumvented by using a fixed algorithm for the computation of k ⋅ P. Thus, the parenthesis is uniquely determined by k. We can view k ⋅ P as the result produced by this particular algorithm. This result can also be undefined. To compute k ⋅ P as efficiently as possible, you use fast exponentiation with addition rather than multiplication as operation.

Proposition 5.9. If the operation Q + R for two points Q, R ∈ Ẽ(ℤ/nℤ) is not defined, this yields a nontrivial divisor of n.

Proof: Let Q = (x1, y1) and R = (x2, y2). If Q + R is undefined, then there are three possible reasons. The first one is that x1 ≢ x2 mod n, but x2 − x1 is not invertible modulo n. In this case, x2 − x1 is not a multiple of n and not coprime to n. Thus, gcd(x2 − x1, n) is a nontrivial divisor of n. The second possibility is x1 ≡ x2 mod n and y1 ≡ y2 ≢ 0 mod n, but y1 is not invertible modulo n. Now, gcd(y1, n) yields a nontrivial divisor of n. The third case is x1 ≡ x2 mod n, but y1 ≢ ±y2 mod n. We have

![](images/162_1.jpg)

Therefore, ![](images/162_2.jpg) is a multiple of n, but neither y2 + y1 nor y2 −y1 is a multiple of n. But then both gcd(y2 + y1, n) and gcd(y2 −y1, n) are nontrivial divisors of n.

□

If the operation Q + R for two points Q and R during an intermediate step in the computation of k ⋅ P is not defined, then we obtain a nontrivial divisor of n. It remains to explain why we can hope for some addition during the computation to be undefined. Let p ≥ 3 be a prime factor of n. Then, Ẽ(ℤ/pℤ) is an elliptic curve. The hope is that the order of Ẽ(ℤ/pℤ) has only small prime divisors because then k ⋅ (P mod p) = ![](images/o.jpg) in Ẽ(ℤ/pℤ). It is very unlikely that, for all other prime divisors q of n, we also have k ⋅ (P mod q) = ![](images/o.jpg) in Ẽ(ℤ/qℤ). From [Theorem 5.7](#chapter05_2.xhtml_chapter05_2_10), it follows that k ⋅ P is not defined in Ẽ(ℤ/nℤ); otherwise k ⋅ P = ![](images/o.jpg) would follow because only the point at infinity is mapped to the point at infinity mod p. This in turn would imply k ⋅ (P mod q) = ![](images/o.jpg) in Ẽ(ℤ/qℤ), contradicting our assumption.

### 5.2.4 Goldwasser–Kilian primality certificates

The idea behind a primality certificate is to provide an efficiently verifiable proof. If a number n has a primality certificate, then the proof should show that n is prime with absolute certainty. One such approach goes back to Henry Cabourn Pocklington (1870–1952).

Theorem 5.10 (Pocklington). Let a, k, n, q ∈ ℕ with n − 1 = q ⋅ k and q > k. Suppose that the following properties are satisfied:

(a)q is prime

(b)an−1 ≡ 1 mod n and

(c)gcd(ak − 1, n) = 1.

Then, n is prime.

Proof: Suppose that n is composite. Then there exists a prime divisor p of n with ![](images/162_3.jpg) Let d be the order of a in (ℤ/pℤ)∗. From (b), we obtain an−1 ≡ 1 mod p. Therefore, d is a divisor of n − 1. From (c), we obtain that d does not divide k. Then, (a)yields that q is a divisor of d. Altogether, we have ![](images/163_1.jpg) But q > k yields ![](images/163_2.jpg) a contradiction. Consequently, n is prime.

□

Example 5.11. We present a proof for the primality of 2 922 259 that (with the help of a computer) can easily be checked. We have 2922259 − 1 = 1721 ⋅ 1698 and

![](images/163_9.jpg)

Both facts can be checked efficiently using fast modular exponentiation and the Euclidean algorithm. If we knew that 1721 is prime, then Pocklington’s theorem would show that 2 922 259 is prime. We use the same approach to give a proof for the primality of 1721\. We have 1721 − 1 = 43 ⋅ 40 and

![](images/163_10.jpg)

Finally, we “prove” that 43 is prime since 43 − 1 = 7 ⋅ 6 and

![](images/163_12.jpg)

Since we know that 7 is prime, the number 43 is prime, too. This in turn implies that 1721 is prime and finally that 2 922 259 is prime. The primality certificate consists of all numbers involved in the proof given earlier:

![](images/163_11.jpg)

The process (in reverse order) can also be used to produce “provable” primes.

◊

The problem with Pocklington’s primality certificates is that they only work for numbers n where n − 1 has a large prime factor. Shafrira Goldwasser (born 1958) and Joseph John Kilian’s algorithm carries Pocklington’s idea over to elliptic curves. Here, by choosing different curves, numerous groups are available. Similar to the situation with integer factorization, one would apply this method only if n has passed a probabilistic primality test such as the Miller–Rabin test.

Theorem 5.12 (Goldwasser and Kilian 1986). Let n ∈ ℕ and let Ẽ(ℤ/nℤ) be a pseudocurve. Let ![](images/o.jpg) ≠ P ∈ Ẽ(ℤ/nℤ) and ![](images/163_7.jpg) a prime number. If q ⋅ P = ![](images/o.jpg) in Ẽ(ℤ/nℤ), then n is prime.

Proof: Let q ⋅ P = ![](images/o.jpg) in E ̃(ℤ/nℤ) and suppose that n is composite. Then there exists a prime factor p of n with ![](images/163_8.jpg) Let d be the order of P mod p in the elliptic curve Ẽ(ℤ/pℤ). From [Theorem5.7](#chapter05_2.xhtml_chapter05_2_10), we have q ⋅ (P mod p) = ![](images/o.jpg) in Ẽ(ℤ/pℤ). This implies d | q. Since q is prime and d ≠ 1, we obtain d = q. Thus, q ≤ |Ẽ(ℤ/pℤ)|. According to the Hasse bound in equation ([5.1](#chapter05_1.xhtml_chapter05_1_9)), however, ![](images/164_1.jpg) and we have a contradiction.

□

Remark 5.13. If you require the stronger assumption ![](images/164_2.jpg) in [Theorem 5.12](#chapter05_2.xhtml_chapter05_2_16), then the statement can be shown without using the Hasse bound. Instead, the weaker (and easy to prove) estimate |Ẽ(ℤ/pℤ)| ≤ 2p + 1 in the earlier proof is sufficient. The assumption ![](images/164_3.jpg) is not a limitation for applications.

◊

Let us now describe Goldwasser and Kilian’s algorithm. An important step in this algorithm is to efficiently determine the number of points on an elliptic curve over a finite field. The first deterministic polynomial time algorithm for this task was derived by René Schoof (born 1955). If m = log(p) is the number of bits of the prime p, it takes ![](images/o.jpg)(m9) operations to compute |Ẽ(ℤ/pℤ)|, and thus in its original form it was not practicable. With some improvements, especially by Arthur Oliver Lonsdale Atkin (1925–2008) and Noam Elkies (born 1966), the computation essentially takes ![](images/o.jpg)(m4) operations. Another ingredient is a probabilistic algorithm for computing square roots in finite fields. This can be done with either Tonelli’s or Cipolla’s algorithm; see [Section 3.5](#chapter03_2.xhtml_chapter03_2_2).

We want to prove that n ∈ ℕ is prime. Moreover, the test shall provide a certificate for this property. For small numbers n, we can solve this by means of a table lookup. Therefore, we can assume n to be sufficiently large. First, by a probabilistic procedure, we convince ourselves that n is prime with high probability. Then, we choose a random pseudocurve Ẽ(ℤ/nℤ) and, for example by using Schoof’s algorithm, we compute the number |Ẽ(ℤ/nℤ)| under the assumption that n is prime. If this calculation is not possible, for example, due to a division by zero, then n is composite. We keep on searching for pseudocurves until |Ẽ(ℤ/nℤ)| = kq for a probable prime q which satisfies ![](images/164_4.jpg) Before we certify q as prime, we choose a random point P = (x, y) on Ẽ(ℤ/nℤ). For this, we repeatedly choose x ∈ ℤ/nℤat random until y ∈ ℤ/nℤ is found such that y2 ≡ x3 +Ax+B mod n. To determine y, we use one of the randomized methods for extracting roots in finite fields. Should the process fail, then the chances of finding a proper divisor of n are good, thus proving that n is composite. In the next step, we compute P'' = k ⋅P in Ẽ(ℤ/nℤ). If k ⋅P is not defined, then n is composite. If P' = ![](images/o.jpg), we search for a new point P ∈ Ẽ(ℤ/nℤ). For P' ≠ ![](images/o.jpg), the point P' must have the order q, otherwise n is composite. If the computation of q ⋅P' = ![](images/o.jpg) in Ẽ(ℤ/nℤ) is successful, then from [Theorem 5.12](#chapter05_2.xhtml_chapter05_2_16), we obtain that n is prime, provided that q is prime. Therefore, we apply the method recursively on input q and thus certify q to be prime. The certificate for the primality of n consists of the parameters of Ẽ(ℤ/nℤ), the point P, and the number q together with a certificate for its primality. If this algorithm yields a result, this result is always correct. However, it cannot be guaranteed that the algorithm always terminates after finitely many steps and returns a result. Due to the diversity of elliptic curves, however, in practice it turns out that the algorithm terminates with very high probability. Moreover, its running time can compete with the AKS algorithm from [Chapter 4](#chapter04.xhtml_chapter04_1) (and, in contrast to the AKS algorithm, it additionally yields a primality certificate, which can be verified efficiently).

## 5.3 Endomorphisms of elliptic curves

In the previous section, we used the Hasse bound from Equation ([5.1](#chapter05_1.xhtml_chapter05_1_9)) to improve the performance of the Goldwasser–Kilian primality test. Without the Hasse bound, we obtain a sufficiently good but slightly weaker result. On the other hand, the Hasse bound is indispensable for a deeper understanding of elliptic curves. The known proofs of this formula are based on the study of endomorphisms. This section provides an introduction to the basic concepts and theorems concerning endomorphisms of elliptic curves. The proofs of many results in this section make nice exercises.

Let k be an algebraically closed field with a characteristic different from 2, and let E(k) be the elliptic curve defined by Y2 = X3 +AX+B. In particular, s(X) = X3 +AX+B has no multiple roots. In [Section 5.1.2](#chapter05_1.xhtml_chapter05_1_16), we defined the polynomial ring k[x, y] over E (k) as

![](images/165_1.jpg)

The element x ∈ k[x, y] is the residue class of X and y is the residue class of Y. In k[x, y], we have y2 = s(x). The image of k[X] in k[x, y] is denoted by k[x]. Since y2 = s(x) in k[x, y], we have y2 ∈ k[x]. Every polynomial f ∈ k[x, y] can uniquely be written as f = υ(x) + yw(x) with υ(x), w(x) ∈ k[x]. Let ![](images/165_2.jpg) Then, ![](images/165_3.jpg) is the norm of f. We have N(f) = 0 if and only if f = 0\. The ring k[x, y] has no zero divisors: if fg = 0 in k[x, y], then N(f)N(g) = 0 in k[x], and therefore N(f) = 0 or N (g) = 0\. Thus, k[x, y] is an integral domain.

We can form the field k(x, y) consisting of all fractions ![](images/165_4.jpg) for polynomials p(x, y), q(x, y) ∈ k[x, y] with q(x, y) ≠ 0\. Two fractions ![](images/165_6.jpg) and ![](images/165_5.jpg) define the same element of k(x, y) if and only if p(x, y)υ(x, y) = u(x, y)q(x, y) in k[x, y]. Addition and multiplication are defined in the same way as for “usual” fractions. We call k(x, y) the function field of E(k); its elements are rational functions. A rational function ![](images/165_7.jpg) induces a (partial) mapping E(k) → k by (a, b) ↦ r(a, b) for P = (a, b) ∈ E (k), and this mapping is defined for almost all P ∈ E(k); it is undefined if and only if q(a, b) = 0.

Lemma 5.14. If two rational functions r(x, y) and t(x, y) in k(x, y) coincide at infinitely many points P ∈ E(k), then r(x, y) = t(x, y).

Proof: Let ![](images/165_8.jpg) and ![](images/165_9.jpg) for p, q, u, υ ∈ k[x, y]. Then, pυ coincides with uq at infinitely many points P ∈ E (k). By [Lemma 5.2](#chapter05_1.xhtml_chapter05_1_18), we see that pυ = uq and thus r = t. If r = p/q for p, q ∈ k[x, y], then we can multiply both the numerator and the denominator by q. This shows that every rational function r(x, y) can be written as

□

![](images/166_1.jpg)

with u(x), υ(x), w(x) ∈ k[x] and w(x) ≠ 0.

The order of a point (see [Theorem 5.3](#chapter05_1.xhtml_chapter05_1_20)) is a concept which can also be applied to rational functions. For r = p/q ∈ k(x, y) and P ∈ E (k), let dp and dq be the orders of p and q at P, respectively. The difference d = dp − dq is a well-defined integer and we call d ∈ ℤ the order of r at P. For d ≥ 0, the image r(P) is defined; this is the case for almost all points of the curve. For d > 0 we speak of a zero or root, and for d < 0 we speak of a pole. By [Theorem 5.4](#chapter05_1.xhtml_chapter05_1_22), rational functions without poles are polynomials.

If the field k has characteristic p > 2 and if A and B belong to a finite field extension q of the prime field p, then we consider the Frobenius automorphism k → k, a ↦ aq. For a ∈ k, we have a = aq if and only if a ∈ q. In particular, Aq = A and Bq = B. Hence, sq(x) = s(xq). It follows that the Frobenius mapping

![](images/166_4.jpg)

is well defined and bijective because for all x, y ∈ k, we have y2 = s(x) if and only if y2q = sq(x) = s(xq). Whenever we mention the Frobenius mapping ϕq in the remainder of this section, we implicitly assume that A, B ∈ q and that q is a prime power.

Let ρ : E (k) → E (k) be a partial function such that there exist rational functions r(x, y), t(x, y) ∈ k(x, y) which satisfy ρ(P) = (r(P), t(P)) for all points P in the domain of ρ. We call ρ a rational morphism if it is defined almost everywhere. The domain of ρ must not contain the poles of r or t. Note that ρ uniquely determines the two rational functions r(x, y) and t(x, y). The composition of rational morphisms is again a rational morphism. The Frobenius mapping ϕq is a typical example of a rational morphism; it is therefore called the Frobenius morphism. Moreover, ϕq is defined everywhere and it is bijective.

We give two important examples of rational morphisms. For every point T = (a, b) ∈ E(k), the translation τ defined by τ(P) = P + T is rational because for all (x, y) ∈ E(k) \ {T, −T}, we have τ(x, y) = (xT , yT) with

![](images/166_3.jpg)

It is just as easy to see that σ(P) = 2P is a rational morphism. A point (x, y) ∈ E (k) with y ≠ 0 satisfies σ(x, y) = (x̂, ŷ) for

![](images/167_1.jpg)

The morphism σ also defines a group homomorphism. This leads to the following notion. An endomorphism of E (k) is a group homomorphism of E ̃(k) into itself, which is either trivial (i.e., it maps E(k) to ![](images/o.jpg)) or it coincides with a rational morphism almost everywhere. We immediately see that nontrivial endomorphisms have a finite kernel because the image of almost every point is in E (k) and, thus, different from O.

Lemma 5.15. If endomorphism α and β coincide at almost all points of E (k), then α = β.

Proof: We may assume that α and β are nontrivial. Let P ∈ E (k). We show that α(P) = β(P). For almost every point T ∈ E(k), we have α(P + T) = β(P + T) ≠ ![](images/o.jpg), and almost all points T ∈ E (k) satisfy α(T) = β(T) ≠ ![](images/o.jpg). We can therefore choose some point T which satisfies both properties. Since α and β are homomorphisms, we obtain

□

![](images/167_4.jpg)

If we set ϕq(![](images/o.jpg)) = ![](images/o.jpg), then the following theorem shows that ϕq is an endomorphism.

Theorem 5.16. The Frobenius morphism ϕq is an endomorphism.

Proof: See [Exercise 5.9](#chapter05_3.xhtml_chapter05_3_25).

□

Theorem 5.17. The endomorphisms form a ringwith the operations defined by (α + β)(P) = α(P) + β(P) and (α ⋅ β)(P) = α(β(P)).

Proof: The endomorphisms of an Abelian group form a ring with these operations. Thus, we only have to show the closure as rational morphisms. This is clear for composition. See [Exercise 5.7](#chapter05_3.xhtml_chapter05_3_23) for addition.

□

The following lemma provides a normal form of endomorphisms.

Lemma 5.18. Let α be a nontrivial endomorphism. Then there exist polynomials p(x), q(x), u(x), υ(x) ∈ k[x] such that ![](images/167_3.jpg) for almost all points (x, y) ∈ E (k). Moreover, neither p(x)/q(x) nor u(x)/υ(x) is constant.

Proof: See [Exercise 5.8](#chapter05_3.xhtml_chapter05_3_24).

□

Theorem 5.19. Let α be an endomorphism with α(P) = (r(P), t(P)) for almost all points P ∈ E (k). Then the following properties hold:

(a)α(P) = (r(P), t(P)) for all points P ∈ E (k) such that r(P) is defined.

(b)The kernel of α is the set of points P ∈ E (k) for which r(P) is not defined.

Proof: By [Lemma 5.18](#chapter05_3.xhtml_chapter05_3_5), we can assume that ![](images/168_2.jpg) and ![](images/168_1.jpg) Therefore, almost all (x, y) ∈ E (k) satisfy

![](images/168_3.jpg)

We may assume that u (x) and υ(x) have no common roots. Since all roots in the denominator υ(x) appear twice, but x3+Ax+B only has simple roots, ![](images/168_4.jpg) has to have a pole at all roots of υ(x). Thus, υ(x) = 0 implies q(x) = 0\. In other words, if r(P) is defined, then t(P) is defined. The rational morphism ρ given by ρ(P) = (r(P), t(P)) is therefore defined at all points where r does not have a pole.

For property (a) it remains to show that ρ(P) = α(P) holds for all points P ∈ E(k) such that ρ(P) is defined. This is done by applying the proof technique from [Lemma 5.15](#chapter05_3.xhtml_chapter05_3_3); the main difference is that we cannot assume ρ to be an endomorphism. For almost all points T ∈ E(k), the mapping P ↦ ρ(P + T) − ρ(T) for P ∈ E(k) is a rational morphism, that is, there exist rational functions r̂, t̂ ∈ k(x, y) such that the rational morphism ρT = (r̂, t̂̂) coincides with this mapping at almost all points P. The image ρT(P) is defined if and only if both r̂(P) and t̂( P) are defined. Note that ρT(P) could be defined even if ρ(P + T) is undefined; for instance, this could be the case for P = −T. Let T be a point such that ρ(T) is defined and it satisfies ρ(T) = α(T). For almost all points P ∈ E(k), we have

![](images/168_5.jpg)

This shows that ρT coincides with α at almost all P and, hence, ρT coincides with ρ at almost all points P. By [Lemma 5.14](#chapter05_2.xhtml_chapter05_2_20), we obtain r̂ = r and t̂ = t, that is, ρT = ρ. Consider a point P ∈ E(k) in the domain of ρ. There exists a point T such that ρ(P+T) = α(P+T) and ρ(T) = α(T). This yields ρ(P) = ρT(P) = α(P), as desired.

For property (b), we show that ρ(P) is defined if and only if α(P) ≠ O. The implication from left to right follows from property (a). For the other direction, let α(P) ≠ ![](images/o.jpg). We find a point T such that ρ(P + T) = α(P + T) and ρ(T) = α(T), and this yields α(P) = ρT(P) = ρ(P). In particular, ρ(P) is defined.

□

Let α be an endomorphism with ![](images/168_6.jpg) for almost all (x, y) ∈ E(k) such that the polynomials p(x) and q(x) have no common roots. The degree of α is

![](images/168_7.jpg)

Note that, by [Lemma 5.14](#chapter05_2.xhtml_chapter05_2_20), the degree of a nontrivial endomorphism is well defined. We call α separable if one of the derivatives p(x) or q(x) is not the zero function. The Frobenius endomorphism ϕq has degree q, but it is not separable. A direct computation shows that multiplication by 2, that is α(P) = 2P, is separable ([Exercise 5.10](#chapter05_3.xhtml_chapter05_3_26)). The degree of α is 4\. This can be computed directly but it also follows from the next theorem.

Theorem 5.20. The following properties hold for each nontrivial endomorphism α:

(a)The group homomorphism α is surjective.

(b)If α is separable, then |ker(α)| = deg(α).

(c)If α is not separable, then |ker(α)| < deg(α).

Proof: We start with the proof of surjectivity. Let P ∈ E(k). Obviously P = (P + T) − T for all T ∈ E(k). If both (P + T) and T belong to the image of α, then so does P. It therefore suffices to show that for almost every point P ∈ E(k) there exists Q ∈ E (k) with α(Q) = P. In particular, we do not need to consider the three points P with P = −P.

Let p(x), q(x), u(x), υ(x) ∈ k[x] be the polynomials given by [Lemma 5.18](#chapter05_3.xhtml_chapter05_3_5). Moreover, we assume that p(x) and q(x) have no common roots. For almost all points (c, d) ∈ E(k), the property α(c, d) = (a, b) implies p(c)/q(c) = a. In particular, c is a root of p(x) − aq(x). We therefore consider polynomials of the form p(x) − aq(x) for a ∈ k.

For almost all a ∈ k, we have deg(α) = degx(p(x) − aq(x)). Note that deg(α) ≥ 1 since p/q is not constant. If P = (a, b) ∈ E(k) is a point such that the polynomial p(x) − aq(x) is not constant, then there exists a root c of this polynomial. For this root, we find some element d ∈ k such that Q = (c, d) and −Q = (c, −d) are the only points on the curve E (k) with c as first component. By [Theorem 5.19](#chapter05_3.xhtml_chapter05_3_6), the first component of α(Q) is ![](images/169_1.jpg) Hence, there are only two possibilities: either α(Q) = P and α(−Q) = −P or α(Q) = −P and α(−Q) = P. Note that Q ≠ −Q since we only consider points P with P ≠ −P. This shows that every root of p(x) − aq(x) accounts for a unique point Q with α(Q) = P; we might have to replace d by −d. In particular, this shows that α is surjective. In addition, since p(x)−aq(x) has at most deg(α) roots, this shows that |ker(α)| = |α−1(P)| ≤ deg(α). If α is not separable, then the derivative p'(x)− aq'(x) of p(x)− aq(x) is zero. In particular, p(x)− aq(x) has multiple roots; this yields |ker(α)| < deg(α).

For the remainder of this proof, let α be separable. Let C ⊆ k be the set of roots of the polynomial p(x)q' (x) − p'(x)q(x). It remains to be shown that there exists a ∈ k such that the polynomial p(x) − aq(x) has no multiple roots and its degree is deg(α). Since there are infinitely many a such that the degree of p(x) − aq(x) is deg(α), there is such an a ∈ k \ {0} with a ≠ p(ĉ)/q(ĉ) for all ĉ ∈ C. Suppose that p(x) − aq(x) has a multiple root c, that is, p(c) − aq(c) = 0 and p'(c) − aq(c) = 0\. The multiplication of the two equations p(c) = aq(c) and aq'(c) = p'(c) yields ap(c)q' (c) = ap'(c)q(c). Since a ≠ 0, we obtain c ∈ C. This contradicts the choice of a because a = p(c)/q(c). If P = (a, b) is a point on the curve, then |ker(α)| = |α−1(P)| ≥ deg(α). This completes the proof of the theorem.

□

Remark 5.21. From [Exercise 5.11](#chapter05_3.xhtml_chapter05_3_27), the mapping P ↦ ϕq(P) − P defines the surjective endomorphism (ϕq − 1), and its kernel consists of the elliptic curve Ẽ(q).

To prove Hasse’s theorem, the following path can be taken. First, show that (ϕq − 1) is separable. Thus, the problem of determining |Ẽ(q)| is reduced to giving a bound for the degree of (ϕq − 1). This is rather difficult and technical. The proof typically uses the concept of Weil pairings and is, for example, presented in [[108](#Bibliography.xhtml_Bibliography_109)]. Weil pairings were defined in 1940 by André Weil (1906–1998).

◊

## Further reading

There is a huge number of scientific articles and textbooks on elliptic curves. Silverman’s book [[97](#Bibliography.xhtml_Bibliography_98)] is a standard reference. However, for the proofs, the author often refers, without further explanation, to the book by Robin Hartshorne (born 1938) on algebraic geometry [[48](#Bibliography.xhtml_Bibliography_48)], which treats the area in a very general way and uses the concept of schemes as defined by Alexander Grothendieck (1928–2014). Hartshorne’s book was not written to be an introduction to the theory of elliptic curves and, therefore, is not suitable for that purpose. A good introduction to the theory of elliptic curves is, for example, book by Washington [[108](#Bibliography.xhtml_Bibliography_109)]. We would further like to mention [[57](#Bibliography.xhtml_Bibliography_58), [65](#Bibliography.xhtml_Bibliography_66)]. Cryptographic applications of elliptic curves are also treated in textbooks such as [[58](#Bibliography.xhtml_Bibliography_59)] by Neal Koblitz (born 1948). However, this book does not prove the group structure. (The proof of the group structure of elliptic curves as given here uses the method of “divisors” and requires no knowledge beyond the scope of the current book.) Koblitz and Victor Saul Miller (born 1947) are considered to be co-founders of elliptic curve cryptography (ECC), see [[56](#Bibliography.xhtml_Bibliography_57)] and [[76](#Bibliography.xhtml_Bibliography_76)]. Since the mid-1980s, cryptography using elliptic curves has developed rapidly and become the most established method in practice other than the RSA cryptosystem.

## Exercises

5.1. A general elliptic curve is defined by an equation of the following type:

![](images/170_1.jpg)

(a)Show that over fields of characteristic different from 2, Equation ([5.2](#chapter05_3.xhtml_chapter05_3_19)) can be transformed into the following form by changing coordinates:

![](images/170_2.jpg)

(b)Show that over fields of characteristic different from 3, Equation ([5.3](#chapter05_3.xhtml_chapter05_3_20)) can be transformed into Weierstrass normal form Y2 = X 3 + AX + B by a coordinate shift of X.

5.2. Show that the polynomial X 3 + AX + B has multiple zeros if and only if 4A3 + 27B2 = 0\. Make sure that your reasoning is also valid for characteristic 2 and 3.

5.3. Let p ≥ 3 be prime and let E be an elliptic curve over ![](images/f_d.jpg)p defined by Y2 = X3 + AX + B. For a ∈ ![](images/f_d.jpg)p we let

![](images/171_1.jpg)

Show that ![](images/171_2.jpg)

5.4. Let E be the curve defined by Y2 = X3 + X + 6 over the field 11.

(a)Show that X3 + X + 6 has no multiple roots in the algebraic closure of 11.

(b)Show that Ẽ(11) is cyclic.

5.5. Let E be the curve defined by Y2 = X3 + X over the field 5.

(a)Show that X3 + X has no multiple roots in the algebraic closure of 5.

(b)Show that Ẽ(5) is isomorphic to the Klein four-group ℤ/2ℤ × ℤ/2ℤ.

Note: In the following exercises, let E (k) always be an elliptic curve given by the equation Y2 = X3 + AX + B over an algebraically closed field k of characteristic different from 2\. Moreover, let 4A3 + 27B2 ≠ 0.

5.6. Show that { P ∈ Ẽ(k) | 3P = ![](images/o.jpg)} is isomorphic to the group ℤ/3ℤ × ℤ/3ℤ.

5.7. Show that, for endomorphisms α and β of an elliptic curve, α + β defined by (α + β)(P) = α(P) + β(P) is also a rational morphism.

5.8. Let α be a nontrivial endomorphism. Show that there exist polynomials p(x), q(x), u(x), υ(x) ∈ k[x] such that ![](images/171_3.jpg) for almost all (x, y) ∈ E(k). In addition, show that neither p(x)/q(x) nor u(x)/υ(x) is constant.

5.9. Show that the Frobenius morphism ϕq is an endomorphism.

Hint: Use that E ̃(k) = Pic0(E(k)) by [Theorem 5.5](#chapter05_2.xhtml_chapter05_2_1).

5.10. Show that the endomorphism α(P) = 2P of E (k) is separable.

5.11. Show that the mapping P ↦ ϕq(P) − P defines a surjective endomorphism (ϕq − 1) and that the kernel consists of the elliptic curve E ̃(q) over q.

## Summary

Notions

–elliptic curve E and E ̃

–point at infinity O

–inverse point![](images/171_4.jpg)

–line, vertical

–addition of points

–polynomial ring over E

–norm N(f)

–degree of a polynomial deg(f)

–order ordP(f)

–divisor

–degree of a divisor deg(D)

–principal divisor div(f)

–Picard group Pic0 (E)

–pseudocurve

–primality certificate

–rational function

–function field

–order of a rational function at P

–zeros and poles

–rational morphism

–Frobenius morphism ϕq

–endomorphism ring

–degree of an endomorphism

–separable endomorphism

Methods and results

–For each elliptic curve E over q, we have |E| ≤ 2q and |Ẽ| ≤ 2q + 1.

–Over algebraically closed fields, every line intersects a curve E ̃ at three points (with multiplicities).

–The addition P + Q = −R is chosen such that P, Q, R are located on a line.

–Every polynomial f ≠ 0 has only finitely many roots on a curve E.

–The representation f = υ(x) + yw(x) in k[x, y] is unique.

–The order of a root of f ∈ k[x, y] is uniquely determined.

–If f ≠ 0 ≠ h and ordP(f) ≤ ordP(h) for all P ∈ E, then f divides h.

–ordP(f ⋅ g) = ordP(f) + ordP(g)

–div(f ⋅ g) = div(f) + div(g)

–deg(f) = deg(div(f))

–E ̃ and Pic0(E) are isomorphic; in particular, E ̃ is a group.

–construction of a point P and a curve E with P ∈ E

–Diffie–Hellman key exchange with elliptic curves

–structure of pseudocurves

–Lenstra’s integer factorization with elliptic (pseudo)curves

–Pocklington’s prime number certification

–Goldwasser and Kilian’s prime number certification

–If two rational functions coincide at infinitely many points, then they are identical.

–P ↦ P + T is a rational morphism.

–P ↦ 2P is a rational morphism.

–Endomorphisms have a finite kernel.

–If two endomorphisms coincide at almost all points, then they are identical.

–The Frobenius morphism is a bijective endomorphism.

–Endomorphisms form a ring.

–normal form of nontrivial endomorphisms

–relation between endomorphisms and their rational morphisms

–Endomorphisms are surjective.

–For separable endomorphisms, the degree is the size of the kernel.

–For nonseparable endomorphisms, the degree is larger than the size of the kernel.

# 6 Combinatorics on words

Combinatorics on words deals with structural statements and properties of words and formal languages. Typical applications are text algorithms such as pattern recognition and the theory of variable length codes. The foundations were laid by the Norwegian mathematician Axel Thue (1863–1922) in the early 20th century. We refer to the Lothaire textbooks [[66](#Bibliography.xhtml_Bibliography_67)–[68](#Bibliography.xhtml_Bibliography_68)] for background information and highlights in this field.

Let Σ be a set. We view Σ as an alphabet and the elements of Σ are therefore called letters. We are mainly interested in the case where Σ is finite. By Σn, we denote the set of sequences of n letters over Σ. For (a1, . . . , an)∈ Σn, we also write a1 ⋅⋅ ⋅ an. We say that a1 ⋅⋅ ⋅ an is a word of length |a1 ⋅⋅ ⋅ an| = n, and its alphabet is alph(a1 ⋅⋅ ⋅ an) = {a1, . . . , an}⊆ Σ. Let Σ∗ denote the set of all (finite) words over Σ.

![](images/173_1.jpg)

We use ε to denote the empty word. It is the only element of Σ∗ of length 0 and whose alphabet is empty. We have 0∗ = {ε}. Once Σ is nonempty, Σ∗ is an infinite set. On Σ∗, we can define a concatenation ⋅ as follows. For a1 ⋅⋅ ⋅ an , b1 ⋅⋅ ⋅ bm ∈ Σ∗ let

![](images/173_5.jpg)

The concatenation is associative and the empty word ε is its neutral element. If x, u, υ, w are words with x = uυw, then u is called a prefix, υ a factor and w a suffix of x. For u ∈ Σ∗,we denote by un the n-fold concatenation u ⋅ ⋅⋅ u of u. If u = xn holds for some n ∈ ℕ, then we call u a power of x.

Together with the concatenation as operation, Σ∗ forms a monoid.[7](#Notes.xhtml_Notes_7)It is the free monoid over the set Σ. The term“free” is motivated by the following algebraic property of Σ∗:

Theorem 6.1 (Universal property). Let M be a monoid and φ: Σ → M a mapping. Then φ can uniquely be extended to a homomorphism φ: Σ∗ → M by defining that φ(a1 ⋅⋅ ⋅ an) = φ(a1) ⋅⋅ ⋅ φ(an) for n ≥ 0.

Proof: For n = 0, we have φ(ε) = 1, as needed for a monoid homomorphism. Let a1 ⋅⋅ ⋅ an , b1 ⋅⋅ ⋅ bm ∈ Σ∗ be two words. Then, we have

□

![](images/173_4.jpg)

This shows that the extension to Σ∗ is a monoid homomorphism. Let ψ: Σ∗ → M be an arbitrary monoid homomorphism such that ψ(a) = φ(a) for all a ∈ Σ. Then, ψ(a1 ⋅⋅ ⋅ an) = ψ(a1) ⋅⋅ ⋅ ψ(an) = φ(a1) ⋅⋅ ⋅ φ(an) = φ(a1 ⋅⋅ ⋅ an). Thus, ψ = φ, proving the uniqueness of the extension of φ.

Example 6.2. Let M be any monoid. The free monoid M∗ over the set M is infinite. Applying [Theorem 6.1](#chapter06.xhtml_chapter06_5) to the identity mapping M → M, we obtain a surjective homomorphism, the evaluation homomorphism

![](images/174_2.jpg)

where m1 ⋅⋅ ⋅ mn is a product in M.

◊

Example 6.3. Let Σ be an arbitrary set. The mapping Σ →ℕ with a ↦ 1 extends to a homomorphism |⋅| : Σ∗ → (ℕ, +, 0), which is the length function w ↦ |w|.

◊

Example 6.4. Applying [Theorem 6.1](#chapter06.xhtml_chapter06_5) to the mapping Σ → 2Σ, a ↦ {a} yields that the alphabet mapping Σ∗ → (2Σ, ∪, ∅) with w ↦ alph(w) is a homomorphism, that is, alph(ε) = ∅ and alph(υw) = alph(υ) ∪ alph(w).

◊

## 6.1 Commutation, transposition and conjugacy

We are interested in the structural relation between words which satisfy certain equations. For example, what can we say about words x and y such that xy = yx? Thus, x and y commute. Since powers of elements commute, there is a simple sufficient condition. If x = rk and y = rm for certain k, m ∈ ℕ, then xy = yx follows. [Theorem 6.5 (b)](#chapter06.xhtml_chapter06_11) tells us that the converse holds in in free monoids.

Besides commutation, we also study transposition and conjugation. Let M be any monoid. Elements x, y ∈ M are called transposed, if there are r, s ∈ M such that x = rs and y = sr. Transposition is a reflexive and symmetric relation, but in general it is not transitive; see [Exercise 6.1](#chapter06.xhtml_chapter06_33). However, we show that transposition is a transitive relation in free monoids.

An element x ∈ M is called conjugate to y ∈ M (more precisely left-conjugate) if there exists z ∈ M such that zx = yz. The conjugacy relation is always reflexive and transitive, but in general it is not symmetric: for example, consider M = a∗ ∪ ba∗ ⊆ {a, b}∗ with the multiplication defined by x ⋅ a = xa and x ⋅ b = b for all x. Then b is conjugate to a, but not vice versa. Conjugation is symmetric in groups and is therefore an equivalence relation since in this case all the three equations zx = yz, x = z−1yz, and y = zxz−1 are equivalent. If elements x, y in a monoid are transposed by x = rs and y = sr, then they are also conjugate because sx = srs = ys. [Theorem 6.5 (a)](#chapter06.xhtml_chapter06_10) states that in free monoids the converse is also true. Thus, in free monoids, conjugation and transposition coincide. We will see in [Section 8.10](#chapter08_3.xhtml_chapter08_3_7) that the statements about commutation, transposition, and conjugation from free monoids carry over to free groups.

The following theorem by Roger Conant Lyndon (1917–1988) and Marcel-Paul Schützenberger (1920–1996) is fundamental in combinatorics on words. It describes the structure of conjugate words. The second part of the theorem deals with pairs of commuting words.

Theorem 6.5 (Lyndon, Schützenberger). Let x, y, z ∈ Σ∗ be words.

(a)If x ≠ ε and zx = yz, then there are r, s ∈ Σ∗ and k ∈ ℕ such that x = sr, y = rs and z = (rs)k r. In particular, conjugation coincides with transposition, and both are equivalence relations.

(b)If xy = yx, then x and y both are powers of the same word r ∈ Σ∗.

Proof: (a) If |z| ≤ |x|, then z is a suffix of x. Therefore, according to the following picture, a word s with y = zs and x = sz exists. Then the claim holds for z = r and k = 0.

![](images/175_1.jpg)

For |z| > |x|, we obtain the following picture:

![](images/175_2.jpg)

Thus, z = z'x = yz' and |z'| < |z| since x ≠ ε. By induction on |z| there exist words r, s ∈ Σ∗ and an exponent k' ∈ ℕ with x = sr, y = rs and z' = (rs)k' r. Now, the claim holds with k = k' + 1.

(b)If x = ε, then the claim holds with r = y. Otherwise,wemay assume, by symmetry, that both x and y are not empty. Using part (a), we obtain x = st = ts and y = (st)k s. By induction on |xy|, the words s and t are powers of the same word r. Thus, the statement is true for x and y, too.

□

Every nonempty word w can be written as w = rk where r is nonempty and k ∈ ℕ is maximal. The r word is called the primitive root of w. If we have k = 1, then w is equal to its primitive root, and we say that w is primitive in this case. A primitive root is uniquely defined. For this and another basic property of primitive words, we refer to [Exercise 6.5](#chapter06.xhtml_chapter06_36) and [Exercise 6.6](#chapter06.xhtml_chapter06_37). [Theorem 6.5 (b)](#chapter06.xhtml_chapter06_11) shows that two words commute if and only if they have the same primitive root.

## 6.2 Fine and Wilf’s periodicity lemma

Nathan Jacob Fine (1916–1994) and Herbert Saul Wilf (1931–2012) gave another sufficient condition for commutativity in free monoids: if um and υn have a sufficiently long prefix in common, then u and υ commute. They gave a tight bound for the meaning of “sufficiently long.” The result is nontrivial and very useful. In order to have a comfortable induction hypothesis, we show a slightly stronger statement. This is a typical example of “loading the induction” where a stronger statement is easier to prove. The proof given here was found by Jeffrey Outlaw Shallit (born 1957).

Theorem 6.6. Let u, υ ∈ Σ∗ be nonempty, s ∈ u{u, υ}∗ and t ∈ υ{u, υ}∗. If s and t have a common prefix of length |u| + |υ| − gcd(|u|, |υ|), then uυ = υu.

Proof: Without loss of generality, assume that |u| ≤ |υ|. The statement is trivial for |u| = |υ|, so let 1 ≤ |u| < |υ|. From gcd(|u|, |υ|) < |υ|, we obtain υ = uw for some nonempty word w. It suffices to show that uw = wu holds, because then uυ = u(uw) = u(wu) = (uw)u = υu follows. Since |s| ≥ |u| + |υ| − gcd(|u|, |υ|) > |u|, we have s ∈ uu{u, w}∗. Since t has uw as a prefix, we can write s = us' and t = ut' for s' ∈ u{u, w}∗ and t' ∈ w{u, w}∗. Now, gcd(|u|, |υ|) = gcd(|u|, |w|) and |υ| = |u| + |w|. Hence, s' and t' have a common prefix of length |u|+|w|−gcd(|u|, |w|). The induction hypothesis yields uw = wu as desired.

□

A natural number p ≥ 1 is a period of the word a1 ⋅⋅ ⋅ an with ai ∈ Σ if ai = ai+p for all 1 ≤ i ≤ n − p. For example, the word aabaabaa has the periods 3, 6, 7, 8\. The length |u| is always a period of a nonempty word u. Fine and Wilf’s periodicity lemma from 1965 is often formulated in the form of [Corollary 6.7](#chapter06.xhtml_chapter06_14): if a sufficiently long word w has two periods, then their greatest common divisor is a period of w, too.

Corollary 6.7 (Periodicity lemma). If a word w with |w| ≥ p + q − gcd(p, q) has two periods p and q, then gcd(p, q) is also a period of w.

Proof: Let w be a prefix of both s = uk and t = υℓ, where |u| = p and |υ| = q. [Theorem6.6](#chapter06.xhtml_chapter06_13) yields uυ = υu. By [Theorem 6.5(b)](#chapter06.xhtml_chapter06_11), u and υ both are powers of a word x. Thus, s also is a power of x and |x| as well as all multiples of it are periods of w. The length of x divides both p and q, therefore |x| also divides gcd(p, q).

□

For all positive integers p, q,we inductively define the pair of words σ(p, q) ∈ {a, b}∗× {a, b}∗ as follows:

![](images/176_1.jpg)

The pair of words (u, υ) = σ(p, q) has the properties |u| = p, |υ| = q, uυ ≠ υu and the words u and υ coincide on the first p + q −gcd (p, q)−1 symbols. Therefore, the bound |u| + |υ| − gcd(|u|, |υ|) in the periodicity lemma is optimal.

For instance, the word w = ap−1bap−1 has the periods p and p+1, but gcd(p, p + 1) = 1 is not a period of w. This is not a contradiction to the periodicity lemma because |w| = 2p − 1 < p + (p + 1) − 1.

## 6.3 Kruskal’s tree theorem

Aword a1 ⋅ ⋅⋅ an with ai ∈ Σ is a subword of υ if υ can be written as υ = υ0a1υ1 ⋅⋅ ⋅ anυn. We write u ≼ υ if u is a subword of υ. The term scattered subword is sometimes used in some works to emphasize the distinction between “subword” and “factor.”

We want to show that, if L is an infinite set of words over a finite alphabet, then there exist two different words u, υ ∈ L with u ≼ υ. This fact is known as Higman’s lemma. We prove it in the slightly more abstract context of quasi-orderings and wellquasi-orderings. This approach allows us to derive Kruskal’s tree theorem by using the same methods. Kruskal’s tree theorem is a generalization of Higman’s lemma to the case of finite trees.

A quasi-ordering (X, ≤) is a set X equipped with a reflexive and transitive relation ≤, that is, ≤ is a subset of X × X and for all x, y, z ∈ X, we have x ≤ x and the implication:

![](images/177_3.jpg)

In contrast to partial orders, quasi-orderings need not be antisymmetric, that is, x ≤ y and y ≤ x does not imply x = y. We write x < y if x ≤ y and y ≰ x. Two elements x, y ∈ X are incomparable if neither x ≤ y nor y ≤ x; otherwise x, y are called comparable. A subset of pairwise comparable elements is called a chain. A subset Y ⊆ X is an antichain if any two different elements of Y are incomparable. A sequence (xi)i∈ℕ with xi ∈ X is decreasing if xi > xi+1 for all i; it is nondecreasing if xi ≤ xi+1 for all i. A sequence (xi)i∈ℕ is called good if i < j exist with xi ≤ xj. If an infinite sequence is not good, then it is bad. A quasi-ordering (X, ≤) is called a well-quasi-ordering if every infinite sequence is good.

Every finite quasi-ordering is a well-quasi-ordering. In particular, the identity on a finite set always defines a well-quasi-ordering. The integers (ℤ, |) with divisibility | form a quasi-ordering, which is not a well-quasi-ordering, because, for example, the sequence of prime numbers is bad. The natural numbers with the usual order (ℕ, ≤) form a well-quasi-ordering: let (xi)i∈ℕ be a sequence in ℕ and let xj be the smallest value in the sequence; then clearly xj ≤ xj+1. The integers (ℤ, ≤), however, do not form a well-quasi-ordering since, for example, the sequence (−i)i∈ℕ is bad. Similarly, the positive real numbers (ℝ≥0, ≤) are no well-quasi-ordering, because ![](images/177_2.jpg) is bad.

One of the main motivations to consider well-quasi-orderings is that, in many respects, they behave like finite sets. An important tool in the interplay between finite and infinite sets is Ramsey’s theorem (Frank Plumpton Ramsey, 1903–1930). This theorem is known in many different variants; here, we only deal with edge colorings of infinite complete graphs with finitely many colors.

Theorem 6.8 (Ramsey 1930). Let V be an infinite set of vertices and C a finite set of colors. For each coloring, ![](images/178_1.jpg) there is an infinite subset X ⊆ V such that ![](images/178_2.jpg) with respect to c is colored with a single color.

Proof: We define finite subsets Xi ⊆ V and infinite subsets Yi ⊆ V satisfying

–Xi ⊆ Xi+1 and Xi+1 \ Xi = {xi+1}, Yi+1 ∪ {xi+1} ⊆ Yi, Xi ∩ Yi = 0,

–for all xi there is a color ri ∈ C with c(xi , y) = ri for all y ∈ Yi.

We start with X0 = 0 and Y0 = V. Now, let Xi and Yi be already defined. We choose an arbitrary vertex xi+1 ∈ Yi and let Xi+1 = Xi ∪{xi+1}. Since C is finite, there is an infinite subset Yi+1 ⊆ Yi \ {xi+1} such that all edges {xi+1, y} for y ∈ Yi+1 have the same color in the coloring c.

We now define X' = ⋃i≥0 Xi and a vertex coloring d : X' → C by d(xi) = ri. Then there is an infinite subset X ⊆ X' such that all vertices in X have the same color r with respect to d. For, xi , xj ∈ X with i < j, we have c(xi , xj) = d(xi) = r because xj ∈ Yi. Therefore, all edges from ![](images/178_3.jpg) in c have the color r.

We now present a simple but useful characterization of well-quasi-orderings.

□

Theorem 6.9. Let (X, ≤) be a quasi-ordering. Then the following properties are equivalent:

(a)(X, ≤) is a well-quasi-ordering, that is, all infinite sequences are good.

(b)There are no infinite decreasing sequences and no infinite antichains.

(c)Every infinite sequence (xi)i∈ℕ in X has an infinite nondecreasing subsequence ![](images/178_6.jpg) that is, we have ![](images/178_5.jpg) for all j.

Proof: The implications from (a) to (b) and from (c) to (a) are trivial. We now show

□

(b)⇒ (c). Let (xi)i∈ℕ be an infinite sequence in X. We define a coloring c on { (i, j) ∈ ℕ| i < j } by

![](images/178_4.jpg)

This defines an infinite complete graph with vertex set ℕ, whose edges show three colors. According to Ramsey’s theorem, there is an infinite monochromatic subset {i1, i2, . . . } ⊆ ℕ. By assumption, the color of this subset can neither be > nor ‖ and thus, ![](images/178_8.jpg) is an infinite nondecreasing sequence.

Remark 6.10. Many results concerning well-quasi-orderings are of the form “If (X, ≤) is a well-quasi-ordering, then (X' , ≤) is one, too.” For example, (Y, ≤) is a well-quasiordering if Y ⊆ X for a well-quasi-ordering (X, ≤); here, the order on Y is the restriction of the order on X. Similarly, a quasi-ordering (X, ≼) is a well-quasi-ordering if (X, ≤) is a well-quasi-ordering and ≤ is a subset of ≼. In this case (X, ≼) is called a coarsening of (X, ≤).

◊

If (X, ≤) and (Y, ≤) are two quasi-orderings, then the product order on X × Y is componentwise: two pairs (x, y), (x' , y) ∈ X × Y satisfy (x, y) ≤ (x' , y) if both x ≤ x' and y ≤ y. The product order is again a quasi-ordering.

Theorem 6.11. If both (X, ≤) and (Y, ≤) are well-quasi-orderings, then the product order (X × Y, ≤) is also a well-quasi-ordering.

Proof: Let (xi , yi)i∈ℕ be a sequence in X ×Y. By [Theorem 6.9 (c)](#chapter06.xhtml_chapter06_19), there is a nondecreasing subsequence (xij )j∈ℕ of (xi)i∈ℕ, that is, we have ![](images/179_3.jpg) for all j. The sequence ![](images/179_7.jpg) has two elements ![](images/179_9.jpg) for k < ℓ. This yields ![](images/179_6.jpg)

□

The following fact about ℕk with componentwise order is often attributed to a paper of Dickson (Leonard Eugene Dickson, 1874–1954) published in 1913 [[22](#Bibliography.xhtml_Bibliography_23)]. It has been rediscovered many times and seems to have been known earlier, too.

Corollary 6.12 (Dickson’s lemma). (ℕk, ≤) is a well-quasi-ordering.

Proof: Since (ℕ, ≤) is a well-quasi-ordering, the claim follows from [Theorem 6.11](#chapter06.xhtml_chapter06_21) by induction on k.

□

By Dickson’s lemma, ℕk cannot contain an infinite antichain, however, arbitrarily large (finite) antichains occur. For example An = {(i, n − i) | 0 ≤ i ≤ n } is an antichain of size n + 1 in ℕ2.

Let (X, ≤) be a quasi-ordering. On words from X ∗, we define the subword relation as follows. Let u = a1 ⋅⋅ ⋅ an with ai ∈ X. We let u ≼ υ if υ has a factorization υ = υ0b1υ1 ⋅⋅ ⋅ bnυn with bi ∈ X and υi ∈ X∗, such that ai ≤ bi for all i. This way, (X∗, ≼) forms a quasi-ordering. If u ≼ υ, then u is called a subword of υ. The following result by Graham Higman (1917–2008) from 1952 states that the subword relation over a well-quasi-ordering is itself a well-quasi-ordering [[49](#Bibliography.xhtml_Bibliography_49)]. We present the proof of Crispin St. John Alvah Nash-Williams (1932–2001); it uses the technique of so-called minimal bad sequences [[80](#Bibliography.xhtml_Bibliography_80)].

Theorem 6.13 (Higman’s lemma). If (X, ≤) is a well-quasi-ordering, then (X∗, ≼) with the subword relation is a well-quasi-ordering, too.

Proof: Suppose that (X∗, ≼) is not a well-quasi-ordering: then there are bad sequences in X ∗. We inductively define a minimal bad sequence (ui)i∈ℕ as follows. Assume we have already constructed u0, . . . , ui−1 suitably. Then for ui, we choose some shortest word such that there exists a bad sequence beginning with u0, . . . , ui. This process defines a bad sequence (ui)i∈ℕ. In particular, all words ui are nonempty. Wewrite ui = aiυi with ai ∈ X and υi ∈ X ∗. The sequence (ai )i∈ℕ by [Theorem 6.9 (c)](#chapter06.xhtml_chapter06_19) contains an infinite nondecreasing subsequence (aij )j∈ℕ. Note that ui ≼ υj implies ui ≼ uj. So, if the sequence (υij )j∈ℕ were bad, then also

![](images/180_4.jpg)

would be bad, contradicting the definition of ![](images/180_10.jpg) Thus, there are k < ℓ with ![](images/180_5.jpg) Using ![](images/180_7.jpg) this yields ![](images/180_9.jpg) in contradiction to the fact that (ui)i∈ℕ is bad. Consequently, there are no bad sequences, and (X∗, ≼) is a well-quasi-ordering.

□

A frequent application of Higman’s lemma is in the case of the well-quasi-ordering (Σ, =) for a finite alphabet Σ. Then, u = a1 ⋅ ⋅⋅ an with ai ∈ Σ is a subword of υ if υ = υ0a1υ1 ⋅⋅ ⋅ anυn for υi ∈ Σ∗. From this special case of Higman’s lemma, one can easily derive Dickson’s lemma: k-tuples (n1, . . . , nk)∈ ℕk are encoded as words ![](images/180_2.jpg) over the alphabet Σ = {a1, . . . , ak}. A sequence (xi)i∈ℕ in ℕk corresponds in this way to a sequence (ui)i∈ℕ of words ui ∈ Σ∗; and xi ≤ xj holds if and only if ui is a subword of u j.

Ageneralization of Higman’s lemma is Kruskal’s tree theorem (Joseph Bernard Kruskal, 1928–2010) from 1960\. It shows that the set of finite trees is a well-quasi-ordering with respect to the subtree relation [[61](#Bibliography.xhtml_Bibliography_62)]. Depending on what kind of trees are considered, one obtains different versions of Kruskal’s tree theorem. We use rooted trees in which the children of each node are ordered. Moreover, the nodes in the trees are labeled with elements from a well-quasi-ordering. This scenario yields one of the most general variants of Kruskal’s tree theorem.

Let X be a set. We inductively define the class of finite trees TX over X as follows:

–Ift1, . . . , tn are trees in 𝓣X, then also x(t1, . . . , tn) is a tree in TX for all x ∈ X.

Here x(t1, . . . , tn) denotes the tree whose root is labeled x and whose children are (in this order) the trees t1, . . . , tn. Since the order of a node’s children is essential, one often speaks of ordered trees. The tree x(t1, . . . , tn) is illustrated in [Figure 6.1](#chapter06.xhtml_chapter06_27). Note that the trees here are oriented from top to bottom; in particular, parent nodes are always depicted closer to the top than their child nodes. For n = 0, we see that every tree consisting only of a root labeled by x belongs to 𝒯X.

![](images/180_3.jpg)

Fig. 6.1. A tree x(t1, . . . , tn).

Let (X, ≤) be a quasi-ordering. We inductively define the subtree relation ≪on TX as follows:

–Letn ≥ 0\. If x ≤ y and si ≪ ti, then for all finite sequences ui of trees from 𝒯X, we have x(s1, . . . , sn)≪ y(u0, t1, u1, . . . , tn, un).

–Ifs ≪ t, then also s ≪ x(t) for all x ∈ X.

–If r ≪ s and s ≪ t, then r ≪ t.

The idea is that s ≪ t if and only if one can obtain the tree s from t by applying the following three operations: (a) replacing the label y ∈ X of some node by x ∈ X, provided that x ≤ y; (b) removing subtrees of an arbitrary node in t; and (c) removing (“skipping”) nodes having only one child. Especially, ≪ is a quasi-ordering. If s ≪ t holds, then we call s a subtree of t. In the following example from 𝓣{a,b} over the well-quasi-ordering ({a, b}, =), we have t3 ≪ t2 ≪ t1, whereas t4 is not a subtree of t1.

![](images/181_1.jpg)

Theorem 6.14 (Kruskal’s tree theorem). If (X, ≤) is a well-quasi-ordering, then (TX , ≪) with the subtree relation is a well-quasi-ordering, too.

Proof: Suppose that (TX , ≪) is not a well-quasi-ordering. Then there are bad sequences. We inductively define a minimal bad sequence (ti)i∈ℕ of trees ti ∈ TX. Let t0, . . . , ti−1 be suitably constructed already. Then we choose a tree ti with a minimum number of nodes such that a bad sequence exists, which begins with t0, . . . , ti. This process yields a bad sequence (ti)i∈ℕ. Let xi be the label of the root of ti. Since (X, ≤) is a well-quasi-ordering, by [Theorem 6.9 (c)](#chapter06.xhtml_chapter06_19) there is an infinite nondecreasing subsequence (xij )j∈ℕ of (xi)i∈ℕ with xij ≤ xij+1\. We write 1![](images/181_3.jpg) with ![](images/181_4.jpg) Let ![](images/181_2.jpg) and S = ⋃j∈ℕ Sj.

Claim. (S, ≪) with the subtree relation is a well-quasi-ordering.

Proof of the claim: Suppose that ![](images/181_6.jpg) is a bad sequence in S. Choose j minimal such that ![](images/181_5.jpg) By omitting a finite number of elements at the beginning of the sequence, we may assume that ![](images/181_7.jpg) Due to the minimality of tij, the sequence

![](images/181_8.jpg)

is good. Since both (ti)i∈ℕ and ![](images/181_10.jpg) are bad, there exist tk and ![](images/181_11.jpg) with k < ij such that ![](images/181_9.jpg) Then ![](images/181_12.jpg) and by the choice of j, we have k < im. This is a contradiction.

By Higman’s lemma, the words S∗ with the subword relation ≼ form a well-quasi-ordering. We consider the sequence (uj)j∈ℕ with ![](images/182_1.jpg) Since it is good, there are k < ℓ with uk ≼ uℓ. Together with xik ≤ xiℓ, we finally obtain tik ≪ tiℓ, a contradiction.

□

The proof of Kruskal’s tree theorem presented here is essentially the one given by Nash-Williams [[80](#Bibliography.xhtml_Bibliography_80)]. Higman’s lemma is a special case of Kruskal’s tree theorem: a word a1 ⋅⋅ ⋅ an ∈ X∗ with ai ∈ X is encoded by the tree a(a1, . . . , an) for a fixed a ∈ X; alternatively one could also use the more vertical encoding a1(a2(⋅ ⋅⋅ an−1(an) ⋅⋅ ⋅ )).

Frequently, one considers trees in which one does not distinguish the order of the children. This variant of Kruskal’s tree theorem can easily be derived from [Theorem 6.14](#chapter06.xhtml_chapter06_29) by using [Remark 6.10](#chapter06.xhtml_chapter06_20). The subtree relation appearing in the unordered case is nothing but the so-called graph minor relation. In a series of 20 publications with altogether more than 500 pages, George Neil Robertson (born 1938) and Paul D. Seymour (born 1950) proved that the finite graphs with the graph minor relation form a well-quasi-ordering. The final result is given in [[88](#Bibliography.xhtml_Bibliography_89)].

## Exercises

6.1. Consider the monoid M = Σ∗/{ac = ca} with generating set Σ = {a, b, c}, where words of the form uacυ and ucaυ are identified with each other; this means we perform operations like we do with words, but with the additional rule ac = ca. So, for example, in M, we have bcaaa = bacaa = baaca = baaac, but abc ≠ cba. Show that the transposition of elements in M is not a transitive relation.

6.2. (Levi’s lemma, named after Friedrich Wilhelm Daniel Levi, 1888–1966) Let M be a monoid. Show that the following properties are equivalent:

(i)M is isomorphic to the free monoid Σ∗ over a set Σ.

(ii) There is a homomorphism φ: M →ℕ with φ−1(0) = 1M, and for all p, q, x, y ∈ M such that pq = xy there exists an element u ∈ M for which either p = xu, y = uq or x = pu, q = uy is satisfied.

6.3. Determine a nonfree monoid, in which for all elements p, q, x, y with pq = xy there is an element u such that either p = xu, y = uq or x = pu, q = uy is satisfied (compare with [Exercise 6.2](#chapter06.xhtml_chapter06_34)).

6.4. Let < be a linear order on Σ. We define the lexicographic order ≺ on Σ∗ by u ≺ υ if u is a proper prefix of υ or u = ras and υ = rbt with r, s, t ∈ Σ∗, a, b ∈ Σ and a < b. Show:

(a)∀w ∈ Σ∗ : u ≺ υ ⇔ wu ≺ wυ

(b)If u is not a prefix of υ, then ∀w, z ∈ Σ∗ : u ≺ υ ⇒ uw ≺ υz.

6.5. A word w ∈ Σ∗ is called primitive, if it cannot be written as w = ui with i > 1.

Show that the following statements are equivalent:

(i)w is primitive.

(ii) w is not a proper factor of w2.

(iii) The cyclic permutation υa of w = aυ with a ∈ Σ is primitive.

6.6. A primitive root of a word w is a primitive word u with w = ui for i ∈ ℕ. Show that every nonempty word w has a unique primitive root.

6.7. A word w ∈ Σ∗ is called Lyndon word if w is primitive and w = uυ ≺ υu holds for each decomposition w = uυ such that u ≠ ε ≠ υ. Here, ≺ again is the lexicographic order induced by a given linear order on the letters. Show that the following statements are equivalent:

(i)w is a Lyndon word.

(ii) For all proper suffixes υ of w, we have w ≺ υ.

(iii) w ∈ Σ or there is a decomposition w = uυ of w into Lyndon words u, υ with u ≺ υ.

6.8. (Lyndon factorization [[16](#Bibliography.xhtml_Bibliography_17)]) Let < be a linear order on Σ and let ≺ be the corresponding lexicographic order on Σ∗. Show that every word w ∈ Σ∗ can uniquely be decomposed into w = ℓ1 ⋅⋅ ⋅ ℓn, where ℓ1, . . . , ℓn are Lyndon words with ℓn ≼⋅ ⋅⋅ ≼ ℓ1.

## Summary

Notions

–letter

–alphabet Σ, words Σ∗

–length of a word

–empty word ε

–concatenation

–free monoid

–prefix

–suffix

–factor

–power

–transposed

–conjugate

–period

–quasi-ordering

–incomparable

–chain, antichain

–decreasing sequence

–nondecreasing sequence

–good/bad sequence

–well-quasi-ordering

–subword

–subword relation ≼

–(ordered) tree

–subtree

–subtree relation ≪

Methods and results

–Universal property of free monoids: each mapping φ: Σ → M can uniquely be extended to a homomorphism φ: Σ∗ → M.

–Lyndon and Schützenberger: x ≠ ε, zx = yz ⇒ x = sr, y = rs, z = (rs)k r.

–xy = yx ⇒ x, y both are powers of a word r.

–periodicity lemma: word w has periods p, q and |w| ≥ p + q − gcd(p, q) ⇒ w has period gcd(p, q).

–Ramsey: for each coloring ![](images/183_1.jpg) with |V| = ∞and |C| < ∞there is X ⊆ V with |X| = ∞ and![](images/183_2.jpg)

–Let (X, ≤) be a quasi-ordering. Then: (X, ≤) is well-quasi-ordering ⇔ there is no infinite properly descending sequence and no infinite antichains ⇔ every infinite sequence has an infinite increasing partial sequence.

–subsets of well-quasi-orderings are well-quasi-orderings.

–coarsenings of well-quasi-orderings are well-quasi-orderings.

–(X, ≤) and (Y, ≤), well-quasi-orderings ⇒ (X × Y, ≤) with componentwise comparison is well-quasi-ordering.

–Dickson’s lemma: (ℕk , ≤) is a well-quasi-ordering.

–Higman’s lemma: The subword relation is a well-quasi-ordering.

–Kruskal’s tree theorem: The subtree relation is a well-quasi-ordering.

# 7 Automata

Various topics in theoretical computer science deal with the classification of formal languages with respect to their complexity, where different disciplines use different measures of “complexity.” Typically, a formal language is a subset of a finitely generated free monoid Σ∗. The word “formal” serves to distinguish these languages from natural languages. In many cases, we omit this adjective and call L ⊆ Σ∗ a language. The classification of languages can be done from rather different points of view. A well-known approach is the Chomsky hierarchy by Avram Noam Chomsky (born 1928), where grammars are used as description mechanisms. The class of regular languages coincides with Type-3 in Chomsky’s hierarchy. This class is particularly robust as it admits various other natural characterizations. In this chapter, we examine regular languages not only within free monoids but also in arbitrary monoids. The two main mechanisms to describe regular languages, regular expressions and deterministic finite state automata, lead to different classes. Therefore, we distinguish between rational and recognizable sets. We will see that rational sets correspond to nondeterministic finite automata and regular expressions, whereas deterministic finite-state automata define recognizable sets. Moreover, there are finitely generated monoids where the class of rational subsets is strictly larger than the class of recognizable sets. [Section 7.3](#chapter07_2.xhtml_chapter07_2_7) shows that the concepts rational and recognizable coincide over finitely generated free monoids, which allows an unambiguous use of the term regular in this context.

Let L and K be the subsets of a monoid M. The product L ⋅ K is defined by L ⋅ K = { uυ | u ∈ L, υ ∈ K }. Moreover, we let L0 = {1} and Ln+1 = L ⋅ Ln for n ∈ ℕ. Thus, we can define the submonoid generated by L as follows:

![](images/185_1.jpg)

By definition, L∗ is the smallest submonoid of M which contains L. The operation L ↦ L∗ is called the Kleene star after Stephen Cole Kleene (1909–1994) or simply the star operation. The Kleene star depends on the ambient monoid M; it must not to be confused with the notation for the free monoid over L. For example, the Kleene star of {a, aa} for a ∈ Σ contains the word aaa = a ⋅ aa = aa ⋅ a = a ⋅ a ⋅ a. However, in the free monoid generated by the alphabet {a, aa}, the words a ⋅ aa, aa ⋅ a and a ⋅ a ⋅ a are all different. Frequently, we use shorthands, for example, we may write LK instead of L ⋅ K or, if u ∈ M, then we identify u with the singleton {u}. It is also common to write L + K to denote the union L ∪ K.

## 7.1 Recognizable sets

The concept of recognizability is based on an algebraic approach to formal language theory. It is particularly well suited to describe the “complexity” of subclasses of regular languages and to decide their membership in subclasses. Star-free languages are the most prominent of one of these subclasses and we discuss them in [Section 7.4](#chapter07_2.xhtml_chapter07_2_16).

Let M and N be monoids. Typically, N is finite. A subset L ⊆ M is recognized by a homomorphism φ: M → N if L = φ−1(φ(L)). In this case, we say that N recognizes the set L ⊆ M. A subset of M is called recognizable if it is recognized by a finite monoid N. The set of all recognizable subsets of M is denoted by REC(M). If φ is given by the images of a generating set Σ of M, then we can test membership of u ∈ L for u = a1 ⋅⋅ ⋅ an with ai ∈ Σ by a “table look-up,”we compute φ(u) = φ(a1) ⋅⋅ ⋅ φ(an) in N and check whether φ(u) belongs to the finite table φ(L) ⊆ N.

Remark 7.1. In a finite monoid M, every subset of Mis recognized by the identity mapping M → M. In particular, finite subsets of a finite monoid are recognizable. In a group G the converse holds; if the finite subsets are recognizable, then G is finite. Indeed, let N be finite and φ: G → N be a surjective homomorphism recognizing the singleton {1}. Then N is a group and {1} is the preimage of the neutral element of N. Therefore, the kernel of φ: G → N is trivial. This means that φ is injective. Hence, G is finite because N is finite.

◊

Theorem 7.2. The class of recognizable sets over a monoid M is a Boolean algebra. This means, it is closed under finite union, finite intersection, and complementation. It is also closed under inverse homomorphisms. This means, if ψ: M' → M is a homomorphism and if L ∈ REC(M), then ψ−1(L) ∈ REC(M).

Proof: Every finite monoid recognizes 0 and M. This shows the closure under empty union and empty intersection. Let L1, L2 be recognizable sets and for i = 1, 2, let φi : M → Ni be a homomorphismwith Li = φ−i 1 (Fi) where Fi = φi(Li). The homomorphism φ1 : M → N1 also recognizes the complementM\L1. Consider ψ: M → N1×N2 with ψ(u) = (φ1(u), φ2(u)). Thenψ−1(F1×F2) = L1∩L2 and ψ−1((F1×N2)∪(N1×F2)) = L1 ∪ L2.

□

Let ψ: M' → M be a homomorphism and let L ⊆ M be recognized by φ: M → N, then ψ−1(L) ⊆ M' is recognized by φ ∘ ψ: M' → N. This shows that the class of recognizable sets is closed under inverse homomorphisms.

We have just seen that recognizable sets are closed under inverse homomorphisms, but, in general, they are not closed under homomorphisms. Consider, for example, the homomorphism ψ: {a, b}∗ → ℤwith a ↦ 1 and b ↦ −1\. The singleton {ε} ⊆ {a, b}∗ is recognizable in {a, b}∗, but ψ({ε}) = {0} ⊆ ℤ is not recognizable in ℤ by [Remark 7.1](#chapter07_1.xhtml_chapter07_1_3). Actually, no nontrivial subset of a∗ is recognizable in the group ℤ. The following example yields an even stronger “nonclosure"property.” It was given by Shmuel Winograd (born 1936) and shows that, in general, recognizable sets are neither closed under product nor under Kleene star.

Example 7.3. We extend the addition from ℤ to M = ℤ∪ {e, a} to an operation on M by e + m = m + e = m for m ∈ M, a + a = 0, and a + k = k + a = k for k ∈ ℤ. This way M = (M, +, e) forms a commutative monoid with e as its neutral element. Consider a homomorphism φ: M → N with φ−1(φ(L)) = L, and let φ̃ : ℤ → N be the restriction of φ to ℤ ⊆ M.With F = φ(L) we have φ̃ −1(F) = φ−1(F) ∩ℤ = L ∩ℤ. Thus, L ∈ REC(M) implies L ∩ ℤ ∈ REC(ℤ). By [Remark 7.1](#chapter07_1.xhtml_chapter07_1_3), we obtain {0} ∉ REC(ℤ). Next, we show that {a} ∈ REC(M). Let N = {e, a, n} be a commutative monoid with neutral element e, zero element n and a+a = n. Let φ: M → N be the homomorphismwith e ↦ e, a ↦ a and k ↦ n for k ∈ ℤ. Then φ−1(a) = {a} and therefore {a} ∈ REC(M). On the other hand, L1 = {a} + {a} = {0} and L2 = {a}∗ = {e, a, 0} are not in REC(M), because otherwise also Li ∩ℤ = {0} ∈ REC(ℤ).

◊

A congruence in a monoid M generalizes the notion of “being congruent modulo n” for integers. By definition, it is an equivalence relation ≡ ⊆ M × M such that u ≡ υ implies xuy ≡ xυy for all u, υ, x, y ∈ M. For u ∈ M, let [u] = {υ ∈ M| u ≡ υ } be its congruence class. The set of congruence classes { [u] | u ∈ M } is denoted by M / ≡ and it forms a monoid with the multiplication

![](images/187_4.jpg)

The operation is well defined because u ≡ u' and υ ≡ υ' yields

![](images/187_5.jpg)

From the corresponding properties of the monoid M, it follows that the operation on M / ≡ is associative with [[1](#Bibliography.xhtml_Bibliography_2)] as neutral element. (It follows “par transport de structures.”) Moreover, the mapping μ : M → M / ≡ with μ(u) = [u] is a surjective homomorphism.

Let L be any subset of M. Then we assign to L the syntactic congruence ≡L by letting u ≡L υ if

![](images/187_6.jpg)

Hence, u can “syntactically” be replaced by υ in any context without changing the membership with respect to L. The relation ≡L is obviously a congruence and the congruence classes form the syntactic monoid of L. It is denoted by Synt(L). The syntactic monoid Synt(L) recognizes the subset L (i.e., μ−1(μ(L)) = L) because for μ(u) = μ(υ) either u, υ ∈ L or u, υ ∉ L. The next theorem implies that Synt(L) is the minimal monoid recognizing L.

Theorem 7.4. Let L ⊆ M and φ: M → N be a homomorphism with L = φ−1(φ(L)). Then, by φ(u) ↦ [u], a surjective homomorphism from the submonoid φ(M) ⊆ N to Synt(L) is defined.

Proof: The mapping φ(u) ↦ [u] is well defined: for φ(u) = φ(υ) and x, y ∈ M we have![](images/188_6.jpg)

Thus [u] = [υ]. Furthermore, φ(M) → Synt(L) : φ(u) ↦ [u] is a surjective mapping. The homomorphism property now follows from 1 = φ(1) ↦ [[1](#Bibliography.xhtml_Bibliography_2)], φ(uυ) = φ(u)φ(υ) as well as φ(uυ) ↦ [uυ] and φ(u)φ(υ) ↦ [u][υ] for all u, υ ∈ M.

Another concept related to recognizability by monoids is acceptance by deterministic automata. An M-automaton A = (Q, ⋅, q0, F) consists of a set of states Q, an initial state q0 ∈ Q, a set of final states F ⊆ Q, and a transition function ⋅ : Q × M → Q satisfying the following properties for all q ∈ Q and u, υ ∈ M.

![](images/188_5.jpg)

We define the set L(A) that is accepted by the M-automaton A by

![](images/188_7.jpg)

In mathematical terms, Q is a set where M acts on the right. We can also think that, by reading an element u ∈ M in a state q,we move from q to state q ⋅ u.

Choosing a generating set Σ ⊆ M, we may represent M-automata as edge-labeled directed graphs. The states are the vertices and, in our graphical representation, an initial state is marked by an incoming arrow, whereas final states are characterized by double circles. We let δ = {(p, u, p ⋅ u) | p ∈ Q, u ∈ Σ } and we draw an edge from p to p ⋅ u which is labeled by u. The edges in this graph are called transitions. If we refer to this representation, we also denote an M-automaton as a tuple A = (Q, Σ, δ, q0 , F). We use the following convention in pictures.

![](images/188_4.jpg)

To determine p ⋅ u for arbitrary pairs (p, u) ∈ Q × M, it is sufficient to factorize u = u1 ⋅⋅ ⋅ un with ui ∈ Σ and then follow the states p, p ⋅ u1, . . . , p ⋅ u1 ⋅⋅ ⋅ un successively. Since Σ is a generating set, this path from p to p ⋅ u exists. M-automata defined this way are complete and deterministic. The automaton is complete because the transition function ℚ × Σ → Q, (q, u) ↦ q ⋅ u is totally defined. It is deterministic because, for each q ∈ Q and for each u ∈ M, there is at most one state q ⋅ u. (In [Section 7.2](#chapter07_1.xhtml_chapter07_1_19), we extend this concept to nondeterministic M -automata.)

We say that a state q ∈ Q is reachable if there is some u ∈ M with q = q0 ⋅ u. Without loss of generality, we can assume that all states are reachable, because removing an unreachable state does not change the accepted set L(A). Let Σ ≠ 0\. Since an M-automaton is complete, we see that δ is finite if and only if Q and Σ are finite. Thus, if M is not finitely generated, then δ is always infinite. If M is finitely generated, then we can choose Σ to be finite and we see that δ is finite if and only if the set of reachable states is finite.

Example 7.5. The set {−1, +1} is a generating set of the monoid ℤ of integers, with the addition as monoid operation. The ℤ-automaton A, defined by A = ({0, 1, 2, 3, 4, 5}, δ, 0, {1, 4}) with δ(q, k) = (q + k) mod 6 has the following graphical representation:

![](images/189_1.jpg)

The set accepted by A is L(*A*) = { k + 6ℓ | k ∈ {1, 4}, ℓ ∈ ℤ}.

◊

To every subset L ⊆ M, you can assign a canonical automaton, which is called the minimal automaton of L. For this purpose, we first define the quotient by an element u ∈ M by L(u) = { υ ∈ M | uυ ∈ L }. These subsets are interpreted as states. L(u) is also commonly denoted by u−1L which is closer to the notation of a (left) quotient. Note that L = L(1) and this is the natural initial state. Formally, the minimal automaton AL of L ⊆ M is defined as follows:

![](images/189_4.jpg)

Let L(u) = L(u). Then

![](images/189_3.jpg)

This shows that L(uυ) = L(uυ). As a consequence, L(u) ⋅ υ is well defined; it does not depend on the choice of representatives for the class L(u). Moreover, L(u) ⋅ 1 = L(u) and (L(u) ⋅ υ) ⋅w = L(uυ) ⋅w = L(uυw) = L(u) ⋅υw. The minimal automaton AL accepts exactly the set L, because L(1) ⋅ u = L(u), and u ∈ L is equivalent to 1 ∈ L(u).

Example 7.6. We consider the set L = {k + 6ℓ | k ∈ {1, 4}, ℓ ∈ ℤ} as in [Example 7.5](#chapter07_1.xhtml_chapter07_1_10). Adding multiples of 3 does not change membership in L. It therefore suffices to determine the languages L(0), L(1) and L(2): L(0) = 1+3ℤ, L(1) = 3ℤ and L(2) = −1+3ℤ. This yields the following minimal automaton AL:

![](images/190_1.jpg)

◊

The following theorem justifies the name “minimal” automaton.

Theorem 7.7. Let L ⊆ M be accepted by an M-automaton A = (Q, Σ, ⋅, q0 , F) and AL the minimal automaton of L. Then q0 ⋅ u ↦ L(u) is a surjective mapping from the set of reachable states of A onto the set of states in AL. In particular, the number of states of AL is at most the number of states of A.

Proof: From q = q0 ⋅ u, we immediately obtain L(u) = {υ | q ⋅ υ ∈ F }. Therefore, the mapping q0 ⋅ u ↦ L(u) is well defined. It is surjective, since for each u ∈ M the reachable state q0 ⋅ u is a preimage of L(u).

□

Automata minimization

[Theorem 7.7](#chapter07_1.xhtml_chapter07_1_12) implicitly provides a minimization method for M-automata. For a state p ∈ Q, let L(p) = {υ ∈ M | p ⋅ υ ∈ F} be the language at p. The set accepted by A is exactly the language at the initial state. Moreover, we see that L(p) = L(q) implies L(p⋅u) = L(q⋅u) for all u ∈ M. Let us merge states which define the samelanguage into a single class [p] and let [p] ⋅ u = [p ⋅ u]. Then [Theorem 7.7](#chapter07_1.xhtml_chapter07_1_12) tells us that the mapping q0 ⋅ u ↦ L(u) induces a bijection between { [p] | p ∈ Q is reachable } and the states { L(u) | u ∈ M } of the minimal automaton.

The following marking algorithm by Edward Forrest Moore (1925–2003) [[77](#Bibliography.xhtml_Bibliography_77)] is applied to an M-automaton with states Q and δ ⊆ Q ×Σ×Q. After preprocessing we know that all states are reachable from the initial state q0.Now, in a first phase, the algorithm marks pairs of states whose components define different languages as explained below. Then, in a second phase one chooses a representative from each set of unmarked states. The first of the two phases satisfies the invariant that a pair (p, q) ∈ Q × Q is only marked if L(p) ≠ L(q). The first phase works as follows:

(1)Choose any linear order ≤ on Q (for example, Q = {1, . . . , n} with the natural order).

(2)Let P = {(p, q) ∈ Q × Q | p < q } be the set of all ordered pairs. (Typically, P is represented as an upper triangular matrix.)

(3)Mark all pairs (p, q) ∈ P if one of the vertices p, q is a final state and the other one is not.

(4)Consider a marked pair (p' , q') ∈ P. Mark all unmarked pairs (p, q) ∈ P where {p' , q'} = {p ⋅ a, q ⋅ a} for some a ∈ Σ. Then, delete the pair (p' , q') from the set P.

(5)Repeat the previous step until all remaining pairs in P are unmarked. Hence, no pairs are deleted anymore.

This concludes the first phase. Let us see that the invariant L(p) ≠ L(q) holds for all marked pairs (p, q). This is certainly true if, say, p is final and q is not final because then 1 ∈ L(p) \ L(q). Now, consider a marked pair (p'' , q'). By induction (and by symmetry in p' and q') we may assume that there is some u' ∈ L(p) \ L(q'). The algorithm marks all pairs (p, q) ∈ P with {p' , q'} = {p ⋅ a, q ⋅ a} for a ∈ Σ. This implies u = au' ∈ (L(p) \ L(q)) ∪ (L(q) \ L(p)). Thus, the invariant L(p) ≠ L(q) is satisfied. As a consequence, if there are p, q ∈ Q with p < q and L(p) = L(q), then the pair (p, q) has not been deleted and it is still a member of P. We also need the converse. Let (p, q) ∈ P with L(p) ≠ L(q) and let u ∈ (L(p) \ L(q)) ∪ (L(q) \ L(p)). If |u| = 0, then (p, q) is marked in step (3) and deleted. In the other case we have u = aυ and υ ∈ (L(p ⋅ a) \ L(q ⋅ a)) ∪ (L(q ⋅ a) \ L(p ⋅ a)). By induction on |u|, either the pair (p ⋅ a, q ⋅ a) or the pair (q ⋅ a, p ⋅ a) is marked. This implies that (p, q) is marked and then deleted in this case, as well.

In the following, we only consider the remaining pairs (p, q) in P. The idea for the second phase is based on the following observation. If we view (p, q) as an undirected edge {p, q}, then, in the resulting undirected graph (Q, P), connected components are cliques. The languages at all states in the same clique are equal and can be identified with the states of AL.

So in the second phase, we assign to every p ∈ Q a state ̂p which is in the same connected component of p. Say, p̂ is minimal with respect to the chosen linear order of Q. There are various ways to do this algorithmically; and one can choose any of them. The set ̂Q = { p̂ | p ∈ Q } is in canonical bijection with the set of states in the minimal automaton AL. The bijection is induced by mapping p = q0 ⋅ u to the quotient L(u). Since we started with an automaton where every state is reachable, we can write p = q0 ⋅ u for some u and the mapping q0 ⋅ u ↦ L(u) is well defined and injective on Q̂ by construction of the ̂δgraph. Finally, we let= {(p̂, a, q̂) | (p, a, q) ∈ δ }. Then, the automaton (̂Q, Σ, ̂δ, ̂q0, F ∩ Q̂) is, up to renaming, the same M-automaton as the minimal automaton *A*L.

Syntactic monoids as transition monoids

To an M-automaton A = (Q, ⋅, q0 , F), we assign its transition monoid by the canonical interpretation of an element in M as a mapping on states; for u ∈ M we define the mapping δu : Q → Q by δu(q) = q ⋅ u. The transition monoid of A is the submonoid { δu | u ∈ M} of the monoid { f : Q → Q | f is function } of all mappings from Q to Q. We have δυ(δu(q)) = q ⋅ uυ = δuυ(q) for all q ∈ Q. Thus, the operation δu ⋅ δυ = δuυ is well defined. The homomorphism that maps u ∈ M to δu recognizes L(A) because we have u ∈ L(A) if and only if δu(q0)∈ F.

Theorem 7.8. There is a canonical isomorphism between the syntactic monoid of L ⊆ M and the transition monoid of the minimal automaton AL.

Proof: Let T be the transition monoid of AL. By [Theorem 7.4](#chapter07_1.xhtml_chapter07_1_7) the homomorphism δu ↦ [u] is a surjection from T onto the syntactic monoid Synt(L). We only have to show that it is injective. So let [u] = [υ], that is, u ≡L υ. For a state L(x) = { y | xy ∈ L } in AL we have δu(L(x)) = L(x) ⋅ u = L(xu). For all y ∈ M this yields the equivalence

□

![](images/192_1.jpg)

and therefore δu(L(x)) = δυ(L(x)). This shows δu = δυ.

The following theorem by John R. Myhill, Sr. (1923–1987) and Anil Nerode (born 1932) states that recognizability and acceptance by M-automata with finitely many states are equivalent [[81](#Bibliography.xhtml_Bibliography_81)].

Theorem 7.9 (Myhill, Nerode). Let L ⊆ M. The following statements are equivalent:

(a)L is recognizable, that is, L ∈ REC(M).

( b) L is accepted by an M-automaton with finitely many states.

(c)The minimal automaton AL has finitely many states.

(d)The syntactic monoid Synt(L) is finite.

Proof: (a) ⇒ (b): Let N be a finite monoid and φ: M → N a homomorphism with φ−1(φ(L)) = L. We define a finite M-automaton AN = (N, ⋅, 1N , φ(L)) with n ⋅ u = n φ(u). Now

□

![](images/192_2.jpg)

that is, AN accepts the set L. (b) ⇒ (c). This follows from [Theorem 7.7](#chapter07_1.xhtml_chapter07_1_12). (c) ⇒ (d). If AL has only finitely many states Q L, then there are only finitely many mappings from Q L to QL. Therefore, the transition monoid of AL is finite and thus, by [Theorem 7.8](#chapter07_1.xhtml_chapter07_1_16), so is the syntactic monoid Synt(L). (d) ⇒ (a): This follows, since the syntactic monoid Synt(L) recognizes the set L.

## 7.2 Rational sets

In this section, we introduce rational sets and extend the concept of M -automata to nondeterministic automata. Rational expressions define rational sets and we show that rational sets and nondeterministic finite M-automata have the same expressive power. The family RAT(M) of rational sets over a monoid M is inductively defined as follows:

–L ∈ RAT(M) for all finite subsets L of M.

–IfK, L ∈ RAT(M), then also K ∪ L ∈ RAT(M) and KL ∈ RAT(M).

–IfL ∈ RAT(M), then also L∗ ∈ RAT(M).

Here, as defined previously, KL = K ⋅ L = {uυ ∈ M| u ∈ K, υ ∈ L }, and L∗ denotes the submonoid of M generated by L. The definition of a rational set is given together with its semantics as a subset of M. Sometimes it is useful to distinguish between the subset L and its syntactic description as a rational (or regular) expression. If + is not used for the monoid operation, then the syntactic operator + has the same meaning as ∪, so a finite set L = {u1, . . . , uk} is given by the expression u1 + ⋅ ⋅⋅ + uk, too. If k = 0, then we use 0 as an expression. We define KL, and L∗ to be rational expressions if K and L are rational expressions. Moreover, brackets are used to avoid ambiguity, for example, the expression a(b + c)∗ is another syntax for {a}{b, c}∗. However, for the monoid M = ℕ×ℕ×ℕwith addition + as operation, the expression (0, 2, 4) + ((0, 1, 2)∪(1, 0, 2))∗ denotes {(0, 2, 4)}{((0, 1, 2), (1, 0, 2))}∗. So, this is a case where + does not mean “union.” We will make sure that there is no risk of confusion. In M as above, the expression (0, 2, 4) + ((0, 1, 2) ∪ (1, 0, 2))∗ describes the set

![](images/193_4.jpg)

Remark 7.10. The class of rational sets is closed under homomorphisms. Indeed, let ψ: M → M' be a homomorphism and let L, K ⊆ M be any languages. If L is finite, then ψ(L) is finite. Moreover, ψ(L ∪ K) = ψ(L) ∪ ψ(K), ψ(L ⋅ K) = ψ(L) ⋅ ψ(K), and ψ(L∗) = (ψ(L))∗.

◊

A nondeterministic M-automaton A = (Q, δ, I, F) consists of a set of states Q, a transition relation δ ⊆ Q × M × Q, a set of initial states I ⊆ Q, and a set of final states F ⊆ Q. It is called finite if δ is a finite set. The elements of δ are called transitions, and the element u ∈ M is the label of the transition (p, u, q). Roughly speaking, the automaton A decorates the elements of M with states, by assigning to each u ∈ M possible runs. A run on A is a sequence of the form

![](images/193_6.jpg)

with (qi , ui , qi+1) ∈ δ for all 1 ≤ i ≤ n. We say r is a run on u ∈ M, if u = u1 ⋅⋅ ⋅ un; it is accepting if q1 ∈ I and qn+1 ∈ F. The accepted set of A is

![](images/193_5.jpg)

Two M -automata are equivalent if they accept the same set. For a given generating set Σ of M, an automaton A is called spelling if δ ⊆ Q × Σ × Q, that is, if all labels are elements of Σ. A spelling nondeterministic M-automaton is called complete if for each state p ∈ Q and each a ∈ Σ, there exists some (p, a, q) ∈ δ. It is called deterministic if the set of initial states I contains exactly one state and if for each state p ∈ Q and each element u ∈ M there is at most one state q ∈ Q such that there is a run pu1q1 ⋅⋅ ⋅ unqn with u = u1 ⋅⋅ ⋅ un and qn = q. For a complete and deterministic spelling automaton, we can define p ⋅ u = q and we obtain an M-automaton in the sense of [Section 7.1](#chapter07_1.xhtml_chapter07_1_2). Conversely, by choosing a generating set Σ for M, each M-automaton as defined in [Section 7.1](#chapter07_1.xhtml_chapter07_1_2) can be converted into a complete and deterministic spelling automaton in the in the sense given earlier. The notion of nondeterministic M-automaton is therefore more general than the term M-automaton as used before.

The following automaton over the monoid ℕ×ℕwith addition as operation recognizes the set { (m, n) | m = n − 4, m even }:

![](images/194_1.jpg)

For the conversion of rational sets to nondeterministic automata, we use the Thompson construction [[103](#Bibliography.xhtml_Bibliography_104)] named after Kenneth Lane Thompson (born 1943). He is a well-known computer science pioneer and primarily known for his work as a co-developer of the Unix operating system.

Lemma 7.11. For each set, L ∈ RAT(M) there is a nondeterministic finiteM-automatonA with L = L(A).

Proof: Let 1 ∈ M be the neutral element. For every rational set L, we construct an automaton AL with the following invariants:

□

–L = L(*A*L)

–*A*L has exactly one initial state i L. It will be the single state without incoming transitions.

–*A*L has exactly one final state fL ≠ i L. It will be the single state without outgoing transitions.

The construction is by induction on the number of nested operations union, product and star, which are necessary to obtain L. If L = {u1, . . . , un} is finite, then AL is the following automaton:

![](images/195_1.jpg)

If L = K ∪ K' for K, K' ∈ RAT(M) and if the automata AK and AK' are constructed already, then AL is given by

![](images/195_2.jpg)

This means that we take the disjoint union of AK and AK ' including all transitions and add a new initial state i L and a new final state fL. If L = KK', then *A*L is defined by

![](images/195_3.jpg)

For L = K ∗ we finally define

![](images/195_4.jpg)

The last construction for L = K ∗ is correct because in AK there is no incoming arc to i k and there is no outgoing arc leaving fK. Thus, L = L(AL) in all cases.

□

Next, we show that for all automata one can assume that there are no ε-transition of the form (p, 1, q). Such a transition allows a spontaneous switch from state p to q. Accordingly, the procedure in the following proof is often referred to as elimination of ε-transitions.

Lemma 7.12. Let A be a nondeterministic finite M-automaton and Σ a given generating set of M. Then there exists an equivalent nondeterministic finite M-automatonBaccepting L with labels from Σ and only one initial state.

Proof: We transform A = (Q, δ, I, F) by a sequence of substitutions into the automaton B = (Q' , δ' , {i}, F) having the desired properties. Since δ is finite, we can assume Q to be finite, too. Let u ∈ M \ (Σ ∪ {1}) and let (p, u, q) ∈ δ be a transition. Then there exists a1, . . . , an ∈ Σ with u = a1 ⋅⋅ ⋅ an and n ≥ 2\. We add new states q1, . . . , qn−1 to Q and remove the transition (p, u, q) from δ. Then we add the transitions

![](images/196_1.jpg)

In this manner, we proceed with every transition whose label is in M \ (Σ ∪ {1}). Next, we add a new state i and transitions { (i, 1, q0) | q0 ∈ I }. From now on, the state i is the only initial state. By introducing more transitions with label 1, we can assume that whenever (p, 1, q) and (q, 1, r) are transitions, then (p, 1, r) is a transition, too. We define the set of final states as

![](images/196_2.jpg) F' = F ∪{ p ∈ Q | (p, 1, q) is a transition with q ∈ F }

This does not change the accepted set. Therefore, we have now obtained an automaton B' = (Q' , δ,' {i}, F), which is equivalent to A and whose labels all are in Σ ∪ {1}.

We now remove all transitions (p, 1, q) ∈ δ' and add the transitions

![](images/196_3.jpg) { (p, a, q) (q, a, q) ∈ δ,' a ∈ Σ }

instead. This yields the automaton B. Each run in *B* has a canonical counterpart in B. Now let r = q0u1q1 ⋅⋅ ⋅ unqn be an accepting run of B' with ui ∈ Σ∪{1}. Since we added all transitive 1-transitions to B' ,we can assume that two consecutive labels ui and ui+1 never are both 1. By construction of F, we can assume that un ≠ 1 (except for n = 0). So if ui = 1, then i < n and ui+1 ≠ 1\. Therefore, in the case ui = 1, we can always replace the partial run qi−1uiqiui+1qi+1 of r by qi−1ui+1qi+1 and obtain an accepting run in B. This shows L(*B*) = L(*B*'). Together with L(*B*') = L(*A*), the proof of the lemma is complete.

□

Generalizing nondeterministic automata, we now allow rational sets as labels. An M-automaton with rational labels is a tuple A = (Q, δ, I, F), where Q, I, F are have the same meaning as in the definition of nondeterministic automata and δ is a subset of Q×RAT(M)×Q. A run ofAis a sequence of the form q0u1q1 ⋅⋅ ⋅ unqn with qi ∈ Q, ui ∈ M and for all i ∈ {1, . . . , n} there is a transition (qi−1, Li , qi)∈ δ with ui ∈ Li. Accepting runs and the accepted set L(*A*) of A are defined as above. As before, A is called finite if δ is a finite set. Of course, this does not mean that a rational set L ∈ RAT(M) which occurs as a label of a transition has to be finite.

Next, we want to show that nondeterministic automata accept rational sets. We do so by changing labels of transitions; see the proof of the next lemma. The method is often referred to as state elimination.

Lemma 7.13. Let A be a finite M-automaton with rational labels. Then L(*A*) ∈ RAT(M).

Proof: Let A = (Q, δ, I, F). Without loss of generality Q = {q2, . . . , qn} with n ≥ 2\. Since the class of rational sets is closed under union, we can assume that for all qi , qj ∈ Q at most one transition (qi , Li,j, qj)∈ δ exists. We add two new states q0 and q1 to Q and obtain the set of states Q' = {q0, . . . , qn}. Define

![](images/197_5.jpg)

The automaton B = (Q' , δ' , {q0}, {q1}) is equivalent to A. Moreover, B satisfies the following invariants; the initial state q0 has no incoming transitions, the final state q1 has no outgoing transitions and for qi , qj ∈ Q' there is at most one transition (qi , Li,j, qj)∈ δ. Moreover, Li,j ∈ RAT(M). In the following, we let Li,j = 0 if there is no transition from qi to qj.

We continue the process of “state elimination” as long as n > 1\. If this is the case, we construct an automaton C = (Q,' δ,' q0, q1) equivalent to B with Q' = {q0, . . . , qn−1} such that C also satisfies the three invariants of B. First, we remove the state qn and all its adjacent transitions, then we replace each transition (qi , Li,j, qj)∈ δ' with i, j < n by ![](images/197_2.jpg) where

![](images/197_6.jpg)

The procedure is also visualized in the following picture:

![](images/197_4.jpg)

By repeatedly eliminating states, we can assume that in B we eventually have n = 1\. By construction, we obtain L(B) = L0,1 ∈ RAT(M).

□

Theorem 7.14. Let M be a monoid and L ⊆ M. Then the following statements are equivalent:

(a)L is rational.

(b)L is accepted by a nondeterministic finite M-automaton.

(c)L is accepted by a nondeterministic finite spelling M-automaton with only one initial state.

(d)L is accepted by a finite M-automaton with rational labels.

Proof: The implication (a) ⇒ (b) is [Lemma 7.11](#chapter07_1.xhtml_chapter07_1_23), and (b) ⇒ (c) can be seen with [Lemma 7.12](#chapter07_1.xhtml_chapter07_1_25). For (c) ⇒ (d) one replaces all transitions (p, u, q) by (p, {u}, q). Finally, (d)⇒(a) is [Lemma 7.13](#chapter07_2.xhtml_chapter07_2_1).

Lemma 7.15. Every rational subset L ⊆ Mis contained in a finitely generated submonoid of M.

Proof: Since every nondeterministic finite automaton Ahas only finitely many edges, only finitely many labels U ⊆ M can occur. In particular, L(A) ⊆ U∗ ⊆ M. Therefore, by [Theorem 7.14](#chapter07_2.xhtml_chapter07_2_2) every rational subset L of M is contained in a finitely generated submonoid of M.

□

A consequence of the previous lemma is that M is a rational subset of M if and only if M is finitely generated. In particular, the class of rational subsets is not closed under inverse homomorphisms, because the homomorphism ψ: M → {1} yields the subset M as preimage of the rational subset {1}. However, rational subsets are closed under homomorphisms, because in nondeterministic automata one can replace every label by its homomorphic image.

The next theorem of Dawson James McKnight, Jr. (1928–1981) characterizes finitely generated monoids by the inclusion of REC(M) into RAT(M), see [[74](#Bibliography.xhtml_Bibliography_74)].

Theorem 7.16 (McKnight). A monoid M is finitely generated if and only if REC(M) ⊆ RAT(M).

Proof: The recognizable set M by [Lemma 7.15](#chapter07_2.xhtml_chapter07_2_4) can only be rational if Mis finitely generated. The converse follows from [Theorem 7.14](#chapter07_2.xhtml_chapter07_2_2) because, if M is finitely generated, then we can view a finite M-automaton (in the sense of [Section 7.1](#chapter07_1.xhtml_chapter07_1_2)) as a nondeterministic spelling automaton.

□

If M is a free monoid over a finite alphabet, then the rational sets inside M are also called regular. In the next section, we deal with regular languages. We will see that the regular languages and the recognizable sets coincide; this is Kleene’s theorem.

## 7.3 Regular languages

We have seen that the classes of recognizable and rational subsets are incomparable, in general. Finite subsets of M are always rational, but they are not recognizable, for example, in infinite groups; see [Remark 7.1](#chapter07_1.xhtml_chapter07_1_3). On the other hand, the recognizable set ℕ over the monoid of natural numbers ℕwith multiplication as operation is not rational since the monoid (ℕ, ⋅, 1) is not finitely generated.

In the following, we will stick to the convention of speaking about languages and words whenwemean subsets and elements in finitely generated free monoids. We now show that the properties of being regular, rational and recognizable are equivalent for finitely generated free monoids. This result is known as Kleene’s theorem on regular languages [[54](#Bibliography.xhtml_Bibliography_54)].

Theorem 7.17 (Kleene). Let Σ be a finite alphabet. Then REC(Σ∗) = RAT(Σ∗).

Proof: The inclusion REC(Σ∗)⊆ RAT(Σ∗) follows from [Theorem 7.16](#chapter07_2.xhtml_chapter07_2_6). Now, let L ⊆ Σ∗ be rational. From [Theorem 7.14](#chapter07_2.xhtml_chapter07_2_2), we know that a spelling nondeterministic finite Σ∗- automaton A = (Q, δ, I, F) with n = |Q| states exists which accepts the language L. Using the so-called subset construction, we design an equivalent deterministic automaton with at most 2n states. The result of this construction is the subset automaton B. The states of B are subsets of Q, which explains the upper bound 2n. The construction starts by defining I ⊆ Q as the unique initial state in B. Suppose that P ⊆ Q has already been defined as a state of B. For each letter a ∈ Σ define

![](images/199_3.jpg)

We add the set P ⋅ a to the set of states of B if it is not there already, making more and more subsets of Q become states of B.

For all words w ∈ Σ∗, the state I ⋅ w of B consists of all states q ∈ Q of A for which a run of A on w, starting in some initial state p ∈ I and ending at q, exists. The proof of this fact is carried out by induction on the length of w. Accordingly, we define the final states of B as the set of subsets which contain at least one final state of A. So, B defines the desired deterministic automaton, which accepts L.

□

Let Σ be a finite alphabet, then we denote by REG(Σ∗) the family of regular languages. [Theorem 7.17](#chapter07_2.xhtml_chapter07_2_10) says REG(Σ∗) = REC(Σ∗) = RAT(Σ∗). By general closure properties of recognizable and rational sets, [Theorem 7.2](#chapter07_1.xhtml_chapter07_1_4) and [Remark 7.10](#chapter07_1.xhtml_chapter07_1_20), we obtain the following assertion.

Corollary 7.18. Let Σ be a finite alphabet. Then REG(Σ∗) is a Boolean algebra. If φ: Σ∗ → Γ∗ is any homomorphism to a finitely generated monoid, then we have φ(REG(Σ∗))⊆ REG(Γ∗) and φ−1(REG(Γ∗))⊆ REG(Σ∗).

The corresponding constructions in [Corollary 7.18](#chapter07_2.xhtml_chapter07_2_11) are effective. This means, if regular languages L and K are given, for example, by rational expressions, then we can effectively construct a recognizing homomorphism or a rational expression for, say, L \ K. The next theorem states another useful closure property for regular languages, but effectiveness is not always guaranteed.

Theorem 7.19. Let Σ be a finite alphabet, L ∈ REG(Σ∗) be a regular language and K ⊆ Σ∗ be any language. Then the quotient

![](images/199_4.jpg)

is regular. Moreover, if K is regular, and if L and K are specified by accepting finite automata, then we can effectively find an automaton accepting LK−1.

Proof: Let us assume that L is given by some finite automaton with state space Q and set of final states F. In order to define an accepting automaton for LK−1 we enlarge the set of final states to the new set

![](images/200_5.jpg)

It is clear that the new automaton accepts the quotient LK−1. If K is given by a finite automaton, then we can use, for example, the product automaton construction to compute F.

The effectiveness in [Theorem 7.19](#chapter07_2.xhtml_chapter07_2_12) is given if K belongs to a class of formal languages where first, the class is closed under intersection with regular sets and second, we can decide emptiness. So, [Theorem 7.19](#chapter07_2.xhtml_chapter07_2_12) is effective for “context-free” but not for “context-sensitive” languages; see for example [[51](#Bibliography.xhtml_Bibliography_51)].

Over a finitely generated free monoid Σ∗ the concepts of deterministic and nondeterministic finite automata are equivalent. Henceforth, we say that a nondeterministic finite automaton (Q, δ, I, F) is spelling if the transition relation δ is a subset of Q×Σ×Q. We also use the notation NFA as an abbreviation for a spelling automaton. We use the abbreviation ε-NFA if δ ⊆ Q × (Σ ∪ {ε}) × Q. The subset construction in the proof of [Theorem 7.17](#chapter07_2.xhtml_chapter07_2_10) shows that for every ε-NFA with n states there exists an equivalent deterministic one with at most 2n states. Equivalence means that they both accept the same language L ⊆ Σ∗. Minimization leads to the minimal automaton AL and its transition monoid is the syntactic monoid Synt(L); it is the smallest recognizing monoid for L. This construction yields ![](images/200_2.jpg) because first, AL has at most 2n states (and this bound is tight) and second, for an automaton A with s states, the transition monoid has at most ss states (and this bound is tight again). However, if we start with an ε-NFA with n states which accepts a language L, then the proof of the next theorem shows that we can realize a recognizing homomorphism inside the monoid of Boolean n × n-matrices. This yields |Synt ![](images/200_7.jpg) . To see the difference, consider n = 3\. The number ![](images/200_6.jpg)is greater than 10 million, but ![](images/200_8.jpg) Another advantage of using n × n-matrices is that they can be multiplied efficiently.

Theorem 7.20. Let Σ be finite and *A* an ε-NFA over Σ∗ with n states. Then, the syntactic monoid of L = L(*A*) has at most ![](images/200_9.jpg)elements.

Proof: Let A = (Q, δ, I, F) where without loss of generality Q = {1, . . . , n}. By assumption, we have δ ⊆ Q × (Σ ∪ {ε}) × Q. Removing ε-transitions does not increase the set of states. Thus, without loss of generality we may assume δ ⊆ Q × Σ × Q. For each letter a ∈ Σ, we define a Boolean n × n-matrix Aa ∈ n×n by letting the entry ![](images/200_3.jpg) to be 1 if ![](images/200_4.jpg) otherwise. The Boolean values ' = {0, 1} with the disjunction ∨ as addition and the conjunction ∧ as multiplication form a semiring, and, hence, the Boolean n × n-matrices with multiplication forma monoid n×n. Thus, the mapping a ↦ φ(a) = Aa defines a homomorphism φ from Σ∗ to ![](images/b.jpg)n×n. If w = a1 ⋅⋅ ⋅ am is a word and φ(w) = B = Aa1 ⋅⋅ ⋅ Aam, then Bi,j = 1 is true if and only if there is a path from i to j labeled by w. Moreover, for P = {B ∈ n×n | ∃i ∈ I, j ∈ F : Bi,j = 1 }, we obtain φ−1(P) = L. Therefore, φ recognizes the language L. By [Theorem 7.4](#chapter07_1.xhtml_chapter07_1_7), the syntactic monoid is the homomorphic image of a submonoid of n×n. Therefore, it contains at most 2n2 elements.

□

An important consequence of Kleene’s theorem is that the class of regular languages is closed under finite intersection and complementation. As shown by the following example, RAT(M) is not closed under finite intersection, in general. Moreover, if RAT(M) is not closed under finite intersection, then it is not closed under complementation by the rules of De Morgan (Augustus De Morgan, 1806–1871).

Example 7.21 (Nonclosure under finite intersection). Let M = {a, c}∗ × b∗. Algebraically M is a direct product of two free monoids. Let L = (a, b)∗(c, 1)∗ and K = (a, 1)∗(c, b)∗. The sets L, K ⊆ M are rational. We can represent the intersection L ∩ K by the set { (ancn, bn) | n ∈ ℕ}. Consider the projection π : M → {a, c}∗ which erases the second component. This is a homomorphism and the image of (ancn, bn)∈ M is ancn. Thus, π(L ∩ K) = { ancn | n ∈ ℕ}. It is clear that for m ≠ n the words am and an are not syntactically equivalent. This is true for all four languages L, K, L ∩ K ⊆ M, and π(L ∩ K). Hence, none of them is recognizable. The point is that {a, c}∗ is free. Hence by Kleene’s theorem, π(L ∩ K) is not rational. Since the rational subsets are closed under homomorphic, L ∩ K is not rational.

◊

## 7.4 Star-free languages

A fundamental result by Schützenberger relates star-free languages (defined in the following) to finite aperiodic monoids [[92](#Bibliography.xhtml_Bibliography_93)].Here, a monoid N is called aperiodic if there exists n ∈ ℕ such that un+1 = un for all u ∈ N. Aperiodic monoids are orthogonal to groups. A nontrivial group is never aperiodic; and if in an aperiodic monoid M an element u has a right-inverse υ with uυ = 1, then u = υ = 1. Indeed, if uυ = 1, then unυn = 1 for all n ∈ ℕ. Now, if in addition un+1 = un for some n, then u = u unυn = un+1υn = unυn = 1\. (The situation for υ is symmetric.) Thus, aperiodic monoids are also called group-free.

Local divisors

We begin with a useful construction on monoids, which simplifies the proof of [Theorem 7.22](#chapter07_2.xhtml_chapter07_2_22) and is also the main tool in [Section 7.5](#chapter07_2.xhtml_chapter07_2_30). Local divisors also show up in [Section 7.6](#chapter07_3.xhtml_chapter07_3_23). For further applications, we refer to [[23](#Bibliography.xhtml_Bibliography_24)–[30](#Bibliography.xhtml_Bibliography_30)].

Let M be a monoid and c ∈ M. We define a new operation ∘ on its subset cM ∩ Mc by

![](images/201_2.jpg)

Assume that xc = x'c and cy = cy'. Then xc ∘ cy = xcy = x'cy = x'cy' = x'c ∘ cy'. This shows that ∘ is well defined. Let cx = xc and cy be elements of cM ∩ Mc. Then cx ∘ cy = x'c ∘ cy = x'cy = cxy. Computation rules of M carry over to cM ∩ Mc. In particular, the operation ∘ on cM ∩ Mc is associative, because the operation of M is associative. Thus, Mc = (cM ∩ Mc, ∘, c) is a monoid with c as its neutral element; it is called the local divisor of M at c. If xn = xn+1 for all x ∈ M, then a straightforward computation shows that we have yn = yn+1 for all y in the local divisor Mc, too. Indeed, let cx = yc ∈ cM ∩ Mc and n ∈ ℕ. Taking the fold power of xc in the monoid Mc, we obtain xnc. Thus, any local divisor of an aperiodic monoid is aperiodic. Actually, Mc is the homomorphic image of the submonoid { x ∈ M | xc ∈ cM } under the mapping φ(x) = xc. The mapping φ is a homomorphism since φ(x)φ(y) = (xc) ∘ (yc) = xyc = φ(xy) and φ(1) = c, which is the neutral element in Mc. Moreover, since each y ∈ Mc = cM ∩Mc can be written as y = xc, we obtain φ(x) = y and φ is surjective. Hence, Mc is indeed a “divisor” in the sense of [Section 7.5](#chapter07_2.xhtml_chapter07_2_30). Moreover, if c is idempotent (i.e., c2 = c), then Mc is isomorphic to the so-called local submonoid cMc of M. These two properties coined the notion of local divisor. If M is aperiodic and 1 ≠ c ∈ M, then we have seen cm ≠ 1 for all m ∈ M. Therefore, |cM ∩ Mc| < |M|. This is the crucial property that make local divisors attractive for induction.

SF = AP

As an application of the algebraic approach for recognizable languages, we present a decidable characterization of star-free languages. Decidability means that for any standard way to represent a regular language L, say, for example, by an accepting NFA, there is an algorithm which returns “yes” if and only if L is star free. Moreover, in the positive case it gives a star-free expression for L.

The family SF(M) of star-free sets over M is inductively defined as follows:

–IfL is a finite subset of M, then L ∈ SF(M).

–IfK, L ∈ SF(M), then also K ∪ L ∈ SF(M) and KL ∈ SF(M).

–IfL ∈ SF(M), then also M \ L ∈ SF(M).

Since SF(M) is closed under finite union and complementation, SF(M) is closed under finite intersection, too. In contrast to a regular expression, a star-free expression may use complementation, but but no Kleene star. This explains its name “star-free.”

Consider the singletons {aa} and {ab} in {a, b}∗. Singletons are star free by definition. In [Example 7.25](#chapter07_2.xhtml_chapter07_2_28), we will see that {aa}∗ is not a star-free language, whereas {ab}∗ is star free (if a ≠ b). Thus, a star in the syntactic description does not tell us whether the corresponding language is star free or not. The example {aa}∗ also shows that the class of star-free languages is not closed under Kleene star. Regular star-free languages are regular. However, over arbitrary monoids, the class of rational sets and the class of star-free sets are incomparable, in general.

The next theorem by Schützenberger is often considered the second most important fundamental theorem on regular languages (after Kleene’s theorem).

Theorem 7.22 (Schützenberger). Let L ⊆ Σ∗ be a language over a finite alphabet Σ. Then the following assertions are equivalent:

(a)L is star free.

(b)The syntactic monoid Synt(L) is finite and aperiodic.

(c)L is recognized by a finite aperiodic monoid.

The remainder of this section is devoted to the proof of this theorem. For a finite alphabet Σ, the class of regular star-free languages SF(Σ∗) can alternatively be defined as follows: first, 0 ∈ SF(Σ∗), second, if a ∈ Σ, then {a} ∈ SF(Σ∗), and third, for languages K, L ⊆ SF(Σ∗) the languages K ∪ L, Σ∗ \ L, and KL are elements of SF(Σ∗). Let Γ ⊆ Σ, then Γ∗ is star free

![](images/203_1.jpg)

Moreover, SF(Γ∗) ⊆ SF(Σ∗) because given a star-free expression for L ∈ SF(Γ∗), we can substitute every complementation Γ∗ \ K by (Σ∗ \ K)∩ Γ∗. We can replace an intersection by using complementation, union, and complementation. This yields a star free expression for L over the alphabet Σ.

Lemma 7.23. The syntactic monoid of a star-free language is aperiodic.

Proof: We show that for every star-free language L ∈ SF(Σ∗), there exists a number n(L) ∈ℕsuch that for all x, y, u ∈ Σ∗:

□

![](images/203_3.jpg)

We set n(0) = 1, and for a ∈ Σ, we define n({a}) = 2\. Now let K, L ∈ SF(Σ∗) be languages for which n(L) and n(K) are suitably defined already. Then, we let n(Σ∗ \L) = n(L), as well as n(K ∪ L) = max(n(K), n(L)) and n(KL) = n(K)+ n(L)+1\. We only prove the correctness of n(KL); the according proofs for the other constructions are similar. Let w = xun(K)+n(L)+2y ∈ KL. We assume that the splitting of w = w1w2 into w1 ∈ K and w2 ∈ L is done within one of the u-factors. Splittings inside x or y are easier. Let u = uu, w1 = xun1u' ∈ K and w2 = uun2 y ∈ L with n1 +1+ n2 = n(K)+ n(L)+2\. We have either n1 ≥ n(K)+1 or n2 ≥ n(L)+1.Without loss of generality, let n1 ≥ n(K)+1\. By our assumptions, xun1−1u' ∈ K and hence xun(K)+n(L)+1y ∈ KL. Analogously, one can show that xun(K)+n(L)+1y ∈ KL implies xun(K)+n(L)+2y ∈ KL.

The difficult part in the proof of Schützenberger’s theorem is handled next. We present the proof from [[62](#Bibliography.xhtml_Bibliography_63)].

Lemma 7.24. If L ⊆ Σ∗ is recognized by a finite aperiodic monoid M, then L is star free.

Proof: Let φ: Σ∗→M be a homomorphism recognizing L.Wehave L =⋃p∈φ(L) φ−1(p). Therefore, it suffices to show for all p ∈ M, that φ−1(p) is star free. Let Σ1 = {a ∈ Σ | φ(a) = 1 }. In aperiodic monoids uυw = 1 implies uυ = 1 and this implies υ = 1\. Hence, ![](images/204_1.jpg)

□

Next, let p ≠ 1. For c ∈ Σ with φ(c) ≠ 1, we define Σc = Σ \ {c}. Restricting φ to the domain ![](images/204_2.jpg) now yields the homomorphism ![](images/204_3.jpg) with w ↦ φ(w). Since each word w with φ(w) ≠ 1 contains a letter c with φ(c) ≠ 1, we obtain

![](images/204_4.jpg)

The language ![](images/204_5.jpg) contains the prefix before the first c and ![](images/204_6.jpg) corresponds to the suffixes after the last c. By induction on the size of the alphabet, we obtain that ![](images/204_7.jpg) and ![](images/204_8.jpg) are elements of ![](images/204_9.jpg) It remains to show that for p ∈ φ(c)M∩Mφ(c) the language φ−1 (p)∩cΣ∗∩Σ∗c is star free. Let ![](images/204_10.jpg) We define a substitution

![](images/204_19.jpg)

where ![](images/204_12.jpg) Here, T∗ denotes the free monoid over the set T rather than the Kleene star. The mapping σ replaces maximal c-free factors υ by φc(υ). Let ψ: T∗ → Mφ(c) be the homomorphism into the local divisor of M at φ(c), that results from T → M φ(c) with φc(w) → φ(cwc) by the universal property of free monoids ([Theorem 6.1](#chapter06.xhtml_chapter06_5)). For w = cυ1cυ2 ⋅⋅ ⋅ cυk ∈ {ε} ∪ cΣ∗ with ![](images/204_13.jpg) and k ≥ 0, we have

![](images/204_17.jpg)

Thus,

![](images/204_20.jpg)

and hence φ−1(p) ∩ cΣ∗ ∩ Σ∗c = σ−1ψ−1(p) ⋅ c. Therefore, it is sufficient to show that σ−1ψ−1(p) ∈ SF(Σ∗). Recall that we have φ(c) ≠ 1, hence |Mφ(c)| < |M| since M is aperiodic. By induction on the size of the recognizing monoid, we obtain ψ−1(p) ∈ SF(T∗), and by induction on the size of the alphabet φ−c 1 (t) ∈ SF(Σ∗) for all t ∈ T. By structural induction, we now show that σ−1(K) ∈ SF(Σ∗) for every language K ∈ SF(T∗):

![](images/204_18.jpg)

The last relation holds because of σ(cw1cw2) = σ(cw1)σ(cw2).

□

Proof of Theorem 7.22: If L is recognized by a finite aperiodic monoid, then, by [Lemma 7.24](#chapter07_2.xhtml_chapter07_2_25), L is star free. If L is star free, then by [Lemma 7.23](#chapter07_2.xhtml_chapter07_2_23) Synt(L) is aperiodic. With Kleene’s theorem ([Theorem 7.17](#chapter07_2.xhtml_chapter07_2_10)), we obtain SF(Σ∗) ⊆ RAT(Σ∗) and that all star-free languages are recognizable. By [Theorem 7.9](#chapter07_1.xhtml_chapter07_1_18), Synt(L) is finite. Since Synt(L) recognizes the language L, there is some finite aperiodic monoid recognizing L. Schützenberger’s theorem follows.

Given a regular expression for L, we can effectively compute the corresponding syntactic monoid. Given a finite monoid we can check whether x|M|+1 = x|M| for all x ∈ M. This last condition expresses that a finite monoid is aperiodic. Thus, whether a given regular language is star free can be checked using this method.

Example 7.25. Let Σ = {a, b}. The language L = (ab)∗ ∈ RAT(Σ∗) is star free, because

![](images/205_2.jpg)

The syntactic monoid of L has six elements {1, a, b, ab, ba, 0}. It is aperiodic because x3 = x2 for all elements x. In contrast, the syntactic monoid of the language (aa)∗ ∈ RAT({a}∗) is the group ℤ/2ℤ, so (aa)∗ is not star free.

◊

Star-free languages play a central role in formal verification. In this area, specifications are formulated using some simple logical formalism; and many popular logics turn out to have exactly the same expressive power as star-free languages. For a survey, refer to [[24](#Bibliography.xhtml_Bibliography_25)].

## 7.5 Krohn–Rhodes theorem

Krohn and Rhodes studied the structure of finite monoids via decompositions. In 1965, they showed that every finite monoid can be represented as a wreath product of flip–flops and finite simple groups [[59](#Bibliography.xhtml_Bibliography_60)]; here, a flip–flop is a three element monoid. A representation as a wreath product of flip–flops and finite simple groups is called a Krohn–Rhodes decomposition. The most common presentation of the Krohn–Rhodes theorem uses so-called transformation monoids; see [[29](#Bibliography.xhtml_Bibliography_29), [38](#Bibliography.xhtml_Bibliography_38), [60](#Bibliography.xhtml_Bibliography_61), [87](#Bibliography.xhtml_Bibliography_88), [101](#Bibliography.xhtml_Bibliography_102)]. The concept of transformation monoids is a mixture of automata and monoids. Gérard Lallement (1935–2006) published a proof of the Krohn–Rhodes theorem in 1971, which only uses monoids in the traditional sense [[63](#Bibliography.xhtml_Bibliography_64)]; unfortunately, his proof had a flaw, and the corrected version relies on a more technical notion of wreath products [[64](#Bibliography.xhtml_Bibliography_65)]. The proof presented here only uses monoids in the traditional sense, too, but it is inspired by a similar proof using transformation monoids [[29](#Bibliography.xhtml_Bibliography_29)]. The main technique is local divisors as introduced in [Section 7.4](#chapter07_2.xhtml_chapter07_2_16). As a byproduct of this approach, we do not use any semigroups which are not monoids.

We start this section with an introduction to some useful terminology, including divisors and wreath products. In order to prove that a monoid T divides some given wreath product, it is often more illustrative to apply the so-called wreath product principle. Then, we consider flip–flops and their generalizations; monoids where every nonneutral element is a right zero. We present a decomposition technique for arbitrary finite groups into simple groups. A group G is simple if {1} and G are its only normal subgroups. The induction parameter in our proof of the Krohn–Rhodes theorem is the number of elements x satisfying {x} ≠ Mx ≠ M, that is, the elements which are neither a right zero nor invertible. We decompose a monoid M into a local divisor Mc and an augmented submonoid N#. The latter is a monoid extension of N, where, for every element x ∈ N, there exists a unique right zero ![](images/206_1.jpg) such that ![](images/206_2.jpg) for all x, y ∈ N. Moreover, the right zeros of N are also right zeros in N #

We need the following notions to state the Krohn–Rhodes theorem; further details aregiven in the following. AmonoidM is a divisor of a monoid N ifM is a homomorphic image of a submonoid of N. Let MN be the set of all mappings f : N → M. The wreath product M ≀ N is the set MN × N with the composition (f, a)(g, b) = (h, ab) where the mapping h : N → M is defined by h(x) = f(x)g(xa) for x ∈ N. The flip–flop monoid U2 = {1, a, b} with neutral element 1 is defined by xa = a and xb = b for all x ∈ U2.

Theorem 7.26 (Krohn, Rhodes). Let M be a finite monoid. Let CM be the closure of U2 and all simple group divisors of M under wreath products. Then M divides a monoid in CM.

A simple group divisor is a divisor which is a simple group. Another way of stating the Krohn–Rhodes theorem is by saying that every finite monoid M divides a sequence of wreath products where each factor is either the flip–flop U2 or a simple group divisor of M; such a sequence is called a Krohn–Rhodes decomposition of M. We note that the wreath product ≀ on monoids is not associative, that is, in general (M ≀ N) ≀ T is not isomorphic to M ≀ (N ≀ T). The corresponding operation on transformation monoids is associative.

Throughout this section, for a finite monoid M, we let CM be the smallest class of finite monoids containing U2 and the simple group divisors of M such that the wreath product of any two monoids in CM is again in CM. After some preparatory work (on divisors and wreath products), we prove the Krohn–Rhodes theorem by showing that it holds for bigger and bigger classes of monoids until, at the end of this section, we are able to give the proof for arbitrary monoids.

Divisors and surjective partial homomorphisms

Let M and N be monoids. If a submonoid U of N and a surjective homomorphism φ: U → M exist, then M is a divisor of N. In this case, we write M ≺ N. The intuitive idea is that N is more powerful than M (for instance, in the sense that every language recognizable by M is also recognizable by N). A group divisor is a divisor which forms a group. In many cases, it is more convenient to work with surjective partial homomorphisms to prove M ≺ N. A partial mapping ψ: N → M is a partial homomorphism if ψ(nn) is defined whenever both ψ(n) and ψ(n) are defined, and then we have ψ(nn) = ψ(n)ψ(n' ). As usual, the partial homomorphism ψ is surjective if for every m ∈ M there exists n ∈ N with ψ(n) = m. As shown in the following lemma, a surjective partial homomorphism is a mere reformulation of division.

Lemma 7.27. We have M ≺ N if and only if there exists a surjective partial homomorphism ψ: N → M.

Proof: First, let M ≺ N. Then there is a submonoid U of N and a surjective homomorphism ψ: U → M. The mapping ψ is a surjective partial homomorphism from N to M. For the other direction, let ψ: N → M be a partial homomorphism. The domain of ψ is a subsemigroup U of N. If U contains the neutral element 1 of N, then ψ(n) = ψ(n ⋅ 1) = ψ(n)ψ(1) for all n ∈ U. This shows that ψ(1) is neutral for all elements ψ(n). Since ψ is surjective, we obtain ψ(1) = 1.Hence, ψ: U → Mis a surjective homomorphism. If 1 ∉ U, let φ: U ∪ {1} → M be defined by φ(1) = 1 and φ(n) = ψ(n) for n ∈ U. Then U ∪ {1} is a submonoid of N and φ is a surjective homomorphism.

□

We freely apply [Lemma 7.27](#chapter07_2.xhtml_chapter07_2_42) without further reference.

Lemma 7.28. If M ≺ N and N ≺ T, then M ≺ T.

Proof: Let ψ1 : N → M and ψ2 : T → N be surjective partial homomorphisms. Then their composition ψ1 ∘ ψ2 : T → M is a surjective partial homomorphism.

□

Wreath products

For a monoid M and an arbitrary set X, let MX = {f : X → M | f is a mapping }. For f, g ∈ MX, we define f ∗ g by (f ∗ g)(x) = f(x) g(x). The set MX can be interpreted as a product of |X| copies of M, and ∗ is the pointwise operation on the components. In particular, MX forms a monoid with ∗ as the operation.

Let M and N be two monoids. For g : N → M and a ∈ N the mapping ag: N → M is defined by (ag)(x) = g(xa). Note that a(f ∗ g) = af ∗ ag. We can now define an operation on MN × N as follows. For pairs (f, a) and (g, b) in MN × N, we set

![](images/207_3.jpg)

For the set MN × N with this operation, we write

![](images/207_4.jpg)

and call it the wreath product of M and N. Next, we show that M ≀ N forms a monoid. The neutral element is (ι, 1) with ι(x) = 1 for all x ∈ N. Consider (f, a), (g, b), (h, c) ∈MN × N. Then the following computation shows that the operation in M ≀ N is associative:

![](images/208_4.jpg)

Next, we show that the direct product is a divisor of the wreath product.

Lemma 7.29. Let M and N be two monoids. Then M × N ≺ M ≀ N.

Proof: Let U be the submonoid ofMN ×N consisting of all the elements (f, a) such that f is constant, that is, there exists m ∈ M with f(x) = m for all x ∈ N. A surjective homomorphism φ: U → M × N is given by φ(f, a) = (f(1), a). Note that f(1) = f(x) for all x ∈ N since f is constant. This yields φ((f, a) (g, b)) = φ(f ∗ ag, ab) = (f(1) g(a), ab) = (f(1) g(1), ab) = (f(1), a) (g(1), b) = φ(f, a) φ(g, b).

□

As the following lemma shows, the division relation between monoids carries over to wreath products.

Lemma 7.30. If M ≺ S and N ≺ T, then M ≀ N ≺ S ≀ T.

Proof: Let σ : S → M and τ : T → N be surjective partial homomorphisms. Let

![](images/208_5.jpg)

be the functions in ST which are compatible with σ and τ. For (g, t) ∈ G × T, we define ψ(g, t) = (σ(g), τ(t)) ∈ MN × N by (σ(g))(n) = σ(g(τ−1(n))). By choice of G, the term σ(g(τ−1(n))) defines a unique element in M. For every mapping f : N → M, we can choose an extension fe ∈ G such that fe(t) = s for some s ∈ σ−1(f(τ(t))). If τ(t) is undefined, then fe(t) can be chosen arbitrarily; for instance, we could set fe(t) = 1 whenever τ(t) is undefined. If (f, n) ∈ MN × N and τ(t) = n, then ψ(fe , t) = (f, n). This shows that ψ is surjective. It remains to show that ψ is a partial homomorphism. Suppose that ψ(g, t) and ψ(ĝ, t̂) are defined. Then

![](images/208_6.jpg)

Note that if τ(t1) = τ(t2) is defined, then τ(t1t) = τ(t2t) is defined and thus σ(tĝ(t1)) = σ(ĝ(t1t)) = σ(ĝ(t2t)) = σ(tĝ(t2)). Therefore, we indeed have tĝ ∈ G and, hence, g ∗ tĝ ∈ G.

□

The combination of [Lemmas 7.28](#chapter07_2.xhtml_chapter07_2_43), [7.29](#chapter07_2.xhtml_chapter07_2_45) and [7.30](#chapter07_3.xhtml_chapter07_3_1) tells us that division ≺ is transitive and that it is compatible with wreath products and direct products. For instance, if both M and N divide some monoid in CT, then so do M ≀N andM ×N. Remember that CT is the closure of U2 and all simple group divisors of the monoid T under wreath products. We will apply these properties of division without further reference.

If ν : A∗ → N is a homomorphism to a monoid N, then we can consider the alphabet Aν = N × A and the length-preserving mapping ![](images/209_1.jpg) defined by

![](images/209_6.jpg)

for ai ∈ A. One can think of σν as decorating the ith letter ai with the element ν(a1 ⋅⋅ ⋅ ai−1) ∈ N. The homomorphism ν defines an automaton with states N whose transition function is given by n ⋅ a = nν(a). The initial state is the neutral element 1\. This allows to interpret the letter (ν(a1 ⋅⋅ ⋅ ai−1), ai) as a pair consisting of the previous state ν(a1 ⋅⋅ ⋅ ai−1) and the current letter ai.

Using these notions, we can introduce the wreath product principle as a method for showing division of wreath products. If M uses the decorated word σν(u) as input, then this behavior can also be realized by the wreath product M ≀ N on u.

![](images/209_3.jpg)

Fig. 7.1. Visualization of the wreath product M ≀ N as a cascade operation.

Proposition 7.31 (Wreath product principle). Let M, N, and T be monoids, and let φ: A∗ → T be a surjective homomorphism. Suppose there exist homomorphisms ν : A∗ → N and ![](images/209_7.jpg) such that, for all words u ∈ A∗, the images ν(u) and μ(σν(u)) together determine φ(u), that is,

![](images/209_8.jpg)

for all u, υ ∈ A∗. Then T ≺ M ≀ N.

Proof: For a ∈ A, we define fa : N → M by fa(n) = μ(n, a). Let ψ: A∗ → M ≀ N be the homomorphism defined by ψ(a) = (fa , ν(a)) for a ∈ A. For every word u = a1 ⋅⋅ ⋅ akwith ai ∈ A, the image ψ(u) = (f, ν(u)) satisfies

![](images/210_4.jpg)

This yields

![](images/210_5.jpg)

In particular, ψ(u) = ψ(υ) implies both ν(u) = ν(υ) and μ(σν(u)) = μ(σν(υ)), and thus it implies φ(u) = φ(υ). Therefore, ψ(u) ↦ φ(u) defines a surjective partial homomorphism M ≀ N → T.

□

There exists a converse of the wreath product principle as stated in [Proposition 7.31](#chapter07_3.xhtml_chapter07_3_4); see [Exercise 7.14](#chapter07_6.xhtml_chapter07_6_11): if T ≺ M ≀ N, then there exist homomorphisms ν and μ with the above properties. However, this direction uses a direct product of |N| copies of M when defining μ.

Using the notation from [Proposition 7.31](#chapter07_3.xhtml_chapter07_3_4), we give an automata theoretic view on the wreath product principle; see [Figure 7.1](#chapter07_3.xhtml_chapter07_3_3) for a sketch. Suppose we are given an input a1 ⋅⋅ ⋅ ak with ai ∈ A. Let n0 = 1 and ni = ν(a1 ⋅⋅ ⋅ ai) for i ≥ 1\. The homomorphism σ decorates the letter ai with ni−1. To this end, we can view ν as an automaton which reads ai and updates its state from ni−1 to ni = ni−1 ⋅ ν(ai ). Let m0 = 1 and mi = μ((n0, a1) ⋅⋅ ⋅ (ni−1, ai)) for i ≥ 1\. In step i, the automaton for μ reads the decorated letter (ni1, ai) and it updates its state by mi = mi1 ⋅ μ(ni1, ai).

![](images/210_3.jpg)

Now, the wreath product principle says the following. If, for every input a1 ⋅⋅ ⋅ ak, we can deduce the element φ(a1 ⋅⋅ ⋅ ak)∈ T from (nk , m k), then the wreath product principle tells us that T ≺ M ≀ N.

Right zeros and units

An element x of a monoid M is a right zero if ax = x for all a ∈ M. This is equivalent to saying that Mx = {x}. If x ∈ M is a right zero and a is an arbitrary element of M, then the products xa and ax = x are also right zeros. For every set X there is a monoid such that all elements in X are right zeros and there is no other element except for the neutral element 1U ∉ X. We define this monoid UX = X ∪ {1U} with neutral element 1U by xy = y for all x, y ∈ X. Associativity follows because a product of elements in X,regardless of the order of execution, is always the last element. We write 1U for the neutral element in UX since in some of our applications given as follows, X will be a monoid (in which case X contains an element 1 different from 1U). If |X| = |Y|, then UX and UY are isomorphic. Therefore, we also write Un instead of UX with |X| = n.

Proposition 7.32. U2n ≺ Un × U2

Proof: Let X = {x1, . . . , xn}, Y = {y1, . . . , yn}, and Z = {x, y}. We show that UX∪Y ≺ UX × UZ. We define a surjective partial homomorphism ψ: UX × UZ → UX∪Y by ψ(xi , x) = xi and ψ(xi , y) = yi as well as ψ(1U, 1U) = 1U. Obviously, ψ is surjective. It is a partial homomorphism since ψ(xi , z)ψ(xj , ẑ) = ψ(xj , ẑ) = ψ((xi , z)(xj , ẑ)) for all z, ẑ ∈ Z.

□

Since Un is a submonoid of Un+m for all m, n ≥ 0, we trivially have U2n−1 ≺ U2n.Hence, by repeatedly applying [Proposition 7.32](#chapter07_3.xhtml_chapter07_3_7), we see that Un divides the direct product of at most 1 +log n copies of U2. This leads to the following observation. Remember that CM denotes the wreath product closure of U2 and all simple group divisors of M.

Corollary 7.33. For every monoid M and every n ≥ 0, the monoid Un divides a monoid in CM.

Proof: By [Proposition 7.32](#chapter07_3.xhtml_chapter07_3_7), the monoid Un divides some k-fold direct product of U2. Hence, it divides some k-fold wreath product of U2. The claim follows since U2 ∈ CM and CM is closed under wreath products.

□

The following theorem yields Krohn–Rhodes decompositions of finite groups G because these can be decomposed iteratively until no nontrivial normal subgroups remain.

Theorem 7.34. Let G be a group and N a normal subgroup of G. Then G ≺ N ≀ (G/N).

Proof: Let H = G/N and let h1, h2, . . . , ∈ G with h1 = 1 be the representatives of the cosets of N, that is, for all x ∈ G there is a unique i with Nhi = Nx. We can identify H with {h1, h2, . . . } by the bijection Nhi ↦ hi. For g ∈ G let [g] = hi, if Ng = Nhi. Note that [[1](#Bibliography.xhtml_Bibliography_2)] = h1 = 1\. The operation in H is given by [x][y] = [xy]. This is well defined because, for all x, y ∈ G, we have N[x][y] = Nxy = N[xy].

For g ∈ G, let fg : H → N be given by fg(x) = xg[xg]−1. Note that xg[xg]−1 ∈ N since Nxg = N [xg]. We define a surjective partial homomorphism ψ: N ≀ H → G by ψ(fg , [g]) = fg(h1)[g] = fg(1)[g]. Since fg(1)[g] = g[g]−1[g] = g, the mapping ψ is indeed surjective. It remains to show that ψ is a partial homomorphism. Consider two elements (fa , [a]) and (fb, [b]) in NH × H. For every x ∈ H, we have

![](images/211_2.jpg)

This shows that fa ∗ [a]fb = fab. Thus,

![](images/212_3.jpg)

□

An interpretation of [Theorem 7.34](#chapter07_3.xhtml_chapter07_3_9) in terms of the wreath product principle is as follows. Let N be a normal subgroup of a group G and let H = G/N. By choosing representatives for the cosets, we can assume H ⊆ G. Moreover, the representative of the coset N is 1\. Let [g] denote the image of g ∈ G in H. Suppose we are given a sequence a1 ⋅⋅ ⋅ ak of elements in G and we want to compute the resulting product. First, H decorates the input sequence by (p0, a1) ⋅⋅ ⋅ (pk−1, ak) where pi = [a1 ⋅⋅ ⋅ ai]∈ H. We obtain pi by pi−1 ⋅ [ai]. In the next phase, N reads the decorated input and it computes qi = a1 ⋅⋅ ⋅ ai[a1 ⋅⋅ ⋅ ai]−1 ∈ N. This is done by qi = qi−1 ⋅ [a1 ⋅⋅ ⋅ ai−1]ai[a1 ⋅⋅ ⋅ ai]−1 = qi−1 ⋅ pi−1ai[pi−1ai]−1. In particular, the element pi−1ai[pi−1ai]−1 is uniquely determined by the decorated letter (pi−1, ai).

![](images/212_2.jpg)

Finally, the value of the product a1 ⋅⋅ ⋅ ak in G is obtained as q kp k. By the wreath product principle, this shows G ≺ N ≀ H.

Corollary 7.35. If G is a finite group, then G divides a monoid in CG.

Proof: The proof is by induction on |G|. If G is simple, then G ∈ CG. Otherwise, there exists a nontrivial normal subgroup N of G. By induction, the group N divides a monoid in CN and the group G/N divides a monoid in CG/N. We have CN ∪ CG/N ⊆ CG. Thus, by [Theorem 7.34](#chapter07_3.xhtml_chapter07_3_9), the group G divides a monoid in CG.

□

We note that the wreath product of two groups is again a group. Since U2 is not involved in the above decomposition of groups, every finite group G divides a group in CG.

Remember that an element x of a monoid M is invertible if there exists y ∈ M with xy = yx = 1\. If M is finite, then this is equivalent to Mx = M; see [Exercise 1.3](#chapter01_4.xhtml_chapter01_4_17). The invertible elements of M are also called units. The following theorem leads to the Krohn–Rhodes decomposition of monoids M such that all elements x ∈ M satisfy either Mx = {x} or Mx = M, that is, every element is either a right zero or invertible.

Theorem 7.36. If a monoid M can be written as a union of Z and G such that all elements in Z are right zeros and all elements in G are invertible, then M ≺ UZ ≀ G.

Proof: We can assume that M is nontrivial and, hence, Z and G are disjoint. For z ∈ Z, we define the mapping fz : G → UZ by fz(g) = zg−1. Note that zg−1 is indeed a right zero. Let ι : G → UZ with ι(g) = 1U be the constant mapping to the neutral element 1U of UZ. We set 1U g = g for all g ∈ G. This allows us to define a surjective partial homomorphism ψ: UZ ≀ G → M by ψ(f, g) = f(1) g if f is either of the form f = fz or f = ι. The mapping ψ is surjective since ψ(ι, g) = g for g ∈ G and ψ(fz, 1) = z for z ∈ Z.

□

It remains to show that ψ is a partial homomorphism. Consider h ∈ G and (f, g) ∈ UZ ≀ G such that ψ(f, g) is defined. Then

![](images/213_6.jpg) and for z ∈ Z we have![](images/213_7.jpg)

where the second to last equality uses the fact that z is a right zero.

Suppose M is a union of right zeros Z and units G. The decomposition in [Theorem 7.36](#chapter07_3.xhtml_chapter07_3_12) can also be formulated in terms of the wreath product principle. We want to evaluate a sequence a1 ⋅⋅ ⋅ ak of elements in M by using a decoration mechanism and products in Z and G, only. Let gi be the value of a1 ⋅⋅ ⋅ ai when ignoring all right zeros. Formally, all right zeros are mapped to the neutral element of G. The component for UZ reads the decorated input (1, a1)(g1, a2)⋅ ⋅⋅ (gk−1, ak). Whenever it reads a letter (gi−1, ai) for some right zero ai ∈ Z, it sets its state to ![](images/213_3.jpg) If ai is in G, then the state zi = zi−1 does not change. Finally, the value of the product a1 ⋅⋅ ⋅ ak is obtained as

zkgk. Suppose i is maximal such that ai is a right zero. Then, a1 ⋅⋅ ⋅ ak = ai ⋅ ai+1 ⋅⋅ ⋅ ak and ai+1 ⋅ ⋅⋅ ak is a group element. This yields ![](images/213_4.jpg) as desired. For example, consider the input abybzaa for a, b ∈ G and y, z ∈ Z. This yields the following picture:

![](images/213_5.jpg)

We obtain the result zaa of the product abybzaa by multiplying the last two states z(abb)−1 ⋅abbaa. Since it is always possible to compute the value of a1 ⋅⋅ ⋅ ak from the pair of states at the end of the run, the wreath product principle yields M ≺ UZ ≀ G.

Corollary 7.37. If every element in a finite monoid M is either a right zero or a unit, then M divides a monoid in CM.

Proof: Let Z be the right zeros in M, and let G be the units. By [Theorem 7.36](#chapter07_3.xhtml_chapter07_3_12) it suffices to show that each of UZ and G divides a monoid in CM. The claim for UZ follows by [Corollary 7.33](#chapter07_3.xhtml_chapter07_3_8), and the claim for G follows by [Corollary 7.35](#chapter07_3.xhtml_chapter07_3_11).

□

Neither right zero nor unit

By [Corollary 7.37](#chapter07_3.xhtml_chapter07_3_14), the Krohn–Rhodes theorem holds for monoids M, which can be written as disjoint union of right zeros and units. Hence, the “difficult” elements of M are exactly those which are neither a right zero nor a unit, that is, the elements x ∈ M with {x} ≠ Mx ≠ M. This leads to the following definition. For a monoid M let

![](images/214_2.jpg)

Lemma 7.38. If N is a finite submonoid of a monoid M, then K(N) ⊆ K(M).

Proof: Let x ∈ K(N). Since x is not a right zero, there exists a ∈ N with ax ≠ x. Thus, x is not a right zero in M either. Suppose that x has an inverse y ∈ M. The element x generates a cyclic subsemigroup 〈x〉 of N. Since 〈x〉 is finite, there exists n ≥ 1 with x2n = xn; see [Exercise 1.6 (a)](#chapter01_4.xhtml_chapter01_4_19). Multiplication by yn yields xn = 1\. Then, y = xn−1 ∈ 〈x〉 ⊆ N, and x is already invertible in N.

□

Remember that the local divisor of M at c ∈ M is the set Mc = cM ∩ Mc with the operation xc ∘ cy = xcy. We have seen in [Section 7.4](#chapter07_2.xhtml_chapter07_2_16) that Mc is a divisor of M. It is the homomorphic image of the submonoid { x ∈ M | xc ∈ cM } of M.

Lemma 7.39. Let M be a finite monoid, and let c ∈ K(M). Then |K(Mc)| < |K(M)|.

Proof: Since c ∈ K(M) \ K(Mc), it suffices to show that K(Mc)⊆ K(M). If x ∈ cM ∩ Mc is a right zero in M, then yx = x for all y ∈ M. In particular, for all yc ∈ cM we have yc ∘ x = yx = x. Hence, x is a right zero in Mc. Suppose that there exists an element x ∈ cM ∩ Mc which is invertible in M. Then, yx = 1 for some y ∈ M. It follows that M = Myx ⊆ Mx ⊆ Mc ⊆ M and hence M = Mc; this is a contradiction since c is not invertible in M. Therefore, we have K(Mc)⊆ K(M), as desired.

□

Augmented monoids

Let M be a monoid. Every element a ∈ M induces a mapping τa : M → M by τa(x) = xa. If two such mappings τa and τb coincide, then a = τa(1) = τb(1) = b. Thus, every mapping τa uniquely determines the element a ∈ M. Moreover, there is a strong connection between the composition of mappings and the product in M. This is more evident if we reverse the order of the composition; let τaτb = τb ∘ τa, that is, we first apply τa and then we apply τb. With this notation, we have τaτb = τab. This gives an interpretation of the elements of M as mappings M → M. The mapping τa is constant if and only if a is a right zero. If we add all constant mappings, then { τb | b ∈ M } together with the set of constants is closed under composition; in particular, it forms a monoid. If a is a right zero, then the constant mapping x ↦ a is τa ∈ { τb | b ∈ M }. If a is not a right zero, then the mapping x ↦ a is not in { τb | b ∈ M } and we have introduced a new element.

We reproduce the augmentation of constants on the monoid M without the detour over mappings. Let the augmented monoid M# of M be given by the disjoint union

![](images/215_1.jpg)

The idea is that if a is not a right zero, then we add the “constant mapping to a.” The operation on M is extended to M# by

![](images/215_2.jpg)

for x ∈ M# and a, b ∈ M. The neutral element of M is also neutral in M#. A straightforward computation shows that the operation on M# is associative. Thus, M # forms a monoid extension of M.

All elements in { x̄ | x ∈ M is not a right zero} are right zeros in M#, every right zero in M is also a right zero in M #, and the invertible elements in M and M# coincide. Therefore, we have K(M) = K(M#).

Lemma 7.40. If G ≺ M# and G is a group, then G ≺ M.

Proof: Since 1 ∈ M ⊆ M#, it suffices to consider the case |G| ≥ 2\. Let U ⊆ M# be a submonoid and φ: U → G a surjective homomorphism.We consider mutually inverse elements a, b ∈ G\{1} and arbitrary preimages e, x, y ∈ U with φ(e) = 1, φ(x) = a and φ(y) = b. Suppose that e is a right zero; then 1 = φ(e) = φ(xe) = φ(x)φ(e) = a ⋅ 1 = a in contradiction to the choice of a. Suppose that x is a right zero. Then a = φ(x) = φ(yx) = φ(y)φ(x) = ba = 1 yields a contradiction. Thus, U does not contain any right zeros. Since all elements in M# \M are right zeros, we obtain U ⊆ M. This shows G ≺ M.

□

Proof of the Krohn–Rhodes theorem

The central part in our proof of the Krohn–Rhodes theorem is the following result. It gives a decomposition of Mas a wreath product of a local divisor Mc and an augmented submonoid N#.

Theorem 7.41. Let M be a monoid generated by A; let c ∈ A and N be the submonoid of M generated by A \ {c}. Then

![](images/215_9.jpg)

Proof: Let Z = {x̄ | x ∈ N is not a right zero } be disjoint from N, and let N# = N ∪ Z be the augmented monoid. We extend ![](images/215_4.jpg) to a mapping ![](images/215_5.jpg) : N → N # by setting x̄ = x if x ∈ N is a right zero. Then for all x ∈ N the element x is a right zero in N#. In N#, we have ![](images/215_6.jpg) for all a, b ∈ N. For each element x ∈ N # there exists a unique element n ∈ N with ![](images/216_1.jpg) we denote this element by x̂. Let U1 = {1, 0} with the usual multiplication of integers as operation.

□

Let φ: A∗ → M be the natural homomorphism, and let ν : A∗ → N# × U1 be the homomorphism defined by

![](images/216_2.jpg)

We want to apply the wreath product principle. The extended alphabet is Aν = N# × U1 × A and the length-preserving mapping σ : A∗ → Aνis given by σ(a1 ⋅⋅ ⋅ ak) = (1, a1)(ν(a1), a2) ⋅⋅ ⋅ (ν(a1 ⋅⋅ ⋅ ak−1), ak). The mapping σ adds information given by ν to a word. We define a homomorphism ![](images/216_3.jpg) by ∗

![](images/216_7.jpg)

for a ∈ A \ {c}, x ∈ N# and e ∈ U1. Note that (1U , c) is the neutral element of UN × Mc.

Consider a word u = a1 ⋅⋅ ⋅ ak with ai ∈ A. We show that φ(u) is uniquely determined by the combination of ν(u) and μ(σ(u)). In its first component, the homomorphism ν multiplies the letters in u from left to right, except that whenever it sees the letter c, it restarts its evaluation from ![](images/216_5.jpg) Moreover, the second component of ν keeps track of whether there already was an occurrence of c. The mapping σ provides μ with this evaluation of ν. The homomorphism μ ignores all letters a ∈ A \ {c}.When seeing the first occurrence of the letter c, the homomorphism μ stores the evaluation of ν at the prefix before the first c in its UN component, and this value remains unchanged in the rest of the computation. At all future c’s, the homomorphism μ takes the evaluation x̂ of the factor between the current c and the previous c, and it updates its current value m by m ∘ cx̂c = mx̂c. In particular, at every point after the first c, the Mc component contains the evaluation of the input from the first c up to the previous c. For instance, the word u = aacaacacca for a ∈ A \ {c} leads to the following picture.

![](images/216_6.jpg)

The components for U1 and N # can only read the input from A∗. The components for Mc and UN, on the other hand, each have access to the first three lines.

Suppose that ν(u) = (x, e) ∈ N# × U1 and μ(σ(u)) = (n, m) ∈ UN × Mc. If e = 1, then u contains no letter c and, thus, φ(u) = x. Suppose that e = 0. In this case, the letter c occurs in u. If we write u = prs for p, s ∈ (A \ {c})∗ and r ∈ cA∗ ∩ A∗c, then we have φ(p) = n, φ(r) = m and φ(s) = x̂. This shows φ(u) = n ⋅ m ⋅ x̂. In any case, ν(u) and μ(σ(u)) uniquely determine φ(u). By the wreath product principle, this yields M ≺ (UN × Mc)≀ (N# × U1).

□

We can finally prove the Krohn–Rhodes theorem from page 194; that is, we start with U2 and the simple group divisors of M as building blocks, and we show that M can be composed from these using wreath products and division.

Proof of the Krohn–Rhodes theorem (Theorem 7.26): The proof is by induction on |K(M)|. If K(M) = 0, then the claim follows from [Corollary 7.37](#chapter07_3.xhtml_chapter07_3_14).

Now let K(M) ≠ 0\. Let A be a minimal set of generators for M. Then there is a generator c ∈ A ∩ K(M). Let N be the submonoid of M generated by A \ {c}. The minimality of A yields c ∉ N. By [Lemma 7.38](#chapter07_3.xhtml_chapter07_3_16), we have K(N#) = K(N) ⊆ K(M) \ {c}. [Lemma 7.40](#chapter07_3.xhtml_chapter07_3_19) shows that every group divisor of N # is also a group divisor of Mand hence CN# ⊆ CM. By induction, the monoid N# divides a monoid in CM. [Lemma 7.39](#chapter07_3.xhtml_chapter07_3_17) shows |K(Mc)| < |K(M)|, and thus, by induction, Mc divides a monoid in CMc ⊆ CM. Finally, we conclude that M divides a monoid in CM by [Corollary 7.33](#chapter07_3.xhtml_chapter07_3_8) and [Theorem 7.41](#chapter07_3.xhtml_chapter07_3_20).

## 7.6 Green’s relations

Throughout this section, M denotes a monoid. If M is finite, then for all x ∈ M there are minimal t ≥ 0, p ≥ 1 (t = threshold and p = period) such that xt+p = xt. Let k be minimal such that t ≤ kp < t + p. Then [Exercise 1.6 (b)](#chapter01_4.xhtml_chapter01_4_20) shows that xkp is the unique idempotent power of x. Moreover, if n = |M|, then xkp = xn!. Hence, for each finite monoid M there is a positive natural number ω such that xω is idempotent for every x ∈ M. In the following, we define the notion of D-class. In a finite monoid M, the D-class D(s) of an element s ∈ M consists of all elements t ∈ M such that MsM = MtM. A main result in this section has been stated first in [[18](#Bibliography.xhtml_Bibliography_19)]; the local divisors M s and M t are isomorphic as soon as MsM = MtM. As a consequence, classical results concerning Green’s relations have a natural and transparent algebraic interpretation.

Let us start with a general notion of ideals in monoids. A left ideal (resp. right ideal, resp. two-sided ideal) in a monoid M is a subset I ⊆ M such that M I ⊆ I (resp. I M ⊆ I, resp. M IM ⊆ I). Our focus is on principal ideals. A principal ideal is of the form Mx, xM, and MxM, where x ∈ M. The concept of ideals leads to natural partial orders ≤L, ≤R, ≤J and induced equivalence relations ∼L, ∼R, ∼J. They are given by

![](images/217_2.jpg)

Instead of ∼*L*, ∼*R*, ∼J, we also write *L*, *R*, and J for the corresponding subsets in M × M. These are three out of five relations referred to as Green’s relations. The other two relations are *H* and *D*, defined by *H* = L ∩ R and *D* = *L* ∘ *R*.

The relations were introduced and first studied by James Alexander Green (1926–2014) in 1951\. As the other four, *D* is an equivalence relation. For finite monoids this follows from [Lemma 7.42](#chapter07_3.xhtml_chapter07_3_26) which shows *J* = D. Since the definition of *J* is symmetric, *J* = *D* implies *D* = *L* ∘ *R* = *R* ∘ *L*. In [Exercise 7.18](#chapter07_6.xhtml_chapter07_6_12), we will see that the latter assertion *L* ∘*R* = *R*∘*L* holds even in infinite monoids; and therefore D always is an equivalence relation. But, in general, we may have *D* ⊊ *J*. This is shown in [Exercise 7.1 (c)](#chapter07_6.xhtml_chapter07_6_7). The picture is as follows:

![](images/218_5.jpg)

If G is a group, then H = J = G × G. Hence Green’s relations tell us nothing about the group. However, they are fundamental in the theory of (finite) semigroups.

If a monoid M contains a group G as a subsemigroup, then all elements in G are *H*-equivalent. Let e ∈ G be its neutral element, then e is idempotent. This implies G ⊆ *H*(e). In particular, if M is finite and x ∈ M, then xω is the neutral element in the finite cyclic group {xt, . . . , xt+p−1} (where xt = xt+p and p ≥ 1) and xt ∼*H* ⋅⋅ ⋅ ∼*H* xt+p−1.

Lemma 7.42. Let M be a finite monoid and s, t be J-equivalent elements. Then the following assertions hold:

(a)If s ≤*R* t (resp. s ≤*L* t), then s ∼*R* t (resp. s ∼*L* t).

(b)*L*(s) ∩ *R*(t) ≠ 0

(c)J = *D* = *L* ∘ *R* = *R* ∘ *L*; therefore, *D* is an equivalence relation.

Proof: Since s ∼*J* t, we can write s = ptu and t = qsυ.

(a)Since s ≤*R* t, we may assume that s = tu ∈ tM. Hence,

![](images/218_6.jpg)

This implies t ≤R s. We conclude s ∼R t.

(b)We have

![](images/218_7.jpg)

As a consequence, s ≤L qs ≤L s and hence, s ∼L qs. By symmetry; s ∼*R* sυ. This implies qsM = qsυM = tM; and qs ∈ *L*(s) ∩ *R*(t).

(c)We have shown that *L*(s) ∩ *R*(t) ≠ 0\. Thus, there exists z with s ∼*L* z ∼*R* t. We obtain J ⊆ *L* ∘ R. The other inclusion *L* ∘ R ⊆ J is trivial. Therefore, J = L ∘ *R*. By symmetry, J = *R*∘*L*. By definition,D = *L*∘R. Thisproves the claim *J* = D = *L*∘*R* = *R*∘*L*. Now, D is reflexive because L and *R* are reflexive. It is symmetric since *L* ∘ *R* = *R* ∘ *L*. It is transitive since

□

![](images/218_8.jpg)

Let M be a finite monoid and s ∈ M. Recall the definition of a local divisor M s. It is the set sM ∩ Ms together with the multiplication xs ∘ sy = xsy. The neutral element is s. Note that the *H*-class *H*(s) is a subset of sM ∩ Ms. It turns out that *H*(s) is exactly the set of units in M s.

Indeed, let x ∼H s, then s = yx for some y. We have ys ∈ Ms; and since sM = xM we have ys ∈ ysM = yxM = sM. Hence, ys ∈ sM ∩ Ms and ys ∘ x = yx = s. Thus, every element in *H*(s) has an inverse with respect to ∘. For the other direction, let ys = syˮ ∈ sM ∩ Ms such that ys ∘ x = yx = s and x ∘ syˮ = xyˮ = s. Then, we have s ∈ xM ∩ Mx. This shows that x ∼H s. Thus, H(s) is the set of units in the local divisor. If we endow the set *H*(s) with the operation ∘, then it becomes a group. It is called the Schützenberger group of the H-class *H*(s). It has been known that all Schützenberger groups in a given D-class D are isomorphic. Actually, a more general statement is true: if s, t ∈ D, then the local divisors M s and M t are isomorphic. This will be shown next.

Generalization of Green’s lemma

The following theorem is a slightly enriched version of Green’s classical lemma.

Theorem 7.43. Let M be a monoid and s, t be R-equivalent elements such that s = tu and t = sυ. Then the right multiplication ⋅υ, mapping x to xυ, induces a bijection Ms → Mt, x ↦ xυ. The mapping ⋅υ enjoys the following additional properties:

(a)It induces an isomorphism between the local divisors M s and M t.

(b)It maps *L*(s) bijectively onto *L*(t).

(c)If M is finite, then ![](images/219_1.jpg) respects H-classes. More precisely, if M is finite, then H(x) ⋅ υ = *H*(xυ) for x ∈ *L*(s).

Proof: Let x ∈ Ms. Then xυ ∈ Mt and xυu = x since sυu = s. This shows that ![](images/219_2.jpg) Mt is injective and ![](images/219_3.jpg) is surjective. By symmetry, ![](images/219_4.jpg) is bijective. Since sMυ ⊆ tM, we also have a bijection between sM ∩ Ms and tM ∩ Mt.

□

(a)Consider the bijection φ: sM ∩ Ms → tM ∩ Mt with φ(x) = xυ. Then we have φ(xs ∘ sy) = φ(xsy) = xsyυ and φ(xs) ∘ φ(sy) = xt ∘ syυ = xsyυ. Hence, φ(xs ∘ sy) = φ(xs) ∘ φ(sy); and φ is an isomorphism between the local divisors M s and M t.

(b)Let x ∈ *L*(s), then Mxυ = Msυ = Mt. Hence, *L*(s) ⋅ υ ⊆ *L*(t). By symmetry, *L*(t) ⋅ u ⊆ *L*(s). This implies that ⋅υ induces a bijection between *L*(s) and *L*(t).

(c)Let x ∈ *L*(s), then xυ ∼L t. Trivially, xυ ≤R x. Moreover, xυ ∼J x since xυ ∼L t ∼J s ∼L x. By [Lemma 7.42](#chapter07_3.xhtml_chapter07_3_26), we conclude xυ ∼R x. This says that H(x) is mapped to *H*(xυ). Again, as xυu = x, we obtain H(x) ⋅ υ = *H*(xυ).

Remark 7.44. In [Exercise 7.1 (b)](#chapter07_6.xhtml_chapter07_6_6), we see that [Lemma 7.42](#chapter07_3.xhtml_chapter07_3_26) fails for infinite monoids M, in general. More precisely, there are examples where s ∼J t and s ≤R t, but s ̴̸ R t. We can choose the same example to find s ∼*J* t and *L*(s) ∩ R(t) = 0.

Finally, if M is infinite, then *L*(s) → *R*(t), x ↦ xυ does not always respect H-classes. Thus in general, the finiteness assumption in [Theorem 7.43 (c)](#chapter07_4.xhtml_chapter07_4_3) is necessary, too.

◊

The following corollary generalizes what is known as Green’s theorem.

Corollary 7.45. Let M be a finite monoid and let s, t be *J*-equivalent. Then the local divisors M s and M t are isomorphic. In particular, the Schützenberger groups *H*(s) and *H*(t) are isomorphic and therefore |*H*(s)| = |*H*(t)|.

If e ∈ M is an idempotent, then H(e) is a subgroup in the monoid M.

Proof: Since s ∼*J* t there is some r ∈ *R*(s) ∩ *L*(t) by [Lemma 7.42](#chapter07_3.xhtml_chapter07_3_26). Hence, by [Theorem 7.43](#chapter07_4.xhtml_chapter07_4_2) (and left–right symmetry), we know that the local divisors M s, M r, and M t are isomorphic. Hence their groups of units are isomorphic. These groups of units are the Schützenberger groups *H*(s), *H*(r), and *H*(t).

□

If e ∈ M is an idempotent, then the multiplication ∘ in the local divisor is exactly the same as in M. Indeed e2 = e implies xe ⋅ ey = xey = xe ∘ ey.

Egg boxes

[Lemma 7.42](#chapter07_3.xhtml_chapter07_3_26) shows that we can partition each D-class of a finite monoid into a disjoint union of L- (resp. R-) classes. These L- (resp. R-) classes are pairwise incomparable with respect to <L (resp. <R). Drawing L-classes as vertical columns and R-classes as horizontal rows, the H-classes partition the box such that each H-class appears as an egg. By [Corollary 7.45](#chapter07_4.xhtml_chapter07_4_5), all eggs have a natural structure of a group; it is the Schützenberger group which in turn is the group of units in the corresponding local divisor. Eggs in the same box are isomorphic. The isomorphism between *H*(s) and *H*(t) is given by a mapping x ↦ pxυ. So, all eggs in one box have the same shape.

The monoid U1 = {1, 0} with the usual multiplication of integers is an idempotent semigroup. It is the smallest monoid which is not a group. Another small monoid without nontrivial subgroups is the syntactic monoid of (ab)∗ as mentioned in [Example 7.25](#chapter07_2.xhtml_chapter07_2_28). It is the monoid ![](images/220_1.jpg) having six elements {1, a, b, ab, ba, 0}. Here 0 acts as a zero; 0x = x0 = 0 for all ![](images/220_2.jpg) Moreover, a2 = b2 = 0 and aba = a, bab = b. The egg boxes of U1 and ![](images/220_3.jpg) are depicted in [Figure 7.2](#chapter07_4.xhtml_chapter07_4_6). As usual, if a D-class D is drawn as an egg box, then the *H*-classes containing an idempotent are usually marked by putting a star ∗ into the upper left corner. There is no ∗ attached to a or b, indicating that a2 = ̸ a and b2 = ̸ b. Indeed, a2 = b2 = 0 and hence, x3 = x2 for all ![](images/220_6.jpg) The monoid ![](images/220_4.jpg) belongs to the family of Brandt monoids ![](images/220_5.jpg)

![](images/221_1.jpg)

Fig. 7.2. Egg box diagrams of U1 and ![](images/221_2.jpg)

Regular D-classes in finite monoids

Throughout this section, e and f denote idempotents in a finite monoid. Thus, e = e2 and f = f 2. Let K ∈ {L, *R*,*D*}, we say that a K-class is regular if it contains an idempotent.

An element s in a monoid is called regular if there is some t such that s = sts. Thus, t is “almost” an inverse of s.

Proposition 7.46. Let M be a finite monoid. Let s ∼*J* t and let D = *J*(s) the corresponding *D*-class. If st ∈ D, then we have st ∈ *R*(s)∩L(t) and the *H*-class *L*(s)∩R(t) contains an idempotent element. Vice versa, if L (s) ∩ *R*(t) contains an idempotent element, then st ∈ *R*(s) ∩ *L*(t) ⊆ D.

Proof: We have st ≤R s and st ≤L t. Hence, if st ∼J s, then st ∈ R(s) ∩ *L*(t) by [Lemma 7.42](#chapter07_3.xhtml_chapter07_3_26). By Green’s lemma, the mapping x ↦ x ⋅ t induces a bijection from *L*(s) onto *L*(st) = *L*(t). Thus, there is a unique e ∈ *L*(s) such that et = t. Moreover, z ↦ z ⋅ t preserves *R*-classes. Hence, e ∼R t. Therefore, e = ty for some y. We obtain e2 = ety = ty = e; and e ∈ *L*(s) ∩ *R*(t) is idempotent.

□

For the other direction, let e2 = e ∈ *L*(s) ∩ *R*(t). Then t ∈ eM and hence et = t. By Green’s lemma, the mapping x ↦ x ⋅ t induces a bijection from *L*(e) onto *L*(et) = L (t). We have s ∈ *L*(e). Therefore, *H*(s) is mapped into *H*(st). In particular, st ∼*L* t and st ∈ D. Moreover, st ∈ *R*(s) ∩ *L*(t).

Lemma 7.47. Let M be a finite monoid, and let s ∈ M be regular with srs = s. Then sr is idempotent and s ∼R sr. Thus, the R-class of every regular element contains an idempotent.

Proof: Since srs = s, we have srsr = sr and sr is idempotent. Moreover sM = srsM ⊆ srM ⊆ sM. Hence s ∼*R* sr.

□

Lemma 7.48. Let M be a finite monoid, let e ∈ M be idempotent and e ∼R s with e = sr. Then s is regular.

Proof: We have s ∈ eM, hence s = es. From e = sr, by right multiplication of s, we obtain the equality s = es = srs; thus, s is regular.

Proposition 7.49. Let M be a finite monoid and let D be a D-class in M. Then the following assertions are equivalent:

(a)There are s, t ∈ D with st ∈ D.

(b)D is regular, that is, D contains an idempotent element.

(c)D contains a regular element.

(d)Every L-class and every R-class in D contains an idempotent.

(e)Every element in D is regular.

Proof: [Lemma 7.47](#chapter07_4.xhtml_chapter07_4_8) and [Lemma 7.48](#chapter07_4.xhtml_chapter07_4_9) imply that D contains an idempotent if and only if it contains a regular element. This shows the equivalence of (b) and (c), and it shows that (e) implies (a).

□

If there are s, t ∈ D with st ∈ D, then D contains an idempotent; and D is regular by [Proposition 7.46](#chapter07_4.xhtml_chapter07_4_7). Thus (a) implies (b).

If e ∈ M is idempotent, then all elements in R(e) are regular by [Lemma 7.48](#chapter07_4.xhtml_chapter07_4_9). By symmetry, all elements in L (e) are regular, too.

As a consequence, every L-class and every R-class in D contains an idempotent from [Lemma 7.47](#chapter07_4.xhtml_chapter07_4_8), showing that (b) implies (d). Applying [Lemma 7.48](#chapter07_4.xhtml_chapter07_4_9) again, we see that all elements in D are regular, and therefore (d) implies (e), which completes the proof.

## 7.7 Automata over infinite words

Around 1960, Julius Richard Büchi (1924–1984) introduced an automaton model for languages over infinite words which resembles nondeterministic finite automata [[12](#Bibliography.xhtml_Bibliography_13), [13](#Bibliography.xhtml_Bibliography_14)]. Büchi’s original motivation for this concept was to prove decidability for monadic second-order logic over (ℕ, ≤). This formalism is abbreviated as MSO(ℕ, ≤). In the logic MSO(ℕ, ≤), it is possible to quantify over both elements and subsets. However, the only admissible atomic predicates are x ≤ y and x ∈ X. Büchi’s decidability result is far from obvious taking into account that first-order logic over the naturals with addition and multiplication is undecidable [[46](#Bibliography.xhtml_Bibliography_46)]. We will show the decidability of MSO(ℕ, ≤) in [Corollary 7.63](#chapter07_5.xhtml_chapter07_5_12) following Büchi’s ideas closely. His formalism uses the framework of infinite words, which is our starting point.

Let Σ be a finite alphabet. Σω denotes the set of infinite sequences a1a2 ⋅⋅ ⋅ with ai ∈ Σ. The elements of Σω are called infinite words or sometimes also ω-words. Accordingly, an ω-language is a subset of Σω. Instead of ω-language, we simply use the term language if the context is clear. For U ⊆ Σ∗ and L ⊆ Σω, the concatenation of U and L is UL = {uα ∈ Σω | u ∈ U, α ∈ L }. We write Σ+ for the set of finite nonempty words Σ∗ \ {ε}. If V ⊆ Σ+, then Vω = {υ1υ2 ⋅⋅ ⋅ ∈ Σω | υi ∈ V } is the infinite iteration of V.

A Büchi automaton A = (Q, δ, I, F) over Σ consists of a finite set of states Q, a set of initial states I ⊆ Q, a set of final states F ⊆ Q and a transition relation δ ⊆ Q × Σ × Q. A run of a finite or infinite word α = a1a2 ⋅⋅ ⋅ with ai ∈ Σ is a sequence of the form

![](images/223_7.jpg)

where (qi , ai+1, qi+1) ∈ δ for all i ∈ ℕ. The run r is accepting if first, q0 ∈ I and second, qi ∈ F holds for infinitely many i ∈ ℕ. Thus, no run on a finite word is accepting. If final states of A are visited infinitely often, then there is a specific state q ∈ F that is visited infinitely often because Q is finite. We write ![](images/223_2.jpg) for a finite word w ∈ Σ∗ if in A there is a run on w from state p to q. By ![](images/223_3.jpg) we indicate that, on w, there is a run from p to q which visits a final state. In particular, ![](images/223_4.jpg) is satisfied if either p ∈ F or q ∈ F, or both. The language accepted by a Büchi automaton *A* is defined by

![](images/223_6.jpg)

A language L ⊆ Σω is called ω-regular if L is accepted by a Büchi automaton.

Remark 7.50. The notion of Büchi automaton is robust. We may allow variants without changing the class of ω-regular languages; for example, it is sometimes convenient to move the acceptance condition from states to transitions. In this model, the component F denotes a set of final transitions, F ⊆ δ, and a run r = q0a1q1a2 ⋅⋅ ⋅ is accepted if there are infinitely many indices i such that (qi , ai , qi+1) ∈ F. We may ask for a single initial state or we may work with a set I of initial states. Another variant (for both acceptance modes: states or transitions) is that we allow δ to be any finite relation δ ⊆ Q ×Σ∗ ×Q. In particular, wemay allow ε-transitions (p, ε, q). For the notion of run we can use the definitions above if we replace the condition ai ∈ Σ by ai ∈ Σ∗. As in the framework of finite words, none of these variants changes the expressive power. The solution to [Exercise 7.21](#chapter07_6.xhtml_chapter07_6_13) provides details.

In the following, if we refer to a Büchi automaton, then, by default, we mean acceptance by final states and the “spelling version,” where δ ⊆ Q × Σ × Q. If we allow ε-transitions, then we assume acceptance by final states and δ ⊆ Q × (Σ ∪ {ε}) × Q.

◊

### 7.7.1 Deterministic Büchi automata

A Büchi automaton A = (Q, δ, I, F) is deterministic if |I| = 1, δ ⊆ Q × Σ × Q, and for all (p, a) ∈ Q × Σ there is at most one state q ∈ Q with (p, a, q) ∈ δ. Languages accepted by deterministic Büchi automata are called accordingly deterministic ω-regular or deterministic for short. An example of a deterministic language is “there are infinitely many factors aa.” We first depict a nondeterministic Büchi automaton for it and then a deterministic one.

![](images/224_1.jpg)

This automaton is not deterministic, because the initial state has two outgoing aedges. The following deterministic Büchi automaton recognizes the same language:

![](images/224_2.jpg)

The difference between the two automata is that the first one guesses when a factor aa appears, whereas the second one is eager to count more aa’s. Note that, in both automata, the choice for the final state is unique. This is not always the case, for example, consider the language of infinite words not starting with ab and without any factor bab. The following deterministic automaton accepts this language, but we might choose the state in the middle as a final state as well. Since final states are not unique and since all states in the automaton above are reachable, complementing the final states in that deterministic Büchi automaton does not yield the complement for the accepted language.

![](images/224_3.jpg)

Next, consider the language L of all words with infinitely many a’s. Each of the following two deterministic Büchi automata accepts L with two states, which is obviously minimal. However, the two automata have a different structure. Thus, in contrast to the situation with finite words, there are no canonical minimal automata.

![](images/224_4.jpg)

The final states in both automata above are unique; changing the set of final states changes the accepted language. Still, complementing the final states does not lead to the complement for the accepted language. Indeed, for any nonempty set of final states, both automata accept the infinite word (ab)ω. Actually, more is true: the complement of “infinitely many a’s” is “finitely many a’s,” but there is no deterministic Büchi automaton which accepts the language “finitely many a’s” (as soon as there is a second letter b). There is a nondeterministic one: the following nondeterministic Büchi automaton “guesses” the transition from {a, b}∗ to the suffix bω.

![](images/225_1.jpg)

Define K = {a, b}∗bω which is the language “finitely many a’s” and thus, the complement of the deterministic language “infinitely many a’s.” Let us show that K cannot be accepted by any deterministic Büchi automaton. By contradiction, let A = (Q, δ, {q0}, F) be a deterministic Büchi automaton with L(A) = K. There exists an accepting run on abω ∈ K. Hence, we have q0 ⋅ abn1 ∈ F for some n1 ∈ ℕ. The word abn1abω belongs to K and therefore, there exists n2 ∈ ℕwith q0 ⋅abn1abn2 ∈ F. Going on this way, we finally obtain an infinite word α = abn1abn2abn3 ⋅⋅ ⋅ , which infinitely often visits a final state of A. Since α ∉ K, this is a contradiction. Consequently, there is no deterministic Büchi automaton accepting the language “finitely many a’s.” Thus, the class of deterministic ω-regular languages is not closed under complementation. This is again in contrast to the situation of finite words where, by Kleene’s theorem, every finite nondeterministic automaton is equivalent to a finite deterministic one.

### 7.7.2 Union and intersection

As in the finitary case, we have closure under finite union and finite intersection. The following result (and its proof) hold for the class of ω-regular languages as well as for the subclass of deterministic ω-regular languages.

Theorem 7.51. If L1, L2 ⊆ Σω are recognized by (deterministic) Büchi automata, then so are L1 ∪ L2 and L1 ∩ L2.

Proof: The proof for the union L1 ∪ L2 is easy using the usual product automaton construction. Hence, we concentrate on the intersection, but this slightly more involved construction can also be used for the union L1 ∪ L2, so our construction covers both cases. For i ∈ {1, 2}, let Ai = (Qi , δi , {q0,i}, Fi) be a (deterministic) Büchi automaton with L(Ai) = Li. If A1 and A2 are deterministic, then the construction leads to a deterministic Büchi automaton, otherwise we end up in a nondeterministic one. We use a variant of the product automaton construction by adding a third component.

Let Q = Q1×Q2×{1, 2} and q0 = (q0,1, q0,2, 1). The transition relation δ ⊆ Q×Σ×Q behaves like δ1 on the first component and like δ2 on the second component. In the third component, the automaton keeps track of in which component it expects to see a final state next. More formally, we define ((p1, p2, j), a, (q1 , q2, j)) to be in δ if first, (p1, a, q1)∈ δ1, (p2, a, q2)∈ δ2 and second

![](images/226_1.jpg)

Now, the automaton B = (Q, δ, {q0}, F) with F = (Q1 × F2 × {1, 2}) ∪ (F1 × Q2 × {1, 2}) accepts the language L1 ∪ L2, and C = (Q, δ, {q0}, F) with F' = F1 × Q2 × {1} accepts L1 ∩ L2.

□

In contrast to the class of deterministic languages, the full class of ω-regular languages is also closed under complementation by [Corollary 7.60](#chapter07_5.xhtml_chapter07_5_3). This result is due to Büchi, but the proof is more involved than for finite words.

### 7.7.3 Omega-rational languages

Throughout this section Σ denotes a finite alphabet. By Kleene’s theorem, we have REC(Σ∗) = RAT(Σ∗) = REG(Σ∗). So, the notions of recognizable and rational coincide, and the notation regular is common. The same is true for languages over infinite words. We begin with the definition of ω-rational languages. As we have done for RAT(Σ∗), we define ω-rational languages inductively.

–IfV ∈ RAT(Σ∗), then (V \ {ε})ω is an ω-rational language.

–IfU ∈ RAT(Σ∗) and L ⊆ Σω is an ω-rational language, then UL is ω-rational.

–A finite union of ω-rational languages is ω-rational.

Note that the empty set 0 and Σω are ω-rational. We also know that (V \ {ε}) ⊆ Σ+ is rational (= regular) if and only if V ⊆ Σ∗ is rational (= regular).

Example 7.52. A singleton {α} is rational if and only if there are two finite nonempty words u, υ ∈ Σ+ such that α = uυω. An infinite word of the form uυω is called ultimately periodic. Let Σ = {0, . . . ,9}. Then every real number in the interval [0, 1] has a decimal representation of the form 0.α, where α ∈ Σω. For example, 1/3 = 0.3ω. We have 1 = 0.9ω and 1/10 = 0.1 = 0.10ω = 0.09ω, so the representation is not unique. Nevertheless, a real number 0.α is a rational number if and only if the singleton {α} is ω-rational.

Lemma 7.53. All ω-rational languages are ω-regular.

Proof: The proof mimics the constructions for the finitary case. Let A = (Q, δ, I, F) be a finite automaton accepting V \ {ε}. According to [Remark 7.50](#chapter07_4.xhtml_chapter07_4_16), we allow a set of initial states and that Ahas ε-transitions. We add a new state qω and we let qω to be new initial and only final state. Moreover, we add ε-transitions from qω to all initial states and we add ε-transitions from all final states to qω. If desirable, we remove ε-transitions by some standard procedure; see [Exercise 7.21](#chapter07_6.xhtml_chapter07_6_13). The resulting nondeterministic Büchi automaton accepts (V \ {ε})ω.

For the concatenation, let A = (Q, δ, I, F) be a finite automaton for U and B = (P, δ' , I' , F) a Büchi automaton for L. Again, we allow ε-transitions. We let C be the disjoint union of A and B; and we add ε-transitions from all final states in F to all initial states in I. In C, we let I be the set of initial states and F' the set of final states.

For the union there is nothing new; the disjoint union of two Büchi automata is a Büchi automaton (with a set of initial states) which accepts the union of the accepted languages.

◊

Theorem 7.54. Let L ⊆ Σω. The following properties are equivalent:

(a)L is ω-regular.

(b)L is a finite union of languages UVω for regular languages U, V ⊆ Σ+ such that UV ⊆ U and V2 ⊆ V.

(c)L is a finite union of languages UVω for regular languages U, V ⊆ Σ+.

(d)L is ω-rational.

Proof: (a)⇒(b): LetA = (Q, δ, I, F) be a Büchi automaton with L(A) = L. For p, q ∈ Q let ![](images/227_1.jpg) All languages Lpq are regular. We have

□

![](images/227_2.jpg)

Hence, L is a finite union on languages ![](images/227_4.jpg) We have Lpq Lqq ⊆ Lpq and ![](images/227_3.jpg) The implications (b)⇒(c) and (c)⇒(d) are trivial. (d)⇒(a) follows from [Lemma 7.53](#chapter07_4.xhtml_chapter07_4_25).

The criterion whether L(*A*) ≠ 0 for a Büchi automaton A is as follows. It is nonempty if and only if there are states (p, q) ∈ I × F such that there are nonempty paths from p to q and from q to q. If such paths exist, then we may assume that the path from p to q is labeled by some nonempty word u ∈ Σ+ and that the path (cycle) from q to q is labeled by some nonempty word υ ∈ Σ+. Thus, we have L(*A*) ≠ 0 if and only if there are u, υ ∈ Σ+ with uυω ∈ L(*A*). Recall from [Example 7.52](#chapter07_4.xhtml_chapter07_4_24) that an infinite word of the form uυω for u, υ ∈ Σ+ is called ultimately periodic. Therefore, if *A* = (Q, δ, I, F) accepts a nonempty language, then *A* accepts ultimately periodic words. For singletons, we have the equivalence: {α} is ω regular if and only if α is ultimately periodic.

Remark 7.55. We know by [Theorem 7.51](#chapter07_4.xhtml_chapter07_4_21) that the class of ω-regular languages is closed under intersection. Hence, every nonempty intersection of ω-regular languages contains an ultimately periodic word. Let us give a direct proof which does not rely on this closure property. For this consider two Büchi automata Ai = (Qi , δi , Ii , Fi) for i = 1, 2. We write ![](images/228_1.jpg) if for u ∈ Σ+ there is a run ![](images/228_2.jpg) in each Ai. Now assume that there exists an infinite word α ∈ L(*A*1)∩L(*A*2), then, by the pigeon hole principle, there are three words u, x, y ∈ Σ+ and there are three pairs (q01, q02)∈ I1 × I2, (f1, p2)∈ F1 × Q2, and (p1, g2)∈ Q1 × F2 such that

![](images/228_8.jpg)![](images/228_9.jpg)![](images/228_10.jpg)

–uxy is a finite prefix of α.

Thus, we have u(xy)ω = ux(yx)ω ∈ L(A1)∩ L(A2).

◊

### 7.7.4 Recognizability of omega-regular languages

Let φ: Σ+ → S be a homomorphism to a finite semigroup S. For s ∈ S, we write [s] as an abbreviation for the set φ−1(s) = {u ∈ Σ+ | φ(u) = s }. The homomorphism φ recognizes an ω-language L ⊆ Σω if

![](images/228_11.jpg)

In particular, from [s][t]ω ∩ L ≠ 0, we obtain [s][t]ω ⊆ L. In the literature, we find the notion of strong recognition and weak recognition. Our definition refers to the strong version. To see the difference, φ weakly recognizes L ⊆ Σω if

![](images/228_12.jpg)

If φ recognizes an ω-language L, then φ weakly recognizes L, too. This is immediate from the definition. The converse is not true. Indeed, consider the language L ⊆ {a, b}+ which is defined by “infinitely many a’s.” Define S = {a, b} with the multiplication aa = ba = a and bb = ab = b. The canonical homomorphism φ: {a, b}+ → S weakly recognizes L since we have L = [a]ω (due to [a] = {a, b}∗a). Hence, [b]ω ∩ L ≠ 0, because (ab)ω has infinitely many a’s and infinitely many b’s. However, [b]ω is not a subset of L since bω ∈ [b]ω. Thus, φ does not recognize L.

The following lemma is an application of combinatorics to infinite words. It provides a technique that is used frequently within the theory of ω-regular languages.

Lemma 7.56. Let φ: Σ+ → S be a homomorphism to a finite semigroup S and let α ∈ Σω be an infinite word. Then there are s, e ∈ S with se = s and e2 = e such that α ∈ [s][e]ω. In particular, Σω = ⋃{ [s][e]ω | s, e ∈ S, se = s, e2 = e }.

Proof: Let α = u1u2 ⋅⋅ ⋅ be a factorization with ui ∈ Σ+. Consider the infinite complete graph with vertex set ℕ. An edge {i, j} with i < j is colored with the element c(i, j) = φ(ui+1 ⋅⋅ ⋅ uj)∈ S. By Ramsey’s theorem ([Theorem 6.8](#chapter06.xhtml_chapter06_18)) there is an infinite subset I of ℕ and e ∈ S with c(i, j) = e for all i, j ∈ I with i < j. For i, j, k ∈ I with i < j < k, we obtain e = c(i, k) = c(i, j)c(j, k) = e2. Hence, e = e2 is idempotent. It follows α ∈ [ c(0, i)][e]ω for every i ∈ I. Fix any i ∈ I and let s = c(0, i)e ∈ S. Then, we have α ∈ [ s][e]ω with se = s and e2 = e.

□

Proposition 7.57. Let φ: Σ+ → S be a homomorphism to a finite semigroup S recognizing a language L ⊆ Σω. Then L is ω-regular. Moreover, φ recognizes the complement Σω \ L, too.

Proof: The language L is ω-regular by [Theorem 7.54](#chapter07_4.xhtml_chapter07_4_27) since it a finite union of languages of the form [s][t]ω and [s], [t] ⊆ Σ∗ are regular. Let α ∈ Σω \ L. By [Lemma 7.56](#chapter07_4.xhtml_chapter07_4_31) there are s, e ∈ S with α ∈[s][e]ω. Since φ recognizes L we must have Σω \ L=⋃{ [s][t]ω | s, t ∈ S, [s][t]ω ∩ L = 0}.

□

There are different ways to define a syntactic congruence for an ω-language L ⊆ Σω; see, for example, [[102](#Bibliography.xhtml_Bibliography_103)]. Arnold’s syntactic congruence ≡L (André Arnold, born 1945) is based on the idea to focus on ultimately periodic words [[3](#Bibliography.xhtml_Bibliography_4)]. This makes sense, because, as we have seen earlier, every nonempty ω-regular language contains at least one ultimately periodic word.

We will see that Arnold’s congruence captures the notion of recognizable ω-regular languages. For u, υ ∈ Σ+, we define u ≡L υ if for all x, y, z ∈ Σ∗ the following two conditions are satisfied:

![](images/229_3.jpg)

Let [u]L = { υ ∈ Σ+ | u ≡L υ } be the equivalence class of u. For u ≡L u' and υ ≡L υ, we have

![](images/229_4.jpg)

and thus uυ ≡L uυ. It follows that the operation [u]L ⋅ [υ]L = [uυ]L is well defined. Therefore, the set of equivalence classes Synt(L) = {[u]L | u ∈ Σ+ } forms a semigroup. We call Synt(L) the syntactic semigroup of L and μL : Σ+ → Synt(L) with μL(u) = [u]L the syntactic homomorphism.

The situation with syntactic semigroups over infinite words is more complicated than over finite words. For example, the syntactic homomorphism μL does not necessarily recognize the ω-language L. Indeed, let α ∈ Σω be an ω-word that is not ultimately periodic, then the syntactic semigroup of the language {α} has only one element: all words considered in the definition of ≡{α} are ultimately periodic and none of them is in {α}. The claim follows because a semigroup with at most one element cannot recognize any language other than 0 or Σω.

If, on the other hand, a language L is recognized by a homomorphism to any finite semigroup, then L is also recognized by μL. This is shown next.

Lemma 7.58. Let L ⊆ Σω and let φ: Σ+ → S be a homomorphism to a finite semigroup S recognizing L. Then μL : Σ+ → Synt(L) recognizes the language L and φ(u) ↦ μL(u) defines a surjective homomorphism from the subsemigroup φ(Σ+)⊆ S onto Synt(L).

Proof: First, we show that the mapping φ(u) ↦ μL(u) is well defined. Let φ(u) = φ(υ). We obtain

![](images/230_12.jpg)

where the last equivalence in both lines uses φ(u) = φ(υ). Thus, φ(u) = φ(υ) implies u ≡L υ. As a consequence, μL induces a well-defined surjective homomorphism

![](images/230_13.jpg)

Next, we show that the syntactic homomorphism recognizes L. Let r, t ∈ Synt(L) such that ![](images/230_4.jpg) We know that e = tn is idempotent for n = |S|!. Let s = re, then ![](images/230_3.jpg) and ![](images/230_6.jpg) It is enough to show that ![](images/230_7.jpg) By contradiction, assume ![](images/230_5.jpg) By [Proposition 7.57](#chapter07_4.xhtml_chapter07_4_33) (Σω \ L) is ω-regular. Hence, ![](images/230_8.jpg) is a nonempty intersection of two ω-regular languages. Hence, there is an ultimately periodic word ![](images/230_9.jpg) (Use [Remark 7.55](#chapter07_4.xhtml_chapter07_4_28) or the closure under intersection of ω-regular languages.) Since se = s and e2 = e, we find p, q ∈ ℕ and a factorization υ = υ1υ2 such that w = uυpυ1 ∈ [s]L and z = υ2υqυ1 ∈ [e]L. This is true because there are only finitely many factorizations υ = υ1υ2, but there are infinitely many splittings of υ caused by ![](images/230_10.jpg) So, there must be at least one repetition.

Since υ = υ1υ2, we obtain uυω = wzω ∉ L. Now, ![](images/230_11.jpg) is also a nonempty ω-regular language. The very same arguments apply; and we find x ∈ [s]L and y ∈ [e]L with xyω ∈ L. However, w ≡L x and z ≡L y. Hence xyω ∈ L if and only if wzω ∈ L. This is a contradiction.

□

[Lemma 7.58](#chapter07_5.xhtml_chapter07_5_1) tells us that if L is recognized by a homomorphism to a finite semigroup, then Synt(L) is, up to isomorphism, the uniquely determined smallest semigroup recognizing L. In the following theorem, the equivalence of (a) and (b) is due to Büchi. By [Proposition 7.57](#chapter07_4.xhtml_chapter07_4_33), it is the main step in showing that the class of ω-regular languages is closed under complementation. The equivalence of (b) and (c) is due to Arnold.

Theorem 7.59. Let L ⊆ Σω. The following properties are equivalent:

(a)L is ω-regular.

(b)L is recognized by a homomorphism φ: Σ+ → S to a finite semigroup S.

(c)The syntactic semigroup Synt(L) is finite and the syntactic homomorphism μL : Σ+ → Synt(L) recognizes L.

(d)L is weakly recognized by a homomorphism ψ: Σ+ → T to a finite semigroup T.

Proof: (a)⇒(b): Let*A* = (Q, δ, {q0}, F) be a Büchi automaton that accepts L. Wedefine an equivalence relation ≡A on Σ+ such that we have u ≡A υ if and only if the following two equivalences are satisfied for all p, q ∈ Q:

![](images/231_1.jpg)

Let [u]A = {υ ∈ Σ+ | u ≡A υ }. If u ≡A u' and υ ≡A υ, then uυ ≡A uυ. Therefore, the operation [u]A[υ]A = [uυ]A is well defined, the set SA = {[u]A | u ∈ Σ+ } forms a semigroup and φA : Σ+ → SA with u ↦ [u]A defines a surjective homomorphism. The equivalence class of u is completely determined by the function δu : Q × Q → {1, 2, 3} with

![](images/231_2.jpg)

Thus, if = then u ≡υ. Since the number of mappings Q × Q → {1, 2, 3} is 2 δu δυ, A 3|Q|, the semigroup SA is finite.

It remains to show that φA recognizes the language L. Let ![](images/231_3.jpg) and ![](images/231_4.jpg) Then there are factorizations α = u0υ1υ2 ⋅⋅ ⋅ and β = û0v̂1v̂2 ⋅⋅ ⋅ with u0 ≡A u ≡A û0 and υi ≡A υ ≡A v̂i. Since α ∈ L, there are states q0, q1, . . . with q0 ∈ I and

![](images/231_6.jpg)

such that ![](images/231_5.jpg) holds infinitely often. Then

![](images/231_7.jpg)

and for infinitely many i we have ![](images/231_8.jpg) Therefore, β is accepted by A, which shows that β ∈ L.

The implication (b)⇒(c) is [Lemma 7.58](#chapter07_5.xhtml_chapter07_5_1). The direction (c)⇒(d) is trivial. The direction (d)⇒(a) is a special case of [Theorem 7.54](#chapter07_4.xhtml_chapter07_4_27). Indeed, if φ weakly recognizes L, then L is a finite union of ω-rational languages having the form [s][t]ω. By [Theorem 7.54](#chapter07_4.xhtml_chapter07_4_27) such a language is ω-regular.

□

Corollary 7.60 (Büchi). The class of ω-regular languages is a Boolean algebra. This means, it is closed under finite union and complementation.

Proof: The equivalence (a) ⇔ (b) together with [Proposition 7.57](#chapter07_4.xhtml_chapter07_4_33) shows closure under complementation. Closure under union is clear: ω-regular languages are ω-rational.

□

### 7.7.5 Monadic second-order logic over infinite words

The syntax of MSO over a finite alphabet Σ uses first-order variables, denoted by x, y, z, . . . , and monadic second-order variables, denoted by X, Y, Z, . . . . First-order variables represent natural numbers (= positions in an infinite word) and the monadic second-order variables represent subsets of ℕ (= sets of positions). Using this interpretation, we have a natural semantics for formulas like 0 ∈ X (saying that the first position 0 is in X), x ∈ X, y = x + 1, x ≤ y, X ⊆ Y for positions and subsets of positions in every (finite or) infinite word. Let u = a0a1a2 ⋅⋅ ⋅ ∈ Σω (with ai ∈ Σ) be an infinite word over Σ. The infinite word u is formally defined as a mapping u : ℕ → Σ with u(i) = ai for all i ∈ ℕ. This yields a natural semantics for the formula λ(x) = a; it is true for u at position x ∈ ℕ if and only if u(x) = a.

As usual in a logical formalism, MSO allows us to use the constant ⊥ (for false), Boolean connectives ∧, ∨ (for and, or), ¬ (for negation), → (for implication), as well as quantifiers ∀x, ∃x, ∀X, ∃X over first- and second-order variables. The syntax can be reduced by reading, for example, a formula ∀xφ as a macro for ¬∃x¬φ. So, we allow some freedom in the precise choice of the syntax. As usual in logic, a formula without free variables is called sentence. It means a formula where every occurrence of a variable is in the scope of some quantifier bounding that variable. If φ ∈ MSO is a sentence, then we define u ' φ to be true if φ evaluates to true under the interpretation given by u. We obtain the language

![](images/232_4.jpg)

For example, “∃x : λ(x) = a” describes the ω-regular language Σ∗aΣω. The formula “∃x∀y : λ(y) = a ∨ x < y” means “u begins with the letter a.” In order to have an example which uses second-order variables, consider the language L = { aa2nbω | n ∈ ℕ}; it is the set of infinite words which begin with an odd number of a’s followed by bω. Hence, there is a natural partition into three sets. A subset O of odd positions labeled by a, a subset E of even positions labeled by a, and the rest R. For the specification of L, it is enough to use two second-order variables

![](images/232_3.jpg)

An obvious question is whether there is an equivalent first-order sentence describing L. This is actually not the case, but we do not prove it here. The interested reader is referred to the survey [[24](#Bibliography.xhtml_Bibliography_25)]. The criterion for first-order definable language is that their syntactic monoids are aperiodic. In the case of L as given earlier Synt(L) contains the cyclic group ℤ/2ℤ. The group takes care that we alternate between odd and even positions. So L is not aperiodic and therefore not first-order definable.

In dealing with logic it is convenient to define macros like a ∈ λ(X). For us, the formula is a shorthand for “∃x : x ∈ X ∧ ∀x : x ∈ X → (λ(x) = a).” We can also define X ∩ Y = 0 as the macro “∀x : x ∈ X → x ∉ Y.” It is easy to see that we can express all formulas defined so far if we restrict the set of atomic formulas to be

![](images/233_10.jpg)

For example, we can write y = x + 1 as the formula x < y ∧ ∀z : x < z → y ≤ z.

Lemma 7.61. Let A be a Büchi automaton with A = (Q, Σ, δ, I, F) and Q = {1, . . . , n}. Then, we can construct an MSO-sentence φ such that L(A) = L(φ). Moreover, φ has the form

![](images/233_9.jpg)

where ψ uses only second-order variables in {X1, . . . , Xn} and all of them are free in ψ. In particular, every ω-regular language is MSO-definable.

Proof: The idea is as follows. Consider u ∈ L(A). Then there is a run

![](images/233_3.jpg)

which starts in I and visits some state in F infinitely often. Thus, we obtain a natural partition of ℕ into subsets Xp (where p ∈ Q) such that following the path ![](images/233_4.jpg) ![](images/233_5.jpg) we have x ∈ Xp for p = qx. This leads to the following formula:

![](images/233_8.jpg)

where ψ(X1, . . . , Xn) = ψ0 ∧⋅ ⋅⋅ ∧ ψ3 and the ψk are defined as follows:

–ψ0 = ⋁i∈I 0 ∈ Xi, that is, we start in an initial state.

–ψ1 = ⋁f∈F ∀x∃y : x < y ∧ y ∈ Xf , that is, we visit a final state infinitely often.

–ψ2 = ⋀i≠j(Xi ∩ Xj = 0), that is, we are never in two states simultaneously.

–ψ3 = ⋀i ⋀a∈Σ((λ(x) = a ∧ x ∈ Xi) →⋁i,a,j)∈δ x + 1 ∈ (Xj) describes a run.

This proves the claim L(A) = L(φ).

□

A fundamental result of Büchi states the converse of [Lemma 7.61](#chapter07_5.xhtml_chapter07_5_7); if L ⊆ Σω definable in MSO, then we can construct a Büchi automaton A such that L = L(A). The analog for finite words was known earlier; it is attributed to Büchi, Calvin C. Elgot (1922–1980), and Boris Avraamovich Trakhtenbrot (born 1921).

Theorem 7.62 (Büchi). A language L ⊆ Σω is MSO-definable if and only if it is accepted by some nondeterministic Büchi automaton.

Proof: The direction from automata to MSO follows from [Lemma 7.61](#chapter07_5.xhtml_chapter07_5_7). For the other direction it is convenient to concentrate on second-order variables. We switch to the fragment MSO0 of MSO, where we do not allow any first-order variables. The set of atomic formulas in MSO0 is defined as follows:

![](images/233_11.jpg)

We have to explain the semantics of |X| = 1, X < Y and a ∈ λ(X). We define the meaning of |X| = 1 by the formula ∃x∀y : x ∈ X ∧(y ∈ X → x = y). Thus, |X| = 1 means that X is a singleton. As it is an atomic formula, it is not a macro in MSO0. We define the meaning of X < Y by the formula ∃x ∀y : x ∈ X ∧ y ∈ Y → x < y. Thus, X < Y means that there is a first position in X which is before all positions in Y. Themeaning of a ∈ λ(X) should be self-explaining; the semantics is defined by ∃x : x ∈ X ∧λ(x) = a.

The transformation of an MSO sentence into an equivalent sentence over MSO0 is easy. We start with a sentence, hence there are no free variables. Moreover, ∀x : ψ(x) has the same meaning as ¬∃x¬ψ(x). Therefore, it is enough to transform a sentence φ = ∃x : ψ(x) into MSO0. To do so, introduce a fresh monadic second-order variable Zx and replace φ by ∃Zx : |Zx| = 1 ∧ ψ(Zx). Thus, in ψ all free occurrences of x are substituted by Zx. For example, the sentence ∀x∃y : x < y is equivalent with ∀Zx ∃Zy : |Zx| ≠ 1 ∨ (|Zy| = 1 ∧ Zx < Zy). As a consequence, we can view every MSO sentence as a sentence in MSO0.

In order to finish the proof, we need an interpretation of formulas with free variables. Assume that a formula φ in MSO0 uses X1, . . . , Xn as free variables. (We write φ = φ(X1, . . . , Xn) to indicate this.) Consider the augmented alphabet Γn = Σ×{0, 1}n. Then, we can think that an ω-word ![](images/234_1.jpg) consists of n + 1 infinite rows: the first row is an infinite word u ∈ Σω, the other rows are infinite words over {0,1}. We can also think of a one-sided infinite tape which is divided into n + 1 tracks numbered from 0 to n.

Given ![](images/234_2.jpg) we have an interpretation I(Xi) = { x ∈ ℕ| wi(x) = 1 }. This means x ∈ I (Xi) if and only if on the ith track of w at position x is 1\. Using this interpretation, we obtain a for every ![](images/234_3.jpg) a well-defined truth value

![](images/234_10.jpg)

The strategy to show that L(φ) defines an ω-regular language for a sentence φ ∈ MSO is now as follows:

(1)Rewrite φ into the fragment MSO0

(2)Rewrite φ into prenex normal form. Thus, without restriction, we have

![](images/234_11.jpg)

In ψ(X1, . . . , Xn) all variables are free and ψ is a Boolean combination of atomic formulas as in ([7.2](#chapter07_5.xhtml_chapter07_5_9)); and each Qi is either the quantifier ∀ or ∃.

Let ψ be an atomic formula. Then the construction of a Büchi automaton *A*ψ accepting the word ![](images/234_6.jpg) with w ' ψ is straightforward:

–Forψ = (a ∈ λ(Xi)), the automaton Aψ accepts those ![](images/234_7.jpg) where there is a position x such that w0(x) = a and wi(x) = 1\. Thus, the automaton accepts those words w in ![](images/234_8.jpg) which belong to some ![](images/234_9.jpg) where (a, i) denotes any letter in Γn with a on track 0 and the symbol 1 on track i.

–Forψ = (|Xi| = 1), the automaton Aψ accepts those ![](images/235_1.jpg) where wi ∈ 0∗10ω and wi is the contents on track i.

–Forψ = (Xi < Xj), the automaton Aψ accepts those ![](images/235_2.jpg) with υi ∈ 0ω.

–Forψ = (Xi ⊆ Xj), the automaton Aψ accepts all ![](images/235_3.jpg) such that for all x with wi(x) = 1, we have wj(x) = 1, too.

–Forψ = (Xi = 0), the automaton Aψ accepts those ![](images/235_4.jpg) where wi = 0ω.

Using the fact that ω-regular languages are closed under finite union and complementation, we can construct a Büchi automaton An such that

![](images/235_5.jpg)

Since ∀Xnψn(X1, . . . , Xn) is equivalentwith ¬∃Xn¬ψn(X1, . . . , Xn) and since ω-regular languages are closed under complementation, we can ignore negations. Hence, it is enough to construct a Büchi automaton An−1 for the language

![](images/235_6.jpg)

under the assumption that some automaton An is already known such that

![](images/235_7.jpg)

This final step, to construct An−1, uses projection. Assume that An has state space Q and the transition relation δ ⊆ Q × Γn × Q. Then we define

![](images/235_8.jpg)

□

Replacing δ by δ' in An, we obtain An−1; and we are done.

Corollary 7.63. Monadic second-order logic MSO(ℕ, ≤) is decidable.

Proof: Given a sentence φ in MSO(ℕ, ≤), [Theorem 7.62](#chapter07_5.xhtml_chapter07_5_8) gives a method to construct a Büchi-automaton Aφ such that φ is true if and only if L(Aφ) ≠ 0\. The method is effective because the translations from formulas to automata and all Boolean operations on automata are effective.

□

## 7.8 Presburger arithmetic

Gödel’s incompleteness theorem states that it is impossible to check algorithmically whether a given arithmetic formula over the natural numbers is true; the formal language of true arithmetic sentences is undecidable. If we do not allow multiplication, then the situation changes drastically. This is the framework of Presburger arithmetic; and it is decidable. More precisely, Presburger arithmetic, named after Mojżesz Presburger (1904–1943), consists of all true statements that can be expressed in first-order logic over natural numbers with addition [[86](#Bibliography.xhtml_Bibliography_87)].

The syntax of the logic FO[ℕ, +] is defined inductively as follows:

–Forvariablesx, y, z and constants n ∈ ℕ, the formulae x = n and x + y = z belong to FO[ℕ, +].

–Ifφ and ψ belong to FO[ℕ, +], then φ ∨ ψ and ¬φ belong to FO[ℕ, +].

–Ifφ is in FO[ℕ, +], then ∃x φ belongs to FO[ℕ, +].

It is enough to give this reduced syntax as we may use the shorthand notation φ ∧ ψ for ¬(¬φ ∨ ¬ψ) and ∀x φ for ¬∃x ¬φ. An occurrence of a variable x is free in φ if it does not belong to the scope of a quantifier which binds x. As above, sentence is a formula without free variables. The truth value of a sentence is uniquely determined. For example, ∃x : x = 0 is true, but ∀x : x = 0 is false. We write φ(x1, . . . , xn) to indicate that x1, . . . , xn are the free variables of φ, but we do not insist that all xi actually occur in φ. Hence, if φ = ∃x : x = 0, then, by a slight abuse of notation, φ(y, z) indicates that we view φ as a formula in free variables y and z.

Presburger arithmetic is defined as the set of true sentences in FO[ℕ, +]. We want to show now that Presburger arithmetic can be decided with the help of automata; that is, for a given sentence φ of FO[ℕ, +], we give a decision procedure which answers the question whether φ is true. The focus is more on an application of already introduced techniques (constructions on automata) rather than presenting the most efficient methods. According to [Section 7.1](#chapter07_1.xhtml_chapter07_1_2), a Σ∗-automaton is a complete and deterministic automaton over Σ∗. In this section, we consider finite automata, only. Each formula φ(x1, . . . , xk) defines a subset of ℕk by

![](images/236_3.jpg)

Here, φ(n1, . . . , nk) denotes the formula that results from substituting each free occurrence of xi in φ by ni. For example, φ(x1, . . . , xk , y) = ∃z(z + z = y) defines the set ℕk × 2ℕ.

The notion of semilinear set refers to a class of subsets in a commutative monoid. We mainly consider semilinear sets in ℕk, but our results hold more generally, for example, in the free Abelian group ℤk.We will see that the notions of semilinear sets and rational sets coincide in commutative monoids. Let (M, +, 0) be a commutative monoid. A subset L of M is called linear if we can write L = p0 + {p1, . . . , pℓ}∗ for some p0, . . . , pℓ ∈ M. Thus, in additive notation, a linear set has the form

![](images/236_2.jpg)

Note that L has a canonical interpretation in M because for p ∈ M and n ∈ ℕ the notation n ⋅ p means the n-fold sum p + ⋅⋅ ⋅ + p. By definition, a linear set is rational in M. So is any finite union of linear sets. This leads to the following definition. A subset L of M is called a semilinear set if it is a finite union of linear sets. It follows that semilinear sets are rational, too.

For example, if we consider the monoid ℕ2 with pointwise addition, the set L = { (m, n) ∈ℕ2 | m, n ≥ 1 } is linear because L = (1, 1) + ℕ(1, 0) + ℕ(0, 1). The union S of L with the singleton {(0, 0)} is semilinear but not linear. Indeed, S is a commutative submonoid ofℕ2; and a linear set, which is submonoid, is finitely generated, but S is not finitely generated. To see this, note that a linear set ![](images/237_1.jpg) is a submonoid of ℕ2 if and only if p0 = (0, 0). Now assume, for the sake of contradiction, that S = (0, 0) ∪ (1, 1) + ℕ(1, 0) + ℕ(0, 1) is finitely generated. Then there exists a generator (ℓ, n) of S where ℓ is maximal. We have (ℓ + 1, 1) ∈ S, but we cannot generate it by any subset in { (m, n) ∈ℕ2 |m = 0 ∨ (m ≤ ℓ ∧ n ≥ 1) }.

Let us show that rational subsets in a commutative monoids are semilinear. Finite subsets are semilinear. The product of semilinear sets L and K is L + K. In order to see that L+K is semilinear, it is enough to show that L +K is linear if L and K are linear. This is obvious, because ![](images/237_2.jpg)

The class of semilinear sets is closed under star-operation, because (K ∪ L)∗ = K∗L∗ and (p0 + {p1, . . . , pℓ}∗)∗ = {0} ∪ (p0 + {p0, . . . , pℓ}∗). Therefore, a subset in a commutative monoid is semilinear if and only if it is rational. It follows directly from the definition that semilinear sets in ℕk are definable in Presburger arithmetic. The converse was established in [[39](#Bibliography.xhtml_Bibliography_39)] and [[45](#Bibliography.xhtml_Bibliography_45)]. Essentially, to prove the converse amounts to show that semilinear sets in ℕk are closed under complementation. Boolean operations on semilinear sets are effective. Hence, we obtain the result that Presburger arithmetic is decidable, [Theorem 7.64](#chapter07_5.xhtml_chapter07_5_20). The aim of this section is to prove [Theorem 7.64](#chapter07_5.xhtml_chapter07_5_20) by simple automata theoretical constructions.

We represent elements of ℕk as words over the alphabet {0, 1}k according to their binary representation; a bit sequence b0 ⋅⋅ ⋅ bℓ ∈ {0, 1}∗ is a representation of n, if ![](images/237_3.jpg) The least significant bit is on the left and trailing zeros at the right end of the sequence are allowed. For example, 001, 0010, 00100, ... represent the number 4\. Every string in 0∗, including the empty word, represents the number 0\. Actually, due to the possibility of leading zeros, each number has infinitely many representations. Elements in {0, 1}k can be presented by column vectors. A word

![](images/237_4.jpg)

is an encoding of a tuple (n1, . . . , nk) ∈ℕk if for all 1 ≤ i ≤ k the ith track b0,i ⋅⋅ ⋅ bℓ,i is a representation of ni. Accordingly, this approach is sometimes called track technique. The other way round, if each ni is represented by some ui ∈ {0, 1}∗, then we may append zeros to the tail such that all ui have the same length ℓ for 1 ≤ i ≤ k. Thus, every tuple (n1, . . . , nk) ∈ ℕk has a representation by some u ∈ ({0, 1}k)∗. Again, there are infinitely many representations.

Consider a formula φ(x1, . . . , xk) in free variables x1, . . . , xk. We define the language L(φ) specified by φ(x1, . . . , xk) as

![](images/238_1.jpg)

That is, L(φ(x1, . . . , xk)) consists of all encodings of those tuples (n1, . . . , nk)∈ ℕk which satisfy φ(x1, . . . , xk). If φ is a sentence, then we have k = 0; and the sentence φ is false if and only if L(φ) = 0.

Theorem 7.64 (Presburger 1929). Presburger arithmetic is decidable.

Proof: The idea is as follows. Given a formula φ = φ(x1, . . . , xk)∈ FO[ℕ, +],we effectively construct a finite ({0, 1}k)∗-automaton Aφ such that L(Aφ) = L(φ(x1, . . . , xk)). The result follows, because we can test L(φ(x1, . . . , xk)) ≠ 0 by graph reachability. In particular, we can test whether φ(x1, . . . , xk) is satisfiable. A sentence in FO[ℕ, +] is true if and only if it is satisfiable. The construction of the automaton Aφ is by structural induction on the formula. The general scheme is as follows. Whenever we consider an automaton A over ({0, 1}k)∗, then we also view it as an automaton over ({0, 1}k+1)∗, we replace each transition with label u ∈ ({0, 1}k)∗ by two transitions, one with label (u, 0) ∈ ({0, 1}k+1)∗, the other one with label (u, 1) ∈ ({0, 1}k+1)∗. As a consequence, it is enough to construct an automaton for formulas φ(x1, . . . , xk) where each xi has a (visible) free occurrence in φ.

We start with the formula φ(x1) = (x1 = n) where n ∈ ℕ. Let b0 ⋅⋅ ⋅ bℓ ∈ {0, 1}∗ be the shortest representation of n. An automaton with ℓ+2 states for the formula x1 = n, is given by

![](images/238_2.jpg)

As explained earlier, the automaton also represents φ(x1, . . . , xk) for all k ≥ 1.

For x1 + x2 = x3, we use the following automaton. It has two states: we are in the left state if the “carry bit” for the addition is 0, if the carry is 1, then we are in right state.

![](images/239_1.jpg)

Since, for example, in a formula x + y = z some of the variables might be equal, we need an automaton for the formula x1 = x2. This is given by

![](images/239_2.jpg)

By [Corollary 7.18](#chapter07_2.xhtml_chapter07_2_11), the family REG(Σ∗) is a Boolean algebra. We have seen earlier that the corresponding constructions are effective. Thus, given φ and ψ, we effectively find automata for L(¬φ) = ({0, 1}k)∗ \ L(φ) and for L(φ ∨ ψ) = L(φ) ∪ L(ψ).

Now, suppose that φ = ∃xk ψ(x1, . . . , xk). Let π : {0, 1}k → {0, 1}k−1 be defined by π(b1, . . . , bk) = (b1, . . . , bk−1); it is the projection to the first k − 1 components. By symbol-wise application, π : ({0, 1}k)∗ → ({0, 1}k−1)∗ defines a homomorphism, where the last track is omitted. Again, we may use [Corollary 7.18](#chapter07_2.xhtml_chapter07_2_11) to see that π(L(ψ)) is regular. Alternatively, we can apply the projection to the labels of the transitions. This yields a nondeterministic finite automaton accepting π(L(ψ)). However, it might be that L(φ) ≠ π(L(ψ)). (Indeed, consider the formula x1 = 1 ∧ ∃x2 : x2 = 01\. We have 1 ∈ L(φ)\π(L(ψ)). On the other hand, 10⋅0∗ ⊆ L(φ)∩π(L(ψ)).) The solution is given by [Theorem 7.19](#chapter07_2.xhtml_chapter07_2_12), we construct an automaton which accepts the quotient π(L(ψ)){0∗}−1. The result follows because

![](images/239_4.jpg)

□

The automata-theoretic approach cannot be extended to arithmetic over natural numbers with addition and multiplication. For example, the formula x ⋅ y = z does not have any suitable representation by finite automata. However, the problem is deeper. Gödel’s incompleteness theorem[[46](#Bibliography.xhtml_Bibliography_46)] shows that arithmetic over natural numbers with addition and multiplication is undecidable. Moreover, Yuri Matiyasevich (born 1947) showed that Hilbert’s tenth problem is undecidable. Hilbert had posed this problem in the elaboration to his famous lecture at the International Congress of Mathematicians in the year 1900:

Given a Diophantine equation with any number of unknown quantities and with rational integral numerical coefficients: To devise a process according to which it can be determined in a finite number of operations whether the equation is solvable in rational integers.

Thus, the problem asks to decide the existential fragment without negation in the theory of natural numbers with addition and multiplication. When Matiyasevich showed the undecidability of Hilbert’s tenth problem in 1970 (at the early age of 22), he used previous work by Martin Davis (born 1928), Hilary Putnam (born 1926), and Julia Robinson (1919–1985); see [[71](#Bibliography.xhtml_Bibliography_71)]. Nowadays, the solution to Hilbert 10 is frequently attributed to all four persons, for example, by Matiyasevich himself.

## 7.9 Solutions of linear Diophantine systems

Our approach to solve linear Diophantine systems is closely related to [[9](#Bibliography.xhtml_Bibliography_10)]. It is also folklore. A linear Diophantine system is a pair (A, c), where A ∈ ℤr×n is an r × n integer matrix and c ∈ ℤr is an integer vector. The problem is to answer the following question: “∃x ∈ ℕn : Ax = c?”

The problem is in some sense harder than the corresponding question for a solution in ℤn, because if we know how to decide the existence of solutions over natural numbers, then we can solve (by guessing the signs for a solution x ∈ ℤn) the problem over integers. In complexity theory, the difference can be made precise. Solving systems of linear equations over ℕ is one of the classical NP-complete problems, where NP-hardness is easy to show (even in unary notation), but the proof for the containment in NP (if the entries are given in binary) is more involved [[51](#Bibliography.xhtml_Bibliography_51)]. The same problem over ℤ is easier in the sense that it can be solved in deterministic polynomial time [[33](#Bibliography.xhtml_Bibliography_33), [52](#Bibliography.xhtml_Bibliography_52)]. Over ℤ, the problem becomes however immediately NP-complete if we consider inequalities by asking “∃x ∈ ℤn : Ax ≤ c?” For natural numbers this makes no difference as the sentence ∃x ∈ ℕn : Ax ≤ c is equivalent to the sentence ∃x, y ∈ ℕn : y + Ax = c. Complexity issues and such transformations are not in our focus, but deciding, whether a linear Diophantine systems has a solution, is certainly one of the most fundamental problems in integer arithmetic. Why is this problem decidable at all? The first answer is that “∃x ∈ ℕn : Ax = c?” is expressible in Presburger arithmetic; and we know that Presburger arithmetic is decidable by [Theorem 7.64](#chapter07_5.xhtml_chapter07_5_20). However, for a fundamental result we would like to have a more direct proof which does not involve an excursion to first order logic over naturals with addition. Assume that Alice wants to explain to Bob in a very short time, say 20 min, that the set of solvable linear Diophantine systems is decidable. Assume further that this fact is entirely new to Bob; in particular he does not know anything about Presburger arithmetic. Alice might start to explain something with Cramer’s rule, determinants or Gaussian elimination – just the standard way to do it. But then she realizes that Bob never heard about any of these terms, so better not start with a course on linear algebra within a time slot of 20 min. Even if Bob knows how to solve Ax = c in rationals, it is not a priori clear that he knows how to solve Ax = c in integers or in positive integers. What Bob knows are basic matrix operations and the notion of linear Diophantine system.

Alice explores the idea of “nondeterministic algorithms” in order to show that linear Diophantine systems are indeed solvable. She achieves more: she presents a simple and easy-to-understand method which not only provides on input (A, c) an answer whether Ax = c holds for some x ∈ ℕn; in addition, she describes the set of all solutions. Here, the solution set ![](images/241_4.jpg) is defined by![](images/241_5.jpg)

The 1-norm is defined as usual ‖c‖1 = Σi |ci| and ‖A‖1 = Σi,j |aij|.Without restriction, by introducing slack variables and dummy equations we can assume without loss of generality that r = n and

![](images/241_6.jpg)

Let us now explain the approach of Alice. According to her advice, we construct a nondeterministic finite automaton (NFA). We define first a finite directed graph G where the nodes are integer vectors b ∈ ℤn such that ‖b‖1 ≤ ‖A‖1. Thus, there are at most ![](images/241_7.jpg) nodes. The arcs of G are labeled by affine mappings of type x ↦ λx + e with λ ∈ {1, 2} and e ∈ ℕn with ‖e‖1 ≤ n.

We define b = 0 ∈ ℤn to be the final state and the vector c to be the initial state in G. In this way, G becomes an NFA. The set of labels on paths from the initial to the final state yields a rational set R = L(A) of affine mappings from ℕn to itself.[8](#Notes.xhtml_Notes_8)The construction of the arcs in G is based on the following idea. Consider a node b ∈ ℤn and assume that some x ∈ ℕn satisfies Ax = b. Let x = (x1, . . . , xn) and I = {i ∈ {1, . . . , n} | xi is odd }. Define a new vector x' = x − eI where eI = (ε1, . . . , εn) is the characteristic vector of I, that is, εi = 1 if i ∈ I and εi = 0 otherwise. Then all components in x' are even. Since Ax = b, we conclude that Ax' = b' ∈ 2ℤn for b' = b − AeI. Thus, we can define x'' = x/2 and b'' = b/2, and x'' satisfies Ax'' = b. On the other hand, if x' ∈ ℕn is any vector satisfying Ax'' = b, then x = h(x) satisfies Ax = b, where h is the affine mapping x ↦ 2x + eI.

For all subsets I ⊆ {1, . . . , n} and nodes b in G, we introduce an arc from b to b'' = (b − AeI )/2, provided b'' ∈ ℤn and ‖b‖1 ≤ ‖A‖1. The label of this arc is 2x + eI and denotes the affine mapping x ↦ 2x + eI.

This construction is “sound”: by following the arcs we cannot transform an unsolvable linear Diophantine system into a solvable one.

Next, we prove “completeness”: if b is any node in G and x ∈ ℕn is a vector solving Ax = b, then there exists a path in the graph G from b to the final node 0 such that h(0) = x, where h is the label of that path, interpreted as composition of mappings. We show this claim by induction on ‖x‖1.

The assertion is trivial for ‖x‖1 = 0, because then we must have x = b = 0\. Thus, we may assume that at least one component xi of x = (x1, . . . , xn) is positive. As above, let I = {i ∈ {1, . . . , n} | xi is odd } and eI be the characteristic vector of I. Then b' = b − AeI ∈ 2ℤn and x'' = (x − eI)/2 ∈ ℕn satisfy Ax'' = b'' where b'' = b/2\. Thus, we only need to show that b'' is a node in G, that is, ‖b‖1 ≤ ‖A‖1. This is immediate: we have ‖b‖1 ≤ ‖A‖1 and hence

![](images/242_3.jpg)

We are done by induction because ‖x‖1 < ‖x‖1.

What we have shown is that on input (A, c) we can effectively construct a finite labeled graph G (of singly exponential size) with final state 0 and initial state c which, when viewed as a nondeterministic finite automaton, accepts a rational set R of affine mappings from ℕn to itself such that

![](images/242_4.jpg)

Clearly, Ax = c has a solution if and only if *R* ≠ Ø.

Actually, the graph G is not optimal, as it might contain unreachable nodes and as it always has a selfloop around 0 labeled by x ↦ 2x, even if Ax = c has only finitely many solutions. This is something we do not like because the graph should be acyclic if there are finitely many solutions, only. We prefer to have a graph that encodes solutions in a more efficient way; it should be empty if there are no solutions and it should have no directed cycles if there are only finitely many solutions. For example, in the case that Ax = 0 where A is invertible, so x = 0 is the only solution, the graph we have constructed (and hence the rational set) contains the infinite set of mappings x ↦ 2ℓx for ℓ ∈ ℕ. We can remove the selfloop around 0 by introducing additional arcs. If we are at node 0 and x = 0, then we are at a final node and there is no need to use the selfloop x ↦ 2x at 0\. Therefore, it is enough to consider a nonzero solution x of Ax = 0\. Since x ≠ 0, there is some index 0 ≤ i ≤ n such that xi > 0. Then x' = x − e{i} ∈ ℕn solves Ax' = −Ae{i}, and we have ‖−Ae{i}‖1 ≤ ‖A‖1. Hence, −Ae{i} is a node in G. Thus, we simply add the n arcs from 0 to the nodes −Ae{i} for 1 ≤ i ≤ n and each such arc is labeled by x + e{i}.

This yields a new NFA ![](images/g.jpg)'' which accepts the rational language *R*' = L(![](images/g.jpg)'). The graph ![](images/g.jpg)' for the linear Diophantine system ((1, −1), 2) (representing x1 − x2 = 2) is depicted in [Figure 7.3](#chapter07_6.xhtml_chapter07_6_3). We retain for R' the first two properties of R, but we also obtain a desirable third property

(a)(∃x ∈ ℕn : Ax = c) ⇔ *R*' ≠ Ø

(b){ x ∈ ℕn | Ax = c } = { h(0) ∈ℕn | h ∈ *R*' }

(c)|{ x ∈ ℕn | Ax = c }| <∞ ⇔ |*R*'| <∞

We can then trim the NFA by removing any node that does not lie on a path from initial to final states.

Example 7.65. For simplicity, let r = 1 and n = 2; there is only one equation with two variables. We consider the linear Diophantine system is Ax = 2 were A = (1, −1). We have ‖A‖1 = ‖2‖1 = 2\. Hence G has five states: −2, . . . ,2, where 2 is initial and 0 is final. Replacing the loop around state 0 by arcs labeled x + e{i} yields the graph which is depicted in [Figure 7.3](#chapter07_6.xhtml_chapter07_6_3). The state −2 does not lie on any path from the initial to final vertices; so removing the state −2 produces a smaller G. However, this is not the smallest NFA describing the set of all solutions. For example, an ad hoc construction shown in [Figure 7.4](#chapter07_6.xhtml_chapter07_6_4) also describes all solutions; it has only two states.

![](images/243_1.jpg)

Fig. 7.3. The NFA ![](images/g.jpg)' (before trimming) describing all solutions x ∈ ℕ2 of (1, −1)x = 2.

![](images/243_2.jpg)

Fig. 7.4. The “minimal” NFA 𝓜 describing all solutions x ∈ ℕ2 of (1, −1)x = 2.

◊

## Exercises

7.1. Consider the syntactic monoid Synt(L) for L = {anbn ∈ Σ∗ | n ∈ ℕ} with Σ = {a, b}∗ and a ≠ b. For u ∈ Σ∗ let [u] ∈ Synt(L) denote the syntactic congruence class of the word u.

(a)Show that each congruence class [u]L ∈ Synt(L) contains a unique shortest representing word. Show that the set of all shortest representatives is regular.

(b)Show that *D* = *J* is not true in Synt(L).

(c)Show that there are s, t ∈ Synt(L) such that s ∼*J* t and s ≤*R* t, but s∼*R* t.

7.2. A semigroup S is cyclic if there is an element x ∈ S with S = {xk | k ≥ 1 }. Determine all cyclic semigroups with n elements.

7.3. Let φ: Σ∗ → M be a homomorphism into a finite monoid M. Show that a number n ≥ 1 exists with φ(Σn) = φ(Σ2n). The smallest such number is called the stabilization index of φ.

7.4. Let M be a monoid and let L ⊆ M be recognizable. Show that the language ![](images/244_1.jpg) { u ∈ M | uu ∈ L } is recognizable, too.

7.5. (Mezei’s theorem) Let M1 and M2 be monoids. Showthat L ⊆ M1×M2 is recognizable if and only if L is a finite union of languages of the form K1×K2 with K1 ∈ REC(M1) and K2 ∈ REC(M2).

7.6. Let *A* = (Q, ⋅, q0 , F) be a deterministic M-automaton. Then the complement automaton is *B* = (Q, ⋅, q0 , Q \ F). Show L(*B*) = M \ L(*A*).

7.7. Let *A*1 = (Q1, ⋅, q1, F1) and *A*2 = (Q2, ⋅, q2, F2) be two deterministic M-automata. For an arbitrary subset F ⊆ Q1 × Q2, one can construct the product automaton *B* = (Q1 × Q2, ⋅, (q1, q2), F) with (p, q) ⋅ a = (p ⋅ a, q ⋅ a).

(a)Give a subset F such that L(*B*) = L(*A*1)∪ L(*A*2).

(b)Give a subset F such that L(*B*) = L(*A*1)∩ L(*A*2).

7.8. Let Σ = {a, b} and L = ((ab)∗a ∪ abb)∗ ∈ RAT(Σ∗).

(a)Use the Thompson construction to find a Σ∗-automaton A with L = L(*A*).

(b)Convert A into a spelling automaton A.

(c)Convert A' into a deterministic automaton B.

(d)Determine an automaton C with L(𝓒) = Σ∗ \ L.

(e)Specify a rational expression for Σ∗ \ L.

7.9. Minimize the following automaton.

![](images/244_2.jpg)

7.10. (Brzozowski’s automata minimization) Let Σ be a finite alphabet. For a spelling nondeterministic finite Σ∗-automaton A = (Q, δ, I, F) let *A*ρ denote the automaton (Q, δρ , F, I), where δρ = {(q, a, p) | (p, a, q) ∈ δ } (the symbol ρ stands for reverse). The nondeterministic automaton Aρ accepts the mirror language L(*A*)ρ = { an ⋅⋅ ⋅ a1 | a1 ⋅⋅ ⋅ an ∈ L(*A*), ai ∈ Σ }. Finally, by 𝓟(*A*) we denote the subset automaton of A. Show that for any deterministic finite Σ∗-automaton *A* = (Q, δ, q0, F), in which all states are reachable, the automaton 𝓟(*A*ρ) is the minimal Σ∗-automaton for the language L(*A*)ρ.

Remark: This means that for each spelling nondeterministic automaton after the four operations mirror – subset construction – mirror – subset construction one ends up with the equivalent minimal automaton. This amazing observation is due to Brzozowski (born 1935) [[11](#Bibliography.xhtml_Bibliography_12)].

7.11. A nonempty class of finite monoids V is a variety (also called a pseudovariety in the terminology of universal algebra) if the following two closure properties are satisfied. (i) N ∈ V and N' ≺ N implies N' ∈ V. (ii) N1, N2 ∈ V implies N1 × N2 ∈ V. For any monoid M let 𝓥(M) be the set of all subsets of M which are recognized by a monoid from the variety V. Show:

(a)The subset system 𝓥(M) is closed under finite union, finite intersection and complementation.

(b)We have L ∈ 𝓥(M) if and only if Synt(L) ∈ V.

7.12. Let Σ be a finite alphabet and L ⊆ Σ∗. Show that the following properties are equivalent:

(i)L is a Boolean combination of languages of the form B∗ for B ⊆ Σ.

(ii) For all x, y ∈ Synt(L) we have x2 = x and xy = yx.

7.13. Let M be a finite monoid and C the smallest family of finite monoids containing U2 and being closed under wreath products and divisors. Show:

(a)M is aperiodic if and only if {1} is its only group divisor.

(b)M is aperiodic if and only if M ∈ C.

7.14. Let M and N be monoids and let φ: A∗ → M ≀N be a homomorphism. Show that there exist homomorphisms 𝓥 : A∗ → N and ![](images/245_2.jpg) such that φ(u) = φ(υ) whenever ν(u) = ν(υ) and μ(σν(u)) = μ(σν(υ)).

7.15. Let M and N be monoids. A surjective partial mapping ψ: N → M is a covering if for each m ∈ M at least one element m̂ ∈ N exists with

![](images/245_1.jpg)

for all n ∈ N, for which ψ(n) is defined. The element m̂ is called a cover of m. Show that M is a divisor of N if and only if there exists a covering ψ: N → M.

7.16. Give a covering from Un × U2 to Un+1.

7.17. Let M be a monoid generated by A; let c ∈ A and let N be the submonoid of M generated by A \ {c}. Give a covering from (UN × Mc) ≀ (N# × U1) to M.

7.18. Recall that Green’s relation Dis defined in an arbitrary monoid M as L ∘R. Show that D is an equivalence relation; that is, show L ∘ *R* = *R* ∘ L.

7.19. Let φ: Σ+ → S be a homomorphism into a finite semigroup S and let L ⊆ Σω. Show that L is recognized by φ if and only if the following equality holds:

![](images/246_1.jpg)

7.20. Let φ: Σ+ → S be a homomorphism to a finite semigroup S. Define the relation ∼φ on Σω by letting α ∼φ β if there are factorizations α = u1u2 ⋅⋅ ⋅ and β = υ1υ2 ⋅⋅ ⋅ such that ui, υi ∈ Σ+ and φ(ui) = φ(υi). Show that φ recognizes L if and only if from α ∈ L and α ∼φ β it follows that β ∈ L.

7.21. In [Remark 7.50](#chapter07_4.xhtml_chapter07_4_16), we discussed several variants of Büchi automata: acceptance either by states or transitions and allowing that labels on transitions are words instead of letters. We may also allow a set of initial states and/or that there are no incoming arcs into initial states. Show that these variants do not change the expression power of Büchi automata.

## Summary

Notions

–(formal) language

–Kleene star

–recognizing a language

–recognizability, REC(M)

–syntactic monoid

–M-automaton

–state, transition

–acceptance

–finite state

–nondeterministic

–NFA

–reachable state

–minimal automaton AL

–transition monoid

–rational, RAT(M)

–(accepting) run

–equivalent automata

–spelling automata

–regular language

–star-freeSF(M)

–aperiodic

–local divisorMc

–simple group

–divisor, group divisor

–partial homomorphism

–flip–flopU2

–wreath product M ≀ N

–right zero

–augmented monoid

–Green’s relations *H*, *L* , *R*,*D*, *J*

–Schützenberger group

–infinite words Σω

–ω-language

–Büchi automaton

–ω-regular, ω-rational

–ultimately periodic

–recognizing L ⊆ Σω

–syntactic homom. μL

–Presburger arithmetic

–linear Diophantine systems

Methods and results

–REC(M) is closed under Boolean operations.

–The syntactic monoid is the smallest monoid recognizing L.

–The minimal automaton is the smallest automaton accepting L.

–Moore’s algorithm for automata minimization.

–The syntactic monoid is the transition monoid of the minimal automaton.

–L ∈ REC(M) ⇔ L is accepted by a deterministic M-automaton with |Q| <∞.

–Thompson construction: conversion from RAT to nondeterministic finite automaton.

–Elimination of ε-transitions and construction of spelling automata.

–State elimination: conversion from nondeterministic finite automaton to RAT.

–L ∈ RAT(M) ⇔ L is accepted by a nondeterministic finite M-automaton.

–McKnight: M finitely generated ⇔ REC(M) ⊆ RAT(M).

–Kleene: If Σ is finite, then REC(Σ∗) = RAT(Σ∗).

–Schützenberger: If Σ is finite, then: L ∈ SF(Σ∗) ⇔ Synt(L) finite and aperiodic.

–Krohn–Rhodes: Every finite monoid M is a divisor of a wreath product consisting of monoids U2 and simple group divisors of M.

–For Green’s relations *L*, *R*,*D*, *J*: *D* = *L* ∘ *R* = *R* ∘ *L* and in finite monoids *D* = *J*.

–Ifs ∼D t in a finite monoid M, then the local divisors M s and Mt are isomorphic.

–Schützenberger groups within a D-class are the group of units in local divisors M s.

–“finitely many a’s” cannot be accepted by a deterministic Büchi automaton

–Deterministic languages are closed under union, intersection, but not under complementation.

–Nonempty ω-regular languages contain ultimately periodic words.

–L is ω-regular ⇔ L is ω-rational ⇔ L is recognized by a homomorphism to a finite monoid ⇔ Synt(L) is finite and μL recognizes L

–ω-regular languages form a Boolean algebra: K, L ⊆ Σω are ω-regular ⇒ K ∪ L, K ∩ L, Σω \ L are ω-regular

–Büchi: MSO over infinite words is decidable.

–Presburger arithmetic is decidable.

–Solution sets of linear Diophantine equations have an effective description by finite automata.

# 8 Discrete infinite groups

This chapter concerns some fundamental issues in combinatorial group theory with a focus on discrete infinite groups. The idea is to prepare the reader for more advanced books such as [[7](#Bibliography.xhtml_Bibliography_8), [8](#Bibliography.xhtml_Bibliography_9), [15](#Bibliography.xhtml_Bibliography_16)] or the classics like [[69](#Bibliography.xhtml_Bibliography_69)] or [[93](#Bibliography.xhtml_Bibliography_94)]. In particular, we discuss amalgamated products, HNN extensions, and their normal forms. We cover free groups and their rational subsets, and show that automorphism groups of finitely generated free groups are finitely generated themselves. The proof is based on simple transformations of finite edge-labeled graphs, which have an interpretation in terms of Whitehead automorphisms. Finally, we take a quick look at geometric aspects by determining the algebraic structure of SL(2, ℤ) as the amalgamated product of ℤ/6ℤ and ℤ/4ℤ over their subgroups of order 2, and by determining the algebraic structure of the modular group PSL(2, ℤ) as the free product of ℤ/3ℤand ℤ/2ℤ. The notion of confluent string rewriting is central to our approach.

## 8.1 Classical algorithmic problems

The most fundamental algorithmic problems for finitely presented groups, formulated in about 1910 by Max Dehn (1878–1952) [[21](#Bibliography.xhtml_Bibliography_22)], are as follows:

–Word problem. Is a given group element g (as a word in given generators) the neutral element in the group?

–Conjugacy problem. Are two given elements g and h conjugate?

–Isomorphism problem. Given two finite presentations of groups, are those two groups isomorphic?

It turns out that these problems are undecidable, but this was not known until the mid-1950s. Undecidability of the word problem in finitely presented groups was shown independently in Russia by Pyotr Sergeyevich Novikov (1901–1975) and in the West by William Werner Boone (1929–1983). A modern proof for the (difficult) undecidability result of the word problem can be found in [[100](#Bibliography.xhtml_Bibliography_101)]. The word problem is a special instance of the conjugacy problem, and once we know that the word problem is undecidable, it is fairly easy to see that the isomorphism problem is undecidable, too. The isomorphism problem was actually raised first by Heinrich Franz Friedrich Tietze (1880–1964) in [[104](#Bibliography.xhtml_Bibliography_105)].

## 8.2 Residually finite monoids

In this chapter, we discuss some sufficient criteria for the decidability of the word problem: for example, if we can embed a finitely generated group G into a group of invertible n × n matrices over some suitable ring or field, say, over the rationals ℚ, then the word problem can be solved “easily” by computing the product of matrices. Checking that a product of matrices over the rationals A1 ⋅⋅ ⋅ Ak is the identity matrix can be further reduced to computing the product of matrices with integer coefficients where, moreover, each matrix has determinant 1\. Thus, the word problem in G can be effectively reduced to the computation of products of matrices in the special linear group SL(n, ℤ). Given a product A = A1 ⋅⋅ ⋅ Ak with Ai ∈ SL(n, ℤ) such that A = (aij) is not the identity, we have either aii ≠ 1 for some i or aij ≠ 0 for some i, j with i ≠ j (or both). Hence, there is some prime p such that aii ≢ 1 mod p or aij ≢ 0 mod p. In other words, if A = (aij) ≠ 1 in SL(n, ℤ), then the canonical homomorphism of SL(n, ℤ) onto the finite group SL(n, ℤ/pℤ)witnesses A ≠ 1 because (aij mod p) ≠ 1 in SL(n, ℤ/pℤ). This leads to the notion of residual finiteness which we define for monoids.

We say that a monoid M is residually finite if, for each m, n ∈ M with m ≠ n, there exists some homomorphism h : M → N onto a finite monoid N such that h(m) ≠ h(n). If M = G is a group, this is equivalent to saying that for each g ≠ 1 there exists a homomorphism h : G → N onto a finite group G such that h(g) ≠ 1 (which is the classical definition of residually finite groups). We have just seen that SL(n, ℤ) is residually finite; and, as a consequence, all subgroups of SL(n, ℤ) are residually finite, too.

A group G is called Hopfian if each surjective homomorphism from G to G is an automorphism. The notion of Hopfian group is named after Heinz Hopf (1894–1971). [Exercise 8.9](#chapter08_4.xhtml_chapter08_4_29) shows that all finitely generated residually finite groups are Hopfian. It is known that SL(n, ℤ) is finitely generated for all n ≥ 1; therefore, all SL(n, ℤ) are Hopfian. We study SL(2, ℤ) more closely in [Section 8.12](#chapter08_4.xhtml_chapter08_4_11).

## 8.3 Presentations

The notion of a presentation using a semi-Thue system provides an important technical tool to study various algorithmic problems for monoids and groups, including the word problem.

Throughout this section, Γ denotes an alphabet. Here an alphabet is a (possibly infinite) set of elements, called letters. We follow the notation from [Chapter 6](#chapter06.xhtml_chapter06_1). A word is a sequence of letters w = a1 ⋅⋅ ⋅ am with m ∈ ℕ and ai ∈ Γ for 1 ≤ i ≤ m. The integer m is the length of the word w, which is denoted by |w|. The empty word has length 0, and frequently we denote it by 1 or ε. The set Γ∗ of all words in Γ becomes a free monoid, where the multiplication is the concatenation (a1 ⋅⋅ ⋅ am) ⋅ (b1 ⋅⋅ ⋅ bn) = a1 ⋅⋅ ⋅ amb1 ⋅⋅ ⋅ bn.

If Γ is equipped with a linear order <, then this order induces a lexicographic order on Γ∗. The words are then arranged as in a dictionary: if a, b ∈ Γ with a < b, then a word of the form pau is prior to each word of the form pbυ. One problem with this order is that, prior to b, there are infinitely many words which start with a. This problem can be avoided by considering the length-lexicographic (or shortlex) order, where we have u < υ if |u| < |υ|, and if |u| = |υ| then we order u and υ with respect to the lexicographic order. If Γ is finite, then there are only finitely many words prior to u ∈ Γ∗. Thus, using a shortlex-ordered lexicon, we can find any u ∈ Γ∗ in a finite amount of time.

If Mis any monoid, then we may uniquely extend each mapπ : Γ → M to a monoid homomorphism π : Γ∗ → M such that π(a1 ⋅⋅ ⋅ am) = π(a1) ⋅⋅ ⋅ π(am). Hence, we have a free choice for letters to assign monoid elements, and for each choice we obtain a unique homomorphism. This explains the term free monoid for Γ∗, which was already more specifically described in [Theorem 6.1](#chapter06.xhtml_chapter06_5). If a homomorphism π : Γ∗ → M is surjective, then we say that π is a presentation of M; M is called finitely generated if there exists a presentation where Γ is finite. In other words, there is a finite subset of M such that every element of M can be written as a word over this finite subset. Given a presentation π : Γ∗ → M the word problem of M is the set WP(M) = { (u, υ) ∈ Γ∗ × Γ∗ | π(u) = π(υ) }. The word problem is decidable if there is an algorithm that decides membership in WP(M). In finitely generated monoids, the existence of such an algorithm is actually a property of M and not of π. Indeed, let ψ: Γ∗ → M be another homomorphism. For each a ∈ Γ, there is a word wa ∈ Γ∗ with π(wa) = ψ(a). Hereweuse the fact that π is surjective. To check whether ψ(u) = ψ(υ), we first compute (in linear time) words Wu, Wυ ∈ Γ∗ with π(Wu) = ψ(u) and π(Wυ) = ψ(υ). We then use the existing algorithm for π to test whether π(Wu) = π(Wυ).

## 8.4 Rewriting systems

The concept of a rewriting system is rather general. It consists of a set X and a binary relation ⇒ ⊆ X × X. We write x ⇒ y to express that (x, y) belongs to the relation ⇒. We then say that x can be rewritten in one step to y or that y can be derived in one step from x. Rewriting systems are particularly useful if they satisfy the Church–Rosser property, which is explained below. The property is named after Alonzo Church (1903–1995) and John Barkley Rosser, Sr. (1907–1989).

### 8.4.1 Termination and confluence

If ⇒ ⊆ X × X is a rewriting system, then we use the following notation:

(a)⇐⇒ symmetric closure,

![](images/250_1.jpg)![](images/250_2.jpg)![](images/250_3.jpg)

We also write ![](images/251_1.jpg) if y can be attained in at most (resp. exactly) k steps from x. Note that x ⇒ y ⇐ z implies ![](images/251_2.jpg) but neither ![](images/251_3.jpg) nor ![](images/251_4.jpg) in general. The rewriting system ⇒ is called

(a)strongly confluent if y ⇐x ⇒ z implies that there exists w with ![](images/251_5.jpg)

(b)confluent if ![](images/251_6.jpg) implies that there exists w with ![](images/251_7.jpg)

(c)Church–Rosser if ![](images/251_8.jpg) implies that there exists w with ![](images/251_9.jpg)

(d)locally confluent if y ⇐ x ⇒ z implies that there exists w such that ![](images/251_10.jpg)

(e)terminating or Noetherian if there does not exist an infinite chain

![](images/251_14.jpg)

(f)convergent or complete if it is locally confluent and terminating.

The significance of convergence is that it implies the Church–Rosser property.

Theorem 8.1. The following properties hold:

(a)Strong confluence implies confluence.

(b)Confluence is equivalent to the Church–Rosser property.

(c)Confluence implies local confluence, but the converse does not hold in general.

(d)Convergence implies confluence, that is, a locally confluent system, which is terminating, is confluent.

Proof: The fact that strong confluence implies confluence follows from the inductive argument shown in [Figure 8.1](#chapter08_1.xhtml_chapter08_1_19). The equivalence of confluence and the Church–Rosser property follows from [Figure 8.2](#chapter08_1.xhtml_chapter08_1_20). The statement that confluence implies local confluence is trivial. The converse does not hold, as we can see from the following situation:

![](images/251_15.jpg)

Now, by contradiction, we prove that a terminating and locally confluent system is confluent. Assume that there exists a z such that the system is not confluent starting

![](images/251_13.jpg)

Fig. 8.1. Strong confluence lattice.

![](images/252_1.jpg)

Fig. 8.2. Confluence implies Church–Rosser.

derivations at z. Then there exists ![](images/252_2.jpg) but there is no w with ![](images/252_3.jpg) Then necessarily k ≥ 1 and m ≥ 1\. Since the system is terminating, we may assume that the system is confluent for all z' for which ![](images/252_4.jpg) holds.

![](images/252_5.jpg)

Fig. 8.3. Termination and local confluence imply confluence.

Now consider [Figure 8.3](#chapter08_1.xhtml_chapter08_1_21). Due to local confluence, there exist w11 such that ![](images/252_6.jpg) ![](images/252_7.jpg) But by the choice of z the system is confluent on x1, y1 and w11. This leads us to w21, w12, and eventually to w. Contradiction.

□

For convergent systems, [Theorem 8.1](#chapter08_1.xhtml_chapter08_1_18) provides a procedure to check whether or not ![](images/252_8.jpg) holds: we perform repeated rewritings y = y0 ⇒ ⋅⋅ ⋅ ⇒ ym and z = z0 ⇒ ⋅⋅ ⋅ ⇒ zn until we arrive at elements ym and zn, respectively, for which no further rewritings are possible. Termination guarantees that ym and zn exist. Then we test if ym = zn in X. If this is the case then, of course, ![](images/252_11.jpg) What about the other direction? Certainly, ![](images/252_9.jpg) if and only if ![](images/252_10.jpg) On the other hand, ![](images/252_12.jpg) implies ym = w = zn. From [Theorem 8.1](#chapter08_1.xhtml_chapter08_1_18), the system has the Church–Rosser property. Therefore, if ym ≠ zn, then y and z are in different classes of the equivalence relation ![](images/252_13.jpg)

To make the procedure effective, we need more. We have to represent elements in X so that we can decide if y = z in X. Further, we also need to test whether, for a given x ∈ X, there exists y ∈ X with ![](images/252_14.jpg) and, if so, we must be able to compute such a y effectively.

### 8.4.2 Semi-Thue systems

A rewriting system over words is called a semi-Thue system, named after Thue. More generally, let T be any monoid. Each relation S ⊆ T × T defines a rewriting system ![](images/253_1.jpg) if we define ![](images/253_2.jpg) by the following condition:

![](images/253_11.jpg)

This means that we may replace in x a factor, which is the left component ℓ of a rule (ℓ, r) ∈ S, by the right component r and get y. Elements x ∈ T for which there is no y with ![](images/253_4.jpg) are called irreducible or irreducible normal forms. Theset of all irreducible normal forms with respect to S is denoted by IRR(S). The relation ![](images/253_5.jpg) is a congruence. This means that we may multiply equivalence classes by multiplying representatives and taking the equivalence class of the product

![](images/253_12.jpg)

The congruence classes form a monoid that is denoted differently depending on the context. We write this as ![](images/253_7.jpg) or just T/S. Hence, we may interpret S as the set of defining relations for the quotient monoid T/S. We call S convergent if ![](images/253_8.jpg) has this property. For a convergent system S, the canonical homomorphism T → T/S induces a bijection between IRR(S) and the quotient monoid T/S. The elements of T/S are therefore represented by irreducible normal forms. If T = Γ∗ is a free monoid, then we call S a semi-Thue system. Instead of (ℓ, r) ∈ S, we also write ℓ → r ∈ S for a semi-Thue system.

Example 8.2 (Multiplication table). Let M be any monoid and Γ = M \ {1}. We may view Γ as a possibly infinite alphabet. The system

![](images/253_9.jpg)

reflects the multiplication table of M. The system is trivially convergent, and the set of irreducible normal forms is just M ⊆ Γ∗.

◊

Example 8.3. Let Γ = {a1, . . . , an} an ordered alphabet with ai < aj for i < j. Then S = { ajai → aiaj | i < j } is convergent. The quotient monoid Γ∗/S is isomorphic to ℕn and the set of irreducible ∗∗normal forms is equal to ![](images/253_10.jpg)

◊

Example 8.4. Let Γ = {a, b, c} and S = {ba → ab, ca → ac, cb → bc, abc → 1}. Then Γ∗/S is isomorphic to ℤ×ℤ, but S is not convergent.

◊In the last two examples, the termination of S is obvious because the right components are length-lexicographically smaller than the left components. But how do we know that the first system is (locally) confluent and the second one not? It turns out that we find the answer via “critical pairs.” A critical pair is a pair (u, υ) of words for which rules (ℓ1, r1), (ℓ2, r2) ∈ S and words p, q exist such that one of the following conditions holds (see [Figure 8.4](#chapter08_1.xhtml_chapter08_1_25)):

(a)Overlap critical pair: ℓ1q = pℓ2, |p| < |ℓ1|, u = r1q, υ = pr2, and

![](images/254_1.jpg)

(b)Factor critical pair: pℓ1q = ℓ2, u = pr1q, υ = r2 and

![](images/254_2.jpg)![](images/254_3.jpg)

Fig. 8.4. Sources of critical pairs.

A critical pair arises, therefore, from the presence of two left components that overlap. A semi-Thue system S is locally confluent if and only if, for each critical pair (u, υ), there exists w with ![](images/254_4.jpg) If, in particular, two rules with non-overlapping left components are applicable in a word, then it is clear that both resulting words can be transferred with one rewriting step to the same word. If S is finite, then there are only finitely many critical pairs. This leads to the following decidability result.

Theorem 8.5. It is decidable whether a finite and terminating semi-Thue system S ⊆ Γ∗ × Γ∗ is confluent and, hence, whether it is convergent.

Proof: Since S is finite, there are only finitely many critical pairs. For each such pair (u, υ), we compute ![](images/254_5.jpg) ∈ IRR(S) and ![](images/254_6.jpg) ∈ IRR(S). This is possible because S is finite and terminating. If S is confluent, then there exists some w ∈ Γ∗ with ![](images/254_7.jpg) ![](images/254_8.jpg) Now, û and v̂ are irreducible w.r.t. S, which gives that w = û = v̂ as words. Thus, if û ≠ v̂, then S is not confluent. On the other hand, the equality û = v̂ for all critical pairs is sufficient to guarantee local confluence. Since S is terminating, local confluence implies confluence, hence convergence.

□

Since local confluence and termination imply confluence, [Theorem 8.5](#chapter08_1.xhtml_chapter08_1_26) reduces the problem of deciding convergence (= confluence + termination) of a finite semi-Thuesystem to the problem of deciding termination. The latter problem is, however, undecidable, because the halting problem for Turing machines can be reduced to the problem of deciding termination of some finite semi-Thue system. The reduction is fairly straightforward and left to the interested reader.

A monoid M is finitely presented if it is isomorphic to a quotient monoid Γ∗/S, where S and Γ are finite. The existence of a finite system S with Γ∗/S = M does not depend on the choice of the surjective homomorphism π : Γ∗ → M, but it only depends on M. To see this, we consider a finite S and another surjective homomorphism ψ: Γ∗ → M which induces Γ∗/S' = M, and for which Γ' is finite. We want to show that in S' there is a finite subset S' with Γ∗/S'' = Γ∗/S. First, we have a homomorphism φ: Γ∗ → Γ∗ such that ψ(φ(u)) = π(u) for all u ∈ Γ∗. This follows from the universal property of free monoids (see [Theorem 6.1](#chapter06.xhtml_chapter06_5)). For all a' ∈ Γ, there is a word ua ∈ Γ∗ with ![](images/255_1.jpg) because ψ(a) is equal to some π(ua). Furthermore, for all (ℓ, r) ∈ S we have ![](images/255_2.jpg) since Γ∗/S' = M. But then there already exists a finite subset S'' ⊆ S' with ![](images/255_3.jpg) for all a' ∈ Γ, and we obtain ![](images/255_4.jpg) for all (ℓ, r) ∈ S because Γ and S are finite. We obtain a sequence of homomorphisms:

![](images/255_5.jpg)

where arrows are labeled by the respective homomorphisms that induce these maps. The composition of the homomorphisms gives the bijection induced by π. Hence, ![](images/255_6.jpg) is injective. Since ![](images/255_7.jpg) for all a' ∈ Γ, this map is also surjective. This shows Γ∗/S'' = Γ∗/S, and thus the assertion.

The next example leads to the concept of a free group.

Example 8.6 (Free groups). Let ![](images/255_8.jpg) where ![](images/255_9.jpg) is a disjoint copy of Σ. We extend the map a ↦ a to an involution on Γ by ![](images/255_10.jpg) for all a ∈ Γ and put ![](images/255_11.jpg) Consider now the strongly confluent and convergent system

![](images/255_12.jpg)

The system defines the free group with basis Σ by

![](images/255_13.jpg)

The cardinality of Σ is called the rank of F (Σ). If G is any group, and φ(a) ∈ G is defined for all a ∈ Σ, then we put ![](images/255_14.jpg) and obtain a homomorphism φ: Γ∗ → G with ![](images/255_15.jpg) for all a ∈ Γ. This means that we may extend each map φ: Σ → G uniquely to a group homomorphism φ: F (Σ) = Γ∗/S → G, that is, F (Σ) is “free” on Σ. We also recognize that all words from Σ∗ are irreducible and, hence, we obtain an embedding Σ∗ ⊆ F (Σ), which, a priori, is not initially apparent. For a free group with generators a1, . . . , an, we also write F (a1, . . . , an) instead of F ({a1, . . . , an}). Free groups have been investigated by mathematicians since the end of the 19th century. A systematic study began with papers by Walther Franz Anton Ritter von Dyck[9](#Notes.xhtml_Notes_9)(1856–1934) [[36](#Bibliography.xhtml_Bibliography_36), [37](#Bibliography.xhtml_Bibliography_37)]. Dyck’s name also appears in formal language theory. The term Dyck language was coined, to the best of our knowledge, in [[17](#Bibliography.xhtml_Bibliography_18)]. A Dyck language is the set of all words that have a correct bracketing over a given alphabet of “brackets.” The set of “brackets” forms an alphabet with involution and there are two types of Dyck languages. In the asymmetric type, we distinguish between opening and closing brackets. Thus, if there are (asymmetric) brackets (, ), [, ], then ( [ ][ ] ) ( ) is a well-formed Dyck word, but ( [ ] ] [ ) ( ) is not. In the symmetric version, there is no distinction between “opening” and “closing” brackets; and we recognize the word problem of a free group. Indeed, if the symmetric brackets are given by, for example, ![](images/256_2.jpg) then ![](images/256_1.jpg) is a Dyck word if and only if w is the neutral element in the free group F (a, b).

◊

As a historical side remark: Dyck did not use the presentation chosen here. He presented the free group F (a, b) on two generators in a more sophisticated way by using three letters a, b, c without explicit inverse letters. His rewriting system was

![](images/256_3.jpg)

For Σ = {a, b}, the inclusion {a, b} ⊆ {a, b, c} induces a canonical isomorphism and an alternative presentation of the free group. There are two equivalent views

![](images/256_4.jpg)

Just as the standard presentation for a free group in [Example 8.6](#chapter08_1.xhtml_chapter08_1_28), the system SDyck is also strongly confluent. In addition, SDyck is fully symmetric and it provides the minimal number of monoid generators.

In classical group theory, a group G is called finitely presented if there is a finitely generated free group F (Σ) and finitely many defining elements r1, . . . , rm such that G is isomorphic to F(Σ)/{r1 = 1, . . . , rm = 1}. From the definition, it is clear that a group G is finitely presented if and only if G is finitely presented as a monoid.

Example 8.7 (Free Products). Let I be an index set and Mi be monoids with Γi = Mi \ {1} for i ∈ I. Then each Mi has a convergent presentation given by its multiplication table 𝓜i; see [Example 8.2](#chapter08_1.xhtml_chapter08_1_23). We may assume without restriction that the Γi are pairwise disjoint; and we let Γ = ∪i∈IΓi be their union. It follows that the union 𝓜 = ∪i∈I𝓜i is terminating and locally confluent, because it is confluent on all critical pairs. Thus, Mis convergent. The irreducible normal forms are the words w = a1 ⋅⋅ ⋅ an where n ≥ 0, aj ∈ Γ for 1 ≤ j ≤ n, and for all i ∈ I and 1 ≤ j < n, we have that aj ∈ Γi

implies aj+1 ∉ Γi. The resulting monoid

![](images/257_6.jpg)

is called the free product over the Mi. It has the universal property: if (hi : M i → N)i∈I is a family of homomorphisms to some monoid N, then a unique homomorphism h : ∗i∈IMi → N exists such that each hi is the restriction of h to Mi; and, moreover, each homomorphism h : ∗i∈I Mi → N is of this form. If I = {1, 2}, then we also write M1 ∗ M 2 for its free product.

◊

Example 8.8. Let p, q ∈ ℤ with 0 < p ≤ |q|. The Baumslag–Solitar group BS(p, q) is given by two group generators a, t, and a single defining relation tap t−1 = aq. As monoid generators, we use the alphabet with involution Γ = {a, ā, t, t̄ } where c̄̄ = c. Moreover, we identify c̄m with c−m for m ∈ ℤ. We present BS(p, q) using the following convergent semi-Thue system:

![](images/257_4.jpg)

Local confluence of S is straightforward. Termination follows fromthe fact that letters t, t̄ move to the left by jumps over b blocks where b ∈ {a, ā}. Let us take a closer look. If we apply, say, a rule apm+ut̄ → aut̄aqm, then left of t̄, we either decrease the number of a̅’s (note that p can be negative) or the number of a̅’s is not changed, but the number of a’s is decreased. A more careful analysis for termination is given later in the more general context of HNN extensions in [Theorem 8.19](#chapter08_2.xhtml_chapter08_2_25).

The irreducible normal forms correspond to sequences

![](images/257_5.jpg)

where the following conditions are satisfied:

–k ≥ 0 and θi ∈ {t, t̄} for 1 ≤ i ≤ k

–mk ∈ ℤ.

–If mi = 0, then θi = θi+1 for 1 < i < k.

–Ifθi = t̄, then 0 ≤ mi−1 < p for 1 < i ≤ k.

–Ifθi = t, then 0 ≤ mi−1 < |q| for 1 < i ≤ k.

The computation of normal forms yields a polynomial time algorithm for the word problem if each a block is represented as am where m ∈ ℤand m is written in binary.

◊

The family BS (p, q) (see [Example 8.8](#chapter08_1.xhtml_chapter08_1_36)) of one-relator groups was introduced by Gilbert Baumslag (1933–2014) and Donald Solitar (1932–2008). This rich family provides standard examples for various phenomena in group theory: for instance, the group BS(2, 3) is not Hopfian, that is, there is a surjective homomorphism of BS(2, 3) onto itself, which is not injective. Such a homomorphism is given by t ↦ t and a ↦ a2; see [Exercise 8.10](#chapter08_4.xhtml_chapter08_4_30).

Example 8.9. In [[105](#Bibliography.xhtml_Bibliography_106)], Stephan Waack (born 1954) considered an extension of the Baumslag–Solitar group BS(1, 2) with group generators a, s, t and defining relations sas−1 = tat−1 = a2. This defines the Waack group W. It is a special case of a generalized Baumslag–Solitar group [[42](#Bibliography.xhtml_Bibliography_42)].

The group W has another presentation with generators a, r, t and relations tat−1 = a2 and rar−1 = a. To see this, let r = s−1t. Then a, r, t generate W as well; and it holds

![](images/258_4.jpg)

Thus, the equation rar−1 = a is valid in W. Conversely we have s = tr−1. Hence, from rar−1 = a we can deduce

![](images/258_5.jpg)

This shows the first claim by so-called Tietze transformations.

Second, let us show that we can present W by a convergent semi-Thue system, too. We start with the set of monoid generators Γ = {a, a, t, t, r, r}. As above, we let ![](images/258_7.jpg) for all c ∈ Γ. The rewriting system S has the following rules for all c ∈ Γ and b ∈ {a, a}:

![](images/258_6.jpg)

As for Baumslag–Solitar groups, the system S leads to a polynomial time algorithm to solve the word problem in W.

◊

Actually, polynomial time is not the smallest complexity class for the word problem in Baumslag–Solitar groups BS(p, q) or for the Waack group W. The word problem can be solved in the complexity class “logspace.” More precisely, one can show that the word problems in the groups BS (p, q) (for p > 1) and W have the same complexity as the word problem in free groups up to NC1 reductions [[106](#Bibliography.xhtml_Bibliography_107), [109](#Bibliography.xhtml_Bibliography_110)]. The result in [[109](#Bibliography.xhtml_Bibliography_110)] is actually stronger: the conjugacy problem in generalized Baumslag–Solitar groups is solvable in “logspace.”

## 8.5 Solving the word problem in finitely presented monoids

There is no universal algorithm for solving the word problem. Different methods apply to different classes of groups. As expected, the main tool in this chapter is related to confluent rewriting.

Proposition 8.10. Let M be a finitely presented monoid that has a presentation as M = Γ∗/S by a finite convergent semi-Thue system S ⊆ Γ∗ × Γ∗. Then M has a decidable word problem.

Proof: Recall that S is convergent if and only if it is terminating and confluent. Since S is finite and terminating we can, on input u, υ ∈ Γ∗, effectively compute irreducible normal forms ![](images/259_2.jpg) ∈ IRR(S) and ![](images/259_3.jpg) ∈ IRR(S). Since S is confluent, we have ![](images/259_1.jpg) (and hence u = υ in M) if and only if û and v̂ are identical as words in Γ∗.

It is not necessary that a finite rewriting system be convergent everywhere to decide the word problemin a group G. It is sufficient if the system is terminating (everywhere) and confluent on all words which represent the identity in G. This idea was already present in Dehn’s work; his method is nowadays known as Dehn’s algorithm. This led to the theory of small cancellation groups [[69](#Bibliography.xhtml_Bibliography_69)], and later to the notion of hyperbolic group due to Mikhail Leonidovich Gromov (born 1943) [[47](#Bibliography.xhtml_Bibliography_47)].

In the early 1980s, it was asked whether, for every finitely presented monoid M with a decidable word problem, there exists some finite convergent semi-Thue system S ⊆ Γ∗ × Γ∗ such that M is isomorphic to Γ∗/S. At that time, no method was known to show that a finitely presented monoid M with a decidable word problem does not have a finite convergent presentation. Later, Craig Cecil Squier (1946–1992) found a homological finiteness condition that provides such a method [[98](#Bibliography.xhtml_Bibliography_99)].

Let us present another classical tool to attack word problems. It shows decidability for a rather large class of groups. The proof of [Proposition 8.11](#chapter08_1.xhtml_chapter08_1_47) is an exercise, but it does not give any practical algorithm.

Proposition 8.11. Let M be a residually finite and finitely presented monoid. Then M has a decidable word problem.

Proof: See [Exercise 8.2](#chapter08_4.xhtml_chapter08_4_21).

□

We have seen above that the special linear groups SL(n, ℤ) are residually finite, and below, in [Corollary 8.39](#chapter08_4.xhtml_chapter08_4_19), we see that, as a consequence, free groups are residually finite, too. However, there is also a nice direct proof for this fact.

Proposition 8.12. Free groups are residually finite.

Proof: Let F = F (Σ) be a free group with the basis Σ ⊆ F and ![](images/259_4.jpg) as in [Example 8.6](#chapter08_1.xhtml_chapter08_1_28) (with a = a−1). Let n ≥ 1 and w = a1 ⋅⋅ ⋅ an ∈ Γ∗ with ai ∈ Γ and ![](images/259_5.jpg) Thus, we have w ≠ 1 in F; and the set of prefixes P = { a1 ⋅⋅ ⋅ ai | 0 ≤ i ≤ n } is a finite set with at least two elements: the empty word and the nonempty word w. For each a ∈ Σ, we define a partial injection φa which maps a1 ⋅⋅ ⋅ ai to a1 ⋅⋅ ⋅ aia in case a1 ⋅⋅ ⋅ aia ∈ P. If φa is defined for S ⊆ P, then S is in bijection with φa(S). Hence, P \ S is in bijection with P \ φa(S), too; and we are able to extend φa to a bijection ψa, which is defined everywhere on P. As a consequence, the mapping a ↦ ψa defines a homomorphism h from F (Σ) to the finite permutation group of the set P. We have h(w) ≠ id P since h(w) maps the empty word in P to the nonempty word w ∈ P.

□

Example 8.13. The Waack group W from [Example 8.9](#chapter08_1.xhtml_chapter08_1_38) is finitely presented and has a decidable word problem, but it is not residually finite. Indeed, consider the presentation with monoid generators Γ = {a, a̅, t, t̄, r, r̄} and the convergent system S as in [Example 8.9](#chapter08_1.xhtml_chapter08_1_38). The words tat and rt̄atr̄ are both irreducible w.r.t. S, but different. Now let φ: W → N be any homomorphism to a finite monoid. We may assume that φ is surjective and N is a finite group. Let 〈a〉 be the cyclic subgroup of N, which is generated by φ(a). Let us identify g ∈ W with φ(g) ∈ N using abuse of language. Then the conjugation tat−1 = a2 is an automorphism of 〈a〉; and every element in 〈a〉 is the square of some other element in 〈a〉. In particular, a = a2k in 〈a〉 for some k ∈ ℕ. Hence, in N we have

![](images/260_1.jpg)

Thus, the nontrivial element t−1atrt−1a−1tr−1 in W is mapped to 1 for every homomorphism to a finite monoid. Hence, W is not residually finite.

◊

## 8.6 Free partially commutative monoids and groups

In computer science, partial commutation is a natural concept to investigate concurrent systems. This goes back to the work of Robert Marion Keller (born 1944) [[53](#Bibliography.xhtml_Bibliography_53)]. The idea is that concurrency or independence of events a and b is described by commutativity ab = ba. In this connection, Antoni Mazurkiewicz (born 1934) coined the notion of trace monoid [[72](#Bibliography.xhtml_Bibliography_72)]. He considered a finite alphabet Σ and a relation I ⊆ Σ × Σ, which is assumed to be irreflexive and symmetric. The relation I is called an independence relation since it reflects the abstract behavior of events which occur independently of each other; and therefore (a, b) ∈ I should imply that ab and ba have the same effect. It is also the semantic explanation why I is irreflexive: an action a is not independent of itself. The resulting trace monoid is

![](images/260_2.jpg)

Frequently, we also call M (Σ, I) the free partially commutative monoid over (Σ, I). The latter term also suits better to express the algebraic structure of M (Σ, I).

Example 8.14. Let (Σ, I) be a finite graph.

(a)If I = 0, then M(Σ, I) = Σ∗.

(b)If (Σ, I) is complete, then M(Σ, I) =ℕΣ. In general, M(Σ, I) is between Σ∗ and ℕΣ; and, counting how often a letter appears in a word, defines canonical homomorphisms:

![](images/260_3.jpg)

(c)If (Σ, I) is a disjoint union (Σ1, I1)∪ (Σ2, I2), then M(Σ, I) = M(Σ1, I1)∗ M(Σ2, I2) is the free product as defined in [Example 8.7](#chapter08_1.xhtml_chapter08_1_34).

(d)The complex product of (Σ1, I1) and (Σ2, I2) is defined as the graph (Σ, I), where Σ is the disjoint union of Σ1 and Σ2, and the relation I is given by I1, I2 and all edges between Σ1 and Σ2, that is

![](images/261_11.jpg)

The complex product yields the direct product M (Σ, I) = M (Σ1, I1)× M (Σ2, I2).

(e)If Σ = {a, b, c} and if in M(Σ, I) the relations ac = ca, ab ≠ ba, and bc ≠ cb hold, then M(Σ, I) = (ℕ×ℕ) ∗ℕ.

◊

We extend the relation I to a relation I ⊆ Σ∗ × Σ∗ by setting (u, υ) ∈ I if all letters in u are in the relation I to all letters in υ. Put any linear order ≤ on Σ and consider the semi-Thue system S in ([8.3](#chapter08_2.xhtml_chapter08_2_1)), which is infinite as soon as I ≠ 0\. In the exercises, we discuss the existence of finite convergent systems which represent M (Σ, I):

![](images/261_10.jpg)

The system S terminates because the rules are length preserving, and every rewriting step reduces words lexicographically. A direct consideration of the critical pairs provides local confluence. For instance, we have ![](images/261_3.jpg) and ![](images/261_4.jpg) for a, b, c ∈ Σ, a < b < c, (c, bu) ∈ I, (a, bcuυ) ∈ I.

In particular, we can decide the word problem for M (Σ, I) by determining irreducible normal forms. The set IRR(S) describes the set of the lexicographic normal forms. Since all defining relations are length preserving any lexicographic normal form is in length-lexicographic normal form, too.

Analogously to the monoid case, free partially commutative groups are defined as follows:

![](images/261_9.jpg)

Free partially commutative groups have long been studied in mathematics and play a prominent role. Various names have been introduced for them. They are also called graph groups because the defining relations are given by an undirected graph, or right-angled Artin groups (or RAAGs for short). This naming is explained by the fact that, in the plane, reflections at orthogonal straight lines commute. Graph groups can be embedded into right-angled Coxeter groups. The names refer to Emil Artin (1898–1962) and Harold Coxeter (1907–2003). Coxeter groups also have a direct geometric interpretation and several textbooks are devoted to their rich and beautiful theory [[7](#Bibliography.xhtml_Bibliography_8), [20](#Bibliography.xhtml_Bibliography_21)].

Free partially commutative monoids can be embedded into free partially commutative groups, exactly as free monoids are submonoids of free groups. To see this, consider ![](images/261_6.jpg) where ![](images/261_7.jpg) is a disjoint copy of Σ. We extend the map a ↦ a̅ to an involution on Γ by ![](images/261_8.jpg) for all a ∈ Γ. Then we extend the relation I to Γ by adding the pairs (a, b̄), (a̅, b), (a̅, b) for (a, b) ∈ I. Moreover, we order Σ linearly by ≤ and extend this linear order to Γ in a special unique way. We require that for all a, b ∈ Σ with a < b, we have a < a̅ < b in Γ. With this trick, the following semi-Thue system is convergent:

![](images/262_4.jpg)

We obtain G(Σ, I) = Γ∗/SG. Note that the system S in ([8.3](#chapter08_2.xhtml_chapter08_2_1)) is a subset of SG such that IRR(S) ⊆ IRR(SG). This is enough to imply an inclusion of monoids

![](images/262_5.jpg)

As M (Σ, I) is a submonoid of some group, it is cancellative. This means pυq = pwq implies υ = w for all elements p, q, υ, w. With the help of SG, we may solve the word problem for the group G(Σ, I). Due to the rules aa → 1 the set IRR(SG) consists of the length-lexicographic normal forms. In a suitable implementation, computing irreducible normal forms can be done in linear time [[112](#Bibliography.xhtml_Bibliography_113)].

There is another way to see that free partially commutative monoids embed into groups by embedding M(Σ, I) first into a direct product of free monoids. This is enough because a direct product of free monoids canonically embeds in a direct product of free groups. Since the embedding into a direct product of free monoids is a key property in the theory of free partially commutative monoids, we work this out in detail; and we actually prove a more general result.

The specification of M (Σ, I) has been given by an undirected graph (Σ, I) without loops and multiple edges; but we may also consider its complement graph (Σ, D). Thus, a, b ∈ Σ are connected by an edge in (Σ, D) if a ≠ b and (a, b) ∉ I. We call (Σ, D) a dependence alphabet. A morphism f : (Σ, D) → (Σ' , D) is given by a mapping f : Σ → Σ' which maps edges (a, b) ∈ D to edges (f(a), f(b)) ∈ D. We say that f is an epimorphism if it is surjective on vertices and edges. Given a morphism f : (Σ, D) → (Σ' , D), we can define a homomorphism f ∗ : M(Σ' , I) → M(Σ, I) in the other direction by

![](images/262_3.jpg)

Note that f ∗(a) is well defined since (Σ' , D) has no self-loops and edges must be mapped to edges. (In a slightly more general setting, we could allow self-loops and then we just decide on some ordering in the product to define f ∗(a).) The important point is that f ∗ is well defined as a homomorphism. Indeed, let (a' , b) ∈ I, then we have a' ≠ b' and there is no edge between a' and b' in the graph (Σ' , D) (whether or not there are self-loops). Hence, there cannot be any edge between the sets f −1(a) and f −1(b) in (Σ, D). This means (a' , b) ∈ I' implies f ∗(a)f ∗(b) = f ∗(b)f ∗(a). Hence, f ∗ : M(Σ' , I) → M(Σ, I) is well defined.

Proposition 8.15. Let f : (Σ, D) → (Σ' , D) be a morphism between dependence alphabets. Then f is an epimorphism if and only if f ∗ : M(Σ' , I') → M(Σ, I) is injective.

Proof: If f is not an epimorphism, then either a vertex a' or an edge (a' , b') ∈ D' is not in the range of f . In the former case we have f ∗(a') = 1 and in the latter case we have f ∗(a'b') = f ∗(b'a') but a'b' ≠ ba' in M(Σ' , I). For the other direction, it is enough to recover w' ∈ M(Σ' , I') from its image f ∗(w') ∈ M(Σ, I). This is clear for |w'| ≤ 1\. Hence we may assume that |w'| > 1\. To handle this case endow Σ' and Σ with linear orderings such that a' < b' in Σ' implies a < b in Σ for all a ∈ f −1(a') and b ∈ f −1(b'). Next, compute the lexicographical normal form ŵ for f ∗(w'). In order to check that a' ∈ Σ' is the first letter in the lexicographical normal form for w', we consider all b' ∈ Σ' with a' ≠ b'. If (a' , b) ∈ D', then there are (a, b) ∈ D with f(a) = a' and f(b) = b', because f is surjective on edges. In this case, the first a must be before all b in ŵ. If (a' , b') ∈ I', then f −1(a') and f −1(b') are not empty because f is surjective on vertices. In this case all letters of f −1(a') appear in ŵ before any letter of f −1(b') appears in ŵ. This is due to the choice of the linear order on Σ. Once a' is detected, we are done by induction since M (Σ, I) is cancellative: either by the inclusion ([8.5](#chapter08_2.xhtml_chapter08_2_5)) or by a simple direct argument using the defining relations ab = ba for (a, b) ∈ I.

□

Corollary 8.16. Let M (Σ, I) be a trace monoid andD the collection of subsets {a, b} ⊆ Σ such that (a, b) ∉ I (including the case a = b). For each {a, b} ∈ 𝒟 let πab be the natural projection of M (Σ, I) onto the free monoid {a, b}∗, which is defined by erasing all letters different from a, b. Then, we obtain a canonical embedding

![](images/263_1.jpg)

In particular, every trace monoid is a submonoid of a finite direct product of finitely generated free monoids; and therefore its word problem is solvable in linear time.

The analog of [Proposition 8.15](#chapter08_2.xhtml_chapter08_2_7) and [Corollary 8.16](#chapter08_2.xhtml_chapter08_2_9) fails for free partially commutative groups. For example, consider Σ = {a, b, c} with the linear order a < b < c, where a and c are independent, but (a, b) ∉ I and (b, c) ∉ I. For group elements x, y, let [x, y] = xyx−1y−1 denote the commutator of x and y. It turns out that the lexicographical normal form of [[a, b], [c, b]] is the word

![](images/263_4.jpg)

In particular, [[a, b], [c, b]] ≠ 1 in G(Σ, I). There are two projections πab and πbc of G(Σ, I) onto F(a, b) and F(b, c), respectively. However, πab([c, b]) = 1 and πbc([a, b]) = 1\. Hence, π[[a, b], [c, b]] = 1 in the direct product F(a, b) × F(b, c). Actually, the graph group F(a, b, c)/{ac = ca} is no subgroup of any finite direct product of free groups [[35](#Bibliography.xhtml_Bibliography_35)]. The subgroup structure of RAAGs is rich and complicated. It has been studied from various angles which go far beyond the scope of this textbook. For more advanced topics, see, for example [[34](#Bibliography.xhtml_Bibliography_34), [111](#Bibliography.xhtml_Bibliography_112)].

Based on (Σ, I) the right-angled Coxeter group C (Σ, I) is defined as follows:

![](images/263_5.jpg)

These Coxeter groups are therefore quotients of the respective graph groups. Since nontrivial Coxeter groups have torsion, they cannot appear as subgroups of graph groups.However, every graph group is a subgroup of some right-angled Coxeter group, see [Exercise 8.4](#chapter08_4.xhtml_chapter08_4_24).

## 8.7 Semidirect products

The construction of semidirect products follows the scheme we have seen in the construction of free products in [Example 8.7](#chapter08_1.xhtml_chapter08_1_34). We let M and K be monoids with associated (potentially infinite) alphabets ΣM = M \ {1} and ΣK = K \ {1}. We assume that these alphabets are disjoint, and the monoids share the neutral element 1\. The notion of semidirect product refers to M, K and a monoid homomorphism α : K → Aut(M), where Aut(M) is the automorphism group of the monoid M. For instance, K = M = ℤ (with common neutral element 0) and α(x)(m) = (−1)x ⋅ m. In this section, we write x m instead of α(x)(m) for x ∈ K and m ∈ M. In this notation, we obtain

![](images/264_5.jpg)

The idea now is to realize x m as an inner automorphism xmx−1 = xm. For monoids there is no x−1, in general. Hence, we replace the equation xmx−1 = x m by xm = x mx, which is equivalent in the group case and makes sense in all monoids. As for free products, let Σ = ΣM ∪ ΣK and S = SM ∪ SK. We extend S to a system Sα by

![](images/264_6.jpg)

The system Sα terminates because it reduces length-lexicographically if we choose the letters from ΣM smaller than those from ΣK. Local confluence follows from the above computation rules. Hence, the system Sα is convergent. The normal form computation pushes the elements of K to the right. Then we may interpret IRR(Sα) as the set of pairs in M × K.

The semidirect product M ⋊α K is defined by the set M × K together with the multiplication

![](images/264_7.jpg)

By construction M ⋊α K = Σ∗/Sα is the quotient monoid of the free product M ∗ K with the (additional) defining relations xm = x mx.

Moreover, M and K are embedded in M ⋊α K via M ≅ M ×{1} and K ≅ {1}×K which means that we may consider M and K as submonoids of M ⋊α K. If M and K are groups, then M is a normal subgroup; the conjugation action (1, x)(m, 1)(1, x−1) with x ∈ K, m ∈ M, results in (xm, 1) = (α(x)(m), 1) and, therefore, it becomes an automorphism α(x) ∈ Aut(M).

As an example, we now consider the case K = M = ℤ. There are exactly two semidirect products, the direct product and the non-Abelian group ℤ ⋊ ℤ with the multiplication

![](images/264_8.jpg)

For the case K = ℤ/2ℤ and M = ℤ, the situation is quite similar. We also get only one non-Abelian semidirect product ℤ ⋊ (ℤ/2ℤ) with the multiplication as above, but in the second component the computation is modulo 2.

Example 8.17. The following are typical instances of semidirect products:

–The non-Abelian semidirect product ℤ⋊(ℤ/2ℤ) is isomorphic to the free product (ℤ/2ℤ) ∗ (ℤ/2ℤ). Indeed, let a = (1, 1) ∈ ℤ⋊ (ℤ/2ℤ) and b = (0, 1) ∈ ℤ⋊ (ℤ/2ℤ), then a2 = b2 = (0, 0). Moreover, ab = (1, 0) and, therefore, we have a surjective homomorphism from (ℤ/2ℤ) ∗ (ℤ/2ℤ) = {a, b}∗/{a2 = b2 = 1} onto G. The inverse homomorphism is given by (m, x) ↦ (ab)mbx. It is a homomorphism since (ab)m = (ba)−m in (ℤ/2ℤ) ∗ (ℤ/2ℤ) for m ∈ ℤ.

–The Baumslag–Solitar group BS(1, −1) was defined as the semidirect product ℤ⋊ℤ.

–ThegroupBS(1, 2) corresponds to the semidirect product ![](images/265_2.jpg) Here ![](images/265_3.jpg) is the additive group of the fractions ![](images/265_1.jpg) with p, k ∈ ℤ. The multiplication in ![](images/265_4.jpg) is defined by (r, m) ⋅ (s, n) = (r + 2ms, m + n).

The proof that BS(1, 2) and ![](images/265_5.jpg) are isomorphic is along the same lines as above. For BS(1, 2), we map a to (1, 0) and t to (0, 1) in ![](images/265_6.jpg) The defining relation tat−1 = a2 holds in ![](images/265_7.jpg) the elements (1, 0) and (0, 1) generate the semidirect product; and, finally, the normal form description in Equation ([8.1](#chapter08_1.xhtml_chapter08_1_37)) shows that a ↦ (1, 0), t ↦ (0, 1) induces an injection.

◊

## 8.8 Amalgamated products and HNN extensions

We explain the construction of amalgamated products and HNN extensions for groups, only. We start with the amalgamated product and consider three groups U, G, and H together with two injective homomorphisms φ: U → G and ψ: U → H. For example, U, G and H just can be the finite cyclic groups ℤ/2ℤ, Z /4ℤ and Z /6ℤ, respectively.

We now define the amalgamated product G ∗U H as the quotient group of the free product G ∗ H by

![](images/265_8.jpg)

We recognize the following universal property: the homomorphisms from G ∗U H to a group (or a monoid) K correspond exactly to the pairs (g, h) of homomorphisms g : G → K and h : H → K which fulfill the condition

g(φ(u)) = h(ψ(u)) for all u ∈ U

In [Section 8.12](#chapter08_4.xhtml_chapter08_4_11),we consider the special linear group SL(2, ℤ) of 2 ×2 matriceswith coefficients in ℤ and determinant 1\. If we choose ![](images/265_9.jpg) and ![](images/265_10.jpg) then S hasorder 4 and R has order 6\. In fact, we have ![](images/266_1.jpg) and ![](images/266_2.jpg) In particular, we obtain a pair of homomorphisms ℤ/4ℤ→ SL(2, ℤ) with 1 mod 4 ↦ S and ℤ/6ℤ → SL(2, ℤ) with 1 mod 6 ↦ R. Due to the universal property of amalgamated products, there is a homomorphism of (ℤ/4ℤ) ∗ℤ/2ℤ (ℤ/6ℤ) in SL(2, ℤ) because of the relation S2 = R3. [Theorem 8.38](#chapter08_4.xhtml_chapter08_4_17) shows that this homomorphism in fact is an isomorphism.

Let us return to the general situation G ∗ H/{ φ(u) = ψ(u) | u ∈ U }. It is a priori unclear whether the natural maps G → G ∗U H and H → G ∗U H are injective. In principle, G ∗U H could be the trivial group. However, this is not the case; and to prove thiswe introduce a convergent semi-Thue system S ⊆ Σ∗ ×Σ∗ which represents G ∗U H. Here S and Σ will be infinite if G ∪ H is infinite.

For this, we just may consider the situation that φ: U → G and ψ: U → H are inclusions and that G ∩ H = U. This simplifies the notation.

![](images/266_3.jpg)

We now divide G and H into cosets of U. For this, we choose a complete system A ⊆ G of (left) coset representatives of U in G with 1 ∈ A and a complete system B ⊆ H of (left) coset representatives of U in H with 1 ∈ B. As alphabets we choose ΣA = (U ∪ A) \ {1} and ΣB = (U ∪ B) \ {1} and Σ = ΣA ∪ ΣB. Each element g ∈ G ∪ H has a unique representation as a word cu ∈ Σ∗ with c ∈ A ∪ B and u ∈ U. (For the neutral element 1 ∈ G ∪ H, we have c = u = 1 ∈ A ∩ B ∩ U, and cu = 1 is the empty word.) More precisely, there is a representation of length 0 (g = 1), length 1 (1 ≠ g ∈ U ∪ A ∪ B) or length 2 (otherwise).

We denote elements in G or H with square brackets. The semi-Thue system S consists of the following rules:![](images/266_5.jpg)

Theorem 8.18. The semi-Thue system S of ([8.7](#chapter08_2.xhtml_chapter08_2_18)) is convergent and Σ∗/S is canonically isomorphic to the amalgamated free product G ∗U H.

Proof: First, we convince ourselves that Σ∗/S and G ∗U H are isomorphic. The isomorphism is induced by the natural inclusions ΣA → G and ΣB → H. It is therefore canonical, and this justifies the notation Σ∗/S = G ∗U H. Because ΣA ∩ ΣB ⊆ U, the natural homomorphism Σ∗ → G ∗U H is well defined since in the amalgamated product all u ∈ G ∩ U are identified with u ∈ H ∩ U. The group G ∗U H is generated by the elements of G and H, and these generators can already be represented by words from Σ∗ with length at most two. So the map Σ∗ → G ∗U H is surjective. Due to the claims [υw] = [au] and [υw] = [bu], also the induced map π : Σ∗/S → G ∗U H is well defined and a surjective homomorphism.We have to show that π is injective.

□

For this purpose, we define the maps φG : G → Σ∗/S and φH : H → Σ∗/S by φG(g) = au and φH(h) = bu if [g] = [au], a ∈ A, u ∈ U and [h] = [bu], b ∈ B, u ∈ U, respectively. These maps are well defined, because A and B are complete sets of representatives of the left cosets of U in G and H, respectively. We have to show that φG and φH are homomorphisms. Here the system S comes into play. Let φG(g) = au, φG(g) = au' and φG(gg') = au. With a maximum of four rewriting steps, we obtain

![](images/267_1.jpg)

It follows that φG is a homomorphism. Analogously, φH is a homomorphism. For all u ∈ U = G ∩ H we have φG(u) = φH(u) which means that φG and φH induce a homomorphism φ: G ∗U H → Σ∗/S. Finally, φ(π(c)) = c for all c ∈ Σ which gives that π is injective. The proof that Σ∗/S = G ∗U H was a bit tedious, but purely mechanical. Next, we show that the system S is convergent. This requires to prove termination and local confluence. We start with the termination.

Let x ∈ Σ∗ be a word of length n. We show that for x at most ![](images/o.jpg)(n2) rewriting steps are possible. There are at most n length reductions. Let now C = Σ \ U. We consider the length-preserving rule υw → cu with c ∈ A ∪ B, u ∈ U. Then |cu| = 2 and c ∈ C. For w ∈ U, we would get υ = c which is excluded. Hence, without loss of generality, let w = a' ∈ A, and then also c = a ∈ A. For υ ∈ A the rule has the form aa' → au. An application of the rule aa' → au reduces the number of letters from C. Therefore, altogether a rule of this type can be applied at most n times because no rule application increases the number of letters from C. Thus it is enough to count how often a rule of the type ua' → au with a, a' ∈ A and u, u' can be applied. By such a rule application a letter from U moves to the right, and this can happen at most n times per letter before it reaches the right end. Since we have at most n letters from U, we therefore obtain a maximum of ![](images/o.jpg)(n2) rule applications.

The proof of the local confluence is pure routine by considering all critical pairs. The critical pairs arise from words of length 3\. In such a word, all three letters either belong to ΣA or belong to ΣB. Indeed, if a word υuw consisting of three letters υ, u, w has the middle letter u ∈ U, then either υu is irreducible or υ ∈ U. All words whose letters belong entirely to ΣA or to ΣB have an interpretation in G or H and therefore a unique irreducible normal form, either the form au or the form bu with a ∈ A, b ∈ B and u ∈ U. Thus, the system S represents the amalgamated product G ∗U H and is convergent.

A direct consequence of [Theorem 8.18](#chapter08_2.xhtml_chapter08_2_19) is that G and H embed themselves in G ∗U H as desired: all words of the form au or bu with a ∈ A, b ∈ B and u ∈ U are irreducible. This implies the announced embedding of G∪H into the amalgamated product G ∗U H.

The normal forms in IRR(S) consist of alternating sequences of letters from A and B, and, possibly, a last letter from U. Therefore, each word w ∈ IRR(S) can be written as

![](images/268_1.jpg)

with m ≥ 0, and all ai ∈ A, bj ∈ B and u ∈ U. If we require that, in addition, ai ≠ 1 for 2 ≤ i ≤ m and bj ≠ 1 for 1 ≤ j < m, then the representation is unique.

For many applications, this system S is unnecessarily meticulous. Often we content ourselves with the alphabet Γ = (G ∪ H) \ {1} and rules which reduce words of length 2 or 3 to words in Γ ∪ {1} in each step.

For this purpose, define S' as follows:

![](images/268_2.jpg)

If we start with a word w ∈ Γ∗, then we obtain an irreducible sequence relating to S' of the form

![](images/268_3.jpg) w = g1 ⋅⋅ ⋅ gn

with n ≥ 0, where for n ≥ 1, we have gn , gi ∈ Γ, and gi ∈ G ⇔ gi+1 ∉ G for all 1 ≤ i < n. To implement this effectively, we assume that G is finitely generated by an alphabet Γ0 and H is finitely generated by an alphabet Γ1 where Γ0 ∩ Γ1 = 0\. We further assume that we can effectively determine if a word ![](images/268_11.jpg) belongs to U. Also we assume that, for a word ![](images/268_12.jpg) we can effectively compute a representation as a word in ![](images/268_13.jpg) Finally, we must be able to decide whether g = 1 for ![](images/268_14.jpg)

Let us summarize this again. The word problem in G ∗U H is solvable if the following conditions are satisfied: the word problems in G and H are solvable, the membership problem for the subgroup U is solvable in G and H, and for u ∈ U, we can effectively switch between the representations as words in ![](images/268_8.jpg) Γ∗0 and ![](images/268_9.jpg) Γ∗1 .

We now consider another important construction in combinatorial group theory, the HNN extensions which are named after their inventors Graham Higman (1917–2008), Bernhard Hermann Neumann (1909–2002), and Hanna Neumann (1914–1971). Their explicit construction is given in [[50](#Bibliography.xhtml_Bibliography_50)].

We start with a group G and an isomorphism φ: A → B between subgroups A and B of G. The central idea is to embed G into a bigger group in which φ becomes an inner automorphism, that is, φ is realized by an element t with tat−1 = φ(a) for all a ∈ A. The required property leads to the following construction. Let t be a new symbol and F (t) the free group generated by t; then, we have F (t) ≅ ℤ. The HNN extension of G with respect to φ: A → B is the following quotient group:

![](images/268_10.jpg)

In order to see that G and F (t) can be embedded into the HNN extension, we argue analogously as in the case of amalgamated products. The formal proofs just follow the already known technique step by step.

As the alphabet we now choose Σ = {t, t} ∪ (G \ {1}), and thus obtain a canonical surjective homomorphism Σ∗ → HNN(G; A, B, φ). We choose a complete system C ⊆ G and D ⊆ G of (left) coset representatives of A in G with 1 ∈ C and of B in G with 1 ∈ D, respectively. Each g ∈ G has a unique representation g = ca = db with a ∈ A, b ∈ B, c ∈ C, and d ∈ D. In the HNN extension we have: gt̄ = cat̄ = ct̄φ(a) and gt = dbt = dtφ−1(b). Therefore, we may push the elements of A to the right by means of t−1 = t̄ and analogously the elements of B by means of t. The representatives remain on the left side. This consideration leads us to the following semi-Thue system S:

![](images/269_4.jpg)

The isomorphism between Σ∗/S and HNN(G; A, B, φ) and the local confluence of S are easy to prove, that is, they are purely mechanical and analogously follow the scheme we had for amalgamated products. Some more attention we have to pay to the termination since the system S even increases lengths. Again, let x ∈ Σ∗ be a word of length n. First, we mark all letters in the word except the t’s and the t’s. Then we remove the marking for those 1 ≠ c ∈ C and 1 ≠ d ∈ D where there is a t or t, respectively, on the right. This rule for the markings we retain during the rewriting steps. After a rule application, a new marking can only be generated if, for instance, there is a factor ctt and tt gets deleted. This reduces the number of t’s, and the number of marks is therefore limited in total by n. Hence, each rule application reduces the number of t’s or it reduces the number of markings or some marking will be passed exactly one position closer to the right edge. We thus obtain a maximum of n2 possible rewriting steps.

In particular, we obtain the following theorem:

Theorem 8.19. The system S of equation ([8.8](#chapter08_2.xhtml_chapter08_2_24)) is convergent, and Σ∗/S is canonically isomorphic to the HNN extension

![](images/269_5.jpg)

From [Theorem 8.19](#chapter08_2.xhtml_chapter08_2_25), we obtain that the irreducible normal forms for HNN extensions have the following unique representation:

![](images/269_6.jpg)

with n ≥ 0, h ∈ G and either ri ∈ C and θi = t or ri ∈ D and θi = t for all 1 ≤ i ≤ n. In particular, G and F (t) embed into the HNN extension, and the HNN extension is always a group that has ℤas a quotient group and, therefore, contains ℤas a subgroup, too. As in the case of amalgamated products the system S from ([8.8](#chapter08_2.xhtml_chapter08_2_24)) is unnecessarily meticulous. In order to solve the word problem, we do not need a unique normal form. It is enough to consider Britton reductionswhichwere introduced in [[10](#Bibliography.xhtml_Bibliography_11)] by JohnLeslie Britton (1927–1994). By definition, a Britton reduction means to apply one of the following rules:

![](images/270_5.jpg)

The new system is length reducing and for each word from Σ∗ it provides a Britton reduced word of the form

![](images/270_6.jpg)

with n ≥ 0, g1, . . . , gn, h ∈ G, and θi ∈ {t, t̄} for i = 1, . . . , n and gi ≠ 1 for 2 ≤ i ≤ n. This Britton reduced normal form is not unique: for instance, tφ(b) and bt are both Britton reduced but represent the same element in HNN(G; A, B, φ). Let g = g1θ1 ⋅⋅ ⋅ gnθnh be Britton reduced and θ1, . . . , θn the sequence of the occurring t’s and t̄’s. If we now further apply rules from the convergent system S of ([8.8](#chapter08_2.xhtml_chapter08_2_24)), then we realize that the sequence θ1, . . . , θn does not change anymore. This sequence is therefore determined solely by the group element g. Hence, g ∈ G if and only if n = 0 and h = 1\. If G has a solvable word problem and if we can effectively compute Britton reductions, then the HNN extension G ∗ F (t)/{ tat−1 = φ(a) | a ∈ A } has a solvable word problem.

Example 8.20. The Baumslag–Solitar groups BS(p, q) defined in [Example 8.8](#chapter08_1.xhtml_chapter08_1_36) are HNN extensions of ℤ. The Waack group W defined in [Example 8.9](#chapter08_1.xhtml_chapter08_1_38) is an HNN extension of BS(1, 2) = F (a, t)/{tat−1 = a2}. Actually, we presented two different realizations: BS(1, 2) ∗ F(s)/{sas−1 = a2} and BS(1, 2) ∗ F(r)/{rar−1 = a}. Thus, different looking HNN extensions may define isomorphic groups.

◊

The similarity of the constructions for amalgamated products and HNN extensions is not a coincidence: it is part of the Bass–Serre theory. This theory was outlined by Jean-Pierre Serre (born 1926) [[93](#Bibliography.xhtml_Bibliography_94)] and brought to its final form by Hyman Bass (born 1932).

The Baumslag group BG(1, 2)

Let us consider another HNN extension BG(1, 2) given as

![](images/270_7.jpg)

It is called the Baumslag group. The generator t is redundant and BG(1, 2) is generated by a and b with a single defining relation

![](images/270_8.jpg)

At first glance, this might appear to be a similar definition as the one for the Waack group W above. However, the behavior is quite different. Baumslag constructed his group BG(1, 2) as an example of a not cyclic one-relator group where all its finite quotients are cyclic. Later Gersten showed that the so-called Dehn function grows faster than any elementary function. We do not define these notions here, but due to the discovery of Gersten, the group BG(1, 2) is called the Baumslag–Gersten group in the literature [[84](#Bibliography.xhtml_Bibliography_85)], too.

The word problem in BG(1, 2) is solvable because we can effectively compute the Britton reduced normal form as follows. The input is a word w ∈ {a, a−1, b, b−1, t, t−1}∗, which we decompose

![](images/271_2.jpg)

with m ≥ 0, βi ∈ {b, b−1}∗ and gi ∈ {a, a−1, t, t−1}∗.

If m = 0, then w = g0 ∈ BS(1, 2) is Britton reduced. If m = 1, then w ∉ BS(1, 2), and w is Britton reduced. Now, let m ≥ 2\. We consider all factors of the form βigiβi+1 with ![](images/271_3.jpg)1 ≤ i < m. If βi = b, then we test if ![](images/271_7.jpg) has the form gi = (τ, 0) with τ ∈ ℤ. If yes, then gi = aτ in BS(1, 2), and we replace the factor βigiβi+1 by tτ or (0, τ), respectively, if we calculate directly in the decomposition ![](images/271_4.jpg)Analogously, if βi = b−1 and gi = (0, τ) with τ ∈ ℤ, then we replace βigiβi+1 by aτ or (τ, 0), respectively. After a maximum of m such steps, we obtain a Britton reduced word.

This looks harmless enough, but lo and behold, the exponents can get huge very quickly; see [Exercise 8.11](#chapter08_4.xhtml_chapter08_4_31). This is closely related to the fast growing Dehn functions; and for this reason, the group BG(1, 2) for many years was a candidate for a one-relator group with an extremely difficult word problem. However, it had to be canceled from that list by [[31](#Bibliography.xhtml_Bibliography_31), [78](#Bibliography.xhtml_Bibliography_78)]: the word problem for BG(1, 2) is solvable in cubic time using a data structure called power circuit.

## 8.9 Rational sets and Benois’ theorem

As usual if M is a monoid and R, R' subsets of M, then R ⋅ R' denotes the product R ⋅ R' = {xy ∈ M| x ∈ R, y ∈ R' } and R∗ denotes the submonoid of M, which is generated by R. Ifwe let R0 = {1} and Rn+1 = R ⋅ Rn, we have R∗ = ⋃{ Rn | n ∈ ℕ}. As in [Section 7.2](#chapter07_1.xhtml_chapter07_1_19), we define the family RAT(M) of rational sets inductively:

–Finite subsets R ⊆ M are rational.

–If R, R' are rational, then so are R ∪ R', R ⋅ R' and R∗.

Every finitely generated submonoid N ⊆ M is rational, but there also exist rational submonoids which are not finitely generated. The standard example for this is N = {(0, 0)}∪{ (m, n) ∈ℕ×ℕ|m ≥ 1 }; N is a submonoid of ℕ×ℕ but it cannot be finitely generated because for any finite set of pairs (mi , ni) the element (1, 1 + max{ni}) is in N but not in the submonoid generated by the pairs (mi , ni). The submonoid N is rational because N = {(0, 0)} ∪ {(1, 0)} + ({(1, 0)} ∪ {(0, 1)})∗. For groups the situation is different.

Theorem 8.21. Let H be a rational subgroup of a group G. Then H is finitely generated.

Proof: Since H is rational, there is a finite subset A ⊆ G such that H can be described as a rational set over A∗. For this let π : A∗ → G be the homomorphism induced by the inclusion of A in G, then there is a regular set R ⊆ A∗ with π(R) = H. By Kleene’s theorem, [Theorem 7.17](#chapter07_2.xhtml_chapter07_2_10), the language R will be recognized by a deterministic finite automaton A over the alphabet A and therefore π(L(A)) = H. Without loss of generality we have A = A−1, and for each u ∈ A∗ there is a word ū ∈ A∗ with π(uū) = π(ūu) = 1.

Let n be the number of states of A. It is enough to show that the finite set π(W) with

![](images/272_2.jpg)

generates the subgroup H.

Since π(L(A)) = H, it is sufficient to show that for each word w ∈ L(A) the element π(w) is in the subgroup generated by π(W). We show this by induction on |w|. If |w| ≤ n, then w ∈ W because in this case we may choose the empty word for u. Now, let |w| > n. When reading the word in *A*, we must see one of the n states at least twice. Therefore, let uυ be a prefix of w with |u| < |uυ| ≤ n such that the words u and uυ lead to the same state of A. We write w = uυz. Since the automaton is deterministic, the word uz is recognized, too. Hence, by induction, π(uz) is in the subgroup generated by π(W). Because π(uυū uz) = π(uυz) = π(w) ∈ H and π(uz) ∈ H, we must have π(uυū) ∈ H. Therefore, uυū ∈ W.

□

A classical theorem in formal language theory, [Theorem 7.17](#chapter07_2.xhtml_chapter07_2_10), states that the rational sets of finitely generated free monoids form an effective Boolean algebra. As soon as we meet partial commutation, the situation changes. Let Σ = {a, b, c} be an alphabet with three generators. Consider the (free partially commutative) monoid M = {a, b, c}∗/{ab = ba, bc = cb}. [Exercise 8.6](#chapter08_4.xhtml_chapter08_4_27) shows that the family of rational subsets in M is not closed under intersection.

We are particularly interested in rational sets of finitely generated free groups F (Σ) and want to show that they form an effective Boolean algebra, that is, the family of rational sets is closed under finite union and complementation, and moreover we may effectively compute the finite union and the complementation (and hence the intersection). This statement about free groups was published in 1969 by Benois [[6](#Bibliography.xhtml_Bibliography_7)]. Her proof can be extended to other finitely generated groups and monoids which may be presented by certain confluent semi-Thue systems.

We start very general. For a finite alphabet Γ, a finite semi-Thue system S ⊆ Γ × Γ is called monadic if the following condition is satisfied: for all rules (ℓ, r) ∈ S, we have |ℓ| > |r| ≤ 1\. A monadic system is therefore length reducing and right components are either empty or have exactly one letter. For infinite systems, we additionally require that for each r ∈ Γ ∪ {1} the set L(r) = {ℓ ∈ Γ∗ | (ℓ, r) ∈ S } of the left components is regular. For finite systems this requirement is automatically satisfied.

Theorem 8.22. Let Γ be finite, S ⊆ Γ × Γ be a confluent monadic semi-Thue system, and let M = Γ∗/S be the quotient monoid. Then the family of the rational sets RAT(M) is an effective Boolean algebra. In particular, membership in a rational set is decidable.

Proof: Let π : Γ∗ → M = Γ∗/S be the canonical projection. As just described, we define for r ∈ Γ ∪ {1} the regular set L(r) = {ℓ ∈ Γ∗ | (ℓ, r) ∈ S } of the left components.

For the specification of a rational set R ⊆ M, we use a nondeterministic finite automaton A on Γ such that π(L(A)) = R. We allow ε-edges, which could be removed if necessary, but we require that the edges are labeled only with letters or the empty word. If two nondeterministic finite automata R and R' are given, then the standard constructions in [Section 7.2](#chapter07_1.xhtml_chapter07_1_19) provide automata for R ∪ R, R ⋅ R, and R∗. Intersection can be obtained quite naturally using union and complementation. Hence, for a nondeterministic finite automaton A, it suffices to effectively construct another nondeterministic finite automaton *A*' with π(L(*A*')) = M \ π(L(*A*)).

Next, we give the construction of A' step by step. First, we enlarge the language L(*A*) within Γ∗ without changing R = π(L(*A*)). We “flood” the automaton by more edges. Let Q be the state set of A. For each pair (p, q) ∈ Q2, we define a regular set L(p, q) ⊆ Γ∗, which consists of all words that we would accept if p, were the only initial state and q the only final state. Then we test for each r ∈ Γ ∪ {1} whether L(p, q) ∩ L(r) ≠ 0\. This is an effective test. If the intersection is nonempty, then we insert an edge from p to q with label r in the automaton A, provided it does not already exist. We iterate this procedure repeatedly, until (after a maximum of (|Γ|+1)|Q|2 rounds) finally no new edges can be included. Note, the monadic property implies that we increase the number of edges, but we do not insert new states. The language L(*A*) was not changed: to see this, consider an accepted word urυ, which, when reading r, passes a new edge from the state p to the state q. Then there is a rule (ℓ, r) ∈ S with ℓ ∈ L(p, q). Hence, also uℓυ is accepted, and the accepting path uses the new edge less frequently. This implies π(urυ) = π(uℓυ), which means that the flooding does not change the rational set R. By a slight abuse of language, we continue to refer to the new automaton as A. It now has the following important property: from ![](images/273_1.jpg) and u ∈ L(A) it follows υ ∈ L(A). We define

![](images/273_2.jpg)

Then R̂ is a set of normal forms for R, and π provides a bijection between R̂ and R. Furthermore R̂ ⊆ L(*A*).

As the next step, we construct a nondeterministic finite automaton *A*'' which accepts the complement Γ∗ \ L(*A*); see [Theorem 7.17](#chapter07_2.xhtml_chapter07_2_10). The set π(L(*A*ˮ)) contains more elements than the complement M \ R, but if we consider the intersection with the irreducible words, then, as desired, we obtain

![](images/274_4.jpg)

It remains to show that IRR(S) is regular. For this purpose, we write the complement of IRR(S) as the union of finitely many regular languages Γ∗L(r)Γ∗. Thus, we have effectively found an automaton A' with

![](images/274_3.jpg)

It follows π(L(A)) = M \ R which proves the theorem.

□

Corollary 8.23 (Benois). The rational sets in a finitely generated free group form an effective Boolean algebra.

Proof: [Example 8.6](#chapter08_1.xhtml_chapter08_1_28) shows that the monadic system S = {aā → 1 | a ∈ Γ } is strongly confluent.

□

## 8.10 Free groups

A central theorem about free groups says that their subgroups are free, too. This theorem was first shown by Jacob Nielsen (1890–1959) for finitely generated subgroups [[82](#Bibliography.xhtml_Bibliography_82)] and by Otto Schreier (1901–1929) in general. Like vector spaces and free monoids, free groups are, up to isomorphism, completely determined by their rank, that is, by the cardinality of their basis. For subgroups of finite index we present the rank formula by Schreier, which allows the computation of the rank of the subgroup. We already know from [Corollary 8.23](#chapter08_3.xhtml_chapter08_3_6) that the membership problem in finitely generated subgroups is solvable, because finitely generated subgroups are rational subsets.

Some classical proofs of these results are technical and complicated. In a modern approach one typically follows the ideas of Serre. In [[93](#Bibliography.xhtml_Bibliography_94)], it is shown that a group is free if and only if it acts “freely and without inversion” on trees. Another approach uses Stallings graphs [[99](#Bibliography.xhtml_Bibliography_100)]. These are special deterministic automata on free groups. They are named after John Robert Stallings, Jr. (1935–2008). The approaches of Serre and Stallings are closely related. Essential parts in Stallings’ method can be derived from the ideas of Benois, which we presented in [Section 8.9](#chapter08_2.xhtml_chapter08_2_33). These results were historically more than a decade ahead of Stallings’ graphs, but hardly known among group theorists.

In the following, let F = F (Σ) be a free group with basis Σ. The rank of F is defined as the cardinality |Σ| of Σ. Let us convince ourselves that the rank is well defined, that is, it does not depend on the chosen basis. The proof uses the well-known fact that a vector space, up to isomorphism, is uniquely determined by its dimension.

Theorem 8.24. Let F (Σ) and F (Σ) be isomorphic free groups. Then there is a bijection between the bases Σ and Σ.

Proof: Let F = F (Σ). Consider the subgroup N of F generated by the squares. N consists of products of the form ![](images/275_2.jpg) with k ∈ ℕ and xi ∈ F. The subgroup N of F is normal because ![](images/275_1.jpg) In the quotient group F/N all elements have order 2\. It is therefore Abelian, because xy = xy(yx)2 = (x(yy)x)yx = yx ∈ F /N. Therefore, F /N is an ![](images/f_d.jpg)2-vector space. Now we consider the ![](images/f_d.jpg)2-vector space ![](images/275_3.jpg) which consists of the maps χ : Σ → ![](images/f_d.jpg)2 with χ(b) = 0 for almost all letters b. The set { χa | a ∈ Σ } with χa(a) = 1 and χa(b) = 0 for b ≠ a forms a basis of ![](images/275_5.jpg) ![](images/275_4.jpg) defines a surjective linear map. The inverse map is induced by the homomorphism ρ ![](images/275_6.jpg) a ↦ χa, and this homomorphism gives a linear map ψ: ![](images/275_8.jpg) , a ↦ χa; and we have χa = ψ(φ(χa)) for all χa from the base of ![](images/275_7.jpg) In particular, φ is injective and hence an isomorphism between ![](images/f_d.jpg)2-vector spaces:

![](images/275_9.jpg)

The definition of F /N is independent of the basis of F; and therefore also the dimension of F /N as an ![](images/f_d.jpg)2-vector space. This dimension is equal to the dimension of ![](images/275_10.jpg) that is, equal to |Σ|. Hence, if F (Σ) and F (Σ) are isomorphic, then there is a bijection between Σ and Σ. Certainly, if there is a bijection between Σ and Σ, then F (Σ) and F (Σ) are isomorphic.

In the following, let Γ = Σ ∪ Σ−1 and let π : Γ∗ → F be the homomorphism induced by the inclusion of Γ in F. We may interpret words in Γ∗ as group elements of F. For a word w ∈ Γ∗, we often write w ∈ F instead of π(w) ∈ F. As usual, a word w ∈ Γ∗ is called reduced if it does not contain any factor aa−1 with a ∈ Γ. Now, let G be a subgroup of F. We want to show that G is free. Our goal is more ambitious and, therefore, it can only be achieved with a little additional effort. We present a method for determining the rank of finitely generated groups.

We start with the Schreier graph of the right cosets G\F for G in F. The set of vertices is V = G \ F. The set E of directed edges consists of pairs (u, a) ∈ V × Γ with source s(u, a) = u and target t(u, a) = ua. Note that this graph may contain multiple edges and loops. The number of vertices is the index [F : G], which we denote by n. Here, n is finite or n = ∞. We label the edge (u, a) by λ(u, a) = a. If we define G as the unique initial and final state, then we obtain a deterministic automaton that recognizes the language L ⊆ Γ∗ with π(L) = G.

It proves advantageous to move to a partial automaton. For this, let Q be the set of right cosets Gu that are in the Schreier graph on a path, which is labeled by a reduced word uυ with π(uυ) ∈ G. The set Q may be infinite, and we have

![](images/275_12.jpg)

Now, let K(G, Σ) be the subgraph of the Schreier graph, which is induced by Q. We let E be its edge set. The edges are labeled, and we have G ∈ Q. Hence, we may interpret K(G, Σ) as an automaton by defining G to be the initial and final state. The automaton accepts a language R ⊆ Γ∗ with π(R) ⊆ G. Since each element in G is represented by a reduced word, we actually have π(R) = G. We call the automaton K(G, Σ) the kernel of the Schreier graph.

The graph K(G, Σ) = (Q, E) is connected and it has an edge labeling λ : E → Γ. We orient the edges via their labeling by E+ = {e ∈ E | λ(e) ∈ Σ }. An undirected edge is, according to our convention, a collection {e, ē} of two oriented edges e and e. In our case e is a tuple e = (p, a) with p ∈ Q and a ∈ Γ. Letting ē = (pa, a−1), we have λ(ē) = a−1. If we want to stress that we consider an oriented edge we call it arc. Thus, an arc is the same as an oriented edge.

A tree is a nonempty connected undirected graph (U, T) without loops, multiple edges or cycles. A tree (Q, T) with T ⊆ E is called a spanning tree of (Q, E). Like any connected graph, (Q, E) has a spanning tree (Q, T). In our applications, (Q, E) is connected and countable. In order to show that it has a spanning tree, we arrange the edges in some linear list (e1, e2, . . . ). Let T0 = Ø and inductively define Ti for i ≥ 1 as follows: if the edges in Ti−1 ∪{ ej | j > i } connect all vertices of Q, then let Ti = Ti−1; otherwise let Ti = Ti−1 ∪ {ei}. Finally, define T = ∪i∈ℕTi; and (Q, T) becomes a spanning tree of (Q, T). For arbitrary graphs, the proof is similar using transfinite induction or Zorn’s lemma.

Theorem 8.25. Let G be a subgroup of F = F(Σ). Then G is a free group. In the notation just introduced G is isomorphic to the free group F (Δ) with Δ = E+ \ T where T is a spanning tree (Q, T) of the graph K(G, Σ). Moreover, if Q is finite and if m = |E|/2 ∈ ℕ ∪ {∞} denotes the number of undirected edges in K(G, Σ), then G has rank

![](images/276_4.jpg)

Proof: We interpret G in the free group F (E+). In other words, we interpret K(G, Σ) as an undirected graph and we want to find G as a subgroup in the free group whose generators are the arcs in E+. Recall that we have λ(ē) = λ(e)−1 for all edges e. Hence, we obtain a well-defined homomorphism

![](images/276_5.jpg)

For any two vertices p, q ∈ Q, the uniquely determined shortest path in the spanning tree from p to q is denoted by T[p, q]. This is a sequence of arcs; in particular, we may interpret T[p, q] as an element of F(E+). In the group F(E+), we then have T[p, q] = T[q, p]−1. Next, we define for each arc e an element τ(e) ∈ F (E+) by the sequence of arcs:

![](images/276_6.jpg)

So, we walk in the spanning tree from the coset G to the source of e, pass through e and then, in the spanning tree, go back to the initial vertex G. In particular, we have λ(τ(e)) ∈ G. Moreover, in order to compute λ(τ(e)) ∈ G, we can use any path in K(G, Σ) which starts and ends in the coset G and passes through the arc e.

If t(e) = s(f) for arcs e, f then τ(e) ⋅ τ(f) = T[G, s(e)] ⋅ e ⋅ f ⋅ T[f(e), G] ∈ F(E+) because the middle paths between G and t(e) = s(f) cancel each other.

Now, let e1 ⋅⋅ ⋅ em ∈ E ∗ be a sequence of arcs from G to G; then we have

![](images/277_10.jpg)

for the labeling. In particular, λ(τ(F(E+)) = G because the labels for the sequences of arcs in K(G, Σ) are sufficient to generate G. Note that τ(e) = 1 ∈ F(E+) and λ(τ(e)) = 1 ∈ G for e ∈ T. Thus, we obtain a surjective homomorphism

![](images/277_11.jpg)

It only remains to show that λ ∘ τ is injective because, for nonempty graphs with |Q| vertices, a spanning tree has |Q| − 1 undirected edges. Suppose that λ(τ(w)) = 1 for a reduced word w = e1 ⋅⋅ ⋅ ek with ![](images/277_3.jpg) and k ≥ 0\. Then ![](images/277_4.jpg) for 2 ≤ i ≤ k, and no edge ei belongs to T for 1 ≤ i ≤ k.

The sequence of arcs

![](images/277_12.jpg)

can be reduced for k ≥ 2 by the rules eē → 1 possibly within factors

T[t(ei−1), G]T[G, s(ei )]. But no reduction can involve an arc ![](images/277_5.jpg) because the neighbors remain edges of the spanning tree or have the form ei−1 or ei+1. By performing all reductions, we obtain a reduced chain of arcs f1 ⋅⋅ ⋅ fℓ from G to G with k ≤ ℓand ![](images/277_6.jpg) for all 2 ≤ i ≤ ℓ. We still have λ(f1 ⋅⋅ ⋅ fℓ) = 1\. Suppose that ℓ ≥ 1, then there is an index i with ![](images/277_7.jpg) But t(fi−1) = s(fi ) because we have a sequence of arcs, and this means ![](images/277_8.jpg) which does not hold. This shows that ℓ = 0 and, hence, we have k = 0\. Therefore, w is the empty word.

□

We say that K(G, Σ) is complete if, for each letter a ∈ Γ and every state Gu ∈ Q, we have Gua ∈ Q, too. In this case, there is an edge from Gu to Gua in K(G, Σ) labeled by a. Since in the Schreier graph there is exactly one edge labeled by a from Gu to Gua, the graph K(G, Σ) is complete if and only if it coincides with the Schreier graph. Two situations are of special interest:

Lemma 8.26. If G is a nontrivial normal subgroup or if G is of finite index in F(Σ), then K(G, Σ) is complete and, hence, K(G, Σ) is the Schreier graph.

Proof: Let Gu be a right coset and u = a1 ⋅⋅ ⋅ ak reduced with k ≥ 0 and ai ∈ Γ. We show that Gu ∈ Q. Then K(G, Σ) is the whole Schreier graph, and K(G, Σ) is therefore complete. This is true for k = 0\. Now, let k ≥ 1\. If Σ = {a} is a singleton then G is of finite index n; and by means of Gai for 0 ≤ i ≤ n, we travel through the Schreier graph. Now, let |Σ| ≥ 2 and b ∈ Σ with ak ≠ b. The map Gw ↦ Gwb permutes the right cosets. If G has finite index, then there exists n ≥ 1 with Gubn = Gu. Since ![](images/277_9.jpg) is reduced, it defines a path from G to G. In particular, Gu ∈ Q.

□

Now assume that G is a nontrivial normal subgroup of infinite index in F (Σ) and u = a1 ⋅ ⋅⋅ ak as above. In particular, |Σ| ≥ 2 and there exist a, b ∈ Σ with ak = a ≠ b. By assumption G ≠̸ {1}.Hence, there is a shortest nonempty reduced word w ∈ G. This word cannot have the form cυc−1 with c ∈ Γ because cυc−1 ∈ G implies υ ∈ G, since G is normal. If w neither begins with a−1 nor ends in a, then ![](images/278_1.jpg) is reduced and it describes a path from G to G in K(G, Σ). As a consequence Gu ∈ Q. Thus, we may assume that w either begins with a−1 or ends in a. It cannot be both as we pointed out above. By symmetry let w end in a. Then the first letter of w is some c ≠ a−1. By interchanging the role of b and b−1 if necessary, we may assume that b ≠ c ≠ a−1. As a consequence, ![](images/278_2.jpg) is reduced. Again, uυ describes a path from G to G in K(G, Σ) and therefore Gu ∈ Q.

Lemma 8.27. Let G be a subgroup of a finitely generated free group F (Σ). Then the following statements are equivalent:

(a)The subgroup G is rational.

(b)The subgroup G is finitely generated.

(c)The kernel K(G, Σ) is finite.

Proof: If K(G, Σ) is finite then G is rational. A rational subgroup is finitely generated by [Theorem 8.21](#chapter08_3.xhtml_chapter08_3_2). Hence, let G be finitely generated. We only have to show that Q is finite, where as above K(G, Σ) = (Q, E). Since G is finitely generated, there are finitely many words w1, . . . , wk ∈ Γ∗ such that each element in G can be represented as a product over A = {w1, . . . , wk}. The reading of a word w ∈ A∗ in the Schreier graph uses only a finite part Q' of the right cosets, and all reduced words are formed by reduction of words from A∗. Let Q' be the finite set of vertices that are visited when reading w1w2 ⋅⋅ ⋅ wk in the Schreier graph. Remember that, after reading any of the words wi, we return to the starting node G. Thus, when reading a word from A∗, only vertices from Q' are visited. Since any reduced word representing an element in G can be obtained by reducing a word from A∗, it follows Q ⊆ Q' and Q is finite.

□

Theorem 8.28. Let F = F (Σ) be a finitely generated free group and let G be a nontrivial normal subgroup. Then, G has finite index in F if and only if G is finitely generated.

Proof: If G has finite index then K(G, Σ) is finite and, hence, G is finitely generated by [Lemma 8.27](#chapter08_3.xhtml_chapter08_3_17). Conversely, if G is finitely generated, then K(G, Σ) is finite. Now, [Lemma 8.26](#chapter08_3.xhtml_chapter08_3_15) shows that K(G, Σ) is the Schreier graph. Therefore, the index is finite.

□

We now give the classical form of [Theorem 8.25](#chapter08_3.xhtml_chapter08_3_13).

Theorem 8.29 (Nielsen and Schreier). Subgroups of free groups are free. If F is a finitely generated free group of rank r and G a subgroup of finite index n, then G has finite basis Δ and the following rank formula holds:

![](images/278_3.jpg) |Δ| − 1 = n ⋅ (r − 1)

Proof: Let F = F (Σ). The statement was already proved in [Theorem 8.25](#chapter08_3.xhtml_chapter08_3_13); only the rank formula had a slightly different form. We obtain the classical version directly from [Lemma 8.26](#chapter08_3.xhtml_chapter08_3_15),which says that K(G, Σ) is the Schreier graph. Therefore, |Q| = n = [F : G] and m = n ⋅ r.

Corollary 8.30. If x and y are commuting elements of a free group, then x and y generate a cyclic subgroup.

Proof: The subgroup G generated by x and y is free by [Theorem 8.29](#chapter08_3.xhtml_chapter08_3_18) and commutative by assumption. Hence, G is either trivial or of rank 1\. In both cases G is cyclic.

□

[Corollary 8.30](#chapter08_3.xhtml_chapter08_3_20) corresponds to [Theorem 6.5 (b)](#chapter06.xhtml_chapter06_11) for free monoids. To conclude this section, we show the corresponding result to [Theorem 6.5 (a)](#chapter06.xhtml_chapter06_10) for free groups. For the remainder of this section, let F (Σ) be the free group over Σ and Γ = Σ ∪ Σ−1 ⊆ F (Σ). We write a = a−1 for a ∈ Γ. A word w ∈ Γ∗ is called cyclically reduced if ww is reduced. In particular, w is reduced; and if w begins with a letter a ∈ Γ, then it does not end with a. Each element x ∈ F (Σ) is conjugated to an element, which can be represented by a cyclically reduced word w. Recall that words x, y ∈ Γ∗ are transposed if and only if we can write x = rs and y = sr. Clearly, transposed words represent conjugated words in F (Σ). The next theorem states the converse for cyclically reduced words. It was published by Lyndon and Schützenberger in 1962.

Theorem 8.31. Let F (Σ) be the free group over Σ and x, y ∈ Γ∗ be cyclically reduced. If zxz−1 = y in F (Σ) for some z, then there exist reduced words r, s ∈ Γ∗ with x = sr and y = rs in Γ∗.

Proof: We may assume that z is given by a reduced word in Γ∗. If zx and yz are both reduced then the words are identical and the statement follows from [Theorem 6.5 (a)](#chapter06.xhtml_chapter06_10). Now, let zx be not reduced (the arguments for yz are analogous). Then there is a letter a ∈ Γ such that z = za−1 and x = ax. It follows zxa = zxa = yza = yz' in F(Σ). Since x is cyclically reduced, xa is cyclically reduced, too. By induction on |z| there exist reduced words r' , s' ∈ Γ∗ with xa = s' r' and y = rs. Now, x = ax' and xa are transposed, and also xa and y are transposed. By [Theorem 6.5 (a)](#chapter06.xhtml_chapter06_10) transposition is transitive, and therefore x and y are transposed words.

□

Corollary 8.32. Dehn’s problems, that is, the word problem, the conjugacy problem, and the isomorphism problem are algorithmically solvable for finitely generated free groups.

Proof: The word problem can be solved by free reduction. To solve the conjugacy problem we need to cyclically reduce two input words. Then we have to test if these cyclically reduced words are transposed. This test gives the correct answer by [Theorem 8.31](#chapter08_3.xhtml_chapter08_3_21). Finally, two free groups are isomorphic if and only if their bases have the same cardinality.

□

## 8.11 The automorphism group of free groups

In this section, we give a graph theoretic interpretation of a classical result by Nielsen [[83](#Bibliography.xhtml_Bibliography_83)]: the automorphism group Aut(F) of a finitely generated free group F is finitely generated. The classical proof uses elementary transformations. Our proof is based on the notion of Whitehead automorphisms. In fact, the automorphism group Aut(F) is finitely presented [[70](#Bibliography.xhtml_Bibliography_70)], but we do not show this here.

Whitehead automorphisms

Let F = F (Σ) be a free group of rank n, that is, |Σ| = n. We define a finite family of automorphisms of F which are named after John Henry Constantine Whitehead (1904–1960). Every permutation of Σ induces a Whitehead automorphism of F. There are n! automorphisms of this type. For a ∈ Σ, we define a Whitehead automorphism ia as follows: ![](images/280_1.jpg)

The automorphism ia inverts the letter a and leaves all other letters invariant. There are n automorphisms of this type.

The last set of Whitehead automorphisms is defined for a ∈ Σ and three pairwise disjoint subsets L, R, M of Σ with a ∈ M. Each tuple (a, L, R, M) defines a Whitehead automorphism W(a,L,R,M) as follows:

![](images/280_2.jpg)

There are n4n−1 automorphisms of this type. Sometimes one also counts the inverse automorphism ![](images/280_3.jpg) as a Whitehead automorphism but this does not really matter, because we have ![](images/280_4.jpg) Among the Whitehead automorphisms,we find the subset of elementary Nielsen transformations which consists of the automorphisms ia and λab = W(a,{b},0,{a}).

The following theorem shows that Aut(F(Σ)) is finitely generated. [Exercise 8.14 (a)](#chapter08_4.xhtml_chapter08_4_32) then shows that only four elementary Nielsen transformations are sufficient to generate Aut(F).

Theorem 8.33. The automorphism group Aut(F(Σ)) is generated by the Whitehead automorphisms.

Our proof is based on lectures by Saul Schleimer given at the Centre de Recerca Matemàtica in Barcelona (Catalonia) in September 2012. According to Schleimer and [[107](#Bibliography.xhtml_Bibliography_108)], our proof of [Theorem 8.33](#chapter08_3.xhtml_chapter08_3_25) follows unpublished ideas of Stallings. The intention is not to present the shortest possible proof, but to understand why Whitehead automorphisms form a natural set of generators for Aut(F(Σ)). In fact, we can get even a little more from the proof: without any additional effort it shows that finitely generated free groups are Hopfian.

In the following, X and Y describe finite sets and F (X) and F (Y) the corresponding free groups. Let then X̃ = X ∪ X−1 ⊆ F(X) and Ỹ = Y ∪ Y−1 ⊆ F(Y). We want to study surjective homomorphisms of F (X) onto F (Y). Without loss of generality, wemay assume that Y ≠ 0\. We call a homomorphism π : F (X) → F (Y) a projection if

![](images/281_1.jpg)

That is, a projection is surjective, and letters are either deleted or mapped to letters or their inverses. For X = Y every projection is a product of Whitehead automorphisms. Hence, the following statement generalizes [Theorem 8.33](#chapter08_3.xhtml_chapter08_3_25).

Theorem 8.34. Let φ: F(X) → F(Y) be a homomorphism.

(a)Then it is decidable whether φ is surjective, that is, if φ is an epimorphism.

(b)If φ is an epimorphism, then φ can be factorized as φ = π∘ψwhere π is a projection and ψ a product of Whitehead automorphisms.

[Theorem 8.34](#chapter08_3.xhtml_chapter08_3_28) provides the assertion that finitely generated free groups are Hopfian, because for |X| = |Y| projections are isomorphisms. We also see that if finitely generated free groups are isomorphic, then their rank is equal. (See [Theorem 8.24](#chapter08_3.xhtml_chapter08_3_10) for the general statement including infinitely generated free groups.) Indeed, if |X| < |Y|, then there are no projections from F (X) to F (Y). Thus, epimorphisms (resp. isomorphisms) from F(X) onto F(Y) exist if and only if |X| ≥ |Y| (resp. |X| = |Y|).

The rest of this section is devoted to the proof of [Theorem 8.34](#chapter08_3.xhtml_chapter08_3_28). Without loss of generality, we may assume that X and Y are nonempty finite sets. A graphical realization of a homomorphism of F (X) to F (Y) is a pair (Γ, Φ) where Γ is a marked, connected, edge labeled, finite graph, together with a spanning tree, and Φ is a mapping of X̃ to the set of edges of Γ. Formally, Γ is a tuple (1, V, E, T, λ) and Φ: X̃ → E is a mapping with the following properties:

–The pair(V, E) is a connected graph with vertex set V and finite nonempty edge set E.

–There exists a marked vertex in V, which is denoted by 1.

–For each directed edge e, we denote the source by s(e) ∈ V and the target by t(e) ∈ V. The graph may have loops and multiple edges.

–Toeachedgee ∈ E exactly one edge ē ∈ E is assigned such that s(ē) = t(e), t(ē) = s(e) and ![](images/281_2.jpg)

–λ : E → Ỹ maps each edge e to an element in Ỹ = Y ∪ Y−1 such that λ(ē) = λ(e)−1. The mapping λ induces a homomorphism λ : E ∗ → F (Y).

–Welet E+ = λ−1(Y) be the set of positively oriented edges. (Drawings depict these edges, only.) The homomorphism λ : E ∗ → F (Y) factorizes through the free group F (E+). Hence, we also have a homomorphism λ : F (E+) → F (Y) between free groups.

–(V, T) is a spanning tree of (V, E).

–AnedgeinE \ T is called a bridge.

–Φ induces a bijection between X̃ and the set E \ T of the bridges.

–Wehave![](images/282_1.jpg) for all a ∈ X.

Every graphical realization defines a homomorphism φ: F (X) → F (Y) as follows. Let p, q ∈ V be two vertices. As done earlier, T[p, q] denotes the shortest path in the spanning tree (V, T) from p to q. For a ∈ X and e = Φ(a) ∈ E, we put

![](images/282_6.jpg)

Thus, φΓ (a) is a closed path in (V, E) which starts at the marked vertex 1, walks in the spanning tree from 1 to the source of Φ(a), passes through the edge Φ(a) and then goes back in the spanning tree to the marked vertex 1\. Hence, we may interpret the word φΓ (a) ∈ E∗ also in the free group F(E+). Since φΓ (a−1) = φΓ (a)−1 holds in F (E+),we obtain a well-defined homomorphism φΓ : F (X) → F (E+). Finally, we define

![](images/282_3.jpg)

We obtain the following picture:

![](images/282_4.jpg)

We say that (Γ, Φ) is a graphical realization of φ: F (X) → F (Y). A graphical realization of a homomorphism is by no means unique; see, for example, [Figure 8.5](#chapter08_4.xhtml_chapter08_4_1).

Before we proceed further, let us show that every homomorphism φ: F (X) → F (Y) has some graphical realization (Γ, Φ). This is simple. Consider a ∈ X , then we may write φ(a) as φ(a) = y1 ⋅⋅ ⋅ ym with yi ∈ Ỹ. Because Y ≠ 0 and since we allow factors of the form yy−1, we may assume that m ≥ 2\. For each letter a ∈ X , we draw a cycle of length |φ(a)| with initial and target 1 and label the ith edge with the ith letter in the word φ(a). We add the first m − 1 edges of the cycle to the spanning tree and the last edge em becomes a bridge. Finally, we define Φ(a) = em. The resulting graphical realization of φ looks like a flower with petals of different size.

![](images/282_5.jpg)

Fig. 8.5. Two different graphical realizations of the Whitehead automorphism W(a,{b},{c},{a,d}) .

Given a graphical realization (Γ, Φ) and a word u ∈ (X̃)∗, we may interpret φ(u) as the word φΓ (u) in E ∗ or as an element of the free group F (E+) or by virtue of λ as an element of F (Y). However, there is no risk of confusion.

The trivial homomorphism has a graphic realization by a graph with two points 1 and 2, which are connected in the direction from 1 to 2 by |X| + 1 different arcs and all of them have label y, where y is some fixed letter in the nonempty set Y.

![](images/283_1.jpg)

The identity map id: F(X) → F (X) is realized by a so-called rose. This is a graph with one vertex 1 in which X̃ is the set of loops, and the involution corresponds to the map x ↦ x̄ = x−1. Further, the labeling λ of the loops is induced by the map from X to Ỹ. For idX : F (X) → F (X) the labeling is also the identity.

![](images/283_2.jpg) “Rose of the identity” for X = {a, b, c, d, e}: ![](images/283_3.jpg)

Roses also realize those projections that map letters to letters or their inverses. If π : F (X) → F (Y) is a projection of this form, then we label the loops of the rose with π. The rose shows us whether it encodes a projection. For this, it is necessary and sufficient that all y ∈ Y appear as labels.

![](images/283_4.jpg) Projection of {a, b, c, d, e} onto {a, b, c}: ![](images/283_5.jpg)![](images/284_1.jpg)

Fig. 8.6. Different spanning trees.

![](images/284_2.jpg)

Fig. 8.7. Replacement of the bridge A by the edge e.

In the following pictures, we draw the edges from the spanning tree thicker and as straight lines while the bridges are curved; see [Figure 8.6](#chapter08_4.xhtml_chapter08_4_2).

Example 8.35. We use [Figure 8.7](#chapter08_4.xhtml_chapter08_4_3) and make the following agreement. Let X = E+ \ T = {A, B, C, D, E} (with φ(x) = x) and Y = {a, b, c, d, e}. The edges e ∈ E+ are also indicated with their labels λ(e) ∈ Y. Thus, the upper picture tells us:

![](images/284_4.jpg)

In the lower picture the spanning tree has been changed which leads to new paths:

![](images/285_3.jpg)

This gives the following result:

![](images/285_4.jpg)

Therefore, φ can be factorized as φ' ∘ W(A,{B},{D},{A,C}).

◊

A graphical realization specifies the base point, the orientation, a spanning tree, etc. However, we are interested in homomorphisms only modulo Whitehead automorphisms. Thus, we can think that a graphical realization without a specification of the items above defines a class of homomorphisms. If every member in such a class is obtained from any other member by a multiplication of a Whitehead automorphism, then we do not lose any substantial information. This will become clear in the next subsections.

Free choice of the base point

Let 1' ∈ V be a vertex different from 1 which we want to make the marked initial and final vertex. Instead of (Γ, Φ), we now consider (Γ' , Φ) with Γ' = (1' , V, E, T, λ). Then, for a ∈ X, we may compute φ(a) in F(Y) by φ(a) = λ(T[1, 1] φ(a) T[1, 1' ]) = hφ(a)h−1 where h = λ(T[1, 1]) ∈ F(Y). Therefore, we obtain φ' by applying an inner automorphism γ of F (Y). In particular, φ' is surjective if and only if φ is surjective.

If φ is surjective then, for y ∈ F (Y), there exists x ∈ F (X) with φ(x) = y. In this case φ(a) = φ(xax−1) = φ ∘ ψ, where ψ is an inner automorphism. Hence, ψ is a product of Whitehead automorphisms. We may therefore move the base point around: every vertex can be chosen to be the base point.

Changing the orientation

It is convenient to change the orientation of identically labeled edges simultaneously. Consider a label y ∈ Y and then take λ' = iy ∘ λ as the new edge labeling. This gives a new pair (Γ' , Φ) and defines φ' : F(X) → F(Y) with iy ∘ φ' = φ.

If φ' = γ' ∘ π' for an inner automorphism γ' of F (Y) and a projection π, then we have φ = γ ∘ π for an inner automorphism γ of F (Y) and a projection π. This follows because iy ∘γ' ∘π(a) = iy(h)iy(π(a))iy (h)−1 for some h ∈ F(Y) and because π = iy ∘π' is a projection. Therefore, we may consider (Γ' , Φ) and φ' instead of (Γ, Φ) and φ. Thus, in the drawing: if y ∈ Y, then we are free to change the orientation of all arcs labeled by y without changing the label of these arcs.

Replacing λ(Φ(a)) by its inverse

Let a ∈ X and e = Φ(a) ∈ E \ T be a bridge. If we define Φ'(a) = e and Φ'(b) = Φ(b) for all a ≠ b ∈ X, then we obtain φ' = φ ∘ ia. Since ia is a Whitehead automorphism, in this situation we may consider Φ' and φ' instead of Φ and φ.

Changing the spanning tree

This is the heart of the process. A local change of the spanning tree causes a right multiplication by some Whitehead automorphism. Let A ∈ E \T be a bridge with s(A) = q ≠ 1 and t(A) = 1\. We want to construct a spanning tree T' that contains A, and we want to compute the homomorphism F (X) → F (Y) that results from the modified graphical realization. If there is a parallel edge e ∈ T, that is, s(e) = s(A), t(e) = t(A) with λ(A) = λ(e), then we simply replace A by e in the spanning tree. Now, let Φ(a) = A where a ∈ X. Consider the path T[1, q] = T[1, p] e with e ∈ T and s(e) = p, t(e) = q. This runs in the spanning tree from 1 to the source of A. We remove e, ē from T andwe insert A and Ā into the spanning tree. This defines a new spanning tree T. We define Φ'(a) = e; and for b ∈ X with b ≠ a, we let Φ'(b) = Φ(b). Note that e is a bridge in T'. Let φ' : F(X) → F(Y) be induced by ((1, V, E, T' , λ), Φ'). The path φ(a) = T[1, p]e A has not changed because T[1, p] = T'[1, p] and A = T[q, 1], hence φ(a) = φ(a). Now consider b ∈ X with b ≠ a. Then Φ(b) = B is still a bridge and we have

![](images/286_5.jpg)

There are now four different cases that exactly correspond to the distinctions in Whitehead automorphisms.

(a)The path T'[1, s(B)] begins with the edge Ā, but T'[t(B), 1] does not end with A. Then the following equations hold in the free group F (E+):

![](images/286_6.jpg)

(b)The path T'[1, s(B)] does not begin with the edge Ā, but T'[t(B), 1] ends with A. Then the following equations hold in the free group F (E+):

![](images/286_7.jpg)

(c)The path T'[1, s(B)] begins with the edge Ā and T'[t(B), 1] ends with A. Then the following equations hold in the free group F (E+):

![](images/286_8.jpg)

(d)The path φ(b) does not begin with the edge Ā and does not end with A. Then the whole path contains neither A or Ā. In this case we have φ(b) = φ(b).

The change of the spanning tree thus results in φ' : F(X) → F (Y) where φ = φ' ∘ψ and ψ is a Whitehead automorphism. The inverse of a Whitehead automorphism is a (product of) Whitehead automorphism(s). Hence, φ = φ' ∘ ψ−1. We may therefore change spanning trees in the described manner. This is explicitly done in [Example 8.35](#chapter08_4.xhtml_chapter08_4_4).

Since we also may change the orientation of equally labeled edges, we may assume the following, if necessary: if e, f are equally labeled edges which have the common source 1 and the targets p and q, respectively, and if further 1, p, and q are pairwise distinct, then the above method provides a spanning tree T with e, f ∈ T.

Determinization

We say that a graphical realization (Γ; Φ) is deterministic, if for each u ∈ V and each y ∈ Ỹ there is at most one vertex υ, which is the target t(e) for edges e with s(e) = u and λ(e) = y. Thus, for each word w = y1 ⋅⋅ ⋅ ym ∈ Ỹ∗ there is atmost one vertex q ∈ V, which is reachable from u by a path labeled with w.

Suppose that υ = s(e) = s(f) is the source of two edges e and f , which have the same label y = λ(e) = λ(f) but different final vertices p = t(e) ≠ t(f) = q. This violates the determinism. Note that the determinism is not violated by parallel edges, that is, if t(e) = t(f). We do not have to remove parallel edges with the same labels. They indicate that the homomorphism is not injective, but this fact becomes visible in the projection π at the end, too.

Without restriction we can assume that t(f) ≠ υ; otherwise we interchange the role of e and f . By changing the orientation, if necessary, we may assume that y ∈ Y. By moving the base point we may also assume that υ = 1\. In particular, 1 ≠ q. Furthermore, we may assume that f ∈ T is an edge in the spanning tree.

We now fold the graph along the edges e and f . This means, we identify e with f , ē with f̄, and p with q. Formally, we remove f and f̄ from E and hence also from T. All remaining edges with source or target q get the new source or target p. Finally, we remove the now isolated vertex q. Thus, we obtain a new graph Γ' = (1, V' , E' , T' , λ), which is still connected. Since we have removed exactly one vertex and exactly one undirected edge from T, then (V' , T) is a spanning tree of (V' , E).

Moreover, if 1 ≠ t(e), then we may assume, by the above construction, that e ∈ T is an edge of the spanning tree, too, because then e and f are equally labeled edges which both have the source 1 and the target p and q, respectively, where 1, p, and q are pairwise different. Then e ∈ T, and the folding of e and f does not change the outputs of φ in the group F (Y). This means, we have φ = φ.

![](images/288_1.jpg)

If 1 = t(e), then the situation is somewhat different. Now, e is a loop and thus a bridge. Therefore, there is exactly one a ∈ X̃ with Φ(a) = e, and we have φ(a) = λ(e) = y. Without loss of generality, let a ∈ X and y ∈ Y.

![](images/288_2.jpg)

We compute the new, induced homomorphism φ. We already saw that φ(a) = φ(a). Now, let a ≠ b ∈ X. For φ(b), there are again only the four cases we already know.

(a)φ(b) begins with f but does not end with f̄ .

(b)φ(b) does not begin not with f but ends with f̄ .

(c)φ(b) begins with f and ends with f̄ .

(d)φ(b) contains neither f nor f̄ .

The paths φ(b) arise out of the paths φ(b) by deleting all edges f and f̄ . However, a deletion changes the label and therefore the image in F (Y). To compensate for this, we emphasize that we do not delete the edges f and f̄ in φ(b), but replace f by e as well as f̄ by ē. After this modification, φ(b) becomes a word wb ∈ E ∗, and we obtain λ(φ(b)) = λ(wb)∈ F(Y). The word wb is a closed path in (V' , E), and according to the above cases, in F (Y), we obtain

(a)φ(b) = λ(wb) = λ(e) φ' (b) = φ(a)φ(b) = φ(ab)

(b)φ(b) = λ(wb) = φ(b) λ(ē) = φ(ba−1)

(c)φ(b) = λ(wb) = λ(e) φ' (b) λ(ē) = φ(aba−1)

(d)φ(b) = φ(b)

We remark that φ = φ' ∘ ψ for a Whitehead automorphism ψ.

The rose

By the above procedures, we finally obtain a deterministic graphical realization (̂Γ, ̂Φ) for a homomorphism ̂φ: F (X) → F (Y) such that

![](images/289_4.jpg)

In Equation ([8.9](#chapter08_4.xhtml_chapter08_4_10)), the mapping γ is an inner automorphism of F (Y), and ψ is a product of Whitehead automorphisms of F (X). With ̂Γ, we now can recognize if φ is surjective. First of all, this is the case if and only if ̂φ is surjective. Let us make a preliminary observation. Suppose, w = uzz̄υ is the label of a path in ̂Γ from 1 to 1 with u, υ ∈ Ỹ∗, and z ∈ Ỹ. By determinism an edge e corresponds to the position of z, and for z̄ we may choose the edge ē without changing the vertices on the path. Hence, uυ also describes a path from 1 to 1\. If ŵ is now the reduced word in Ŷ∗, which corresponds to w, then there is a path from 1 to 1, labeled with ŵ.

Suppose, φ is surjective, then certainly y ∈ φ(F(X)) = ̂φ(F(X)) for all y ∈ Y. The letter y is a reduced word and, by the preliminary consideration, the graph ̂Γ contains a loop at 1 labeled by y. This is a necessary condition. Conversely, the existence of these loops is sufficient to guarantee the surjectivity of φ.

For the final part in the proof of [Theorem 8.34](#chapter08_3.xhtml_chapter08_3_28), we may assume that φ: F (X) → F (Y) is surjective. As we have explained above, if y = φ(z), then

![](images/289_5.jpg)

Since an inner automorphism is a product of Whitehead automorphisms, the inner automorphism γ in Equation ([8.9](#chapter08_4.xhtml_chapter08_4_10)) is not needed. Thus, for some product of Whitehead automorphisms ψ of F (X), we may write

![](images/289_6.jpg)

The graph ̂Γ is deterministic, and since φ is surjective, for all y ∈ Y there exists a self-loop at 1 with label y. Thus, there can be no other vertices because of determinism. The final graph ̂Γ is therefore a rose: a graph with one vertex 1, in which the set of loops can be identified with X̃. Therefore, we have λ̂= ̂φ for the labeling and π = ̂φ for the desired projection from F (X) on F (Y). As mentioned above, our notion of determinism does not exclude parallel edges. Thus, we may have |X| > |Y| and several x ∈ X can be mapped to the same y. If this happens, then φ is not injective and parallel self-loops with the same label appear in the rose. This concludes the proof of [Theorem 8.34](#chapter08_3.xhtml_chapter08_3_28).

## 8.12 The special linear group SL(2, ℤ)

The special linear group SL(2, ℤ) consists of all 2 ×2 matriceswith integer coefficients and determinant 1\. This group acts on the complex numbers without the rational numbers by linear fractional transformations: if ![](images/290_1.jpg) and z ∈ ℂ\ℚ, we set

![](images/290_2.jpg)

Since ![](images/290_3.jpg) we have M ⋅ z ∈ ℚonly if z itself is rational. The group SL(2, ℤ) acts on the upper half plane ℍ = {z ∈ ℂ| im(z) > 0 }, and also analogously on { z ∈ ℂ| im(z) < 0 } and ℝ \ ℚ. To see this, write z = r + is and z = r − is with r, s ∈ ℝ. Then

![](images/290_4.jpg)

Since zz̄ ∈ ℝand ad −bc = 1, we obtain that the imaginary part in ![](images/290_12.jpg)is im(z) up to a multiplication by a positive real number. Moreover, the operation is a group operation

![](images/290_5.jpg)

Also M ⋅ z = z for all z if and only if ![](images/290_6.jpg) or ![](images/290_7.jpg) The kernel of the homomorphism corresponding to the group operation is therefore exactly the subgroup {±1} ⊆ SL(2, ℤ), which is also the center of SL(2, ℤ). In general, the center of a group is the subgroup of those elements which commute with all other elements of the group. In particular, the center is a normal subgroup.

The modular group PSL(2, ℤ) is defined as the quotient SL(2, ℤ)/{±1}. Especially, the homomorphism of PSL(2, ℤ) into the group of all invertible maps from ℍ to ℍ is injective. In other words, PSL(2, ℤ) is a discrete subgroup of the group of linear fractional transformations from ℍ to ℍ, in particular, PSL(2, ℤ) acts “faithfully” on the upper half plane. The topic of this section is to give algebraic descriptions of SL(2, ℤ) and PSL(2, ℤ). We will show that SL(2, ℤ) is the amalgamated product of ℤ/4ℤ and ℤ/6ℤsuch that the amalgamation is over their respective cyclic subgroups of order 2; and the modular group is the free product of ℤ/2ℤ and ℤ/3ℤ. We start with the study of the matrices in SL(2, ℤ) without negative entries. This forms a monoid, henceforth denoted by SL(2, ℕ). We will see that SL(2, ℕ) is the free monoid on two generators T and U where T, U ∈ SL(2, ℕ) are given by

![](images/290_8.jpg)

Proposition 8.36. The monoid SL(2, ℕ) is free with basis {T, U}.

Proof: Let ![](images/290_9.jpg) with a, b, c, d ≥ 0\. Then a ≥ c or d ≥ b because ad − bc = 1\. Suppose that a > c and d > b. Then

![](images/290_11.jpg)

and, hence, b = c = 0 and a = d = 1\. Therefore, (a − c)(b − d) ≥ 0 for ![](images/291_1.jpg) That is, if ![](images/291_2.jpg) is not the identity matrix, then either the upper row is strictly greater than the lower, row or, conversely, the lower row is strictly greater than the upper row. Note that a = c and b = d is impossible. A row is strictly greater than another one if, first, it is greater or equal in both components and, second, strictly greater in at least one component. Next, we show that the monoid SL(2, ℕ) is freely generated by T and U. We have

![](images/291_3.jpg)

This shows that every product of a (nonempty) sequence of T’s and U’s results in a matrix with one row strictly greater than the other one. Moreover, each matrix in SL(2, ℕ) can uniquely be written as a product of T’s and U’s. This is true for the identity matrix, which corresponds to the empty word. Now, let ![](images/291_4.jpg) be a matrix in which the upper row is strictly greater than the lower row. Note that c +d > 0\. Then a' = a +c and b' = b + d for a, b ∈ ℕ and

![](images/291_5.jpg)

Thus the first factor must be T. Since a + b + c + d < a' + b' + c + d, we can now decompose ![](images/291_6.jpg) inductively. If the lower row is strictly greater than the upper row, then the first factor is U, and the induction argument remains unchanged.

□

The geometric interpretation of the matrices T and U is given by their effect on a complex number z with im(z) > 0\. For each n ∈ ℤ, we obtain

![](images/291_7.jpg)

In particular, the matrices T and U have both infinite order. Next, we consider the two matrices S, R ∈ SL(2, ℤ) given by

![](images/291_8.jpg)

We have S2 = −1 and R3 = −1; hence, S has order 4 and R has order 6\. Moreover, −R = ST and ![](images/291_9.jpg) Geometrically (in the complex plane) we may interpret S, T, R, and R2 as follows:

![](images/291_10.jpg)

Hence S(z) is an involution, T(z) a translation, and R(z) a rotation of order 3\. Recall that R has order 6 in SL(2, ℤ), but, in the quotient group PSL(2, ℤ), its order is 3.

Lemma 8.37. Any two of the four matrices R, S, T, U generate the group SL(2, ℤ).

Proof: Any two of the four matrices generate the three matrices R, T and U by the above formulas, and hence, also S. This follows by an extensive case distinction. For instance, if we have T and U then we obtain R−1 = R5 by

□

![](images/292_7.jpg)

Now, let ![](images/292_2.jpg) We show that A is in the subgroup generated by S, T, and U. If c = 0 then d ≠ 0, and we replace A by AS. If c < 0 then we replace A by −A = S2A. Now we may assume that c > 0\. If we replace A by TnATn for a sufficiently large n, then, without loss of generality, we obtain a, b, c, d > 0\. Now A is already in the submonoid generated by T and U ([Proposition 8.36](#chapter08_4.xhtml_chapter08_4_13)). This proves the lemma.

Theorem 8.38. The groups PSL(2, ℤ) and SL(2, ℤ) have a presentation with R and S as generators and S2 = R3 = 1 or S4 = R6 = S2R3 = 1, respectively, as defining relations. Consequently, PSL(2, ℤ) is the free product of ℤ/2ℤ and ℤ/3ℤ, and SL(2, ℤ) is the amalgamated product of ℤ/4ℤ with ℤ/6ℤ such that the amalgamation is over their respective cyclic subgroups of order 2.

Proof: The product of the two cyclic groups ℤ/2ℤ and ℤ/3ℤ has a presentation G' = {r, s}∗/{s2 = r3 = 1}. The amalgamated product of ℤ/4ℤ and ℤ/6ℤ, with amalgamation of their respective cyclic subgroups of order 2, has a presentation G = {r, s}∗/ {s4 = r6 = 1, s2 = r3}. Consider the homomorphisms φ: G → SL(2, ℤ) and φ' : G' → PSL(2, ℤ) induced by r ↦ R and s ↦ S. Both homomorphisms are surjective by [Lemma 8.37](#chapter08_4.xhtml_chapter08_4_16). Now, let w ∈ {r, s}∗ with φ(w) = 1 and φ(w) = 1, respectively. If w ∈ s∗ then it follows already w = 1 in G and w = 1 in G, respectively. The analogous statement holds for w ∈ r∗. Each element of G (respectively G), which is not in the subgroup generated by a conjugate of s or r, can be written as a word w = sj0 ri1 (sri2 )⋅ ⋅⋅ (srim )sjm with m ≥ 1 and 0 ≤ j0 ≤ 3 (respectively 0 ≤ j0 ≤ 1), 0 ≤ jm ≤ 1, and 1 ≤ ik ≤ 2 for 1 ≤ k ≤ m. Note that in G, we can move the factors s2 and r3 to the left, and that we have s2 = r3. The only difference between G and G' is the range of j0\. The values for j0 are 0, 1, 2, 3 in G and 0, 1 in G. It is enough to show that φ(w) ≠ 1 for such a word w. After a suitable conjugation with r or r2, if necessary, we may assume that w = ri1 s ⋅⋅ ⋅ rim−1 srim , m ≥ 2, with 1 ≤ ij ≤ 2 for j = 1, . . . , m and 1 ≤ i1, im ≤ 2\. Now, we apply a ping-pong argument: the modular group also operates on ℝ \ ℚ by virtue of the above formulas. We obtain ![](images/292_3.jpg) , ![](images/292_4.jpg) and ![](images/292_5.jpg) . In particular, R and R2 map positive values to negative ones, and S maps negative values to positive ones. Hence, if we apply φ(w) on any arbitrary positive, irrational number like ![](images/292_6.jpg) then we obtain a negative value for φ(w)(z). This implies φ(w) ≠ 1.Since T and U generate a free submonoid in the group SL(2, ℤ), we might suspect that they generate a free subgroup in SL(2, ℤ). But this is in contradiction to [Lemma 8.37](#chapter08_4.xhtml_chapter08_4_16) because SL(2, ℤ) contains elements of order 4\. Nevertheless, both SL(2, ℤ) and PSL(2, ℤ) contain all free groups with finite or countable rank. To show this, it is enough to prove the existence of a subgroup of rank 2\. For this purpose, we consider the following two matrices in SL(2, ℤ):

□

![](images/293_1.jpg)

Corollary 8.39. The matrices A and B generate a free subgroup of rank 2 of the modular group PSL(2, ℤ) and, therefore, also of the group SL(2, ℤ).

Proof: Let W ∈ PSL(2, ℤ) be a nonempty reduced word in A, A−1, B and B−1, written in terms of R and S. By [Theorem8.38](#chapter08_4.xhtml_chapter08_4_17), we may write PSL(2, ℤ) as {R, S}∗/{S2 = R3 = 1}, and we obtain normal forms by cancelling the factors S2 and R3 in W. The normal forms for A, A−1, B, and B−1 are A = RSR, A−1 = R2SR2, B = SRSRS, and B−1 = SR2SR2S.

□

We have to show that W ≠ 1 in PSL(2, ℤ). For this purpose, it is enough to prove by induction that the last letter X ∈ {A, A−1, B, B−1} of W determines the last three letters of the normal form of W in {R, S}∗: for X = A it is RSR, for X = A−1 it is SR2, for X = B it is SRS, and for X = B−1 it is R2S. In particular, the normal form is not the empty word, and therefore W ≠ 1 in PSL(2, ℤ).

Remark 8.40. The embedding of the free group of rank 2 in the group SL(2, ℤ) gives another proof of [Proposition 8.12](#chapter08_1.xhtml_chapter08_1_48). Since SL(2, ℤ) is residually finite, free groups are residually finite, too. In order to see this, it is enough to consider free groups of finite rank; and free groups of finite rank can be embedded into a free group of rank 2 by [Exercise 8.8](#chapter08_4.xhtml_chapter08_4_28), which appears as a subgroup of SL(2, ℤ).

◊

The Baumslag–Solitar group BS(2, 3) from [Example 8.8](#chapter08_1.xhtml_chapter08_1_36) is not Hopfian by [Exercise 8.10](#chapter08_4.xhtml_chapter08_4_30). Hence, it is not residually finite by [Exercise 8.9](#chapter08_4.xhtml_chapter08_4_29). Therefore, in contrast to free groups, BS(2, 3) cannot be embedded into SL(2, ℤ) or into any other linear group.

## Exercises

8.1. Let M = Σ∗/S for a finite length reducing and confluent semi-Thue system S. Show that the word problem for M is decidable in linear time.

8.2. Prove [Proposition 8.11](#chapter08_1.xhtml_chapter08_1_47), that is, show that all residually finite and finitely presented monoids have a decidable word problem.

8.3. Let (Σ, I) be a finite, undirected graph and let

![](images/293_2.jpg)

be the corresponding free partially commutative monoid. A transitive orientation of (Σ, I) is a subset I+ ⊆ I with I = {(a, b), (b, a) | (a, b) ∈ I+ } such that (a, b), (b, c) ∈ I+ implies (a, c) ∈ I+. Show:

(a)Let I+ ⊆ I be a transitive orientation of (Σ, I). Then the semi-Thue system S+ = { ba → ab | (a, b) ∈ I+ } is convergent.

(b)Let S ⊆ Σ2 × Σ2 be a convergent semi-Thue system with Σ∗/S = M(Σ, I). Then I+ = {(a, b) ∈ Σ × Σ | ab ∈ IRR(S) } is a transitive orientation of (Σ, I).

(c)Let M(Σ, I) and M(Σ' , I) be isomorphic, that is, M(Σ, I) ≅ M(Σ' , I). Then the graphs (Σ, I) and (Σ' , I) are isomorphic.

(d)Let M(Σ, I) ≅ (ℕ×ℕ) ∗ℕ. Then the transposition relation (uυ, υu) in M(Σ, I) is not transitive.

(e)How many vertices does the smallest graph without a transitive orientation contain?

8.4. Let C(Σ, I) = Σ∗/{ a2 = 1, ab = ba | (a, b) ∈ I } be a finitely generated right-angled Coxeter group.

(a)Construct a convergent semi-Thue system SRACG ⊆ Σ∗ × Σ∗, which represents C (Σ, I) such that almost all rules are length preserving.

(b)Let G = G(V, E) be a graph group. Find an embedding of G in a Coxeter group C = C(Σ, I).

(c)For (Σ, I) let F be the set of cliques, that is,

![](images/294_4.jpg)

Consider the finite semi-Thue system T ⊆ F∗ × F∗ with the rules

![](images/294_3.jpg)

Show: T is convergent and F∗/ T is isomorphic to the Coxeter group C (Σ, I).

8.5. Show that the class of rational sets is closed under homomorphisms, but not closed under inverse homomorphisms.

Hint: For the nonclosure use the standard fact that { anbn | n ∈ ℕ} is not rational (i.e., regular) for a two letter alphabet {a, b} and that the family RAT({a, b}∗) is closed under intersection.

8.6. Let M = {a, b, c}∗/{ac = ca, bc = cb} be the direct product of the free monoids c∗ and {a, b}∗. Show that the family of rational sets RAT(M) is not closed under intersection. Hint: Reuse ideas from [Exercise 8.5](#chapter08_4.xhtml_chapter08_4_26).

8.7. Show that in free groups, the intersection of two finitely generated subgroups is finitely generated.

Hint: Use that the set of reduced words which belong to a finitely generated subgroup is regular.

8.8. Let F ({a, b}) = F2 be the free group with two generators. Show that the set U = { anba−n | n ∈ ℤ} ⊆ F2 is the basis of a free subgroup. In particular, F2 contains each

free group of finite or countable rank as a subgroup.

8.9. Show that finitely generated, residually finite groups are Hopfian.

8.10. Show that the Baumslag–Solitar group BS(2, 3) = {a, t}∗/{ta2t−1 = a3} is not Hopfian.

8.11. Show that, during the normal form computation (corresponding to [Example 8.20](#chapter08_2.xhtml_chapter08_2_28)) in the group BG(1, 2), extremely long words may arise; for instance, words of the form aτ(n). Here τ : ℕ → ℕis the tower function defined by τ(0) = 1 and τ(n + 1) = 2τ(n).

8.12. Let G be a non-Abelian finite group and let Z (G) denote its center, that is Z (G) = { g ∈ G | ∀h ∈ G: gh = hg }. Show that the index of Z(G) is at least 4.

Using this fact, answer the following question. “What is the probability that two group elements commute?” More precisely, we seek an upper bound for the probability in non-Abelian finite groups, which is tight for certain groups. The answer has been given in a paper (with the question as its title) published by Gustafson in 1973.

8.13. Use [Theorem 6.5](#chapter06.xhtml_chapter06_9) for proving [Corollary 8.30](#chapter08_3.xhtml_chapter08_3_20): commuting elements in a free group lie in a common cyclic subgroup.

8.14. In this exercise, we will show that the automorphism group of a finitely generated free group F (Σ) is generated by at most four elements.

(a)For a ∈ Σ, we define the automorphism ia by ia(a) = a−1 and ia(c) = c for a ≠ c ∈ Σ. For b ∈ Σ with a ≠ b, we further define the automorphisms λab and ρbā by λab(b) = ab, ρbā(b) = ba−1 and λab(c) = ρbā(c) = c for b ≠ c ∈ Σ. (Recall that the automorphisms ia and λab are referred to as the elementary Nielsen transformations.)

First, show that the automorphisms ρba may be expressed by elementary Nielsen transformations. Then use [Theorem 8.34](#chapter08_3.xhtml_chapter08_3_28) to show that the automorphism group of F (Σ) can be generated by the elementary Nielsen transformations.

(b)Show that the automorphism group of F (Σ) is generated by atmost four elements. Moreover, show that three generators are sufficient if F (Σ) has rank 2.

8.15. By [Proposition 8.36](#chapter08_4.xhtml_chapter08_4_13), all words over the alphabet {T, U} (and hence also all bit sequences in {0, 1}∗) may be encoded as 2 × 2-matrices with entries in ℕ. Moreover, each matrix in SL(2, ℕ) describes a unique word in {T, U}∗. Now, let W ∈ {T, U}∗ be a word of length ℓ and let ![](images/295_1.jpg)be the corresponding matrix product. Show that ai ≤ Fℓ+1 for i = 1, 2, 3, 4, where Fℓ+1 is the (ℓ + 1)th Fibonacci number. As usual, F0 = 0, F1 = 1, and Fn+1 = Fn + Fn−1 for n ≥ 1.

8.16. Let A ∈ PSL(2, ℤ) be an element in the modular group of order 2 and ![](images/296_1.jpg) Furthermore, let S ∈ PSL(2, ℤ) with ![](images/296_2.jpg)

(a)Show that a + d = 0.

(b)Show that A and S are conjugated in PSL(2, ℤ).

Hint: Use the normal form Ri1S ⋅⋅ ⋅ Rim−1SRim , m ≥ 2, 1 ≤ ij ≤ 2 for j = 1, . . . , m and i1 = im, as in the proof of [Theorem 8.38](#chapter08_4.xhtml_chapter08_4_17).

8.17. Let n ∈ ℕ, n ≥ 1\. Prove Fermat’s theorem on sums of two squares:

(a)If −1 is a quadratic residue modulo n, that is, −1 ≡ q2 mod n for some q ∈ ℤ, then n is a sum of two squares in ℤ, that is, n = x2 + y2 with x, y ∈ ℤ.

Hint: If −1 ≡ q2 mod n, then there exists p ∈ ℤ with q2 + pn = −1\. Form A(z) = ![](images/296_3.jpg) By [Exercise 8.16 (b)](#chapter08_5.xhtml_chapter08_5_2) the element A ∈ PSL(2, ℤ) is conjugated to S, that is, there exists X ∈ PSL(2, ℤ) with ![](images/296_4.jpg) and XSX−1 = A.

(b)If n = x2 + y2 with x, y ∈ ℤ and gcd(x, y) = 1, then −1 is a square modulo n.

(c)Use [Exercises 8.17 (a)](#chapter08_5.xhtml_chapter08_5_3) and [8.17 (b)](#chapter08_5.xhtml_chapter08_5_4) for showing that a prime number p is a sum of two squares if and only if p = 2 or p ≡ 1 mod 4.

## Summary

Notions

–word problem

–conjugacy problem

–isomorphism problem

–residually finite monoid

–Hopfian group

–presentations of monoids and groups

–rewriting system

–confluence, termination, convergence

–Church–Rosser property

–semi-Thue system

–free group

–free product

–Baumslag–Solitar group BS(p, q)

–Waack group W

–Tietze transformation

–free partially commutative monoid

–graph group

–semidirect product

–amalgamated product

–HNN extension

–Britton reduction

–Baumslag group

–rational set

–rank

–(kernel of the) Schreier graph

–Whitehead automorphism

–Nielsen transformation

–graphical realization

–special linear group SL(2, ℤ)

–modular group PSL(2, ℤ)

Methods and results

–Finitely generated residually finite groups are Hopfian.

–Strong confluence ⇒confluence.

–Confluence ⇔Church–Rosser

–Local confluence and termination ⇒confluence.

–Local confluence can be tested based on critical pairs.

–If S ⊆ Γ∗ × Γ∗ is a finite convergent semi-Thue system, then the word problem in Γ∗/S is decidable.

–Residually finite, finitely presented monoids have a decidable word problem.

–Free groups are residually finite.

–Trace monoids embed into RAAGs and their word problem can be solved in linear time.

–Convergent systems for amalgamated products and HNN extensions.

–Groups embed themselves into their amalgamated products and HNN extensions.

–1 ≠ w ∈ G ∗U H or 1 ≠ w ∈ HNN(G; A, B, φ) ⇒ w is Britton reducible.

–Subgroups are rational subsets if and only if they are finitely generated.

–Benois: rational subsets of a finitely generated free group form an effective Boolean algebra.

–Free groups are isomorphic if and only if their bases have the same cardinality.

–If K(G, Σ) is the kernel of the Schreier graph with edge set E and spanning tree T, then G is isomorphic to the free group F (E+ \ T).

–Nielsen–Schreier theorem: subgroups of free groups are free.

–F finitely generated free group and |G \ F| = n < ∞, then the rank formula (rank(F) − 1) ⋅ n = rank(G) − 1 holds.

–Word / conjugacy / isomorphism problems are decidable for finitely generated free groups.

–Aut(F) is finitely generated by the Whitehead automorphisms.

–The monoid SL(2, ℕ) is free with basis {T, U}.

–SL(2, ℤ) = {R, S}∗/{S4 = R6 = S2R3 = 1} and PSL(2, ℤ) = {R, S}∗/{S2 = R3 = 1} (ping–pong argument)

–Countable free groups are subgroups of PSL(2, ℤ) and SL(2, ℤ).

# Solutions to exercises

## Chapter 1

1.1. Suppose that e and f are neutral. Then, e = ef = f .

1.2. Suppose that y and z are inverses of x, in particular, yx = 1 = xz. Then, y = y ⋅1 = yxz = 1 ⋅ z = z.

1.3. We consider the mapping δ : M → M with δ(x) = ax. It is injective since δ(x) = δ(y) implies x = 1 ⋅ x = bax = b ⋅ δ(x) = b ⋅ δ(y) = bay = 1 ⋅ y = y. Then, δ is also surjective because M is finite. Let c be the element in M that is mapped to 1 ∈ M, that is, 1 = δ(c) = ac. Then, b = b ⋅ 1 = bac = 1 ⋅ c = c and therefore ab = 1.

1.4. The set of all mappings f : ℕ → ℕ forms an infinite monoid with composition as operation. The neutral element is the identity mapping id with id(n) = n. Let a: ℕ→ℕ with a(0) = 0 and a(n) = n − 1 for n ≥ 1\. For the mapping b : ℕ→ℕwith b(n) = n + 1, we have a ∘ b = id, but from (b ∘ a)(0) = b(a(0)) = b(0) = 1, we obtain b ∘ a ≠ id.

1.5. Define c = bab. Then, aca = ababa = aba = a and cac = bababab = babab = bab = c.

1.6 (a) Since S is finite, there are t, p ≥ 1 with xt = xt+p. It follows xj = xj+ℓp for all j ≥ t and ℓ ≥ 0.

![](images/298_1.jpg)

Let k be minimal such that t ≤ kp < t + p. Then, xkp is idempotent since xkp+ip = xkp for all i ≥ 0\. Thus, {xt , xt+1, . . . , xt+p−1} is a cyclic subgroup of order p which has the idempotent element xkp as a neutral element; and we have 1 ≤ kp ≤ |S|. There is only one power of x which is idempotent: it is xkp. Indeed, let xm and xn be idempotent. Then, xn = (xn)2 = (xn)3 = ⋅⋅ ⋅ and thus xm = (xm)n = xmn = (xn)m = xn.

1.6 (b) [Exercise 1.6 (a)](#chapter01_4.xhtml_chapter01_4_19) shows that xℓ is idempotent for some 1 ≤ ℓ ≤ |S|. This implies xmℓ = xℓ for all m ≥ 1\. Therefore, x|S|! is idempotent for all x ∈ S.

1.7. Let x ∈ H and g = φ(x) ∈ G. Then, e = xn ∈ H is idempotent for some n ≥ 1 by [Exercise 1.6 (b)](#chapter01_4.xhtml_chapter01_4_20). We have φ(e) = 1 and therefore φ(eHe) = G. Since eHe ⊆ H and H is minimal, we conclude eHe = H. The element e is neutral in eHe, hence neutral in H. Finally, consider the subset xH of M. It is subsemigroup with φ(xH) = gG = G. Hence, xH = H by minimality of H. Thus, there is some y ∈ H with xy = e. By [Exercise 1.3](#chapter01_4.xhtml_chapter01_4_17), we also have yx = 1\. This shows that H is a group.

1.8 (a) Let e, f be idempotent and ![](images/299_1.jpg) We have ef ⋅ xe ⋅ ef = ef ⋅ x ⋅ ef = ef and xe ⋅ ef ⋅ xe = (x ⋅ ef ⋅ x) ⋅ e = xe. This shows xe = x. Symmetrically, we obtain fx = x. Now, x2 = xe ⋅ fx = x.

1.8 (b) If e is idempotent, then eee = e and hence e = e. Since ![](images/299_2.jpg) for all elements x, [Exercise 1.8 (a)](#chapter01_4.xhtml_chapter01_4_21) shows that ef is idempotent whenever e, f are idempotent. In particular, the impotent elements form a subsemigroup. Finally, ef⋅fe⋅ef = ef⋅ef = ef and fe ⋅ ef ⋅ fe = fe ⋅ fe = fe. This yields ![](images/299_3.jpg) Hence, the subsemigroup of the idempotents is commutative.

1.9. Let an+1 be an arbitrary element in S. Consider the n +1 elements a1 ⋅⋅ ⋅ ai for 1 ≤ i ≤ n + 1\. By the pigeonhole principle, we have a1 ⋅⋅ ⋅ ai = a1 ⋅⋅ ⋅ aj for 1 ≤ i < j ≤ n + 1\. In particular, i ≤ n. For b = ai+1 ⋅⋅ ⋅ aj, we obtain a1 ⋅⋅ ⋅ ai = a1 ⋅⋅ ⋅ aib, as desired.

1.10. Let X be a finite set with 1 U ∉ X. Then, UX = X ∪ {1U} with the operation ab = b for b ∈ X and ab = a for b = 1U forms a monoid with |X| + 1 elements. For Y ⊆ X, UY is a submonoid of UX. We choose X such that |X| is even and Y ⊆ X such that |Y| odd. Now M = UX and U = UY meet the requirements of the exercise.

1.11. Show associativity of ∘ as follows:

![](images/299_5.jpg)

1.12. Let G be a group and x2 = x for some x ∈ G. Let y be the inverse of x, that is, xy = 1\. Then, x = xxy = xy = 1\. Next, let M be finite monoid and let 1 be the only idempotent. Then, as each x has some idempotent power xω with ω ≥ 1 (see [Exercise 1.6 (a))](#chapter01_4.xhtml_chapter01_4_19), we conclude that xω = 1\. Hence, xω−1 is an inverse of x.

1.13 (a) First, we show that every left inverse element is also right inverse. Let h be the left inverse element of g and g' the left inverse element of h. Then, hg = e and gh = e and therefore gh = egh = ghgh = geh = gh = e. Thus, h is the inverse of g. Further, we conclude ge = ghg = eg = g.

1.13 (b) Let |G| > 1 be any set. Define the operation by xy = x for all x, y ∈ G. Then each element e ∈ G satisfies the conditions but G is not a group.

1.13 (c) Let a ∈ G be fixed. There exists e ∈ G with ea = a. For all b ∈ G there exists x ∈ G such that b = ax. Thus, eb = eax = ax = b and e is left neutral. Left inverse elements exist as solutions of ya = e. Thus, G is a group by [Exercise 1.13 (a)](#chapter01_4.xhtml_chapter01_4_23).

1.14 (a) (i) ⇒ (ii): We have 1 ∈ S, so S ≠ 0\. Moreover, for all y ∈ S, also y−1 is in S. Therefore, we have xy−1 ∈ S for all x, y ∈ S. (ii) ⇒ (i): S ≠ 0, so there exists x ∈ S. Thus also 1 = x ⋅ x−1 ∈ S and furthermore x−1 = 1 ⋅ x−1 ∈ S. The closure of S under the group operation follows from xy = x(y−1)−1 ∈ S. Consequently, S is a subgroup of G.

1.14 (b) (i) ⇒ (ii): This follows because S is closed under the group operation and 1 ∈ S. (ii) ⇒ (i): Let x ∈ S. Since S is finite and xi ∈ S for all i > 0, the order r of x is finite. Therefore, 1 = xr ∈ S and x−1 = xr−1 ∈ S. Thus, S is a group.

1.14 (c) Let G be the additive group ℤ and S = ℕ. Then, S is closed under addition but S is not a group.

1.15. (i) ⇒ (ii) is trivial. (ii) ⇒ (i): We have φ(1G) = φ(1G ⋅ 1G) = φ(1G)φ(1G). By [Exercise 1.12](#chapter01_4.xhtml_chapter01_4_22), we have φ(1G) = 1H. Moreover, φ(x−1) = φ(x−1)φ(x)φ(x)−1 = φ(x−1x)φ(x)−1 = 1H ⋅ φ(x)−1 = φ(x)−1.

1.16. By m2 = 1, the element m itself is the inverse of m ∈ M. Furthermore, mn = m ⋅ 1 ⋅ n = m(mn)(mn)n = mm(nm)nn = 1 ⋅ nm ⋅ 1 = nm for all m, n ∈ M. Thus, M is a commutative group.

1.17. Let U be the set of elements having odd order. We have 1 ∈ U, thus U is not empty. We show that U forms a subgroup of G. Let x, y ∈ U and let k be the order of x and ℓ the order of y. Since G is commutative, we have (xy−1)kℓ = xkℓy−kℓ = (xk)ℓ(yℓ)−k = 1\. So, the order of xy−1 divides kℓ. Since kℓ is odd, so is the order of xy−1 and therefore xy−1 ∈ U. [Exercise 1.14 (a)](#chapter01_4.xhtml_chapter01_4_25) yields the desired result.

1.18. Since H is a subgroup, we have HH = H = H −1. Therefore, we can conclude from xH = yH that xHx−1 = xHHx−1 = xHH−1x−1 = xH(xH)−1 = yH(yH)−1 = yHH−1y−1 = yHHy−1 = yHy−1.

1.19 (a) Let g ∈ G. From [G : H] = n, we obtain |{giH | i ≥ 0}| ≤ n. So, there are 0 ≤ j < k ≤ n with gjH = gkH. Multiplying on the left by g−j yields H = gk−jH and thus gk−j ∈ H. Note that i = k − j satisfies 1 ≤ i ≤ n.

1.19 (b) We consider the mapping π : G → SG/H into the symmetric group, where π(g) : G/H → G/H is the mapping xH ↦ gxH. The mapping π is a homomorphism and ker(π) = N. Thus, N is a normal subgroup and |G/N| ≤ n! by the homomorphism theorem. It remains to show that N is the largest normal subgroup contained in H. For this purpose, let K ⊆ H be a normal subgroup of G. Then, K = xKx−1 ⊆ xHx−1 for all x ∈ G. But then, we also have K ⊆ ⋂x∈G xHx−1 = N.

1.20. Let D4 be the symmetry group of a regular rectangle with vertex set {0, 1, 2, 3} as in [Section 1.2](#chapter01_1.xhtml_chapter01_1_28). This group has eight elements and is generated by a rotation δ : n ↦ n + 1 mod 4 and a reflection σ. Remember that σ leaves the vertices 0 and 2 fixed and swaps 1 and 3\. Let τ be the reflection that leaves the vertices 1 and 3 fixed and interchanges 0 and 2\. The subgroup K = 〈σ, τ〉 has index 2 in D4 and is therefore normal. (The group K is isomorphic to the Klein four-group.) Clearly, 〈σ〉 is a normal subgroup of K. Finally, we have δσδ−1 = τ ∉ 〈σ〉 and thus 〈σ〉 is not a normal subgroup of D4.

1.21. First, let G be commutative. Then, f is a group homomorphism because f(x ⋅ y) = (x ⋅ y)−1 = y−1 ⋅ x−1 = x−1 ⋅ y−1 = f(x) ⋅ f(y). Now, let f be a group homomorphism. Then, x ⋅ y = (y−1 ⋅ x−1)−1 = f(y−1 ⋅ x−1) = f(y−1) ⋅ f(x−1) = y ⋅ x. We conclude that G is commutative.

1.22. Let n be the order of a. Then, f(a)n = f(an) = f(1) = 1\. Thus, the order of f(a) divides n.

1.23. Let 0 ≠ r ∈ R. Then the mapping s ↦ sr is injective since sr = sr implies (s − s')r = 0 and thus s − s' = 0\. Due to the finiteness of R, the mapping is also surjective. Therefore, there is a left inverse s of r such that sr = 1\. [Exercise 1.13 (a)](#chapter01_4.xhtml_chapter01_4_23) shows that (R \ {0}, ⋅, 1) is a group and thus R is a skew field.

Remark: Wedderburn’s theorem (named after Joseph Henry Maclagan Wedderburn, 1882–1942) states that every finite skew field is already a field, which means that R, under the given circumstances, is even commutative. Ernst Witt (1911–1991) found a proof in the early 1930s, which even nowadays is still considered to be the simplest one for this result [[1](#Bibliography.xhtml_Bibliography_2)].

1.24. (i)⇒(ii): Let I be an ideal. Then, (I, +, 0) is a normal subgroup of (R, +, 0), and by [Theorem 1.10](#chapter01_1.xhtml_chapter01_1_21), the quotient (R/I, +, I) is a group. Moreover, for the product of the sets r1+I and r2+I,wehave that (r1+I)⋅(r2+I) ⊆ r1r2+r1I+r2I+I⋅I ⊆ r1r2+I+I+I = r1r2+I. Let r1 + I = s1 + I and r2 + I = s2 + I. Then there are i1, i2 ∈ I such that s1 = r1 + i1 and s2 = r2 + i2. Thus, we obtain (s1 + I)(s2 + I) ⊆ s1s2 + I = (r1 + i1)(r2 + i2) + I = r1r2 + r1i2 + r2i1 + i1i2 + I ⊆ r1r2 + r1I + r2I + I + I ⊆ r1r2 + I. This shows that the multiplication given by (r1 + I, r2 + I) ↦ r + I with (r1 + I)(r2 + I) ⊆ r + I is well defined. The associativity of multiplication and the distributive lawon R /I now follow fromthe corresponding laws on R.

(ii)⇒(iii): Let R/I be a ring. Then, φ: R → R/I, r ↦ r + I by [Theorem 1.10](#chapter01_1.xhtml_chapter01_1_21) is a group homomorphism with respect to addition and its kernel is I. It remains to show that φ is a ring homomorphism. We have φ(1) = 1 + I and 1 + I is the neutral element with respect to multiplication in R/I. Furthermore φ(r1)φ(r2) = (r1 + I)(r2 + I) = r1r2 + I = φ(r1r2).

(iii)⇒ (i): Let φ: R → S be a homomorphism of commutative rings with kernel I. By [Theorem 1.10](#chapter01_1.xhtml_chapter01_1_21) I is a normal subgroup of R and thus in particular a subgroup. For r ∈ R, we have φ(rI) = φ(r)φ(I) = φ(r) ⋅ {0} = {0}. Thus, rI is a subset of the kernel I of φ. This shows that I is an ideal.

1.25. We consider the mapping φ: R/I → R/J, r + I ↦ r + J. This mapping is well defined and surjective since I ⊆ J. From (r1 + J) ⋅ (r2 + J) = r1r2 + J, we see that φ is a homomorphism. Let φ(r + I) = J. This is the case if and only if r + J = J. And this, in turn, is the case if and only if r ∈ J. Therefore, ker(φ) = J/I. The claim now follows using the homomorphism theorem.

1.26. (i) If i1, i2 ∈ I and j1, j2 ∈ J, then (i1 + j1) + (i2 + j2) = (i1 + i2) + (j1 + j2)∈ I + J. Hence, I +J is a commutative subgroup because the according properties transfer from I and J to I + J. Moreover, r1(i + j)r2 = r1ir2 + r1jr2 ∈ I + J for i ∈ I, j ∈ J and r1, r2 ∈ R. Thus, I + J is an ideal.

(ii) Consider I = J = 〈X, Y〉 in R = F[X, Y] for a field F. We have X3, Y3 ∈ I ⋅ J. If I ⋅ J is an ideal, then X3 + Y3 ∈ I ⋅ J, that is, X3 + Y3 = (aX + bY)(cX + dY) = acX2 + (ad + bc)XY + bdY2 for suitable a, b, c, d ∈ F[X, Y]. But then the degree of ac must be 1\. Without loss of generality let a = X. Then, dX + bc has to be 0. However, since neither b nor c can contain an X, there is no solution to the equation dX +bc = 0\. So the (complex) product of two ideals, in general, is not an ideal itself.

(iii) We consider I = 〈X〉 and J = 〈Y〉 in R = F[X, Y]. Then, X, Y ∈ I ∪ J, but X + Y ∉ I ∪ J. So in general, I ∪ J is not an ideal.

(iv) The intersection of two groups is a group itself. It remains to show that R(I ∩ J)R ⊆ I ∩ J. Let i ∈ I ∩ J and r1, r2 ∈ R. Since I and J are ideals, we have r1ir2 ∈ I and r1ir2 ∈ J. So r1ir2 ∈ I ∩ J, which shows that I ∩ J is an ideal.

1.27. Let I = 〈6, X2 − 2〉. Assume that I = 〈r(X)〉. Then the degree of r must be less than or equal to the degree of 6 and, thus, the degree of r(x) is 0\. Since 1, 2, 3 ∉ I, we obtain r(X) = ±6. Hence, X2 − 2 ∉ 〈r(X)〉 = I, a contradiction. The quotient ring R/I is not a field because (2 + I)(3 + I) = 6 + I = I. Hence, I cannot be maximal.

1.28. 34 = 81 ≡ 1 mod 16, so the order of 3 divides 4\. Since 32 = 9 ≢ 1 mod 16, the order is 4.

1.29. The group (ℤ/60ℤ)∗ contains φ(60) = φ(22) ⋅ φ(3) ⋅ φ(5) = 16 elements. The orders of the elements are divisors of 16\. All divisors of 16 are even, except for the number 1\. But 1 is the only element of order 1\. Thus, there remain 15 elements with even order.

1.30. ℤ/mnℤ contains an element of order mn. In the group (ℤ/mℤ) × (ℤ/nℤ), however, for each element of order r, we know that r divides lcm(m, n). But from gcd(m, n) > 1, we conclude lcm(m, n) = mn/ gcd(m, n) < mn.

1.31. Using the Euclidean algorithm, we obtain 98 = 2 ⋅ 51 − 4 and 51 = 13 ⋅ 4 − 1. Back substitution yields 1 = 13 ⋅ 4 − 51 = 13(2 ⋅ 51 − 98) − 51 = −13 ⋅ 98 + 25 ⋅ 51\. Thus, s = 25 is the desired number.

1.32. We rewrite the congruences as ni ≡ −1 mod 3, ni ≡ −1 mod 4 and ni ≡ −1 mod 7\. This yields the potential solutions n1 = −1+84 = 83 and n2 = −1+2⋅84 = 167, because 84 = 3 ⋅ 4 ⋅ 7 and we know that modulo 84 the solution is unique. Since the difference between two solutions must be a multiple of 84, the second smallest solution cannot be less than 167.

1.33. For all n ∈ ℕ, the number n4+n2 is even and, thus, 2n4+2n2 = 4m for a suitable integer m. Therefore, 72n4+2n2 = 74m = 492m ≡ (−11)2m ≡ 121m ≡ 1m ≡ 1 mod 60.

1.34.

![](images/303_1.jpg)

We obtain p(z) = z2 + 2z + 2 and z4 + 4 = p(−z) ⋅ p(z). Differentiation yields p(z) = 2z + 2 and p(z) = 2; so p has its only minimum at z = −1 and, we have p(−1) = 1\. Consequently, p(z) ≥ 1 for all z ∈ ℤ. For z4 + 4 to be prime, we must have p(z) = 1 or p(−z) = 1\. This is the case if and only if z = −1 or z = 1\. Both cases yield the value 5.

1.35. Let f = X8 + X7 + X6 + X4 + X3 + X + 1 and g = X6 + X5 + X3 + X. We compute gcd(f, g) using the Euclidean algorithm.

![](images/303_3.jpg)

Thus, gcd(f, g) = 1.

1.36. Suppose that f(X) is not irreducible over 2. Then, f(X) = g(X)h(X) over 2 with deg(g), deg(h) ∈ {1, 2, 3, 4} and deg(g) + deg(h) = 5\. Since f(X) has no root in 2, we conclude deg(g), deg(h) ∈ {2, 3}. Without loss of generality let deg(g) = 2\. The polynomials of degree 2 over 2 are X2+X+1, X2+X, X2+ 1and X2. But only X2+X+1 is irreducible since each of the others has a root in 2. By the division algorithm for polynomials, we find f(x) = (X2 + X + 1)(X3 + X2) + 1\. So, X2 + X + 1 is not a divisor of f(X) and therefore f(X) is irreducible.

1.37. If t = 1, we have f(X) = aiXi for i ∈ ℕ and ai ≠ 0 because 0 ≠ f(X). So, there are no positive roots. Let therefore t ≥ 2\. In general, by division with an appropriate X i, we may assume that a0 ≠ 0\. Then the derivative f (X) is a (t − 1)-thin polynomial and by induction it has at most t−2 roots. Between each pair of real roots of f(X), by Rolle’s theorem (named after Michel Rolle, 1652–1719), there is at least one root of f (X). The claim follows.

1.38 (a) We obtain g(X) = Σi biXi = Σi(ai−1 − λai )Xi. Without loss of generality, we assume that a0 ≠ 0\. Consider an index i − 1 with i ≥ 1 after which in the sequence (a0, . . . , ad) a sign change occurs. Therefore, ai−1 ≠̸ 0 and for ai−1 < 0, we have ai ≥ 0 (respectively for ai−1 > 0 we have ai ≤ 0). It follows that at a sign change ai−1 always has the same sign as bi. Now b0 = −λa0, so b0 and a0 have a different sign, but bd+1 = ad ≠ 0\. Thus, the number of sign changes must have increased.

1.38 (b) Let 0 < λ1 ≤⋅ ⋅⋅ ≤ λk be the sequence of positive real roots with multiplicities. Then, we have f(X) = (X − λ1) ⋅⋅ ⋅ (X − λk)h(X). By k-fold application of [Exercise 1.38 (a)](#chapter01_4.xhtml_chapter01_4_28) the claim follows.

1.39. For n = 0 the statement is clear. Now, let n ≥ 1\. Let ![](images/304_1.jpg) with s, t ∈ ℤ, t ≠ 0 and gcd (s, t) = 1\. Now,

![](images/304_2.jpg)

Then, sn + an−1tsn−1 + ⋅⋅ ⋅ + a0tn = 0\. Thus, t divides sn and therefore t = ±1 because gcd(s, t) = 1\. Hence, r ∈ ℤ. Without loss of generality, assume that t = 1\. We obtain s(sn−1 + an−1sn−2 + ⋅⋅ ⋅ + a1) = −a0, and thus s = r is a divisor of a0.

1.40. We first show that if f(X) is irreducible over ℤ, then it is irreducible over ℚ. Assume that f(X) is reducible over ℚ. Then, there exist coprime numbers s, t ∈ ℕ\ {0} and polynomials g(X), h(X) ∈ ℤ[X] with ![](images/304_3.jpg) such that the greatest common divisor of the coefficients of g(X) is 1 and the greatest common divisor of the coefficients of h(X) is also 1\. Suppose there exists a prime number q such that q divides every coefficient of g(X)h(X). Then, g(X)h(X) mod q is the zero polynomial in (ℤ/qℤ)[X]; this is a contradiction since neither g(X) mod q nor h(X) mod q is zero. Hence, the greatest common divisor of the coefficients of g(X)h(X) is 1\. Now, tf(X) = sg(X)h(X) yields t = ±1\. This shows that f(X) is reducible over ℤ.

It remains to show that f(X) is irreducible over ℤ. Let f(X) = g(X)h(X) with g(X) = brXr + ⋅⋅ ⋅ + b0 and h(X) = csXs + ⋅⋅ ⋅ + c0 for bi , ci ∈ ℤ. We have to show that r = 0 or s = 0\. Since p is a prime divisor of a0 = b0c0 and p2 is not, p either divides b0 or c0, but not both. Let p | b0 and p ∤ c0. Because of p ∤ an = brcs, there exists a smallest index m > 0 with p ∤ bm, but p | bi for all i < m. Letting cj = 0 for j > s, we obtain am = bmc0 + (bm−1c1 +⋅ ⋅⋅ + b0cm). The prime p divides (bm−1c1 +⋅ ⋅⋅ + b0cm), but not bmc0, and thus p does not divide am. Therefore m = n. This shows r = n and s = 0.

1.41 (a) This is a direct consequence of Eisenstein’s criterion.

1.41 (b) We obtain ![](images/304_4.jpg) But ![](images/304_5.jpg) for 1 ≤ i ≤ p − 1 and ![](images/304_6.jpg)

1.42. In the extension considered here, the operation of multiplication is not associative anymore. In particular, (S(X) ⋅ (1 − X)) ⋅ Σi≥0 Xi ≠ S(X) ⋅ ((1 − X) ⋅ Σi≥0 Xi).

1.43. Since the operations are chosen in such a way that they correspond to the according operations in ℝ, we see that ![](images/305_1.jpg) is a subring of ℝ. It remains to show that the inverse of ![](images/305_2.jpg) is an element of ![](images/305_3.jpg) Since at least one of a and b is nonzero and the square root of 2 is not in ℚ, we have a2 ≠ 2b2, that is a2 − 2b2 ≠ 0, and therefore

![](images/305_4.jpg)

1.44. The set I = {g(X) ∈ F[X] | g(α) = 0 } is an ideal. It contains at least one polynomial besides the zero polynomial since p ∈ I. By [Theorem 1.45](#chapter01_3.xhtml_chapter01_3_7), there is a unique polynomial m(X) with leading coefficient 1 which generates I.

1.45. From an ≡ 1 mod pe, we obtain an ≡ 1 mod p and thus, m | n. Since am ≡ 1 mod p, we have am = 1 + bp for some b ∈ ℤ. By [Lemma 1.65](#chapter01_4.xhtml_chapter01_4_1), we have ampe−1 = (1 + bp)pe−1 ≡ 1 + bpe mod pe+1 and therefore ampe−1 ≡ 1 mod pe. This yields n | mpe−1. We conclude ![](images/305_5.jpg)

1.46. The polynomial X − a divides X(q−1)/2 − 1 if and only if a is a root of X(q−1)/2 − 1 if and only if a(q−1)/2 = 1 if and only if a is a square. The last equivalence is Euler’s criterion ([Theorem 1.68](#chapter01_4.xhtml_chapter01_4_6)).

## Chapter 2

2.1. Considering the times of Frederick the Great and Voltaire one can assume that the message was written in French. We obtain: “ce soir sous P a cent sous six.” This reads as “ce soir souper à Sans Souci.” So Frederick the Great was inviting to dinner at his palace in Potsdam, and Voltaire replied with a big “G” and a small “a.” This means “G grand a petit.” So he announced with “j’ai grand appétit” his ravenous appetite.

2.2. It may be natural to conjecture that [Exercise 1.3](#chapter01_4.xhtml_chapter01_4_17) is applicable and that the functions ck and dk have to be mutually inverse. However, this is not the case due to different domains and target sets. As a simple counter-example consider the encryption function ck : {1} → {1, 2} with ck(1) = 1 and the decryption function dk : {1, 2} → {1} with dk(1) = dk(2) = 1.

2.3 (a) From ℤ/77ℤ = ℤ/7ℤ×ℤ/11ℤ, we obtain φ(n) = 6 ⋅ 10 = 60.

2.3 (b) The Euclidean algorithm yields s = 7.

2.3 (c) x ≡ ys = 57 ≡ 47 mod 77.

2.4. We have x = x2⋅13−5⋅5. Thus, we compute (x5)−1 ≡ (5145)−1 ≡ 134 mod 551 with the extende Euclidean algorithm. This yields x ≡ 4382 ⋅ 1345 ≡ 77 mod 551.2.5. We have d(c(x)) = (xe mod n)s mod n ≡ xes ≡ x1+k(pi−1) ≡ x mod pi for some k ∈ ℕ. By the Chinese remainder theorem, we obtain d(c(x)) ≡ x mod n. From x ∈ {0, . . . , n − 1} we conclude d(c(x)) = x.

2.6 (a) The encrypted message is y ≡ 172 ≡ 36 mod n.

2.6 (b) Recall that n = 11 ⋅ 23 = 253\. First, we determine ![](images/306_1.jpg) mod 11 and ![](images/306_2.jpg) mod 23\. By the Chinese remainder theorem, from the conditions z ≡ ±5 mod 11 andz ≡ ±6 mod 23, we obtain the four solutions z ∈ {6, 17, 236, 247}.

2.6 (c) The encoding function is injective on the given domain: suppose there exist x, x ̃ ∈ 00{0, 1}400 with x > x̃ and x2 ≡ x̃2 mod 253\. Then, (x − x̃)(x + x̃) ≡ 0 mod 253\. Now, there are two cases. Either one of the two factors is 0 or one is a multiple of 11, and the other a multiple of 23.We have x − x ̃ ≠ 0 and x + x ̃ ≢ 0 mod 253 because x + x ̃ cannot exceed 120\. Thus, the only remaining case is x − x ̃ being a multiple of 11 or 23\. The numbers x and x ̃ are both multiples of 4\. From ![](images/306_3.jpg) we obtain that x − x ̃ can only be a multiple of 11, and ![](images/306_4.jpg) has to hold. With ![](images/306_5.jpg) this yields ![](images/306_6.jpg) and ![](images/306_7.jpg) In particular, x + x ̃ is not divisible by 23\. This is a contradiction; and it shows that such x and x ̃ cannot exist.

2.7 (a) The number n is prime, so φ(n) = n − 1 = 46 and the order of g is a divisor of 46 = 2 ⋅ 23\. From 52 = 25 ≢ 1 mod 47 and 523 ≡ −1 mod 47, we obtain that the order of g is 46.

2.7 (b) We have A ≡ 5a ≡ 516 ≡ 17 mod 47 and B ≡ 5b ≡ 59 ≡ 40 mod 47\. The secret key is k ≡ Ab ≡ Ba ≡ 21 mod 47.

2.7 (c) B = 40 has already been determined. The ciphertext is computed by y ≡ Ab⋅x ≡ k ⋅ x ≡ 21 ⋅ 33 ≡ 35 mod 47.

2.8. Since each element x ∈ X has a unique image y = h(x), each x is counted in exactly one ‖y‖. Thus, Σy∈Y ‖y‖ = |X|. Substituting this equation into m = Σy∈Y ‖y‖/|Y|, directly yields ![](images/306_8.jpg) A collision (x, x) with h(x) = h(x) = y accounts for two different elements in ‖y‖. The number of these pairs for a fixed y is ![](images/306_9.jpg) This yields ![](images/306_10.jpg) The equation ![](images/306_11.jpg) is obtained using ![](images/306_12.jpg) ![](images/306_13.jpg) and Σy∈Y ‖y‖ = |X|. We have

![](images/306_14.jpg)

In particular, ![](images/306_15.jpg) This yields ![](images/306_16.jpg)

2.9. By definition, h1 is collision resistant. Now, let i ≥ 1 and let ![](images/306_17.jpg) be a collision of hi+1.We may assume that ![](images/306_18.jpg) According to the definition of hi+1, two cases are possible. Either ![](images/307_1.jpg) and thus, ![](images/307_3.jpg) is a collision of hi. Or, in the other case, ![](images/307_2.jpg) is a collision of h1.

2.10. Wehave a80 115 359 ≡ a1 294 755 mod n. Therefore a80 115 359−1 294 755 ≡ 1 mod n. Furthermore, 80 115 359 − 1 294 755 = 78 820 604 = 4 ⋅ 19 705 151\. Since φ(n) = 4pq, we try to find a number b such that b19 705 151 ≢ 1 mod n; see [Section 3.4.4](#chapter03_1.xhtml_chapter03_1_29) for details on this approach. We randomly choose b = 13. Then, 1319 705 151 ≡ 10 067 mod n and 10 0672 ≡ 1 mod n. Thus, (10 067 − 1)(10 067 + 1) ≡ 0 mod n, and we compute gcd(10 066, n) = 719 and gcd(10 068, n) = 839\. This yields the factorization n = 719 ⋅ 839.

2.11 (a) First, let uk(x) = (γ, δ) = (αs , (x − mγ)s−1). Then, βγγδ ≡ αmγγδ ≡ αmγαsδ ≡ αmγαs⋅s−1(x−mγ) ≡ αx mod p, and thus υk(x, γ, δ) = true. Conversely, let υk(x, γ, δ) = true and let t be the discrete logarithm of γ to base α. Then, βγγδ ≡ αx mod p, and thus αx−mγ ≡ γδ ≡ αtδ mod p. We further obtain x − mγ ≡ tδ mod (p − 1). This is equivalent to δ ≡ (x − mγ)t−1 mod (p − 1). Thus, (γ, δ) is a valid signature for x.

2.11 (b) Choose u, υ with gcd(υ, p − 1) = 1\. Define γ = αuβυ mod p, δ = −γυ−1 mod p − 1 and x = uδ mod p − 1\. Then, βγγδ ≡ βγαuδβ−υυ−1γ ≡ αuδ ≡ αx mod p.

2.11 (c) We have to show that βλλμ ≡ αx' mod p holds. Let y = (hγ − jδ)−1 mod p − 1\. Since (γ, δ) is a valid signature, we have γδ ≡ β−γαx mod p. This yields βλλμ ≡ βλ(γhαiβj)δλy ≡ βλ(γδ)hλyαiδλyβjδλy ≡ βλβ−γhλyαxhλyαiδλyβjδλy ≡ βλβ−γhλyαxβjδλy ≡ αxβλ−λ(hγ−jδ)(hγ−jδ)−1 ≡ αx' mod p.

2.12. Let the four people be 1, 2, 3, 4.We have ![](images/307_4.jpg) and the subsets of {1, 2, 3, 4} with two elements are A1 = {1, 2}, A2 = {1, 3}, A3 = {1, 4}, A4 = {2, 3}, A5 = {2, 4} and A6 = {3, 4}. For the first five of these subsets, we randomly choose the keys k1 = (1, 9), k2 = (2, 4), k3 = (3, 5), k4 = (4, 1) and k5 = (5, 1). Then the key for A6 is k6 = (6, 11) since 11 ≡ 7 − (9 + 4 + 5 + 1 + 1) mod 12\. Person 1 gets the keys {k4, k5, k6}, person 2 gets {k2, k3, k6}, person 3 gets {k1, k3, k5} and person 4 gets {k1, k2, k4}. If three of the four participants come together, then they have all the keys kj in their subsets. Thus, they can compute ![](images/307_5.jpg)

2.13. We choose the prime number p = 61\. We share the secret using the polynomial a(X) = 42+a1X ∈ p[X] with the randomly chosen coefficient a1 = 23\. Then, a(1) = 4, a(2) = 27 and a(3) = 50\. Thus, the pairs (1, 4), (2, 27) and (3, 50) shall be distributed. Any two of these pairs can be used to reconstruct the secret. For example, let (1, 4) and (2, 27) be given. We obtain the equations a0 + a1 = 4 and a0 + 2a1 = 27\. We find a0 = 4 − a1 and substitute 4 − a1 for a0 in the second equation. This results in (4 − a1) + 2a1 = 27, so a1 = 23 and further a0 + 23 = 4, or a0 ≡ −19 ≡ 42 mod 61.

2.14. We use a multi-step algorithm based on Shamir’s secret sharing. First, the secret key is distributed between three keys such that two of them are sufficient to reconstruct the secret key. Two of these keys are given to the directors. The third key is again divided into ten keys with the property that seven of them suffice to decrypt the secret. Seven of these ten keys are passed on to the heads of department. The remaining three keys are again divided as secret (for this, a suitable encoding of the three keys as one secret is required). And finally this secret is divided into a total of 87 keys such that eleven of them are sufficient to reconstruct the secret. Obviously, the keys of eleven of the employees can compensate the lack of three department heads, and seven department heads can compensate the lack of a director.

2.15. Let persons 1, 2 and 3 have salaries g1, g2 and g3, respectively. The protocol works as follows: first, person 1 sends a (large) random number z to person 2, who in turn sends z + g2 to person 3\. Since person 3 does not know the number z, it is not possible to infer the salary g2 from this. Then, person 3 sends the sum z + g2 + g3 to person 1\. Person 1 is able to compute the sum g1 + g2 + g3 and thus also the average salary. Person 1 communicates it to the other two persons. This protocol can be easily generalized to cases of more employees.

2.16. Let w1 < ⋅ ⋅ ⋅ < wn be the possible salaries. Let cB be Bob’s public encryption function and dB his private decryption function. Alice randomly chooses x and sends d = cB(x) − a to Bob, where a is her salary. Bob now computes y1, . . . , yn with yi = dB(d + wi). For j such that wj = a, we have yj = x. To conceal his salary, Bob applies a one-way function f and computes zi = f(yi ) for all i ∈ {1, . . . , n}. Without loss of generality let zi ≠ zj + 1 for 1 ≤ i, j ≤ n. (Otherwise, Alice has to choose a new x or Alice and Bob agree upon a different hash function.) If b = wk is Bob’s salary, then he sends the sequence z1, . . . , zk , zk + 1, . . . , zn + 1 to Alice. Now, a ≤ b if and only if f(x) occurs in the sequence.

2.17. The dealer commits himself to a number between 0 and 36\. Then, all players make their bids in plaintext. Finally, the dealer reveals his number.

2.18. The problem can be solved via dynamic programming. We fill a {0, . . . , c} × n table T. By Ti,j, we denote the entry in row i and column j. The table is initialized with T0,j = 1; and then iteratively filled by the following rule.

![](images/308_1.jpg)

The entry Ti,j means that a solution for the weight i already exists using s1, . . . , sj. Thus, a solution of the knapsack instance exists if Tc,n = 1.

2.19. The inverse of u in (ℤ/71ℤ)∗ is w = 5\. Alice chose the ai such that si = ai ⋅w mod 47\. So she used the superincreasing sequence (2, 5, 9, 17, 37). Alice determined c = 90 ⋅ w = 90 ⋅ 5 ≡ 24 mod 71\. The only solution of the knapsack problem is 24 = 1 ⋅ 2 + 1 ⋅ 5 + 0 ⋅ 9 + 1 ⋅ 17 + 0 ⋅ 37\. Therefore, the plaintext is (1, 1, 0, 1, 0).

2.20. For i = 0 the statement is trivial. For i ≥ 0, induction yields:

![](images/308_2.jpg)

## Chapter 3

3.1. Let γ0 > 0 be such that ![](images/309_1.jpg) Let further ε > 0 and n0 ∈ ℕ be numbers such that αin0 ≤ n0 − 1 for all i ∈ {1, . . . , k} and ![](images/309_2.jpg) for all n ≥ n0. Finally, choose γ large enough to ensure that γ0 < γε and f(n) < γn for all n < n0. By induction on n we show that f(n) < γn. For n < n0 the assertion is satisfied by choice of γ. For n ≥ n0 we have

![](images/309_3.jpg)

Remark: A well-known application of the master theorem II is the computation of the median of a sequence of n numbers with only O(n) comparisons. This shows that it is not necessary to sort the whole sequence to determine the median.

3.2. Without loss of generality we assume that a ≠ 0 ≠ b. Divide each of a and b by gcd(a, b). Then, we can independently determine the square roots of the numerator and denominator using binary search.

3.3. The extended binary gcd algorithm is as follows:

![](images/309_4.jpg)

3.4. We have 2(n−1)/2 = 2864 ≡ 1 mod 1729 and by [Theorem 1.70 (c)](#chapter01_4.xhtml_chapter01_4_11) we obtain ![](images/309_6.jpg) (−1)(n2−1)/8 = 1\. Note that 1729 ≡ 1 mod 16 and therefore ![](images/309_5.jpg) is an even number, so 1729 is an Eulerian pseudoprime to base 2.

We write 1728 = 2ℓu = 26 ⋅ 27 and let b = 645 ≡ 227 ≢ 1 mod 1729\. Thus, (b20 , b21 , b22 , b23 , b24 , b25) = (645, 1065, 1, 1, 1, 1) modulo 1729\. Since −1 does not occur in this sequence, 1729 is not a strong pseudoprime to base 2\. Further, for c = 1065, we have c2 ≡ 1 mod 1729\. Consequently, 1064 ⋅ 1066 = (c − 1)(c + 1) ≡ 0 mod 1729\. Therefore, gcd(1064, 1729) = 133 is a nontrivial divisor of 1729 = 133 ⋅ 13 = 7 ⋅ 19 ⋅ 13.

Moreover, let us note that in this particular case out of all a ∈ {1, . . . , n − 1} (or all a ∈ {1, . . . , n − 1} coprime to n, respectively) the Fermat test fails for 75% (or 100%, respectively), the Solovay–Strassen test for 39.5% (or approximately 52.7%, respectively) and the Miller–Rabin test for approximately 9.4% (or 12.5%, respectively). Thus, in particular, 1729 is a Carmichael number.

3.5. Let r be the order of a in (ℤ/nℤ)∗. From (i), we obtain r | n − 1, and with (ii) this yields r = n − 1\. Thus, |(ℤ/nℤ)∗| = n − 1, and n is prime.

3.6. Suppose, fn is prime. Then, Euler’s criterion yields ![](images/310_2.jpg) mod fn. Together with fn ≡ 1 mod 4 using the law of quadratic reciprocity, we obtain ![](images/310_3.jpg) ![](images/310_1.jpg) mod 3\. The converse direction is a consequence of the Lucas test in [Exercise 3.5](#chapter03_3.xhtml_chapter03_3_21).

3.7 (a) By the law of quadratic reciprocity we have ![](images/310_4.jpg) because 2p − 1 ≡ (−1)p − 1 ≡ 1 mod 3 for odd p. Using the well-known quadratic formula it follows that f is irreducible.

3.7 (b) The polynomial g(Y) = Y2 −4Y +1 in K [Y] has the roots X and 4 −X. These are the only zeros of g because K is a field. The coefficients of g are in n, so 0 = g(X)n = g(Xn) follows. Therefore, Xn ∈ {X, 4 − X}. Since the roots of Yn − Y are exactly the elements of n and X ∉ n, we obtain Xn ≠ X and thus Xn = 4 − X. This yields

![](images/310_10.jpg)

Note that a ↦ an is the Frobenius homomorphism and that an = a for all a ∈ n.

3.7 (c) In n and thus also in K by Euler’s criterion we have 2(n−1)/2 = 1 because ![](images/310_6.jpg) Moreover, (X − 1)2 = 2X in K. This yields

![](images/310_11.jpg)

3.7 (d) We define f(X) = X2 − 4X + 1\. For the direction from right to left, let the congruence hold, and let q be the smallest prime divisor of n. In q[X] we have Xn+1 ≡ 1 mod f(X) and X(n+1)/2 ≢ 1 mod f(X). Therefore, in the group of units of R = q[X]/f , the element X has order n + 1\. If n is composite, then ![](images/310_8.jpg) Since R contains q2 elements, we know n ≥ q2 > |R∗|≥ n + 1, a contradiction. Thus, n is prime.

For the converse direction, let n be prime and let K = n[X]/f. In the field, K we have 2X(n+1)/2 = (X − 1)n+1 = −2 and thus X(n+1)/2 = −1, as desired.

3.8. Let R = ℤ/nℤ, let f(X) = X2 − 4X + 1 and let K = R[X]/f . By induction on j we first show that in K the property ℓj = X2j + (4 − X)2j is satisfied. For j = 0 we have ℓ0 = 4 = X + (4 − X). Nowlet j ≥ 0\. Using X(4 − X) = 1, we obtain

![](images/311_1.jpg)

We have X(n+1)/2 = −1 if and only if X(n+1)/2−k = −X−k. For k = (n + 1)/4, together with X−1 = 4 − X, we obtain the equivalence

![](images/311_2.jpg)

The assertion follows from [Exercise 3.7](#chapter03_3.xhtml_chapter03_3_22).

3.9. We have the equivalence an+1 ∈ a1ℤ+⋅ ⋅ ⋅+anℤ ⇔ gcd(a1, . . . , an) | an+1. Here, g = gcd(a1, . . . , an) = gcd(gcd(a1, . . . , an−1), an). In particular, using the extended Euclidean algorithm numbers yi ∈ ℤ with a1y1 + ⋅⋅ ⋅ + anyn = g can be computed. Setting xi = yian+1/g, this yields a solution for the equation.

3.10. We let q = 41, u = 5 and ℓ = 3\. Then, q − 1 = u2ℓ. Furthermore, from g(q−1)/2 ≡ −1 mod 41, we can see that g is not a square in 41. In the second step we now successively determine bits k0, k1 and k2. Let ![](images/311_3.jpg) especially x−1 = a. We determine ki ∈ {0, 1} from k0, . . . , ki−1 and let ki = 0 if and only if ![](images/311_4.jpg) mod q is satisfied.

–For i = 0 we have ![](images/311_5.jpg) mod q and we let k0 = 0\. Note that by Euler’s criterion the inputwould not be a square ifwe would have k0 = 1.

–Fori = 1 we compute x0 = x−1 ⋅ gk020 = x−1 = 2\. This yields ![](images/311_6.jpg) mod q and we let k1 = 1.

–Fori = 2 we compute ![](images/311_7.jpg) mod 41; for the second congruence we use g−1 ≡ 14 mod 41\. Then, we obtain ![](images/311_8.jpg) mod q and we let k2 = 1.

Thus, we obtain k = k0 + 2k1 + 4k2 = 6\. Finally b = 2(u+1)/2g−uk/2 = 23145⋅3 ≡ 24 mod 41 is a square root of 2 in 41. The second solution is 17 = 41 − 24.

3.11. First, let a(p−1)/4 = 1 and b = a(p+3)/8. Then, b2 = a(p+3)/4 = a ⋅ a(p−1)/4 = a ⋅ 1 = a. Now let a(p−1)/4 = −1 and b = 2−1(4a)(p+3)/8. From Euler’s criterion and the law of quadratic reciprocity it follows that ![](images/311_9.jpg) Thus, we obtain b2 = 2−2(4a)(p+3)/4 = 2−2 ⋅ 2(p+3)/2 ⋅ a(p+3)/4 = 2(p−1)/2 ⋅ a(p−1)/4 ⋅ a = (−1) ⋅ (−1) ⋅ a = a.

3.12 (a) From the law of quadratic reciprocity it follows that ![](images/311_10.jpg) so −1 is not a square, that is, X2 = −1 has no solution in p. Since f(X) has degree 2, it is irreducible.

3.12 (b) We have ![](images/311_11.jpg) and ![](images/311_12.jpg) Therefore, more generally, let 1 ≤ b < c ≤ p −1with ![](images/311_13.jpg) and![](images/311_14.jpg) If c = b +1, then we let a = b. Otherwise, we consider d = ⌊(b + c)/2⌋ and compute ![](images/312_1.jpg) Depending on this result being either −1 or 1, we recursively continue the algorithm with the numbers b < d or d < c. This binary search returns the requested number a after atmost O(log p) evaluations of the Jacobi symbol.

3.12 (c) Let a be the number computed in the previous part of the exercise. The elements a + 1 and −1 both are no squares, therefore −(a + 1) is a square. Since p ≡ −1 mod 4, one can efficiently compute b, c ∈ p with b2 = a and c2 = −(a + 1). Now b2 + c2 = −1.We let g = b + cX ∈ p2 .

Assume that g is a square. Then there are s, t ∈ p with (s + tX)2 = g. Thus, s2 − t2 = b and 2st = c. Let h = (s − tX)2. Then, h = b − cX and thus gh = b2 + c2 = −1\. With r = (s + tX)(s − tX) = s2 + t2 ∈ p, we obtain r2 = gh = −1\. This is a contradiction to ![](images/312_2.jpg) Consequently, g is not a square. We can now use the deterministic part of Tonelli’s algorithm to extract roots in p2 .

3.13. We let a = 2 and t = 0, and we observe that (t2 − 4a)11 ≡ −1 mod 23; thus, t = 0 is a valid choice for the first step in Cipolla’s algorithm. We now determine X12 by repeatedly replacing X2 by tX − a = −2 and computing coefficients in ℤ/23ℤ:

![](images/312_3.jpg) X12 = (X ⋅ X2)4 ≡ (−2X)4 = 24(X2)2 ≡ 24(−2)2 ≡ 18 mod (X2 + 2)

So, 18 and 5 = 23 − 18 are the two square roots of 2 in 23.

3.14. For B = {2, 3} we find k = 27 ⋅ 35 = 128 ⋅ 243 = 31 104. Using fast modular exponentiation and a = 2 we further obtain ak ≡ 82 mod n. Now, gcd(ak − 1, n) = gcd(81, 253) = 1 and we did not find a factor.

For B = {2, 3, 5} we find k = 27 ⋅ 35 ⋅ 53 = 128 ⋅ 243 ⋅ 125 = 3 888 000. Using fast modular exponentiation and a = 2 we now obtain ak ≡ 133 mod n. Then, gcd(ak − 1, n) = gcd(132, 253) = 11 andwe have found a nontrivial factor of n.

Let us remark that the p − 1 algorithmwith B = {2, 3} finds a nontrivial factor for roughly 24% of all a ∈ {2, . . . , n − 1}. For B = {2, 3, 5} the probability is 84%.

3.15. We let x0 = y0 = 12 and obtain the following values:

![](images/312_7.jpg)

Thus, 53 is a divisor of n.

3.16. The order n of (ℤ/19ℤ)∗ is 18.We let g = 2, y = 3 and![](images/312_5.jpg) Performing the baby-steps results in the following table B:

![](images/312_6.jpg)

As to the giant-steps, we compute h = 24 = 16 and successively h0 = 1, h1 = 16, h2 ≡ 9\. None of these values can be found in the second row of the table. Finally, for s = 3 we obtain hs ≡ 11, which can be found in the table B at r = 1\. Thus, x = 3 ⋅ m + r = 13 is the desired value.

3.17. Compute the smallest n ≥ 0 with gn = 1\. To this end check the giant-steps s in ascending order and discard the solution r = 0 and s = 0\. A small optimization is the following. If two baby-steps (r, a) and (r' , a) with r < r' occur, one only stores the entry (r, a) in the table B.

3.18 (a) The order of G is 22 = 2⋅11.We have g2 = 9 ≢ 1 mod 23 and g11 ≡ 1 mod 23\. So, 11 is the order of g.

3.18 (b) We let y = 18, we let f : ℤ/qℤ×ℤ/qℤ→ℤ/qℤ×ℤ/qℤ such that

![](images/313_1.jpg)

and we define a sequence (ri , si) with (r1, s1) = (1, 1) and (ri+1, si+1) = f(ri , si) for i ≥ 1\. Further, we let hi = gri ysi mod 23\. For ℓ ∈ {1, 2, 4} we compute the values of (rℓ , sℓ) as well as hℓ; and for k ∈ {1, . . . , ℓ} the values of (rℓ+k , sℓ+k) and hℓ+k are displayed in the following table:

![](images/313_2.jpg)

The algorithm terminates if hℓ = hℓ+k, that is, in the current case at ℓ = 4 and k = 3; the values for ℓ = k = 4 are actually not computed anymore. We have g3y2 = hℓ = hℓ+k = g5y3. If y = gx, then g3+2x = g5+3x and therefore 3 + 2x ≡ 5 + 3x mod 11\. One solution of this congruence is 9. Since 39 ≡ 18 mod 23, this is indeed the desired value. Note that the algorithm does not find the accordance with value 6 of h2 and h5, since the values h5, h6, h7, h8 are exclusively compared with h4.

3.19. We let g = 2 and y = 5\. The order of (ℤ/19ℤ)∗ is n = 18 = 2 ⋅ 32\. We choose parameters as displayed in the following table:

![](images/313_3.jpg)

For p ∈ {2, 3} we have np = n/pe(p), gp = gnp mod q and ![](images/314_1.jpg) mod q. If we let x = 16, then congruences x ≡ 0 mod 2 and x ≡7 mod 32 are satisfied and by [Theorem 3.16](#chapter03_2.xhtml_chapter03_2_24) we know that 16 is the desired value.

To determine the value x3 we write x3 = d0+d1⋅3\. The value d0 can be determined as a solution of the equation ((g3)3)d0 ≡ (y3)3 mod 19\. Now (g3)3 = 43 ≡ 7 mod 19 and (y3)3 = 63 ≡ 7 mod 19 and, moreover, d0 = 1 trivially is a solution. In order to determine d1 we first let z1 = 11\. Then, ![](images/314_2.jpg) mod 19 and d1 is a solution of the congruence ((g3)3)d1 ≡ z1 mod 19, that is, by insertion 7d1 ≡ 11 mod 19\. One solution is d1 = 2 and we obtain x3 = 1 + 2 ⋅ 3 = 7.

3.20. The order of (ℤ/pℤ)∗ is a power of 2\. Using the Pohlig–Hellman algorithm, it suffices to compute discrete logarithms in O(log p) two-element groups.

3.21 (a) A simple computation yields ωb/2 ≡ −1 mod 97 and ωb ≡ 1 mod 97.

3.21 (b) ![](images/314_3.jpg)

3.21 (c) The degree of f ∗ g is 3, therefore we can choose b = 4 and use ω = −22 as primitive bth root of unity. This yields the following course of the FFT on input f (left) and g (right):

![](images/314_4.jpg)

These flowcharts have the following meaning: if f, f0, f1 are polynomials such that f(X) = f0(X2) + Xf1(X2) and w = (1, ω, ω2, . . . , ωb−1), then ![](images/314_6.jpg) symbolizes the recursion and ![](images/314_5.jpg) the merge of the results, where addition and multiplication are meant componentwise. We compute the componentwise product (3, −22, 1, 22) ⋅ (5, 33, −1, −29) ≡ (15, 50, −1, 41) mod 97\. As to the inverse transformation, we use the same scheme, only the primitive bth root of unity used here is ω−1 = 22\. Then

![](images/314_7.jpg)

To obtain the result, we have to multiply 8 + 20X + 20X2 + 12X3 by b−1 = −24 and we end up with (f ∗ g)(X) = 2 + 5X + 5X2 + 3X3.

3.22. Let u and υ be natural numbers with a binary representation of at most n bits. The time complexity of the method is dominated by the time needed for the FFT and therefore it is ![](images/o.jpg)(n log n). There are at most m = ⌈n/64⌉ indices i, for which ui as well as υi are nonzero. We consider the product

![](images/315_5.jpg)

with the usual convention that uj = υj = 0 for j < 0 and for j ≥ m. In order to have the zj = Σk u kυj−k uniquely determined by wj, the inequality zj < p1p2p3 has to hold. At most m summands in zj are nonzero, and each of these summands is bounded by 264. Therefore, we obtain zj ≤ m ⋅ 264 ⋅ 264\. Since pi > 256 it suffices, if the number m of 64-bit blocks of u and υ satisfies m ≤ 23⋅56/22⋅64 = 240. Furthermore, 2m ≤ 256 has to hold in order to have no overflow in the Fourier transform. This already follows from the fact that m ≤ 240. Therefore, using this method numbers with a binary representation of 64 ⋅ 240 bits can be multiplied. This corresponds to a binary representation of more than eight terabytes. With very large primes pi (as close to 64 bits as possible) even larger numbers can be multiplied.

## Chapter 5

5.1 (a) If the characteristic is not 2, we complete the square on the left-hand side of Equation ([5.2](#chapter05_3.xhtml_chapter05_3_19)) and obtain ![](images/315_2.jpg) where t is a quadratic polynomial in X̃ , which we push to the right-hand side. Now let ![](images/315_3.jpg) and ![](images/315_4.jpg) and gather the coefficients on the right-hand side.

5.1 (b) Let X ̂ = X − ê/3 and combine the coefficients.

5.2. Our computations are performed in an algebraically closed field k. If the polynomial has a multiple root, then we have X3 + AX + B = (X − a)2(X − b) for some a, b ∈ k. Multiplying out and comparing coefficients yields 2a + b = 0, 2ab + a2 = A and −a2b = B. By substituting b = −2a in the second and third equation, we obtain A = −3a2 and B = 2a3. It follows that 4A3+27B2 = −4⋅27a6+27⋅4a6 = 0 independent of the field’s characteristic. For the converse, let 4A3 + 27B2 = 0\. If the characteristic is neither 2 nor 3, then this yields (−A/3)3 = (B/2)2. Let a be a square root of −A/3; then A = −3a2 and B = 2a3. For b = −2a the same computation as in the first part yields (X − a)2(X − b) = X3 + AX + B and thus, a is a multiple root. If the characteristic is 2, then 4A3 + 27B2 = 0 if and only if B = 0\. Then, X3 + AX = X(X2 + A) = X(X + a)2 for a ∈ k with a2 = A. If the characteristic is 3, then 4A3 + 27B2 = 0 is equivalent to A = 0.We obtain X3 + B = (X + b)3 for b ∈ k with b3 = B.

5.3. Let s(X) = X3 + AX + B.We show that for every a ∈ p there are ![](images/316_1.jpg) points in E (p) with the value a in the X-coordinate. If s(a) = 0, then (a, 0) is the only point. If ![](images/316_2.jpg) then there exists a square root b ∈ p of s(a) and the two points (a, b) and (a, −b) are the only ones with this X-coordinate. If ![](images/316_3.jpg) then no point on the curve has the value a as an X-coordinate. This yields

![](images/316_4.jpg)

5.4 (a) 4 ⋅ 13 + 27 ⋅ 62 = 8 ≠ 0 in 11. By [Exercise 5.2](#chapter05_3.xhtml_chapter05_3_21), this proves the claim.

5.4 (b) For each x ∈ 11 we distinguish the three possible cases whether x3 + x + 6 equals 0, is a square in 11 or is not a square in 11. Then, we obtain from [Exercise 5.3](#chapter05_3.xhtml_chapter05_3_22) the set E(11) = {(2, 4), (2, 7), (3, 5), (3, 6), (5, 2), (5, 9), (7, 2), (7, 9), (8, 3), (8, 8), (10, 2), (10, 9)}. Therefore, |Ẽ(11)| = |E(11)∪ ![](images/o.jpg)| = 12 + 1 = 13 is prime and thus Ẽ(11) is cyclic.

5.5 (a) 4 ⋅ 13 = −1 ≠ 0 in 5. By [Exercise 5.2](#chapter05_3.xhtml_chapter05_3_21), this proves the claim.

5.5 (b) Similar to the previous exercise, we obtain E(5) = {(0, 0), (2, 0), (3, 0)}. Each of these three elements is of order 2. Hence, Ẽ(5) is isomorphic to the Klein four-group; any two elements of E (5) generate the group.

5.6. It is easy to see that { P ∈ Ẽ(k) | 3P = ![](images/o.jpg)} is a subgroup of Ẽ(k). Let P = (a, b) ∈ E (k) be a point of order 3\. We have b ≠ 0 because otherwise P would be of order 2\. Moreover 2P = −P and therefore ![](images/316_5.jpg) Together with b2 = a3 + Aa + B, this yields 3a4 + 6Aa2 + 12Ba − A2 = 0.We therefore consider the polynomial t(X) = 3X4 + 6AX2 + 12BX −A2. Every point of order 3 would lead to the same polynomial; in particular, the X-coordinate of every point in { P ∈ E(k) | 3P = ![](images/o.jpg)} is a root of t. Moreover, every root of t is the X-coordinate of two different points in { P ∈ E(k) | 3P = ![](images/o.jpg)}. If n is the number of different roots of t, then |{ P ∈ E(k) | 3P = ![](images/o.jpg)}| = 2n ≤ 8.

The derivative of t is t(X) = 12(X3 + AX + B). The polynomial t' has no multiple roots because X3 + AX + B has three distinct roots. Therefore, t has no triple roots. Suppose that t(X) has two different double roots c ≠ d. Then, t(X) = 3(X−c)2(X−d)2 = 3(X2 − 2cX + c2)(X2 − 2dX + d2). Comparing coefficients at X3 yields 0 = −6(c + d). Then, c = −d and therefore t(X) = 3(X2 − c2)2 = 3X4 − 6c2X2 + 3c4. This implies B = 0 as well as A = −c2 and A2 = −3c4. We obtain A = B = 0, which contradicts 4A3 + 27B2 ≠ 0\. Therefore, t has at least two simple roots c1 ≠ c2. We further have ![](images/316_6.jpg) for i ∈ {1, 2}. Thus for suitable di ≠ 0 we can find four different points (ci , ±di) on E (k). By construction of t, all four points Pi satisfy 2Pi = −Pi. This shows that all four points have order 3\. Every Abelian group, in which at least four elements have order 3, contains ℤ/3ℤ×ℤ/3ℤ. So there are at least 8 points of order 3.

5.7. We may assume that neither α nor β is trivial. For α = β, we have (α + β)(P) = 2α(P), and in this case α + β is rational. Next, we consider the case α(P) = (f(P), g(P)) and β(P) = (f(P), h(P)) for almost all P ∈ E(k). We may assume that α ≠ β, and therefore g (P) ≠ h(P) for almost all points P ∈ E(k). Then the only possibility is g(P) = −h(P) for infinitely many P ∈ E(k). This implies g = −h in k(x, y). Thus, α(P) = −β(P) for almost all P ∈ E (k), and furthermore α = −β by [Lemma 5.15](#chapter05_3.xhtml_chapter05_3_3). This shows that α + β is the trivial endomorphism.

The only remaining case is α(P) = (f1(P), g(P)) and β(P) = (f2(P), h(P)) for almost all P ∈ E(k) such that f1−f2 ≠ 0 ∈ k(x, y). So for almost all P,we have f1(P) ≠ f2(P) and using the addition formula on the elliptic curve for points with different x-coordinate we find the corresponding rational morphism for α + β.

5.8. Let α(P) = (r1(P), r2(P)) for almost all P ∈ E(k). We already know that we can write ![](images/317_1.jpg) Since α is an endomorphism, we have α(x, −y) = −α(x, y). Therefore, υ1(x) = 0 ∈ k[x] and u2(x) = 0 ∈ k[x]. This yields the desired polynomials p(x) = u1(x), q(x) = q1(x), u(x) = υ2(x) and υ(x) = q2(x). If p(x)/q(x) or u(x)/υ(x) were constant, then the image of α would be a finite set, in contradiction to the kernel being finite.

5.9. We only have to show that ϕq is a group homomorphism. Since ϕq is a bijection on E(k), the inverse mapping ![](images/317_2.jpg) is defined and it suffices to show that ψ is a group homomorphism. We identify Ẽ(k) with Pic0(E(k)) according to [Theorem 5.5](#chapter05_2.xhtml_chapter05_2_1). The mapping P → ψ(P) induces an automorphism of the group of divisors by ΣP∈E(k) n PP →ΣP∈E(k) npψ(P), which we denote by ψ, too. It remains to show that principal divisors are mapped to principal divisors because then ψ induces a homomorphism on Pic0(E(k)). Consider a principal divisor div(f) = ΣP∈E(k) ordP(f)P with f ∈ k[x, y]. We obtain

![](images/317_3.jpg)

By [Theorem 5.3](#chapter05_1.xhtml_chapter05_1_20), we obtain ordϕq(P)(f) = q ⋅ ordP(f) = ordP(f q) for all P ∈ E(k). Thus, ψ(div(f)) = div(f q) is a principal divisor. Therefore, ψ induces an automorphism of the Abelian group E ̃(k). Hence, the inverse mapping ϕq is a homomorphism, too.

5.10. We write the rational morphism α as α = (f(x, y), g(x, y)) with f(x, y) = ![](images/317_4.jpg) For a suitable polynomial p(x), we have ![](images/317_5.jpg) for s(x) = x3 + Ax + B. Since s(x) has no multiple roots, s(x) is not the zero polynomial. For y = 0 there must be a pole at ![](images/317_6.jpg) Therefore, p(x) and s(x) have no common zeros.

5.11. The Frobenius morphism ϕq is an endomorphism, therefore (ϕq − 1) is one as well (according to [Theorem 5.17](#chapter05_3.xhtml_chapter05_3_4)). The kernel (except for ![](images/o.jpg)) consists of exactly the points (a, b) ∈ E(k) with a = aq and b = bq. Hence, we have (a, b) ∈ E(q). (See for example the proof of [Theorem 1.61](#chapter01_3.xhtml_chapter01_3_28)).

## Chapter 6

6.1. We denote the fact that u and υ are transposed by u ∼ υ. Then abc = a(bc) ∼ (bc)a = bac = (ba)c ∼ c(ba) = cba, but abc ≁ cba.

6.2. For the implication (i) ⇒ (ii) we may assume that M = Σ∗. Let φ(a) = 1 for all a ∈ Σ. Then φ: Σ∗ → ℕ defines a homomorphism with φ(w) = 0 if and only if w is empty (the number φ(w) is the length of w). The empty word is the neutral element of Σ∗. If pq = xy, then we write p = a1 ⋅⋅ ⋅ ak, q = ak+1 ⋅⋅ ⋅ am, x = b1 ⋅⋅ ⋅ bℓ, y = bℓ+1 ⋅⋅ ⋅ bn with ai , bj ∈ Σ. From pq = xy, we obtain m = n and ai = bi for all i ∈ {1, . . . , n}. Without loss of generality let k ≥ ℓ, otherwise we exchange (p, q) and (x, y). With u = aℓ+1 ⋅⋅ ⋅ ak, we therefore get p = xu and y = uq.

Now let M be a monoid satisfying (ii). ForM̃ = M\{1} ,we let Σ = M̃ \{ ab | a, b ∈M̃ }. The set Σ contains those elements of M which are not decomposable. By induction over φ(w), we show that each element from M can be written as a product of elements from Σ. If φ(w) = 0, then w is the neutral element, which appears as the empty product. Now let φ(w) > 0\. If w ∈ Σ, then there is nothing to show. So let w = uυ with u, υ ∈ M̃ . Then φ(u) < φ(u) + φ(υ) = φ(w). Analogously, φ(υ) < φ(w). By induction, u and υ can be written as products of elements from Σ and thus also w = uυ. This shows that M is generated by Σ.

Finally, let a1 ⋅⋅ ⋅ am = b1 ⋅⋅ ⋅ bn with ai , bj ∈ Σ. In order to show that M corresponds to the free monoid Σ∗, we have to prove that m = n and ai = bi for all i ∈ {1, . . . , m}. This is done by induction on m + n. For m = 0, we have 0 = φ(1) = φ(b1 ⋅⋅ ⋅ bn) = φ(b1) + ⋅⋅ ⋅ + φ(bn). From φ(c) > 0 for all c ∈ Σ, we obtain n = 0. Now let m ≥ 1. φ(b1 ⋅⋅ ⋅ bn) = φ(a1 ⋅⋅ ⋅ am) > 0 yields n ≥ 1\. Thus, there is u ∈ M with a1 = b1u, b2 ⋅⋅ ⋅ bn = ua2 ⋅⋅ ⋅ am or b1 = a1u, a2 ⋅⋅ ⋅ am = ub2 ⋅⋅ ⋅ bn. Without loss of generality let a1 = b1u and b2 ⋅⋅ ⋅ bn = ua2 ⋅⋅ ⋅ am. From a1, b1 ∈ Σ and the construction of Σ it follows that u = 1; this shows a1 = b1 and a2 ⋅⋅ ⋅ am = b2 ⋅⋅ ⋅ bn. Inductively, we obtain m = n and ai = bi for all i ∈ {2, . . . , m}.

6.3. Consider any nontrivial group G. Then G, viewed as a monoid, is not free. For pq = xy choose u = p−1x ∈ G. Then pu = x and q = uy.

6.4 (a) Let u ≺ υ. If u is a proper prefix of υ, then wu is a proper prefix of wυ. If u = ras and υ = rbt with r, s, t ∈ Σ∗, a, b ∈ Σ and a < b, then wu = (wr)as and wυ = (wr)bt. Thus, in both cases, wu ≺ wυ. Conversely, let wu ≺ wυ. If wu is a proper prefix of wυ, then u is a proper prefix of υ. If wu = ras and wυ = rbt and a < b, then |w| ≤ |r|. Let r' = wr. Then u = ras and υ = rbt, and therefore u ≺ υ.

6.4 (b) Since u is not a prefix of υ, we consequently have u = ras and υ = rbt with r, s, t ∈ Σ∗, a, b ∈ Σ and a < b. This yields uw = ra(sw) and υz = rb(tz) and therefore uw ≺ υz.

6.5. (i) ⇒ (ii): Suppose that w is a proper factor of w2, that is, w2 = uwυ with u ≠ ε ≠ υ. Then there are words s, t ∈ Σ∗ such that uw = wt and wυ = sw. From that we obtain |u| = |t|, |υ| = |s| and w = st = us = tυ, and further u = t and s = υ, which implies w = st = us = ts. By [Theorem 6.5](#chapter06.xhtml_chapter06_9), w is not primitive. (ii) ⇒ (i): If w = ui with i > 1 then w2 = u2i = u(ui)ui−1 and w is a proper factor of w2. (i) ⇔ (iii) holds because w = ui with i > 1, u = au' if and only if υa = u(au)i−1a = (ua)i. The root ua of υa, therefore, is the cyclic permutation of the root u of w.

6.6. Let u and υ be primitive roots. Then, without loss of generality w = ui = υj with 1 ≤ i ≤ j. For i = 1, w is primitive and therefore u = υ = w. For i ≥ 2, we have |u| + |υ| ≤ |w| and by the periodicity lemma, gcd(|u|, |υ|) is a period of w, too. But this yields u = υ.

6.7. (i) ⇒ (ii): Let υ be a proper suffix of w = uυ. We first show that υ cannot be a proper prefix of w. Assume to the contrary that w = υt. By [Theorem 6.5](#chapter06.xhtml_chapter06_9) we hace υ = (rs)k r, u = rs and t = sr for r, s ∈ Σ∗. Since w is primitive, we may assume that r ≠ ε and rs ≠ sr. Since w is a Lyndon word, we obtain w = (rs)k+1r ≺ r(rs)k+1. Using [Exercise 6.4](#chapter06.xhtml_chapter06_35) the word r can be reduced at the beginning, and we obtain (sr)k+1 ≺ (rs)k+1. Again by [Exercise 6.4](#chapter06.xhtml_chapter06_35) we can multiply this equation from the right by r and obtain (sr)k+1 r ≺ (rs)k+1r = w. This is a contradiction to w being a Lyndon word. Thus, no proper suffix of a Lyndon word w can occur as a prefix of w. If υ ≺ uυ = w, then by [Exercise 6.4](#chapter06.xhtml_chapter06_35) we have υu ≺ uυ. This is not possible because w is a Lyndon word. Therefore, w ≺ υ as required. (ii) ⇒ (i): For factorizations w = uυ, we have uυ ≺ υ ≺ υu. If w = ui with i > 1 then w ≺ u ≺ ui = w. Thus, w is primitive, and therefore a Lyndon word. In the remainder of the solution we use (i) ⇔ (ii). (i) ⇒ (iii): The statement is clear for w ∈ Σ. So let w ∉ Σ. Since all letters are Lyndon words, one can decompose w = uυ with maximal |υ|, such that u ≠ ε and υ is a Lyndon word. We have u ≺ uυ ≺ υ since uυ is a Lyndon word. It remains to show that u is a Lyndon word, too. Without loss of generality, let u ∉ Σ, otherwise u is already a Lyndon word. Now consider a proper suffix u' of u. The word uυ is not a Lyndon word because υ was chosen to be maximal. Thus, there is a suffix t of uυ with t ≺ uυ. From u' ≺ t follows u' ≺ t ≺ uυ and then t = us. The word s is a suffix of the Lyndon word υ, and thus υ ≺ s, which implies uυ ≺ us = t, a contradiction. Therefore, t ≼ u' and altogether, we obtain u ≺ uυ ≺ t ≼ u. From (ii) now follows that u is a Lyndon word, as we had to show. (iii) ⇒ (i): If w ∈ Σ, then the statement is clear. So let w = uυ with u ≺ υ for Lyndon words u, υ. We first show the auxiliary claim uυ ≺ υ. If u is not a prefix of υ, then this follows from [Exercise 6.4](#chapter06.xhtml_chapter06_35). If υ = uυ, then υ ≺ υ' because υ is a Lyndon word. But then uυ ≺ uυ' = υ. We now show that uυ ≺ s for every proper suffix s of uυ. If s is a suffix of υ, then uυ ≺ υ ≺ s. Otherwise, s = tυ. Since t is a proper suffix of u, we have u ≺ t and therefore uυ ≺ tυ = s by [Exercise 6.4](#chapter06.xhtml_chapter06_35). So uυ is a Lyndon word.

6.8. Since each letter in Σ is a Lyndon word, there exists a decomposition of w into Lyndon words. Let w = ℓ1 ⋅⋅ ⋅ ℓn be such a decomposition with minimal n. If ℓi ≺ ℓi+1 at one place i ∈ {1, . . . , n − 1}, then ℓiℓi+1 by [Exercise 6.7](#chapter06.xhtml_chapter06_38) is a Lyndon word. This is impossible since n was chosen to be minimal. Therefore, ℓn ≼ ℓn−1 ≼ ⋅⋅ ⋅ ≼ ℓ1. Thus, there is a decomposition of the required kind. It remains to show the uniqueness of this decomposition. So let ![](images/320_2.jpg) be two such decompositions. We show that ![](images/320_1.jpg) and then get the result by the inductive hypothesis for ![](images/320_3.jpg) So without loss of generality let ![](images/320_4.jpg) with i ≥ 1 and υ being a nonempty prefix of ![](images/320_6.jpg) Then by [Exercise 6.7](#chapter06.xhtml_chapter06_38), we have ℓ1 ≺ υ. Moreover, ![](images/320_5.jpg) since υ is a prefix of ![](images/320_7.jpg) Altogether, we obtain ℓ1 ≺ ℓ1, a contradiction.

## Chapter 7

7.1 (a) We can express Synt(L) as a regular set as follows:

![](images/320_8.jpg)

To see that these are the shortest words, calculate [ba]L = {a, b}∗ba{a, b}∗, [an]L = {an} for n ≥ 1, and [abbn]L = {akbk+n | k ≥ 1 }. The result follows by symmetry in a and b.

7.1 (b) Consider ab and x, y, r, s ∈ Synt(L) such that xyab ≡L ab and ab ≡L abrs. Then we have x = y = r = s = ε. Hence, [ab] ∼*D* [u] implies u = ab as words. On the other hand [aab] ∼*J* [ab] because (aab)b ≡L ab. Hence, *D* ≠ *J*.

7.1 (c) We have [abb] ≤*R* [ab], but there is no word u such that [ab] = [abbu].

7.2. As we saw in the solution of [Exercise 1.6 (a)](#chapter01_4.xhtml_chapter01_4_19), there are numbers t, p ∈ ℕ with p ≥ 1 and xt = xt+p. If we choose t and p minimal, then S = {x, . . . , xt+p−1} and n = t + p − 1\. In particular, the semigroup is uniquely determined by t ∈ {1, . . . , n} and different values for t define nonisomorphic semigroups.

7.3. The set product ⋅ defines an associative operation on the power set 2M, we let A ⋅ B = {ab ∈ M| a ∈ A, b ∈ B }. Therefore, n = (2|M|)! satisfies An = A2n for all A ⊆ M. Especially, φ(Σn) = φ(Σ)n = φ(Σ)2n = φ(Σ2n).

7.4. Let φ: M → N be a homomorphism into a finite monoid N which recognizes L. Let P = { x ∈ N | x2 ∈ φ(L) }. Then

![](images/320_14.jpg)

Thus, ![](images/320_10.jpg) and ![](images/320_11.jpg) is recognized by N.

7.5. First, let L = K1 ×K2 and for i ∈ {1, 2} let φi : Mi → Ni be a homomorphism into a finite monoid Ni with Ki = φ−i 1 (φi(Ki)). Let ψ: M1 ×M2 → N1 × N2 with ψ(m1, m2) = (φ1(m1), φ2(m2)). Then

![](images/320_13.jpg)

So, L is recognizable. The direction from right to left now follows, because the class of recognizable languages is closed under union.

For the converse, let φ: M1 ×M2 → N be a homomorphism into a finite monoid N with φ−1(φ(L)) = L. For i ∈ {1, 2}, we define the homomorphisms ψ1 : M1 → N and ψ2 : M2 → N by ψ1(m1) = φ(m1, 1) and ψ2(m2) = φ(1, m2). This yields the homomorphism ψ: M1 × M2 → N × N with ψ(m1, m2) = (ψ1(m1), ψ2(m2)). We now show that the homomorphism ψ recognizes the language L. To this end, let

![](images/321_1.jpg)

Then, we have

![](images/321_5.jpg)

and therefore ψ−1(ψ(L)) = ψ−1(ψ(ψ−1(P))) = ψ−1(P) = L. So, ψ recognizes the set L. We obtain

![](images/321_3.jpg)

that is, L is of the desired form.

7.6. We have u ∈ L(B) ⇔ q0 ⋅ u ∈ Q \ F ⇔ q0 ⋅ u ∉ F ⇔ u ∈ M \ L(A).

7.7 (a) Choose F = F1 × Q2 ∪ Q1 × F2. Then u ∈ L(*B*) if and only if (q1, q2) ⋅ u ∈ F. This is equivalent to q1 ⋅ u ∈ F1 or q2 ⋅ u ∈ F2 and therefore to u ∈ L(*A*1)∪ L(*A*2).

7.7 (b) Choose F = F1 × F2. Then u ∈ L(*B*) if and only if (q1, q2)⋅ u ∈ F. This is equivalent to q1 ⋅ u ∈ F1 and q2 ⋅ u ∈ F2 and therefore to u ∈ L(*A*1)∩ L(*A*2).

7.8 (a) We apply the Thompson construction from [Lemma 7.11](#chapter07_1.xhtml_chapter07_1_23), which yields the following automaton.

![](images/321_4.jpg)

7.8 (b) The construction of [Lemma 7.12](#chapter07_1.xhtml_chapter07_1_25) first inserts intermediate states:

![](images/322_1.jpg)

Removing 1-edges and unreachable states yields the following spelling automaton

![](images/322_2.jpg)

7.8 (c) We use the power set construction of [Theorem 7.17](#chapter07_2.xhtml_chapter07_2_10). Notice that the automaton is already minimal.

![](images/322_3.jpg)

7.8 (d) It is sufficient to interchange final and nonfinal states in B.

![](images/323_1.jpg)

7.8 (e) We use the construction from [Lemma 7.13](#chapter07_2.xhtml_chapter07_2_1) to obtain a rational expression.

First, we add the distinguished initial and final state and re-number all states. Note that in the resulting automaton there is at most one edge between any two states except for the loop at q6. Therefore, we also replace the loop’s labeling by {a, b}.

![](images/323_2.jpg)

Next, we eliminate the state q8.

![](images/323_3.jpg)

Eliminating q7 results in the following automaton.

![](images/324_1.jpg)

The next state to eliminate is q6.

![](images/324_2.jpg)

After eliminating q5, we have

![](images/324_3.jpg)

Then, we eliminate q4 ...

![](images/325_1.jpg)

... and q3.

![](images/325_2.jpg)

Thus, we obtain

![](images/325_4.jpg)

as a rational expression for the complement.

7.9. We can merge q5 and q6 into one state as well as q2, q3 and q4. This yields the following automaton.

![](images/325_3.jpg)

7.10. States in 𝓟(*A*ρ) are subsets of Q. In this automaton, we have P⋅a = { q∈Q | ∃p∈P: (q, a, p) ∈ δ }. Moreover, F is the initial state and P ⊆ Q is a final state if and only if q0 ∈ P. Since L(𝓟(*A*ρ)) = L(*A*)ρ it suffices to show that different states in 𝓟(*A*ρ) define different languages. So, let P ≠ P' and without loss of generality q ∈ P \ P'. By assumption, there is a word w = a1 ⋅⋅ ⋅ an with ai ∈ Σ and q0 ⋅ a1 ⋅⋅ ⋅ an = q. Thus, wρ = an ⋅⋅ ⋅ a1 belongs to the language of of P. Since A is deterministic, wρ can only be accepted from those states in 𝓟(*A*ρ), which contain q. In particular, wρ does not belong to the produce of P'.

7.11 (a) The claim follows using the construction in the proof of [Theorem 7.4](#chapter07_1.xhtml_chapter07_1_7) together with the fact that V is closed under direct products.

7.11 (b) The monoid Synt(L) recognizes the language L. Since V is closed under divisors, the claim finally follows from [Theorem 7.4](#chapter07_1.xhtml_chapter07_1_7).

7.12. Let (2Σ , ∪, 0) be the monoid of subsets of Σ and alph: Σ∗ → 2Σ the canonical homomorphism defined by a ↦ {a}. Then, alph is surjective and recognizes each language L which is a Boolean combination of languages of the form B∗ for B ⊆ Σ. In 2Σ the equations x2 = x and xy = yx are valid. The syntactic monoid of L is a homomorphic image of 2Σ, so the equations x2 = x and xy = yx hold there, too.

Now let φ: Σ∗ → M be a homomorphism recognizing L and let M be a monoid in which the equations x2 = x and xy = yx are valid. Let u = a1 ⋅⋅ ⋅ an be a word with ai ∈ Σ. Due to the equations in M we have φ(u) = Πa∈alph(u) φ(a). Therefore, the value φ(u) is determined by alph(u). Using the notation [A] for { u ∈ Σ∗ | alph(u) = A }, we obtain ![](images/326_1.jpg)

Thus, L is of the desired form. It should be noted that finiteness of M was not used in the proof. The image φ(Σ∗) is finite as a consequence of the equations alone.

7.13 (a) Divisors of aperiodic monoids are aperiodic. For the direction from left to right, it is therefore sufficient to consider an aperiodic group G. In G, we have 1 = gn(g−1)n = gn+1(g−1)n = g ⋅ 1 = g for n ∈ ℕ. So the group G contains only the neutral element.

Now let all group divisors of M be trivial. We set n = |M|!. After [Exercise 1.6 (b)](#chapter01_4.xhtml_chapter01_4_20), we have xn = x2n for all x ∈ M. For each x ∈ M the set U = {1} ∪ { xm |m ≥ n } is a submonoid of M. The mapping φ: U → {xm |m ≥ n } with φ(1) = xn and φ(xm) = xm for m ≥ 1 defines a surjective homomorphism since xm ⋅ xn = xn ⋅ xm = xn ⋅ xn+m' = xnxnxm' = x2nxm' = xnxm' = xm. Moreover, G = {xm | m ≥ n } is a group with neutral element xn. The inverse of xm is x(n−1)m because xm⋅x(n−1)m = xnm = xn. By assumption |{ xm | m ≥ n }| = 1 and thus xn = xn+1.

7.13 (b) If M is aperiodic, then M ∈ C follows from the Krohn–Rhodes theorem and the first part of the exercise. For the converse, we note that U2 is aperiodic, and that divisors of aperiodic monoids are aperiodic. It remains to show that the wreath product of aperiodic monoids is aperiodic. Let n ∈ ℕ and M, N be two aperiodic monoids with xn = xn+1 for all x ∈ M ∪ N. We now consider the wreath product M ≀ N and we show that (f, x)2n = (f, x)2n+1 for all (f, x) ∈ MN × N. We have

![](images/327_1.jpg)

Now, xn = xm for all m ≥ n yields

![](images/327_7.jpg)

For f ∈ MN and x ∈ N, we have xnf ∈ M and hence, (xnf)n = (xnf)n+1. In N we have x2n = x2n+1. Thus,

![](images/327_3.jpg)

This shows that M ≀ N is aperiodic.

7.14. We identify M|N| with MN. Suppose φ(a) = (fa , na) with fa : N → M and na ∈ N. Let ν(a) = na and μ(n, a) = nfa. By induction on |u|,we obtain φ(u) = (ψ(σν (u)), ν(u)) for all u ∈ A∗.

7.15. First, let M ≺ N. Then there is a submonoid U of N and a surjective homomorphism φ: U → M. The partial mapping φ: N → M defines a covering of M by N. Each preimage from φ−1(m) is a cover of m ∈ M.

For the other direction, let ψ: N → M be a covering. We define

![](images/327_4.jpg)

We have 1 ∈ U because 1 is a cover of the neutral element of M. Let â and b ̂ be covers of a, b ∈ M. Then ψ(n)ab = ψ(nâ)b = ψ(nâb̂). Thus, âb̂ is a cover of ab ∈ M. This shows that U is a submonoid of N. We define a mapping φ: U → M by φ(â) = a. Suppose that â = b̂. Then â is both a cover of a and of b. Since ψ is surjective, there exists n ∈ N with ψ(n) = 1\. Then a = ψ(n)a = ψ(nâ) = ψ(nb̂) = ψ(n)b = b. This shows that φ is well defined. Now, φ(1) = 1 and φ(âb̂) = ab = φ(â)φ(b̂) because âb̂ is a cover of ab. This shows that φ is a surjective homomorphism.

7.16. Let X = {x0, . . . , xn}, let Y = X \ {x0} and let Z = {x0, t} with t ≠ x0. We show that UX ≺ UY × UZ. For this, we define a covering ψ: UY × UZ → UX by

![](images/327_5.jpg)

A cover of the neutral element 1U is (1U, 1U), a cover of x0 is (1U , x0), and a cover of xi with i ≥ 1 is given by (xi , t); this is true because for all x ∈ UX, we have

![](images/327_6.jpg)

Thus, in all cases ψ(y, z)x = ψ((y, z) x̂).

7.17. We use the notation from the proof from [Theorem 7.41](#chapter07_3.xhtml_chapter07_3_20). We define a partial mapping ψ: (UN × Mc)N#×U1 × N# × U1 → M, and show that it is a covering. The elements of (UN × Mc)N#×U1 are written as pairs of mappings (f, g) with f : N# × U1 → UN and g : N# × U1 → Mc. For (f, g, x, e) ∈ (UN × Mc)N#×U1 × N# × U1 with x ∈ N# and e ∈ U1, we define

![](images/328_1.jpg)

For e = 1 and g(1, 1) ≠ c as well as for e = 0 and f(1, 1) = 1U we have ψ undefined. The mapping ψ is surjective since M can be written as M = N ∪ N ⋅Mc ⋅N; this follows from the fact that a product w = a1 ⋅⋅ ⋅ an with ai ∈ A either does not contain the element c, or w can be factored directly before the first c and directly behind the last c (these two occurrences of c might possibly coincide). The first part N in the union N ∪ N ⋅ M c ⋅ N is covered by e = 1, while the second part occurs as image of the elements (f, g, x, 0) with f(1, 1) ∈ N.

If w = a1 ⋅⋅ ⋅ an ∈ M and each ai is covered by âi, then â1 ⋅⋅ ⋅ ân is a cover of w. Therefore, it suffices to show that each generator a ∈ A has a cover. We let ĉ = (fc , gc , 𝟷̄, 0), and for a ≠ c we let â = (fa , ga , a, 1), where

![](images/328_5.jpg)

for x ∈ N # and e ∈ U1. Now one can easily verify that indeed covers are defined. For completeness, we present the corresponding calculations.

Let u = (f, g, x, e) ∈ (UN × Mc)N#×U1 × N# × U1 and a ∈ A \ {c}. We first consider the case e = 1 and g(1, 1) = c. Then

![](images/328_6.jpg)

Here, the product f(1, 1) x∗ is computed in UN. Recall that the mapping (x, e)fc : N# × U1 → UN is defined by ((x, e)fc )(y, k) = fc(yx, ke), the mapping f ∗ f ' is defined by (f ∗ f )(y, k) = f(y, k) f (y, k), and g ∗ g' results from (g ∗ g)(y, k) = g(y, k) ∘ g' (y, k). Let again e = 1 and g(1, 1) = c. Then

![](images/328_7.jpg)

For the second to last equality note that ![](images/329_1.jpg) For e = 0, we obtain the following computations:

![](images/329_18.jpg)

and

![](images/329_17.jpg)

Thus, ψ is a covering.

7.18. We need to prove that for all x, y ∈ M the following equivalence holds.

![](images/329_19.jpg)

By symmetry it is enough to show the implication from left to right. Hence, assume that there are x, y, z ∈ M such that x ∼*L* z ∼*R* y. Since x ∈ Mx = Mz, there exists t ∈ M with x = tz. There also exists s ∈ M with y = zs. Observe that x ∼*L* z implies xw ∼*L* zw and x ∼*R* y implies wx ∼*R* wy for all w ∈ M. Therefore, we know that tz ∼*R* ty and xs ∼*L* zs. From this we get

![](images/329_20.jpg)

7.19. Consider any s, t ∈ S. Let e = t|S|! be the idempotent power of t; see [Exercise 1.6 (a)](#chapter01_4.xhtml_chapter01_4_19). We have e2 = e and hence (se)e = se. The consequence is [s][t]ω ⊆ [se][e]ω. But this all we need to see the claim.

7.20. We first assume that φ recognizes the language L. Let α ~φ β and α ∈ L with α = u1u2 ⋅⋅ ⋅ , β = υ1υ2 ⋅⋅ ⋅ and φ(ui) = xi = φ(υi). We want to show that β ∈ L. By [Lemma 7.56](#chapter07_4.xhtml_chapter07_4_31) there exists t ∈ S and a sequence of indices 1 ≤ i1 < i2 < ⋅ ⋅⋅ with xij+1 ⋅⋅ ⋅ xij+1 = t for all j ≥ 1\. In particular, for the words ![](images/329_11.jpg) and ![](images/329_10.jpg) υij+1 ⋅⋅ ⋅ υij+, we have 1![](images/329_7.jpg) Let ![](images/329_8.jpg) and ![](images/329_12.jpg) Then ![](images/329_6.jpg) for s ∈ S and ![](images/329_13.jpg) as well as ![](images/329_9.jpg) From α ∈ [s][t]ω ∩ L follows [s][t]ω ⊆ L, and with β ∈ [s][t]ω, we finally obtain β ∈ L.

Consider α ∈ [s][t]ω ∩ L and β ∈ [s][t]ω. Then, the factorization resulting from α, β ∈ [s][t]ω yields α ∼φ β. Therefore, β ∈ L and [s][t]ω ⊆ L.

7.21. We start with a Büchi automaton A = (Q, δ, {q0}, F) where F ⊆ Q is a set of final state and δ ⊆ Q × Σ × Q.We enlarge the class of automata by allowing automata of the form (Q, δ, I, F) where now I ⊆ Q is a set of initial states and δ ⊆ Q × Σ∗ × Q is finite. An infinite word is accepted if and only if and there exists a factorization α = u1u2 ⋅⋅ ⋅ into finite words ui and a run

![](images/329_14.jpg)

which starts in q0 ∈ I and which visits final states infinitely often.

Next, we shift the acceptance conditions to transitions. We define the set of final transitions T ⊆ δ by T = {(p, u, q) ∈ δ | q ∈ F }. In this model a run as above is accepting if and only if first, q0 ∈ I and second, there are infinitely many i with (qi , ui+1, qi+1) ∈ T. It is clear that every ω-regular language can still be accepted in the new model.

Now, we reduce the class of automata again.We move again to the situation where I = {q0} and where moreover, there are no incoming transitions to q0\. This is trivial. We add a new state q0 and we add nonfinal ε-transitions from q0 to all states in I. Next, we only allow labels on transitions which are either letters or the empty word ε. This is again standard: if we have (p, u, q) ∈ δ with |u| ≥ 2 then we introduce new states and we split the transition into a path of length |u|. The new transitions are final if and only if (p, u, q) ∈ T. In the notation, we arrived at an automaton B = (Q, δ, {q0}, T) with δ ⊆ Q × (Σ ∪ {ε}) × Q and T ⊆ δ. Having such an automaton, we “flood” it with additional transitions. For each letter a ∈ Σ and each pair (p, q) ∈ ℚ× Q we check whether there is a path ![](images/330_1.jpg) which is labeled by a = aa. If (p, a, q) ∈ T, we do nothing. If (p, a, q) ∈ δ \ T, but ![](images/330_2.jpg) uses a final transition, then we augment T by replacing T with T ∪ {(p, a, q)}. If (p, a, q) ∉ δ, then then we augment δ by replacing δ with δ ∪ {(p, a, q)}. This procedure is repeatedly applied until no changes in T or δ occur anymore. The procedure terminates after at most 2 ⋅ |Σ| ⋅ |Q|2 steps. We constructed an automaton B' = (Q, δ' , {q0}, T) with δ ⊆ δ' ⊆ Q × (Σ ∪ {ε}) × Q and T ⊆ T' without changing the accepted language. The point is that we can throw away all ε-transitions in δ' we are never forced to use them. Thus, without restriction, all labels on transitions are letters. The new automaton is denoted by B'' = (Q, δ,' {q0}, T ). The final step is to shift the acceptance conditions back to states. For this, we let Q' be a disjoint copy of Q and we let Q̃ = Q ∪ Q'. For each (p, a, q) ∈ δ, we introduce an additional transition (p' , a, q) ∈ δ where p' ∈ Q' is the copy of p. Moreover, for each final transition (p, a, q) ∈ T, we introduce an additional transition (p, a, q) ∈ δ where q' ∈ Q' is the copy of q. The new set of transitions is denoted by Q̂. This yields an Büchi automaton ![](images/330_3.jpg) In this automaton all states from Q' are final. There is only one initial state and this state does not have incoming transitions. Moreover, as a matter of fact there are no transition between final states. If we compare the original language L(*A*) with L(𝓒), then we see that they are equal.

## Chapter 8

8.1. The idea is that we first compute ![](images/330_4.jpg) ∈ IRR(S) and ![](images/330_5.jpg) ∈ IRR(S) and then compare the irreducible words ŵ and ẑz letter by letter. It is therefore sufficient to give an algorithm which, on input w ∈ Σ∗, computes ![](images/330_6.jpg) ∈ IRR(S) in time ![](images/o.jpg)(|w|).

We choose δ > 0 with |ℓ| ≥ (1 + δ)|r| for all (ℓ, r) ∈ S. This is possible because S is finite and length reducing. Then we assign to each word pair (u, υ) its weight γ(u, υ) = |u| + (1 + δ)|υ|. We start with the word pair (1, w) where 1 is the empty word. Let |w| = n. Then γ(1, w) = (1 + δ)|w| = (1 + δ)n and 1 ∈ IRR(S). We keep as an invariant that we only generate word pairs (u, υ) with u ∈ IRR(S) and uυ = w in M, that is, ![](images/331_1.jpg) The goal is to get the word pair (ŵ, 1) after finitely many steps. If this is not yet attained, then υ = aυ' for some a ∈ Σ and υ'  ∈ Σ∗. If now ua ∈ IRR(S), that is, if ua is irreducible, then we replace the pair (u, υ) in one time step by the pair (ua, υ'). Here the weight has been reduced by the constant δ. Now, let ua be reducible. Then necessarily ua = uℓ for some (ℓ, r) ∈ S. In this case, we take one step to rewrite the pair (u, υ) by the pair (u'  , rυ'). For the weights we obtain γ(u'  , rυ') ≤ γ(u'ℓ, υ') = γ(ua, υ') ≤ γ(u, υ) − δ. So, in both cases the invariant is preserved. Therefore, the algorithm is correct and computes ŵ in time ![](images/331_2.jpg)

8.2. We may assume that the monoid is given as M = Γ∗/S where S ⊆ Γ∗ ×Γ∗ is finite. On input u, υ, we have to check whether ![](images/331_3.jpg) For this we run two algorithms in parallel, both of which work in stages. In stage n, the first one computes the list of words w such that ![](images/331_4.jpg) If, at some point, the first algorithm detects ![](images/331_5.jpg) then we stop with the positive answer u = υ in M.

In stage n, the second algorithm computes the list of all homomorphisms h : M →N where N is a finite monoid (say, given by its multiplication table) such that |N| ≤ n. The list is effectively computable because there are n|Γ| mappings h from Γ to N if N is a finite monoid of size n; each such mapping defines a homomorphism h : Γ∗ → N; and h defines a homomorphism h : M → N if and only if h(ℓ) = h(r) for all (ℓ, r) ∈ S. Having constructed this list of homomorphisms, we check whether h(u) ≠ h(υ). If, at some point, the second algorithm detects h(u) ≠ h(υ), then we stop with the negative answer u ≠ υ in M.

Since Mis residually finite, one of the two algorithms will eventually stop with the correct answer.

8.3 (a) The system S+ terminates because it is length-lexicographically reducing for the order on Σ induced by I+. It is locally confluent because if ![](images/331_6.jpg) then ![](images/331_7.jpg)

8.3 (b) For all pairs (a, b) ∈ I, we must have either ba → ab ∈ S or ab → ba ∈ S. Let I+ = {(a, b) ∈ Σ × Σ | ba → ab ∈ S }.

Then first I = {(a, b), (b, a) | (a, b) ∈ I+ }. Suppose that I+ is not a transitive orientation. Then there are (a, b), (b, c) ∈ I+ with (a, c) ∉ I+. That means, S contains rules ba → ab and cb → bc but no rule ca → ac. For n ∈ ℕ consider the rewritings ![](images/331_8.jpg) The factors anbn and bncn are irreducible, because if, for instance, there were another irreducible word in the class of anbn,then in this word a factor ba would have to appear. But this is not possible. Now, also cnan is irreducible because either (a, c) ∉ I or ac → ca ∈ S. Since S is finite we necessarily have cnanbn, bncnan ∈ IRR(S) for sufficiently large n, contradicting cnanbn = bncnan ∈ M(Σ, I).

8.3 (c) Let M = M (Σ, I). By virtue of ([8.2](#chapter08_1.xhtml_chapter08_1_53)) we may assign each element of M with a length. Therefore, M is generated by the elements of length 1, and this generating set is minimal. We have Σ = (M \ {1}) \ (M \ {1})2, and hence Σ is determined by M. The edge set I results from the elements from Σ, which are different but commute in M.

8.3 (d) By [Exercise 8.3 (c)](#chapter08_4.xhtml_chapter08_4_23) we have Σ = {a, b, c} and I = {(a, c), (c, a)} with ac = ca, ab ≠ ba and bc ≠ cb in M. Then abc and cab are transposed, and also cab = acb and cba are transposed. But there is no transposition of abc which directly leads to cba.

8.3 (e) All graphs with four vertices have a transitive orientation but the cycle C 5 with 5 vertices and 5 edges does not. Hence, the answer is 5.

8.4 (a) We choose a linear order for Σ. Then the system is almost identical to the system of equation ([8.3](#chapter08_2.xhtml_chapter08_2_1)) or equation ([8.4](#chapter08_2.xhtml_chapter08_2_4)), respectively. In addition, we just have to delete all squares of letters.

![](images/332_2.jpg)

8.4 (b) Let Ṽ be a disjoint copy of V and Σ = V∪Ṽ. For (a, b) ∈ E,weput (a, b), (ã, b), (a,b̃) and (ã, b̃) into I, but no other pairs. In particular, a and ã do not commute in C. We now consider the homomorphism φ: G → C, induced by a ↦ aã. (Recall that (a, b) ∈ E implies aãab̃= bb̃aã in C.) It remains to show that φ is injective. For this purpose, we first choose a linear order for Σ, in which the elements a and ̃a are disposed whenever they are adjacent to each other. Because V ⊆ Σ this also induces a linear order on Σ. Now, let 1 ≠ g ∈ G and let w ∈ V∗ be a length-lexicographically shortest word representing g. Then φ(w) is an irreducible normal form for the system SRACG from the solution of [Exercise 8.4 (a)](#chapter08_4.xhtml_chapter08_4_25), because the factors ãa and ̃aa prevent that identical elements are next to each other.

8.4 (c) The convergence of T is pure routine. We only show that φ: Σ → ![](images/f.jpg), a → {a}, induces an isomorphism φ: C(Σ, I) → ![](images/f.jpg)∗/T. For (a, b) ∈ I, we obtain φ(a)φ(b) = {a, b} in ![](images/f.jpg)∗/T. Furthermore φ(a2) = 0 = 1 in ![](images/f.jpg)∗/T for a ∈ Σ. Since φ(Σ) generates the group ![](images/f.jpg)∗/ T, the map φ is surjective. Now, consider the map ψ: ![](images/f.jpg) → C(Σ, I), F → Πa∈F a. Since F ∈ ![](images/f.jpg) is a clique, it does not matter in which order we evaluate the product Πa∈F a ∈ C(Σ, I). Because of the rules in T the map ψ induces a homomorphism F∗/T onto C(Σ, I). Since ψ(φ(a)) = a for all a ∈ Σ, the homomorphism φ is injective.

8.5. Closure under homomorphisms is straightforward from the definition. For the nonclosure under inverse homomorphisms, consider the homomorphism h :{a, b}∗ →ℤ where h(a) = 1 and h(b) = −1\. Then we have

![](images/333_2.jpg)

As a finite set {0} is rational; and a∗b∗ is rational, too.

8.6. In M,we consider the intersection R = (ac)∗b∗∩a∗(bc)∗ of two rational subsets. It is the set of all elements w ∈ M which have the same number of a’s, b’s, and c’s. Assume that R is rational and consider the projection π : M → {a, b}∗ which deletes all c’s. By [Exercise 8.5](#chapter08_4.xhtml_chapter08_4_26) we see that π(R) is rational (i.e., regular) in {a, b}∗. But this is a contradiction, because π(R) = { anbn | n ∈ ℕ} is not regular.

8.7. Let G1 and G2 be two finitely generated subgroups of a free group F. Without loss of generality, let F = F (Σ) be a finitely generated free group. By [Section 8.9](#chapter08_2.xhtml_chapter08_2_33), the sets of the reduced words in (Σ ∪ Σ−1)∗, which represent the elements of G1 and G2, are in each case regular. The intersection of regular languages is regular, and this provides a regular set for the intersection G1 ∩ G2.

8.8. Let K be the kernel of the projection F2 →ℤ, a ↦ 1, b ↦ 0\. The Schreier graph of K has as vertex set { Kan | n ∈ ℤ}, and each vertex Kan has two outgoing edges, labeled by a (to vertex Kan+1) and a−1 (to vertex Kan−1), as well as two loops with labels b and b−1, respectively.

The edges labeled with a or a−1 form a spanning tree. Let Δ be the set of edges labeled with b. By [Theorem 8.25](#chapter08_3.xhtml_chapter08_3_13), the kernel K is isomorphic to the free group F (Δ). An according isomorphism is defined in the proof of that theorem. This exactly yields the set U as the image of Δ.

8.9. Let G be a group generated by k elements and φ: G → G a surjective automorphism. Suppose that φ is not injective. Then there exists an element 1 ≠ g ∈ G with φ(g) = 1\. Since G is residually finite there exists a surjective homomorphism π : G → E onto a finite group E with π(g) ≠ 1\. Now, for n ∈ ℕ consider the homomorphism πn : G → E, given by πn(h) = π(φn(h)). Since φ is surjective, we find hn ∈ G with φn(hn) = g. Therefore, πn(hn) = π(g) ≠ 1 but πn+1(hn) = π(φ(g)) = π(1) = 1\. Hence, πm(hn) = 1 for all m > n; especially πm ≠ πn for all m ≠ n. A homomorphism from G to E is determined by the images of the k generators. Hence, there are at most |E|k homomorphisms. This is a contradiction, and therefore φ must be injective.

8.10. We show that BS(p, q) is not Hopfian if p and q do not have the same set of prime divisors. Let r be a prime number which divides p but not q. In the reverse case use the isomorphism BS(p, q) → BS(q, p) given by a ↦ a and t ↦ t−1. We consider the element [a, tap/r t−1]. Here [x, y] = xyx−1y−1, the commutator of x and y; [x, y] = 1 if and only if xy = yx. The word [a, tap/r t−1] = atap/r t−1a−1ta−p/rt−1 is Britton reduced, that is in particular [a, tap/r t−1] ≠ 1\. But it is contained in the kernel of the homomorphism φ: BS(p, q) → BS(p, q) with t ↦ t and a ↦ ar. The homomorphism φ therefore is not injective. But φ is surjective because r and q are coprime, and therefore a can be represented as a product of the elements φ(a) = ar and φ(tap/r t−1) = aq. That means, BS(p, q) is not Hopfian under the given conditions on p and q.

8.11. In the group BG(1, 2) = BS(1, 2) ∗ F(b)/{bab−1 = t}, we have baeb−1 = te and teat−e = a2e . Ifwe define A(0) = a and A(n + 1) = bA(n)b−1abA(n)−1b−1, then A(n) has only exponential length, but the normal form of A(n) has the form aτ(n).

8.12. The center is a normal subgroup in G and since G is not commutative, the quotient group G/Z(G) is not trivial. If the index of Z(G) in G is less than 4, then G/Z(G) is cyclic. Assume by contradiction that this is possible. Then there exists some a ∈ G such that g, h ∈ G can be written as products g = akb and h = aℓc, where k,ℓ ∈ ℕ and b, c ∈ Z (G). This is a contradiction because:

![](images/334_6.jpg)

Now, let us derive an upper bound for the probability that a pair (g, h) ∈ G × G satisfies gh = hg. For g ∈ G let C(g) = {h ∈ G | gh = hg } be the centralizer of g. It is a subgroup, and for g ∉ Z(G), we obtain |C(g)| ≤ |G|/2\. As we have just seen, the probability for a randomly chosen g to be in the center Z (G) is at most 1/4. In that case, every h commutes with g, but if g ∉ Z (G), then at most half of the h commute with g. Since at least 3/4 are not in the center, we conclude that the desired upper bound is given by 1/4 + 3/4 ⋅ 1/2 = 5/8.

Finally, to see that the bound is sharp consider the dihedral group D with 8 elements: the center has index 4 and the centralizer of each element outside the center has index 2\. Note that there are infinitely many groups where the bound 5/8 is sharp: if H is any finite Abelian group, then the bound is sharp for D × H, too.

8.13. Let x, y ∈ F with xy = yx. We may assume that x and y are reduced. If xy is also reduced, then this holds also for yx and the statement follows from [Theorem 6.5 (b)](#chapter06.xhtml_chapter06_11). Without loss of generality, let |x| > |y|. Then we may write x = x's and y = s−1y' for a maximum suffix s of x, which is not empty. For y = s−1, we have xy = x' = yx = yx'y−1, that is, x'y = yx', and the statement follows by induction on |x|. Therefore, without loss of generality, we may assume that y' is not the empty word. Conjugation with s gives sxs−1 = sx' and sys−1 = y's−1, and these elements commute. If sx' is not reduced then we may apply induction on |xy|, and the statement follows. Now, let sx' be reduced. But then the word sx'y's is reduced because of the maximality of |s| and the symmetry in x and y, and we may apply [Theorem 6.5 (b)](#chapter06.xhtml_chapter06_11) again.

8.14 (a) We have ρbā = i b ∘ λab ∘ i b. Therefore, it is enough to show that every Whitehead automorphism can be expressed by automorphisms of the form ia, λab and ρba. First, consider the permutation πab of Σ, which interchanges the two letters a, b with a ≠ b and leaves all other letters fixed. We have ![](images/334_2.jpg) because ![](images/334_4.jpg) and ![](images/334_3.jpg) as well as ![](images/334_5.jpg) Hence, all transpositions can be expressed as desired, and therefore all permutations of Σ because the complete permutation group of Σ is generated by the transpositions. It remains to show that the Whitehead automorphisms of the form W(a,L,R,M) can be expressed as desired. But this is possible because W(a,L,R,M) = Πb∈L∪M λab ⋅Πc∈R∪M ρca.

8.14 (b) We may assume that |Σ| ≥ 2\. The permutation group of Σ is generated by a transposition and a cyclic permutation of length |Σ|. If |Σ| = 2, we only need the transposition. Moreover, for a single pair (a, b) with a, b ∈ Σ, the automorphisms ia and λab are sufficient for generating all regular and elementary Nielsen transformations. Finally, the statement follows from [Exercise 8.14 (a)](#chapter08_4.xhtml_chapter08_4_32).

8.15. The solution can be obtained by induction on ℓ by showing min{a1, a3}, min{a2, a4}≤ Fℓ and max{a1, a3}, max{a2, a4}≤ Fℓ+1.

8.16 (a) Let A ∈ PSL(2, ℤ) be an element of order 2\. Let ![](images/335_1.jpg) In matrix representation we have

![](images/335_2.jpg)

If both b and c were 0, then we would have a = d = ±1 and hence A(z) = z for all z, in contradiction to the fact that A has order 2\. So b ≠ 0 or c ≠ 0, and a + d = 0 follows.

8.16 (b) Let ![](images/335_3.jpg) and ![](images/335_4.jpg) Suppose that, in PSL(2, ℤ), the matrix A is not conjugated to S. Since R has order 3, possibly after a suitable conjugation, we may assume that A = Ri1 S ⋅⋅ ⋅ Rim−1SRim , m ≥ 2, with 1 ≤ iℓ ≤ 2 for 1 ≤ ℓ ≤ m and i1 = im. But, as in the proof of [Theorem 8.38](#chapter08_4.xhtml_chapter08_4_17), this matrix A has infinite order, which is a contradiction. Therefore, in PSL(2, ℤ), the matrix A is conjugated to S.

8.17 (a) Let −1 be a quadratic residue modulo n. Then there are p, q ∈ ℤ with −q2 − pn = 1\. Define A ∈ PSL(2, ℤ) with ![](images/335_5.jpg) An easy calculation shows that A has order 2\. From [Exercise 8.16 (b)](#chapter08_5.xhtml_chapter08_5_2), we know that, in PSL(2, ℤ), the matrix A is conjugate to S. This means, there is a matrix X ∈ PSL(2, ℤ) with ![](images/335_6.jpg) and XSX−1 = A. Hence, we obtain

![](images/335_7.jpg)

Since n ∈ ℕ, we have n = x2 + y2.

8.17 (b) Since gcd(x, y) = 1, there exist u, υ ∈ ℤ with xυ − yu = 1\. We construct X ∈ PSL(2, ℤ) with ![](images/335_9.jpg) It follows ![](images/335_8.jpg) and q = −υy − ux. From −q2 − pn = 1, we obtain −1 ≡ q2 mod n.

8.17 (c) The case p = 2 is trivial. Now, let p ≥ 3\. For p = x2 + y2, we automatically have gcd(x, y) = 1\. Now, [Exercises 8.17 (a)](#chapter08_5.xhtml_chapter08_5_3) and [8.17 (b)](#chapter08_5.xhtml_chapter08_5_4) show that p is a sum of two squares if and only if −1 is square modulo p; and −1 is a square modulo p if and only if (ℤ/pℤ)∗ has an element of order 4\. The multiplicative group (ℤ/pℤ)∗ is cyclic and has order p − 1\. It contains an element of order 4 if and only if p ≡ 1 mod 4.

# Bibliography

[[1](#chapter07_1.xhtml_chapter07_1_6)]M. Aigner and G. M. Ziegler. Proofs from THE BOOK. Springer, 2014.

[[2](#chapter03_1.xhtml_chapter03_1_15)]W. R. Alford, A. J. Granville and C. B. Pomerance. There are infinitely many Carmichael numbers. Ann. of Math. (2), 140:703–722, 1994.

[[3](#chapter07_4.xhtml_chapter07_4_35)]A. Arnold. A syntactic congruence for rational ω-languages. Theoret. Comput. Sci., 39:333–335, 1985.

[[4](#chapter02_1.xhtml_chapter02_1_6)]F. L. Bauer. Decrypted Secrets: Methods and Maxims of Cryptology. Springer, 2006.

[[5](#chapter02_1.xhtml_chapter02_1_35)]G. Baumslag, B. Fine, M. Kreuzer and G. Rosenberger. A Course in Mathematical Cryptography. Walter de Gruyter, 2015.

[[6](#chapter08_3.xhtml_chapter08_3_3)]M. Benois. Parties rationelles du groupe libre. C. R. Acad. Sci. Paris, Sér. A, 269:1188–1190, 1969.

[[7](#chapter08_1.xhtml_chapter08_1_2)]A. Björner and F. Brenti. Combinatorics of Coxeter groups, Springer, 2005.

[[8](#chapter08_1.xhtml_chapter08_1_3)]O. Bogopolski. Introduction to group theory. European Mathematical Society, 2008.

[[9](#chapter07_5.xhtml_chapter07_5_25)]A. Boudet and H. Comon. Diophantine equations, Presburger arithmetic and finite automata. In CAAP 1996, Proceedings, volume 1059 of LNCS, pages 30–43. Springer, 1996.

[[10](#chapter08_2.xhtml_chapter08_2_26)] J. L. Britton. The word problem. Ann. of Math., 77:16–32, 1963.

[[11](#chapter07_6.xhtml_chapter07_6_10)] J. A. Brzozowski. Canonical regular expressions and minimal state graphs for definite events. In Proc. Sympos. Math. Theory of Automata (New York, 1962), pages 529–561, 1963.

[[12](#chapter07_4.xhtml_chapter07_4_12)] J. R. Büchi.Weak second-order arithmetic and finite automata. Zeitschrift für mathematische Logik und Grundlagen der Mathematik, 6:66–92, 1960.

[[13](#chapter07_4.xhtml_chapter07_4_13)] J. R. Büchi. On a decision method in restricted second-order arithmetic. In Proc. Int. Congr. for Logic, Methodology, and Philosophy of Science, pages 1–11\. Stanford Univ. Press, 1962.

[[14](#chapter02_1.xhtml_chapter02_1_7)] J. Buchmann. Introduction to Cryptography. Springer, 2014.

[[15](#chapter08_1.xhtml_chapter08_1_4)] T. Camps, V. große Rebel and G. Rosenberger. Einführung in die kombinatorische und die geometrische Gruppentheorie. Heldermann Verlag, 2008.

[[16](#chapter06.xhtml_chapter06_39)] K.-T. Chen, R. H. Fox and R. C. Lyndon. Free differential calculus, IV – The quotient groups of the lower central series. Ann. of Maths., 68(1):81–95, 1958.

[[17](#chapter08_1.xhtml_chapter08_1_33)] N. Chomsky and M.-P. Schützenberger. The algebraic theory of context-free languages. In Comp. Prog. and Formal Systems, pages 118–161\. North-Holland, 1963.

[[18](#chapter07_3.xhtml_chapter07_3_24)] A. Costa and B. Steinberg. The Schützenberger category of a semigroup. Semigroup Forum, pages 1–17, 2014.

[[19](#chapter04.xhtml_chapter04_3)] R. Crandall and C. B. Pomerance. Prime Numbers: A Computational Perspective. Springer, 2010.

[[20](#chapter08_2.xhtml_chapter08_2_2)] M. W. Davis. The geometry and topology of Coxeter groups. Princeton Univ. Press, 2008.

[[21](#chapter08_1.xhtml_chapter08_1_8)] M. Dehn. Ueber unendliche diskontinuierliche Gruppen. Math. Ann., 71:116–144, 1911.

[[22](#chapter06.xhtml_chapter06_22)] L. E. Dickson. Finiteness of the odd perfect and primitive abundant numbers with n distinct prime factors. Amer. J. Math., 35(4):413–422, 1913.

[[23](#chapter07_2.xhtml_chapter07_2_18)] V. Diekert and P. Gastin. Pure future local temporal logics are expressively complete for Mazurkiewicz traces. Inform. Comput., 204:1597–1619, 2006.

[[24](#chapter07_2.xhtml_chapter07_2_29)] V. Diekert and P. Gastin. First-order definable languages. In Logic and Automata: History and Perspectives, Texts in Logic and Games, pages 261–306\. Amsterdam Univ. Press, 2008.

[[25](#chapter07_2.xhtml_chapter07_2_18)] V. Diekert and M. Kufleitner. Bounded synchronization delay in omega-rational expressions. In CSR 2012, Proceedings, volume 7353 of LNCS, pages 89–98\. Springer, 2012.

[[26](#chapter07_2.xhtml_chapter07_2_18)] V. Diekert, M. Kufleitner, K. Reinhardt and T. Walter. Regular languages are Church–Rosser congruential. J. ACM, 62:1–39, 2015.

[[27](#Preface.xhtml_Preface_3)] V. Diekert, M. Kufleitner and G. Rosenberger. Diskrete algebraische Methoden. Walter de Gruyter, 2013.

[[28](#Preface.xhtml_Preface_2)] V. Diekert, M. Kufleitner and G. Rosenberger. Elemente der Diskreten Mathematik. Walter de Gruyter, 2013.

[[29](#chapter07_2.xhtml_chapter07_2_32)] V. Diekert, M. Kufleitner and B. Steinberg. The Krohn–Rhodes theorem and local divisors. Fundamenta Informaticae, 116(1–4):65–77, 2012.

[[30](#chapter07_2.xhtml_chapter07_2_19)] V. Diekert, M. Kufleitner and P. Weil. Star-free languages are Church–Rosser congruential. Theoret. Comput. Sci., 454:129–135, 2012.

[[31](#chapter08_2.xhtml_chapter08_2_31)] V. Diekert, J. Laun and A. Ushakov. Efficient algorithms for highly compressed data: The word problem in Higman’s group is in P. Int. J. Algebr. Comput., 22(8):1–19, 2012.

[[32](#chapter04.xhtml_chapter04_4)] M. Dietzfelbinger. Primality testing in polynomial time: From randomized algorithms to ‘PRIMES is in P’. Springer, 2004.

[[33](#chapter07_5.xhtml_chapter07_5_26)] P. D. Domich, R. Kannan and L. E. Trotter Jr. Hermite normal form computation using modulo determinant arithmetic. Math. Oper. Res., 12:50–59, 1987.

[[34](#chapter08_2.xhtml_chapter08_2_11)] C. Droms. Graph groups, coherence and three-manifolds. J. Algebra, 106(2):484–489, 1985.

[[35](#chapter08_2.xhtml_chapter08_2_10)] C. Droms. Subgroup of graph groups. J. Algebra, 110:519–522, 1987.

[[36](#chapter08_1.xhtml_chapter08_1_31)] W. Dyck. Ueber Aufstellung und Untersuchung von Gruppe und Irrationalität regulärer Riemann’scher Flächen.Math. Ann., XVII:473–509, 1881.

[[37](#chapter08_1.xhtml_chapter08_1_32)] W. Dyck. Gruppentheoretische Studien. Math. Ann., XX:1–44, 1883.

[[38](#chapter07_2.xhtml_chapter07_2_33)] S. Eilenberg. Automata, Languages, and Machines, volume B. Academic Press, 1976.

[[39](#chapter07_5.xhtml_chapter07_5_17)] S. Eilenberg and M.-P. Schützenberger. Rational sets in commutative monoids. J. Algebra, 13:173–191, 1969.

[[40](#chapter02_1.xhtml_chapter02_1_33)] T. ElGamal. A public key cryptosystem and a signature scheme based on discrete logarithms. IEEE T. Inform. Theory, 31:469–472, 1985.

[[41](#chapter04.xhtml_chapter04_5)] B. Fine and G. Rosenberger. Number theory: An introduction via the distribution of primes. Birkhäuser, 2007.

[[42](#chapter08_1.xhtml_chapter08_1_40)] M. Forester. Splittings of generalized Baumslag–Solitar groups. Geometriae Dedicata, 121:43–59, 2006.

[[43](#chapter03_3.xhtml_chapter03_3_13)] M. Fürer. Faster integer multiplication. SIAM J. Comput., 39(3):979–1005, 2009.

[[44](#chapter02_2.xhtml_chapter02_2_14)] M. R. Garey and D. S. Johnson. Computers and Intractability: A Guide to the Theory of NP-Completeness. W. H. Freeman, 1979.

[[45](#chapter07_5.xhtml_chapter07_5_18)] S. Ginsburg and E. H. Spanier. Semigroups, Presburger formulas and languages. Pac. J. Math., 16:285–296, 1966.

[[46](#chapter07_4.xhtml_chapter07_4_14)] K. Gödel. Über formal unentscheidbare Sätze der Principia Mathematica und verwandter Systeme I. Monatshefte für Mathematik und Physik, 38:173–198, 1931.

[[47](#chapter08_1.xhtml_chapter08_1_45)] M. Gromov. Hyperbolic groups. In Essays in Group Theory, number 8 in MSRI Publ., pages 75– 263\. Springer, 1987.

[[48](#chapter05_3.xhtml_chapter05_3_12)] R. Hartshorne. Algebraic Geometry. Springer, 1997.

[[49](#chapter06.xhtml_chapter06_23)] G. Higman. Ordering by divisibility in abstract algebras. P. Lond. Math. Soc., Third Series, 2:326–336, 1952.

[[50](#chapter08_2.xhtml_chapter08_2_22)] G. Higman, B. Neumann and H. Neumann. Embedding theorems for groups. J. London Math. Soc., 24:247–254, 1949.

[[51](#chapter07_2.xhtml_chapter07_2_14)] J. E. Hopcroft and J. D. Ullman. Introduction to Automata Theory, Languages and Computation. Addison-Wesley, 1979.

[[52](#chapter07_5.xhtml_chapter07_5_27)] R. Kannan and A. Bachem. Polynomial algorithms for computing the Smith and Hermite normal forms of an integer matrix. SIAM J. Comput., 8:499–507, 1979.

[[53](#chapter08_1.xhtml_chapter08_1_51)] R. M. Keller. Parallel program schemata and maximal parallelism I. Fundamental results. J. ACM, 20(3):514–537, 1973.

[[54](#chapter07_2.xhtml_chapter07_2_9)] S. C. Kleene. Representation of events in nerve nets and finite automata. In Automata Studies, pages 3–40\. Princeton Univ. Press, 1956.

[[55](#chapter03_1.xhtml_chapter03_1_10)] D. E. Knuth. The art of computer programming. Vol. 2: Seminumerical Algorithms. Addison-Wesley, 1997.

[[56](#chapter05_3.xhtml_chapter05_3_15)] N. Koblitz. Elliptic curve cryptosystems. Mathematics of Computation, 48:203–209, 1987.

[[57](#chapter05_1.xhtml_chapter05_1_3)] N. Koblitz. Introduction to Elliptic Curves and Modular Forms. Springer, 1993\. First edn. 1984.

[[58](#chapter05_3.xhtml_chapter05_3_14)] N. Koblitz. A Course in Number Theory and Cryptography. Springer, 1994.

[[59](#chapter07_2.xhtml_chapter07_2_31)] K. Krohn and J. L. Rhodes. Algebraic theory of machines. I: Prime decomposition theorem for finite semigroups and machines. Trans. Amer. Math. Soc., 116:450–464, 1965.

[[60](#chapter07_2.xhtml_chapter07_2_34)] K. Krohn, J. L. Rhodes and B. Tilson. The prime decomposition theorem of the algebraic theory of machines. In Algebraic Theory of Machines, Languages, and Semigroups, Chapter 5, pages 81–125\. Academic Press, 1968.

[[61](#chapter06.xhtml_chapter06_26)] J. B. Kruskal. Well-quasi-ordering, the Tree Theorem, and Vazsonyi’s conjecture. Trans. Amer. Math. Soc., 95(2):210–225, 1960.

[[62](#chapter07_2.xhtml_chapter07_2_24)] M. Kufleitner. Star-free languages and local divisors. In DCFS 2014, Proceedings, volume 8614 of LNCS, pages 23–28\. Springer, 2014.

[[63](#chapter07_2.xhtml_chapter07_2_37)] G. Lallement. On the prime decomposition theorem for finite monoids. Math. Systems Theory, 5:8–12, 1971.

[[64](#chapter07_2.xhtml_chapter07_2_38)] G. Lallement. Augmentations and wreath products of monoids. Semigroup Forum, 21(1):89– 90, 1980.

[[65](#chapter05_3.xhtml_chapter05_3_13)] S. Lang. Elliptic Curves: Diophantine Analysis. Grundlehren der mathematischen Wissenschaften 231\. Springer, 2010.

[[66](#chapter06.xhtml_chapter06_2)] M. Lothaire. Combinatorics on Words, volume 17 of Encyclopedia of Mathematics and Its Applications. Addison-Wesley, 1983\. Reprinted by Cambridge Univ. Press, 1997.

[[67](#chapter06.xhtml_chapter06_2)] M. Lothaire. Algebraic Combinatorics on Words, volume 90 of Encyclopedia of Mathematics and Its Applications. Cambridge Univ. Press, 2002.

[[68](#chapter06.xhtml_chapter06_3)] M. Lothaire. Applied Combinatorics on Words, volume 105 of Encyclopedia of Mathematics and Its Applications. Cambridge Univ. Press, 2005.

[[69](#chapter08_1.xhtml_chapter08_1_5)] R. Lyndon and P. Schupp. Combinatorial Group Theory. Springer, 2001. First edn. 1977.

[[70](#chapter08_3.xhtml_chapter08_3_24)] W. Magnus, A. Karrass and D. Solitar. Combinatorial Group Theory. Interscience Publishers, 1966\. Reprint of the 2nd edn. (1976): 2004.

[[71](#chapter07_5.xhtml_chapter07_5_23)] Yu. V. Matiyasevich. Hilbert’s Tenth Problem. MIT Press, 1993.

[[72](#chapter08_1.xhtml_chapter08_1_52)] A. Mazurkiewicz. Concurrent program schemes and their interpretations. DAIMI Rep. PB 78, Aarhus University, 1977.

[[73](#chapter01_1.xhtml_chapter01_1_18)] J. H. McKay. Another proof of Cauchy’s group theorem. Am. Math. Monthly, 66:119, 1959.

[[74](#chapter07_2.xhtml_chapter07_2_5)] J. D. McKnight. Kleene quotient theorem. Pac. J. Math., pages 1343–1352, 1964.

[[75](#chapter02_2.xhtml_chapter02_2_15)] R. Merkle and M. M. Hellman. Hiding information and signatures in trapdoor knapsacks. IEEE T. Inform. Theory, 24(5):525–530, 1978.

[[76](#chapter05_3.xhtml_chapter05_3_16)] V. Miller. Use of elliptic curves in cryptography. In Advances in Cryptology – CRYPTO 85, volume 218 of LNCS, pages 417–426, Springer, Berlin, 1985.

[[77](#chapter07_1.xhtml_chapter07_1_13)] E. F. Moore. Gedanken-Experiments on Sequential Machines. In Automata Studies, pages 129–153\. Princeton Univ. Press, Princeton, New Jersey, 1956.

[[78](#chapter08_2.xhtml_chapter08_2_32)] A. G. Myasnikov, A. Ushakov and W. Dong-Wook. The Word Problem in the Baumslag group with a non-elementary Dehn function is polynomial time decidable. J. Algebra, 345:324–342, 2011.

[[79](#chapter04.xhtml_chapter04_14)] M. Nair. On Chebyshev-type inequalities for primes. Am. Math. Monthly, 89(2):126–129, 1982.

[[80](#chapter06.xhtml_chapter06_24)] C. St. J. A. Nash-Williams. On well-quasi-ordering finite trees. Mathematical Proceedings of the Cambridge Philosophical Society, 59(04):833–835, 1963.

[[81](#chapter07_1.xhtml_chapter07_1_17)] A. Nerode. Linear automaton transformations. Proc. Amer. Math. Soc, 9(4):541–544, 1958.

[[82](#chapter08_3.xhtml_chapter08_3_8)] J. Nielsen. Om regning med ikke-kommutative faktorer og dens anvendelse i gruppeteorien. Mat. Tidsskr. B, 1921:78–94, 1921.

[[83](#chapter08_3.xhtml_chapter08_3_23)] J. Nielsen. Die Isomorphismengruppe der freien Gruppen. Math. Ann., 91, 1924.

[[84](#chapter08_2.xhtml_chapter08_2_30)] A. N. Platonov. An isoparametric function of the Baumslag–Gersten group. (Russian) Vestnik Moskov. Univ. Ser. I Mat. Mekh., 3:12–17, 2004\. Russian. Engl. transl. Moscow Univ. Math. Bull. 59(3):12–17, 2004.

[[85](#chapter03_2.xhtml_chapter03_2_1)] C. B. Pomerance, J. L. Selfridge and S. S. Wagstaff Jr. The pseudoprimes to 25 ⋅ 109\. Math. Comput., 35:1003–1026, 1980.

[[86](#chapter07_5.xhtml_chapter07_5_14)] M. Presburger. Über die Vollständigkeit eines gewissen Systems der Arithmetik ganzer Zahlen, in welchem die Addition als einzige Operation hervortritt. Comptes Rendus du I congrès de Mathématiciens des Pays Slaves, pages 92–101, 1929.

[[87](#chapter07_2.xhtml_chapter07_2_35)] J. L. Rhodes and B. Steinberg. The q-theory of finite semigroups. Springer, 2009.

[[88](#chapter06.xhtml_chapter06_31)] N. Robertson and P. D. Seymour. Graph minors. XX. Wagner’s conjecture. J. Comb. Theory, Ser. B, 92:325–357, 2004.

[[89](#chapter01_4.xhtml_chapter01_4_15)] G. Rousseau. On the Jacobi symbol. Journal of Number Theory, 48(1):109–111, 1994.

[[90](#chapter05_1.xhtml_chapter05_1_4)] B. Schoeneberg. Elliptic Modular Functions. Springer, 1974.

[[91](#chapter03_3.xhtml_chapter03_3_12)] A. Schönhage and V. Strassen. Schnelle Multiplikation großer Zahlen. Computing, 7:281–292, 1971.

[[92](#chapter07_2.xhtml_chapter07_2_17)] M.-P. Schützenberger. On finite monoids having only trivial subgroups. Inf. Control, 8:190–194, 1965.

[[93](#chapter08_1.xhtml_chapter08_1_6)] J.-P. Serre. Trees. Springer, 1980\. French original 1977.

[[94](#chapter02_2.xhtml_chapter02_2_7)] A. Shamir. How to share a secret. Commun. ACM, 22:612–613, 1979.

[[95](#chapter02_2.xhtml_chapter02_2_16)] A. Shamir. A polynomial-time algorithm for breaking the basic Merkle–Hellman cryptosystem. IEEE Trans. Inform. Theor., 30:699–704, 1984.

[[96](#chapter02_1.xhtml_chapter02_1_17)] C. E. Shannon. Communication theory of secrecy systems. Bell System Technical Journal Volume, XXVIII:656–715, 1949.

[[97](#chapter05_3.xhtml_chapter05_3_11)] J. H. Silverman. The Arithmetic of Elliptic Curves. Springer, 2009.

[[98](#chapter08_1.xhtml_chapter08_1_46)] C. Squier. Word problems and a homological finiteness condition for monoids. J. Pure Appl. Algebra, 49:201–217, 1987.

[[99](#chapter08_3.xhtml_chapter08_3_9)] J. R. Stallings. Topology of finite graphs. Invent. Math., 71:551–565, 1983.

[[100](#chapter08_1.xhtml_chapter08_1_9)] J. Stillwell. Classical Topology and Combinatorial Group Theory. Springer, 1993.

[[101](#chapter07_2.xhtml_chapter07_2_36)] H. Straubing. Finite Automata, Formal Logic, and Circuit Complexity. Birkhäuser, 1994.

[[102](#chapter07_4.xhtml_chapter07_4_34)] W. Thomas. Automata on infinite objects. In Handbook of Theoretical Computer Science, Chapter 4, pages 133–191\. Elsevier, 1990.

[[103](#chapter07_1.xhtml_chapter07_1_22)] K. Thompson. Regular expression search algorithm. Commun. ACM, 11:410–422, 1968.

[[104](#chapter08_1.xhtml_chapter08_1_10)] H. Tietze. Ueber die topologische Invarianten mehrdimensionaler Mannigfaltigkeiten. Monatsh. Math., 19:1–118, 1908.

[[105](#chapter08_1.xhtml_chapter08_1_39)] S. Waack. Tape complexity of word problems. In FCT 1981, Proceedings, volume 117 of LNCS, pages 467–471\. Springer, 1981.

[[106](#chapter08_1.xhtml_chapter08_1_41)] S. Waack. The parallel complexity of some constructions in combinatorial group theory. J. Inf. Process. Cybern., 26(5–6):265–281, 1990.

[[107](#chapter08_3.xhtml_chapter08_3_27)] R. D. Wade. Folding free-group automorphisms. Q. J. Math., 2013.

[[108](#chapter05_3.xhtml_chapter05_3_10)] L. C. Washington. Elliptic Curves: Number Theory and Cryptography. Chapman & Hall/CRC, 2008.

[[109](#chapter08_1.xhtml_chapter08_1_42)] A. Weiß. The word and conjugacy problem in generalized Baumslag–Solitar groups is solvable in logspace. ALFA 2015, Bordeaux, June 15–17, 2015\. Unpublished, 2015.

[[110](#chapter02_1.xhtml_chapter02_1_25)] M. J. Wiener. Cryptanalysis of short RSA secret exponents. IEEE T. Inform. Theory, 36(3):553–558, 1990.

[[111](#chapter08_2.xhtml_chapter08_2_12)] D. Wise. From Riches to Raags: 3-Manifolds, Right-Angled Artin Groups, and Cubical Geometry. American Mathematical Society, 2012.

[[112](#chapter08_2.xhtml_chapter08_2_6)] C. Wrathall. The word problem for free partially commutative groups. J. Symbolic Comput., 6(1):99–104, 1988.

# Index

A

Abel, N. H. [1](#chapter01_1.xhtml_chapter01_1_2), [2](#chapter01_1.xhtml_chapter01_1_4), [3](#chapter01_2.xhtml_chapter01_2_1)

Abelian [1](#chapter01_1.xhtml_chapter01_1_4)

accepted language [1](#chapter07_4.xhtml_chapter07_4_15)

accepted set [1](#chapter07_1.xhtml_chapter07_1_8), [2](#chapter07_1.xhtml_chapter07_1_19)

accepting run [1](#chapter07_1.xhtml_chapter07_1_19)

addition chain [1](#chapter03_1.xhtml_chapter03_1_9)

addition law on elliptic curve [1](#chapter05_1.xhtml_chapter05_1_14)

addition theorem [1](#chapter01_2.xhtml_chapter01_2_8)

Adleman, L. V, [1](#chapter02_1.xhtml_chapter02_1_24)

Advanced Encryption Standard [1](#chapter01_3.xhtml_chapter01_3_17)

AES see [Advanced Encryption Standard](#Index_1.xhtml_Index_1_2)

Agrawal, M. VI, [1](#chapter04.xhtml_chapter04_1)

AKS primality test [1](#chapter04.xhtml_chapter04_1)

algebraic closure [1](#chapter01_3.xhtml_chapter01_3_25)

algebraic number [1](#chapter01_1.xhtml_chapter01_1_1)

algebraically closed field [1](#chapter01_3.xhtml_chapter01_3_25)

algorithm

–AKS [1](#chapter04.xhtml_chapter04_1)

–baby-step giant-step [1](#chapter03_2.xhtml_chapter03_2_18)

–binary gcd [1](#chapter03_1.xhtml_chapter03_1_9), [2](#chapter03_3.xhtml_chapter03_3_17), [3](#chapter09_2.xhtml_chapter09_2_3)

–Brzozowski’s minimization [1](#chapter07_6.xhtml_chapter07_6_8)

–Cipolla [1](#chapter03_2.xhtml_chapter03_2_5)

–Dehn [1](#chapter08_1.xhtml_chapter08_1_44)

–division [1](#chapter03_3.xhtml_chapter03_3_2)

–elliptic curve integer factorization [1](#chapter05_2.xhtml_chapter05_2_9)

–Euclidean [1](#chapter01_2.xhtml_chapter01_2_10)

–extended Euclidean [1](#chapter01_2.xhtml_chapter01_2_14)

–fast exponentiation [1](#chapter03_1.xhtml_chapter03_1_8)

–fast Fourier transform [1](#chapter03_3.xhtml_chapter03_3_5)

–fast modular exponentiation [1](#chapter03_1.xhtml_chapter03_1_8)

–index calculus [1](#chapter03_2.xhtml_chapter03_2_25)

–Karatsuba [1](#chapter03_2.xhtml_chapter03_2_27)

–marking [1](#chapter07_1.xhtml_chapter07_1_11)

–Moore’s minimization [1](#chapter07_1.xhtml_chapter07_1_11)

–Pohlig–Hellman [1](#chapter03_2.xhtml_chapter03_2_22)

–Pollard’s p −[1](#chapter01_1.xhtml_chapter01_1_1) [2](#chapter03_2.xhtml_chapter03_2_11)

–Pollard’s ρ (factorization) [1](#chapter03_2.xhtml_chapter03_2_11)

–Pollard’s ρ (logarithm) [1](#chapter03_2.xhtml_chapter03_2_20)

–probabilistic primality test [1](#chapter03_1.xhtml_chapter03_1_12)

–quadratic sieve [1](#chapter03_2.xhtml_chapter03_2_13)

–Schönhage–Strassen [1](#chapter03_3.xhtml_chapter03_3_9)

–Tonelli [1](#chapter03_2.xhtml_chapter03_2_3)

Alice VIII, [1](#chapter02_1.xhtml_chapter02_1_5)

almost all [1](#chapter01_2.xhtml_chapter01_2_27)

alphabet [1](#chapter06.xhtml_chapter06_1), [2](#chapter06.xhtml_chapter06_6), [3](#chapter08_1.xhtml_chapter08_1_12)

alternating group [1](#chapter01_2.xhtml_chapter01_2_1)

amalgamated product [1](#chapter08_2.xhtml_chapter08_2_15)

antichain [1](#chapter06.xhtml_chapter06_15)

aperiodic monoid [1](#chapter07_2.xhtml_chapter07_2_15)

arc [1](#chapter08_3.xhtml_chapter08_3_12)

Arnold, A. [1](#chapter07_4.xhtml_chapter07_4_32), [2](#chapter07_5.xhtml_chapter07_5_1)

Artin, E. [1](#chapter08_1.xhtml_chapter08_1_54)

associativity [1](#chapter01_1.xhtml_chapter01_1_4)

–elliptic curves [1](#chapter05_1.xhtml_chapter05_1_14), [2](#chapter05_1.xhtml_chapter05_1_25)

asymptotic estimate [1](#chapter03_1.xhtml_chapter03_1_1)

Atkin, A.O. L. [1](#chapter05_2.xhtml_chapter05_2_17)

attack

–brute-force [1](#chapter02_1.xhtml_chapter02_1_8)

–chosen-ciphertext [1](#chapter02_1.xhtml_chapter02_1_5)

–chosen-plaintext [1](#chapter02_1.xhtml_chapter02_1_5)

–ciphertext-only [1](#chapter02_1.xhtml_chapter02_1_5)

–known-plaintext [1](#chapter02_1.xhtml_chapter02_1_5)

–man-in-the-middle [1](#chapter02_1.xhtml_chapter02_1_23)

–Shamir [1](#chapter02_2.xhtml_chapter02_2_17)

–Wiener [1](#chapter02_1.xhtml_chapter02_1_24)

augmented monoid [1](#chapter07_3.xhtml_chapter07_3_18)

automata minimization [1](#chapter07_1.xhtml_chapter07_1_11)

–Brzozowski [1](#chapter07_6.xhtml_chapter07_6_8)

–Moore [1](#chapter07_1.xhtml_chapter07_1_11)

automaton [1](#chapter07_1.xhtml_chapter07_1_8)

–Büchi [1](#chapter07_4.xhtml_chapter07_4_15)

–complement [1](#chapter07_6.xhtml_chapter07_6_8)

–complete [1](#chapter07_1.xhtml_chapter07_1_8), [2](#chapter07_1.xhtml_chapter07_1_21)

–deterministic [1](#chapter07_1.xhtml_chapter07_1_8), [2](#chapter07_1.xhtml_chapter07_1_21)

–deterministic Büchi [1](#chapter07_4.xhtml_chapter07_4_15)

–equivalent [1](#chapter07_1.xhtml_chapter07_1_21)

–finite [1](#chapter07_1.xhtml_chapter07_1_19), [2](#chapter07_1.xhtml_chapter07_1_26)

–minimal [1](#chapter07_1.xhtml_chapter07_1_9)

–minimization [1](#chapter07_1.xhtml_chapter07_1_11)

–nondeterministic [1](#chapter07_1.xhtml_chapter07_1_19)

–product [1](#chapter07_6.xhtml_chapter07_6_8)

–run [1](#chapter07_1.xhtml_chapter07_1_19), [2](#chapter07_1.xhtml_chapter07_1_26), [3](#chapter07_4.xhtml_chapter07_4_15)

–spelling [1](#chapter07_1.xhtml_chapter07_1_21), [2](#chapter07_2.xhtml_chapter07_2_13)

–subset [1](#chapter07_2.xhtml_chapter07_2_8)

–trim [1](#chapter07_6.xhtml_chapter07_6_2)

–with rational labels [1](#chapter07_1.xhtml_chapter07_1_26)

automorphism [1](#chapter01_1.xhtml_chapter01_1_5)

–Frobenius [1](#chapter01_2.xhtml_chapter01_2_10), [2](#chapter05_3.xhtml_chapter05_3_1)

–graph [1](#chapter01_1.xhtml_chapter01_1_29)

–inner [1](#chapter08_2.xhtml_chapter08_2_13)

–Whitehead [1](#chapter08_3.xhtml_chapter08_3_22)

automorphism group [1](#chapter01_1.xhtml_chapter01_1_29)

axiom of choice [1](#chapter01_3.xhtml_chapter01_3_25)

B

baby-step giant-step algorithm [1](#chapter03_2.xhtml_chapter03_2_18)

bad sequence [1](#chapter06.xhtml_chapter06_15)

basis of a free group [1](#chapter08_1.xhtml_chapter08_1_27)

Bass, H. [1](#chapter08_2.xhtml_chapter08_2_27)

Baumslag, G. [1](#chapter08_1.xhtml_chapter08_1_35)

Baumslag group [1](#chapter08_2.xhtml_chapter08_2_27)

Baumslag–Gersten group [1](#chapter08_2.xhtml_chapter08_2_29)

Baumslag–Solitar group [1](#chapter08_1.xhtml_chapter08_1_35)

Benois, M. [1](#chapter08_3.xhtml_chapter08_3_1), [2](#chapter08_3.xhtml_chapter08_3_5)

Benois’ theorem [1](#chapter08_3.xhtml_chapter08_3_5)

Bézout, É. [1](#chapter01_2.xhtml_chapter01_2_14)

Bézout’s lemma [1](#chapter01_2.xhtml_chapter01_2_14)

big-![](images/o.jpg) see [![](images/o.jpg)-notation](#Index_2.xhtml_Index_2_1)

binary gcd [1](#chapter03_1.xhtml_chapter03_1_9), [2](#chapter03_3.xhtml_chapter03_3_17), [3](#chapter09_2.xhtml_chapter09_2_3)

binomial coefficient [1](#chapter01_2.xhtml_chapter01_2_8)

binomial expansion see [binomial theorem](#Index_1.xhtml_Index_1_7)

binomial theorem [1](#chapter01_2.xhtml_chapter01_2_8)

Birkhoff, G. [1](#chapter01_1.xhtml_chapter01_1_2)

birthday paradox [1](#chapter03_1.xhtml_chapter03_1_7)

birthday paradox algorithm see [ρ](#Index_2.xhtml_Index_2_8) [algorithm](#Index_2.xhtml_Index_2_8)

Bob VIII, [1](#chapter02_1.xhtml_chapter02_1_5)

Bombelli, R. [1](#chapter01_1.xhtml_chapter01_1_1)

Boone, W. W. [1](#chapter08_1.xhtml_chapter08_1_1)

Brandt monoid [1](#chapter07_4.xhtml_chapter07_4_4)

bridge [1](#chapter08_3.xhtml_chapter08_3_29)

Britton, J. L. [1](#chapter08_2.xhtml_chapter08_2_27)

Britton reduction [1](#chapter08_2.xhtml_chapter08_2_27)

brute-force attack [1](#chapter02_1.xhtml_chapter02_1_8)

Brzozowski, J. A. [1](#chapter07_6.xhtml_chapter07_6_9)

Brzozowski’s minimization algorithm [1](#chapter07_6.xhtml_chapter07_6_8)

B-smooth number [1](#chapter03_2.xhtml_chapter03_2_15), [2](#chapter03_2.xhtml_chapter03_2_25)

Büchi automaton [1](#chapter07_4.xhtml_chapter07_4_15)

–deterministic [1](#chapter07_4.xhtml_chapter07_4_15)

–run [1](#chapter07_4.xhtml_chapter07_4_15)

Büchi, J. R. VII, [1](#chapter07_4.xhtml_chapter07_4_10), [2](#chapter07_4.xhtml_chapter07_4_22), [3](#chapter07_5.xhtml_chapter07_5_1), [4](#chapter07_5.xhtml_chapter07_5_2), [5](#chapter07_5.xhtml_chapter07_5_6)

Büchi’s theorem [1](#chapter07_5.xhtml_chapter07_5_2), [2](#chapter07_5.xhtml_chapter07_5_6)

C

Caesar, G. J. [1](#chapter02_1.xhtml_chapter02_1_8)

Caesar’s cipher [1](#chapter02_1.xhtml_chapter02_1_8)

cancellative monoid [1](#chapter08_2.xhtml_chapter08_2_3)

Cardano, G. [1](#chapter01_1.xhtml_chapter01_1_1)

Carmichael number [1](#chapter03_1.xhtml_chapter03_1_12)

Carmichael, R. D. [1](#chapter03_1.xhtml_chapter03_1_12)

Cauchy, A. L. [1](#chapter01_1.xhtml_chapter01_1_16)

Cauchy’s theorem [1](#chapter01_1.xhtml_chapter01_1_16)

center of a group [1](#chapter08_4.xhtml_chapter08_4_12), [2](#chapter08_4.xhtml_chapter08_4_28)

centralizer [1](#chapter09_4.xhtml_chapter09_4_8)

chain [1](#chapter06.xhtml_chapter06_15)

channel encoding [1](#chapter02_1.xhtml_chapter02_1_3)

characteristic [1](#chapter01_2.xhtml_chapter01_2_6)

chinese remainder theorem [1](#chapter01_2.xhtml_chapter01_2_23)

Chomsky, A. N. [1](#chapter07_1.xhtml_chapter07_1_1)

Church, A. [1](#chapter08_1.xhtml_chapter08_1_14)

Church–Rosser property [1](#chapter08_1.xhtml_chapter08_1_17)

cipher [1](#chapter02_1.xhtml_chapter02_1_3)

–Caesar [1](#chapter02_1.xhtml_chapter02_1_8)

–monoalphabetic [1](#chapter02_1.xhtml_chapter02_1_8)

–polyalphabetic [1](#chapter02_1.xhtml_chapter02_1_10)

–shift [1](#chapter02_1.xhtml_chapter02_1_8)

–Vigenère [1](#chapter02_1.xhtml_chapter02_1_12)

ciphertext [1](#chapter02_1.xhtml_chapter02_1_3)

Cipolla, M. [1](#chapter03_2.xhtml_chapter03_2_5)

Cipolla’s algorithm [1](#chapter03_2.xhtml_chapter03_2_5)

closed formula see [sentence](#Index_2.xhtml_Index_2_15)

coarsening [1](#chapter06.xhtml_chapter06_20)

coefficient [1](#chapter01_2.xhtml_chapter01_2_27)

–leading [1](#chapter01_2.xhtml_chapter01_2_27)

coincidence index [1](#chapter02_1.xhtml_chapter02_1_13)

collision resistant function [1](#chapter02_1.xhtml_chapter02_1_34)

commutative [1](#chapter01_1.xhtml_chapter01_1_4)

commutative ring [1](#chapter01_2.xhtml_chapter01_2_1)

comparable elements [1](#chapter06.xhtml_chapter06_15)

complement automaton [1](#chapter07_6.xhtml_chapter07_6_8)

complete automaton [1](#chapter07_1.xhtml_chapter07_1_8), [2](#chapter07_1.xhtml_chapter07_1_21)

complete rewriting system [1](#chapter08_1.xhtml_chapter08_1_17)

complex product [1](#chapter08_1.xhtml_chapter08_1_54)

compression see [data compression](#Index_1.xhtml_Index_1_11)

compression function [1](#chapter02_1.xhtml_chapter02_1_34)

computational security [1](#chapter02_1.xhtml_chapter02_1_5)

concatenation [1](#chapter06.xhtml_chapter06_1), [2](#chapter08_1.xhtml_chapter08_1_12)

concurrency [1](#chapter08_1.xhtml_chapter08_1_49)

confluent [1](#chapter08_1.xhtml_chapter08_1_17)

–locally [1](#chapter08_1.xhtml_chapter08_1_17)

–strongly [1](#chapter08_1.xhtml_chapter08_1_17)

congruence [1](#chapter07_1.xhtml_chapter07_1_5), [2](#chapter08_1.xhtml_chapter08_1_22)

–syntactic [1](#chapter07_1.xhtml_chapter07_1_5), [2](#chapter07_4.xhtml_chapter07_4_32)

congruent [1](#chapter01_1.xhtml_chapter01_1_5), [2](#chapter01_2.xhtml_chapter01_2_3)

conjugacy problem [1](#chapter08_1.xhtml_chapter08_1_1)

conjugate element [1](#chapter06.xhtml_chapter06_6)

constant polynomial [1](#chapter01_2.xhtml_chapter01_2_27)

construction

–subset [1](#chapter07_2.xhtml_chapter07_2_8)

–Thompson [1](#chapter07_1.xhtml_chapter07_1_21)

content see [alphabet](#Index_1.xhtml_Index_1_3)

convergent rewriting system [1](#chapter08_1.xhtml_chapter08_1_17)

convolution product [1](#chapter03_3.xhtml_chapter03_3_4)

coprime [1](#chapter01_1.xhtml_chapter01_1_5), [2](#chapter01_2.xhtml_chapter01_2_10), [3](#chapter01_3.xhtml_chapter01_3_9)

coset [1](#chapter01_1.xhtml_chapter01_1_7)

–left [1](#chapter01_1.xhtml_chapter01_1_7)

–right [1](#chapter01_1.xhtml_chapter01_1_7)

cover [1](#chapter07_6.xhtml_chapter07_6_9)

covering [1](#chapter07_6.xhtml_chapter07_6_9)

Coxeter group [1](#chapter08_1.xhtml_chapter08_1_54)

–right-angled [1](#chapter08_2.xhtml_chapter08_2_8)

Coxeter, H. [1](#chapter08_1.xhtml_chapter08_1_54)

critical pair [1](#chapter08_1.xhtml_chapter08_1_24)

–factor [1](#chapter08_1.xhtml_chapter08_1_24)

–overlap [1](#chapter08_1.xhtml_chapter08_1_24)

cryptanalysis [1](#chapter02_1.xhtml_chapter02_1_1)

cryptographic system [1](#chapter02_1.xhtml_chapter02_1_3)

cryptography [1](#chapter02_1.xhtml_chapter02_1_1)

cryptosystem [1](#chapter02_1.xhtml_chapter02_1_3)

–asymmetric [1](#chapter02_1.xhtml_chapter02_1_21)

–Caesar’s cipher [1](#chapter02_1.xhtml_chapter02_1_8)

–Diffie–Hellman [1](#chapter02_1.xhtml_chapter02_1_23), [2](#chapter02_1.xhtml_chapter02_1_29)

–ElGamal [1](#chapter02_1.xhtml_chapter02_1_23), [2](#chapter02_1.xhtml_chapter02_1_31)

–elliptic Diffie–Hellman [1](#chapter05_2.xhtml_chapter05_2_4)

–elliptic ElGamal [1](#chapter05_2.xhtml_chapter05_2_6)

–key exchange [1](#chapter02_1.xhtml_chapter02_1_29)

–Merkle–Hellman [1](#chapter02_1.xhtml_chapter02_1_23), [2](#chapter02_2.xhtml_chapter02_2_12)

–monoalphabetic cipher [1](#chapter02_1.xhtml_chapter02_1_8)

–multi-prime RSA [1](#chapter02_2.xhtml_chapter02_2_27)

–polyalphabetic cipher [1](#chapter02_1.xhtml_chapter02_1_10)

–public-key [1](#chapter02_1.xhtml_chapter02_1_23)

–Rabin [1](#chapter02_1.xhtml_chapter02_1_23), [2](#chapter02_1.xhtml_chapter02_1_26)

–RSA [1](#chapter02_1.xhtml_chapter02_1_23), [2](#chapter02_1.xhtml_chapter02_1_24), [3](#chapter03_1.xhtml_chapter03_1_30)

–shift cipher [1](#chapter02_1.xhtml_chapter02_1_8)

–symmetric [1](#chapter02_1.xhtml_chapter02_1_3)

–Vernam one-time pad [1](#chapter02_1.xhtml_chapter02_1_18)

–Vigenére cipher [1](#chapter02_1.xhtml_chapter02_1_12)

curve [1](#chapter05_1.xhtml_chapter05_1_5)

–elliptic [1](#chapter05_1.xhtml_chapter05_1_1), [2](#chapter05_1.xhtml_chapter05_1_6), [3](#chapter05_2.xhtml_chapter05_2_2)

–pseudo- [1](#chapter05_2.xhtml_chapter05_2_6)

cyclic group [1](#chapter01_1.xhtml_chapter01_1_12)

cyclic semigroup [1](#chapter07_6.xhtml_chapter07_6_8)

cyclically reduced word [1](#chapter08_3.xhtml_chapter08_3_19)

D

𝒟-class [1](#chapter07_3.xhtml_chapter07_3_25)

Damgård, I. B. [1](#chapter02_1.xhtml_chapter02_1_37)

data compression [1](#chapter02_1.xhtml_chapter02_1_3), [2](#chapter02_1.xhtml_chapter02_1_13)

Davis, M. [1](#chapter07_5.xhtml_chapter07_5_22)

De Morgan, A. [1](#chapter07_2.xhtml_chapter07_2_15)

decoding function [1](#chapter02_1.xhtml_chapter02_1_3)

decomposition

–Krohn–Rhodes [1](#chapter07_2.xhtml_chapter07_2_27), [2](#chapter07_2.xhtml_chapter07_2_39)

decreasing sequence [1](#chapter06.xhtml_chapter06_15)

decryption function [1](#chapter02_1.xhtml_chapter02_1_3)

defining relation [1](#chapter08_1.xhtml_chapter08_1_22)

degree

–divisor [1](#chapter05_1.xhtml_chapter05_1_24)

–endomorphism [1](#chapter05_3.xhtml_chapter05_3_7)

–polynomial [1](#chapter01_2.xhtml_chapter01_2_27), [2](#chapter05_1.xhtml_chapter05_1_19)

degree formula [1](#chapter01_2.xhtml_chapter01_2_28)

Dehn function [1](#chapter08_2.xhtml_chapter08_2_29)

Dehn, M. [1](#chapter08_1.xhtml_chapter08_1_1)

Dehn’s algorithm [1](#chapter08_1.xhtml_chapter08_1_44)

del Ferro, S. [1](#chapter01_1.xhtml_chapter01_1_1)

dependence alphabet [1](#chapter08_2.xhtml_chapter08_2_3)

derivative [1](#chapter01_2.xhtml_chapter01_2_4), [2](#chapter01_3.xhtml_chapter01_3_3)

Descartes, R. [1](#chapter01_4.xhtml_chapter01_4_27)

Descartes’ rule of signs [1](#chapter01_4.xhtml_chapter01_4_27)

deterministic automaton [1](#chapter07_1.xhtml_chapter07_1_8), [2](#chapter07_1.xhtml_chapter07_1_21)

deterministic Büchi automaton [1](#chapter07_4.xhtml_chapter07_4_15)

deterministic graphical realization [1](#chapter08_4.xhtml_chapter08_4_7)

deterministic language [1](#chapter07_4.xhtml_chapter07_4_15)

DFA see [deterministic automaton](#Index_1.xhtml_Index_1_12)

DFT see [discrete Fourier transform](#Index_1.xhtml_Index_1_14)

Dickson, L. E. [1](#chapter06.xhtml_chapter06_20)

Dickson’s lemma [1](#chapter06.xhtml_chapter06_20)

differentiation rules [1](#chapter01_3.xhtml_chapter01_3_3)

Diffie, B.W. V, [1](#chapter02_1.xhtml_chapter02_1_21), [2](#chapter02_1.xhtml_chapter02_1_29), [3](#chapter05_2.xhtml_chapter05_2_4)

Diffie–Hellman key exchange [1](#chapter02_1.xhtml_chapter02_1_23), [2](#chapter02_1.xhtml_chapter02_1_29)

–on elliptic curves [1](#chapter05_2.xhtml_chapter05_2_4)

Diffie–Hellman problem [1](#chapter02_1.xhtml_chapter02_1_29), [2](#chapter05_2.xhtml_chapter05_2_6)

digital commitment [1](#chapter02_2.xhtml_chapter02_2_8)

digital signature [1](#chapter02_2.xhtml_chapter02_2_1)

Digital Signature Algorithm [1](#chapter02_2.xhtml_chapter02_2_1)

dihedral group [1](#chapter01_1.xhtml_chapter01_1_29)

direct product [1](#chapter01_2.xhtml_chapter01_2_23)

directed edge [1](#chapter08_3.xhtml_chapter08_3_11)

discrete Fourier transform [1](#chapter03_3.xhtml_chapter03_3_2), [2](#chapter03_3.xhtml_chapter03_3_5)

discrete logarithm [1](#chapter03_2.xhtml_chapter03_2_16), [2](#chapter03_2.xhtml_chapter03_2_18)

–baby-step giant-step algorithm [1](#chapter03_2.xhtml_chapter03_2_18)

–index calculus [1](#chapter03_2.xhtml_chapter03_2_25)

–Pohlig–Hellman algorithm [1](#chapter03_2.xhtml_chapter03_2_22)

–Pollard’s ρ algorithm [1](#chapter03_2.xhtml_chapter03_2_20)

distributivity [1](#chapter01_2.xhtml_chapter01_2_1)

divide [1](#chapter01_1.xhtml_chapter01_1_5)

division [1](#chapter03_3.xhtml_chapter03_3_2)

–polynomial [1](#chapter01_3.xhtml_chapter01_3_6)

divisor [1](#chapter05_1.xhtml_chapter05_1_21), [2](#chapter07_2.xhtml_chapter07_2_39)

–greatest common [1](#chapter01_1.xhtml_chapter01_1_5)

–group [1](#chapter07_2.xhtml_chapter07_2_39)

–local [1](#chapter07_2.xhtml_chapter07_2_20), [2](#chapter07_3.xhtml_chapter07_3_15)

–principal [1](#chapter05_1.xhtml_chapter05_1_24)

–zero [1](#chapter01_2.xhtml_chapter01_2_6)

domain [1](#chapter01_2.xhtml_chapter01_2_6)

–integral [1](#chapter01_2.xhtml_chapter01_2_6)

DSA see [Digital Signature Algorithm](#Index_1.xhtml_Index_1_13)

Dyck language [1](#chapter08_1.xhtml_chapter08_1_29)

Dyck, W. F. A., Ritter von [1](#chapter08_1.xhtml_chapter08_1_29)

E

ECC [1](#chapter05_3.xhtml_chapter05_3_9)

edge

–arc [1](#chapter08_3.xhtml_chapter08_3_12)

–bridge [1](#chapter08_3.xhtml_chapter08_3_29)

–directed [1](#chapter08_3.xhtml_chapter08_3_11)

–source [1](#chapter08_3.xhtml_chapter08_3_11)

–target [1](#chapter08_3.xhtml_chapter08_3_11)

egg box diagram [1](#chapter07_4.xhtml_chapter07_4_4)

Eilenberg, S. [1](#chapter01_1.xhtml_chapter01_1_2)

Eisenstein, F. G.M. [1](#chapter01_4.xhtml_chapter01_4_27)

Eisenstein’s criterion [1](#chapter01_4.xhtml_chapter01_4_27)

element

–comparable [1](#chapter06.xhtml_chapter06_15)

–conjugate [1](#chapter06.xhtml_chapter06_6)

–generating [1](#chapter01_1.xhtml_chapter01_1_12)

–idempotent [1](#chapter01_1.xhtml_chapter01_1_4), [2](#chapter01_4.xhtml_chapter01_4_18)

–incomparable [1](#chapter06.xhtml_chapter06_15)

–inverse [1](#chapter01_1.xhtml_chapter01_1_4), [2](#chapter01_1.xhtml_chapter01_1_5)

–invertible [1](#chapter07_3.xhtml_chapter07_3_10)

–left inverse [1](#chapter01_4.xhtml_chapter01_4_14)

–left neutral [1](#chapter01_4.xhtml_chapter01_4_18)

–neutral [1](#chapter01_1.xhtml_chapter01_1_4), [2](#chapter01_1.xhtml_chapter01_1_5)

–period [1](#chapter07_3.xhtml_chapter07_3_22)

–regular [1](#chapter01_4.xhtml_chapter01_4_18)

–right inverse [1](#chapter01_4.xhtml_chapter01_4_14)

–right neutral [1](#chapter01_4.xhtml_chapter01_4_18)

–square [1](#chapter01_4.xhtml_chapter01_4_3), [2](#chapter03_1.xhtml_chapter03_1_33)

–threshold [1](#chapter07_3.xhtml_chapter07_3_22)

–transposed [1](#chapter06.xhtml_chapter06_6)

–unit [1](#chapter01_2.xhtml_chapter01_2_1), [2](#chapter07_3.xhtml_chapter07_3_10)

–zero [1](#chapter01_1.xhtml_chapter01_1_4)

elementary arithmetic operation [1](#chapter03_3.xhtml_chapter03_3_7)

ElGamal cryptosystem [1](#chapter02_1.xhtml_chapter02_1_23), [2](#chapter02_1.xhtml_chapter02_1_31)

–on elliptic curves [1](#chapter05_2.xhtml_chapter05_2_6)

ElGamal signature [1](#chapter02_2.xhtml_chapter02_2_27)

ElGamal, T. [1](#chapter02_1.xhtml_chapter02_1_31)

Elgot, C. C. [1](#chapter07_5.xhtml_chapter07_5_6)

elimination

–of ε-transitions [1](#chapter07_1.xhtml_chapter07_1_24)

–of states [1](#chapter07_1.xhtml_chapter07_1_26)

elimination of ε-transitions [1](#chapter07_1.xhtml_chapter07_1_24)

Elkies, N. [1](#chapter05_2.xhtml_chapter05_2_17)

elliptic curve [1](#chapter05_1.xhtml_chapter05_1_1), [2](#chapter05_1.xhtml_chapter05_1_2), [3](#chapter05_1.xhtml_chapter05_1_6), [4](#chapter05_2.xhtml_chapter05_2_2)

–group operation [1](#chapter05_1.xhtml_chapter05_1_14)

elliptic curve integer factorization [1](#chapter05_2.xhtml_chapter05_2_9)

elliptic function [1](#chapter05_1.xhtml_chapter05_1_2)

empty word [1](#chapter06.xhtml_chapter06_1), [2](#chapter08_1.xhtml_chapter08_1_12)

encoding function [1](#chapter02_1.xhtml_chapter02_1_3)

encryption function [1](#chapter02_1.xhtml_chapter02_1_3)

endomorphism [1](#chapter05_3.xhtml_chapter05_3_2)

–Frobenius [1](#chapter05_3.xhtml_chapter05_3_2)

–separable [1](#chapter05_3.xhtml_chapter05_3_7)

ε-NFA [1](#chapter07_2.xhtml_chapter07_2_13)

equivalent automata [1](#chapter07_1.xhtml_chapter07_1_21)

ε-transition [1](#chapter07_1.xhtml_chapter07_1_24)

Euclid of Alexandria [1](#chapter01_1.xhtml_chapter01_1_1), [2](#chapter01_2.xhtml_chapter01_2_10)

Euclidean algorith

–extended [1](#chapter01_2.xhtml_chapter01_2_14)

Euclidean algorithm [1](#chapter01_2.xhtml_chapter01_2_10)

–binary [1](#chapter03_1.xhtml_chapter03_1_9)

–binary extended [1](#chapter03_3.xhtml_chapter03_3_17), [2](#chapter09_2.xhtml_chapter09_2_3)

Euler, L. [1](#chapter01_1.xhtml_chapter01_1_1), [2](#chapter01_2.xhtml_chapter01_2_23), [3](#chapter01_4.xhtml_chapter01_4_5), [4](#chapter01_4.xhtml_chapter01_4_31)

Eulerian pseudoprime [1](#chapter03_1.xhtml_chapter03_1_31)

Euler’s criterion [1](#chapter01_4.xhtml_chapter01_4_5)

Euler’s number [1](#chapter01_1.xhtml_chapter01_1_1)

Euler’s theorem [1](#chapter01_2.xhtml_chapter01_2_23)

Euler’s totient function [1](#chapter01_2.xhtml_chapter01_2_23)

evaluation homomorphism [1](#chapter01_2.xhtml_chapter01_2_27), [2](#chapter06.xhtml_chapter06_6)

even permutation [1](#chapter01_2.xhtml_chapter01_2_1)

exponentiation

–fast [1](#chapter03_1.xhtml_chapter03_1_8)

–fast modular [1](#chapter03_1.xhtml_chapter03_1_8)

expression

–rational [1](#chapter07_1.xhtml_chapter07_1_19)

–regular see [rational expression](#Index_2.xhtml_Index_2_9)

–star-free [1](#chapter07_2.xhtml_chapter07_2_20)

extended Euclidean algorithm [1](#chapter01_2.xhtml_chapter01_2_14)

–binary [1](#chapter03_3.xhtml_chapter03_3_17), [2](#chapter09_2.xhtml_chapter09_2_3)

F

φ function see [totient function](#Index_2.xhtml_Index_2_20)

factor [1](#chapter06.xhtml_chapter06_1)

factor critical pair [1](#chapter08_1.xhtml_chapter08_1_24)

factor group see [quotient group](#Index_2.xhtml_Index_2_6)

factor ring see [quotient ring](#Index_2.xhtml_Index_2_7)

fast exponentiation [1](#chapter03_1.xhtml_chapter03_1_8)

–modular [1](#chapter03_1.xhtml_chapter03_1_8)

fast Fourier transform [1](#chapter03_3.xhtml_chapter03_3_5)

fast powering see [fast exponentiation](#Index_1.xhtml_Index_1_18)

Fermat number [1](#chapter03_3.xhtml_chapter03_3_17)

Fermat, P. de [1](#chapter01_2.xhtml_chapter01_2_10), [2](#chapter03_1.xhtml_chapter03_1_12), [3](#chapter05_1.xhtml_chapter05_1_6), [4](#chapter08_5.xhtml_chapter08_5_1)

Fermat primality test [1](#chapter03_1.xhtml_chapter03_1_12)

Fermat’s Last Theorem [1](#chapter05_1.xhtml_chapter05_1_6)

Fermat’s little theorem [1](#chapter01_2.xhtml_chapter01_2_10)

Fermat’s theorem on sums of two squares [1](#chapter08_5.xhtml_chapter08_5_1)

Ferrari, L. [1](#chapter01_1.xhtml_chapter01_1_1)

FFT see [fast Fourier transform](#Index_1.xhtml_Index_1_19)

Fibonacci number [1](#chapter08_4.xhtml_chapter08_4_28)

field [1](#chapter01_1.xhtml_chapter01_1_4), [2](#chapter01_2.xhtml_chapter01_2_1), [3](#chapter01_3.xhtml_chapter01_3_19)

–algebraically closed [1](#chapter01_3.xhtml_chapter01_3_25)

–finite [1](#chapter01_3.xhtml_chapter01_3_25)

–function [1](#chapter05_2.xhtml_chapter05_2_18)

–Galois [1](#chapter01_3.xhtml_chapter01_3_19)

–prime [1](#chapter01_2.xhtml_chapter01_2_6)

–skew [1](#chapter01_2.xhtml_chapter01_2_1)

–splitting [1](#chapter01_3.xhtml_chapter01_3_22)

–sub- [1](#chapter01_2.xhtml_chapter01_2_3)

–used in AES [1](#chapter01_3.xhtml_chapter01_3_17)

field extension [1](#chapter01_3.xhtml_chapter01_3_22)

final state [1](#chapter07_1.xhtml_chapter07_1_8), [2](#chapter07_1.xhtml_chapter07_1_19)

final transition [1](#chapter09_4.xhtml_chapter09_4_3)

Fine, N. J. [1](#chapter06.xhtml_chapter06_12)

finite automaton [1](#chapter07_1.xhtml_chapter07_1_19)

finite field

–used in AES [1](#chapter01_3.xhtml_chapter01_3_17)

finitely generated [1](#chapter01_2.xhtml_chapter01_2_3)

finitely presented group [1](#chapter08_1.xhtml_chapter08_1_29)

finitely presented monoid [1](#chapter08_1.xhtml_chapter08_1_27)

first-order logic [1](#chapter07_5.xhtml_chapter07_5_11)

first-order variable [1](#chapter07_5.xhtml_chapter07_5_5)

flip–flop [1](#chapter01_1.xhtml_chapter01_1_2), [2](#chapter07_2.xhtml_chapter07_2_39)

formal language [1](#chapter07_1.xhtml_chapter07_1_1)

formal power series [1](#chapter01_2.xhtml_chapter01_2_27)

–derivative [1](#chapter01_3.xhtml_chapter01_3_3)

Fourier, J. B. J. [1](#chapter03_3.xhtml_chapter03_3_2)

Frederick the Great [1](#chapter02_1.xhtml_chapter02_1_1), [2](#chapter09_1.xhtml_chapter09_1_9)

free group [1](#chapter08_1.xhtml_chapter08_1_27)

–basis [1](#chapter08_1.xhtml_chapter08_1_27)

–rank [1](#chapter08_1.xhtml_chapter08_1_27), [2](#chapter08_3.xhtml_chapter08_3_5)

free monoid [1](#chapter06.xhtml_chapter06_1), [2](#chapter08_1.xhtml_chapter08_1_14)

free partially commutative group [1](#chapter08_1.xhtml_chapter08_1_54)

free partially commutative monoid [1](#chapter08_1.xhtml_chapter08_1_49)

free product [1](#chapter08_1.xhtml_chapter08_1_35)

free variable [1](#chapter07_5.xhtml_chapter07_5_15)

frequency analysis [1](#chapter02_1.xhtml_chapter02_1_10)

Frobenius automorphism [1](#chapter05_3.xhtml_chapter05_3_1)

Frobenius endomorphism [1](#chapter05_3.xhtml_chapter05_3_2)

Frobenius, F. G. [1](#chapter01_2.xhtml_chapter01_2_10), [2](#chapter05_3.xhtml_chapter05_3_1), [3](#chapter05_3.xhtml_chapter05_3_29)

Frobenius homomorphism [1](#chapter01_2.xhtml_chapter01_2_10)

Frobenius morphism [1](#chapter05_3.xhtml_chapter05_3_1)

function

–collision resistant [1](#chapter02_1.xhtml_chapter02_1_34)

–compression [1](#chapter02_1.xhtml_chapter02_1_34)

–decoding [1](#chapter02_1.xhtml_chapter02_1_3)

–decryption [1](#chapter02_1.xhtml_chapter02_1_3)

–Dehn [1](#chapter08_2.xhtml_chapter08_2_29)

–elliptic [1](#chapter05_1.xhtml_chapter05_1_2)

–encoding [1](#chapter02_1.xhtml_chapter02_1_3)

–encryption [1](#chapter02_1.xhtml_chapter02_1_3)

–hash [1](#chapter02_1.xhtml_chapter02_1_34)

–one-way [1](#chapter02_1.xhtml_chapter02_1_34)

–rational [1](#chapter05_2.xhtml_chapter05_2_18)

–totient [1](#chapter01_2.xhtml_chapter01_2_23)

–tower [1](#chapter08_4.xhtml_chapter08_4_28)

–transition [1](#chapter07_1.xhtml_chapter07_1_8)

function field [1](#chapter05_2.xhtml_chapter05_2_18)

Fürer, M. [1](#chapter03_3.xhtml_chapter03_3_9)

G

Galois field [1](#chapter01_3.xhtml_chapter01_3_19)

Galois, É. [1](#chapter01_1.xhtml_chapter01_1_2), [2](#chapter01_1.xhtml_chapter01_1_5), [3](#chapter01_2.xhtml_chapter01_2_1)

Gauss, J. C. F. [1](#chapter05_1.xhtml_chapter05_1_1)

gcd see [greatest common divisor](#Index_1.xhtml_Index_1_20); [Euclidean algorithm](#Index_1.xhtml_Index_1_16)

generalized Baumslag–Solitar group [1](#chapter08_1.xhtml_chapter08_1_38)

generate [1](#chapter01_1.xhtml_chapter01_1_5)

generated ideal [1](#chapter01_2.xhtml_chapter01_2_3)

generator [1](#chapter01_1.xhtml_chapter01_1_12)

Germain, S. [1](#chapter02_1.xhtml_chapter02_1_29)

Gersten, S. M. [1](#chapter08_2.xhtml_chapter08_2_29)

global solution [1](#chapter02_1.xhtml_chapter02_1_5)

Gödel, K. P. [1](#chapter04.xhtml_chapter04_1), [2](#chapter07_5.xhtml_chapter07_5_11), [3](#chapter07_5.xhtml_chapter07_5_21)

Gödel’s incompleteness theorem [1](#chapter07_5.xhtml_chapter07_5_11), [2](#chapter07_5.xhtml_chapter07_5_21)

Goldwasser, S. [1](#chapter05_2.xhtml_chapter05_2_15), [2](#chapter05_2.xhtml_chapter05_2_17), [3](#chapter05_3.xhtml_chapter05_3_29)

Goldwasser–Kilian primality certificates [1](#chapter05_2.xhtml_chapter05_2_13)

good sequence [1](#chapter06.xhtml_chapter06_15)

graph

–rose [1](#chapter08_3.xhtml_chapter08_3_30), [2](#chapter08_4.xhtml_chapter08_4_9)

–Schreier [1](#chapter08_3.xhtml_chapter08_3_11)

–Stallings [1](#chapter08_3.xhtml_chapter08_3_5)

graph group [1](#chapter08_1.xhtml_chapter08_1_54)

graphical realization [1](#chapter08_3.xhtml_chapter08_3_26), [2](#chapter08_3.xhtml_chapter08_3_29)

–deterministic [1](#chapter08_4.xhtml_chapter08_4_7)

greatest common divisor [1](#chapter01_1.xhtml_chapter01_1_5), [2](#chapter01_2.xhtml_chapter01_2_10), [3](#chapter01_3.xhtml_chapter01_3_9)

Green, J. A. VI, [1](#chapter07_3.xhtml_chapter07_3_25)

Green’s lemma [1](#chapter07_4.xhtml_chapter07_4_1)

Green’s relations [1](#chapter07_3.xhtml_chapter07_3_25)

–D [1](#chapter07_3.xhtml_chapter07_3_25)

–H [1](#chapter07_3.xhtml_chapter07_3_25)

–J [1](#chapter07_3.xhtml_chapter07_3_25)

–L [1](#chapter07_3.xhtml_chapter07_3_25)

–R [1](#chapter07_3.xhtml_chapter07_3_25)

Gromov, M. L. [1](#chapter08_1.xhtml_chapter08_1_44)

Grothendieck, A. VII, [1](#chapter05_3.xhtml_chapter05_3_9)

group [1](#chapter01_1.xhtml_chapter01_1_4), [2](#chapter01_1.xhtml_chapter01_1_5)

–alternating [1](#chapter01_2.xhtml_chapter01_2_1)

–automorphism [1](#chapter01_1.xhtml_chapter01_1_29)

–Baumslag [1](#chapter08_2.xhtml_chapter08_2_27)

–Baumslag–Gersten [1](#chapter08_2.xhtml_chapter08_2_29)

–Baumslag–Solitar [1](#chapter08_1.xhtml_chapter08_1_35)

–center [1](#chapter08_4.xhtml_chapter08_4_12), [2](#chapter08_4.xhtml_chapter08_4_28)

–Coxeter [1](#chapter08_1.xhtml_chapter08_1_54)

–cyclic [1](#chapter01_1.xhtml_chapter01_1_12)

–dihedral [1](#chapter01_1.xhtml_chapter01_1_29)

–finitely presented [1](#chapter08_1.xhtml_chapter08_1_29)

–free [1](#chapter08_1.xhtml_chapter08_1_27)

–free partially commutative [1](#chapter08_1.xhtml_chapter08_1_54)

–generalized Baumslag–Solitar [1](#chapter08_1.xhtml_chapter08_1_38)

–graph [1](#chapter08_1.xhtml_chapter08_1_54)

–Hopfian [1](#chapter08_1.xhtml_chapter08_1_12)

–hyperbolic [1](#chapter08_1.xhtml_chapter08_1_44)

–Klein four- [1](#chapter01_1.xhtml_chapter01_1_30)

–modular [1](#chapter08_4.xhtml_chapter08_4_12)

–multiplicative [1](#chapter01_2.xhtml_chapter01_2_1)

–Picard [1](#chapter05_1.xhtml_chapter05_1_25)

–quotient [1](#chapter01_1.xhtml_chapter01_1_20)

–residually finite [1](#chapter08_1.xhtml_chapter08_1_12)

–right-angled Artin [1](#chapter08_1.xhtml_chapter08_1_54)

–right-angled Coxeter [1](#chapter08_2.xhtml_chapter08_2_8)

–Schützenberger [1](#chapter07_4.xhtml_chapter07_4_1), [2](#chapter07_4.xhtml_chapter07_4_4)

–simple [1](#chapter07_2.xhtml_chapter07_2_39)

–small cancellation [1](#chapter08_1.xhtml_chapter08_1_44)

–special linear [1](#chapter08_1.xhtml_chapter08_1_12), [2](#chapter08_4.xhtml_chapter08_4_9)

–symmetric [1](#chapter01_1.xhtml_chapter01_1_31)

–symmetry [1](#chapter01_1.xhtml_chapter01_1_29)

–Waack [1](#chapter08_1.xhtml_chapter08_1_38)

group divisor [1](#chapter07_2.xhtml_chapter07_2_39)

group homomorphism [1](#chapter01_4.xhtml_chapter01_4_24)

group of units [1](#chapter01_2.xhtml_chapter01_2_1)

group operation on elliptic curve [1](#chapter05_1.xhtml_chapter05_1_14)

group-based cryptography [1](#chapter02_1.xhtml_chapter02_1_23)

group-free monoid see [aperiodic monoid](#Index_1.xhtml_Index_1_4)

Gustafson, W. H. [1](#chapter08_4.xhtml_chapter08_4_28)

H

*H*-class [1](#chapter07_3.xhtml_chapter07_3_25)

halting problem [1](#chapter08_1.xhtml_chapter08_1_27)

Hartshorne, R. [1](#chapter05_3.xhtml_chapter05_3_9)

hash function [1](#chapter02_1.xhtml_chapter02_1_34)

Hasse bound [1](#chapter05_1.xhtml_chapter05_1_8)

Hasse, H. [1](#chapter05_1.xhtml_chapter05_1_8), [2](#chapter05_2.xhtml_chapter05_2_17), [3](#chapter05_3.xhtml_chapter05_3_9)

Hasse’s theorem [1](#chapter05_1.xhtml_chapter05_1_8)

Hellman, M. E. V, [1](#chapter02_1.xhtml_chapter02_1_21), [2](#chapter02_1.xhtml_chapter02_1_29), [3](#chapter02_2.xhtml_chapter02_2_12), [4](#chapter03_2.xhtml_chapter03_2_22), [5](#chapter05_2.xhtml_chapter05_2_4)

Hermite, Ch. [1](#chapter01_1.xhtml_chapter01_1_1)

Higman, G. VI, [1](#chapter06.xhtml_chapter06_20), [2](#chapter08_2.xhtml_chapter08_2_21)

Higman’s lemma [1](#chapter06.xhtml_chapter06_20)

Hilbert, D. [1](#chapter01_1.xhtml_chapter01_1_2), [2](#chapter01_3.xhtml_chapter01_3_17), [3](#chapter07_5.xhtml_chapter07_5_21)

Hilbert’s basis theorem [1](#chapter01_3.xhtml_chapter01_3_17)

Hilbert’s tenth problem [1](#chapter07_5.xhtml_chapter07_5_21)

HNN extension [1](#chapter08_2.xhtml_chapter08_2_21)

homomorphism [1](#chapter01_1.xhtml_chapter01_1_5)

–evaluation [1](#chapter06.xhtml_chapter06_6)

–Frobenius [1](#chapter01_2.xhtml_chapter01_2_10)

–graphical realization [1](#chapter08_3.xhtml_chapter08_3_26), [2](#chapter08_3.xhtml_chapter08_3_29)

–group [1](#chapter01_4.xhtml_chapter01_4_24)

–partial [1](#chapter07_2.xhtml_chapter07_2_41)

–projection [1](#chapter08_3.xhtml_chapter08_3_26)

–ring [1](#chapter01_2.xhtml_chapter01_2_3)

–syntactic [1](#chapter07_4.xhtml_chapter07_4_32)

homomorphism theorem

–groups [1](#chapter01_1.xhtml_chapter01_1_23)

–rings [1](#chapter01_2.xhtml_chapter01_2_4)

Hopf, H. [1](#chapter08_1.xhtml_chapter08_1_12)

Hopfian group [1](#chapter08_1.xhtml_chapter08_1_12)

hyperbolic group [1](#chapter08_1.xhtml_chapter08_1_44)

I

ideal [1](#chapter01_2.xhtml_chapter01_2_3), [2](#chapter07_3.xhtml_chapter07_3_22)

–finitely generated [1](#chapter01_2.xhtml_chapter01_2_3)

–generated [1](#chapter01_2.xhtml_chapter01_2_3)

–left [1](#chapter07_3.xhtml_chapter07_3_22)

–maximal [1](#chapter01_2.xhtml_chapter01_2_4)

–principal [1](#chapter01_2.xhtml_chapter01_2_3), [2](#chapter07_3.xhtml_chapter07_3_22)

–right [1](#chapter07_3.xhtml_chapter07_3_22)

–two-sided [1](#chapter07_3.xhtml_chapter07_3_22)

idempotent element [1](#chapter01_1.xhtml_chapter01_1_4), [2](#chapter01_4.xhtml_chapter01_4_18)

identity [1](#chapter01_1.xhtml_chapter01_1_4)

image [1](#chapter01_1.xhtml_chapter01_1_20), [2](#chapter01_2.xhtml_chapter01_2_4)

incomparable elements [1](#chapter06.xhtml_chapter06_15)

independence [1](#chapter08_1.xhtml_chapter08_1_49)

independence relation [1](#chapter08_1.xhtml_chapter08_1_49)

index

–stabilization [1](#chapter07_6.xhtml_chapter07_6_8)

index calculus [1](#chapter03_2.xhtml_chapter03_2_25)

index of a subgroup [1](#chapter01_1.xhtml_chapter01_1_12)

infinite word [1](#chapter07_4.xhtml_chapter07_4_10)

infix see [factor](#Index_1.xhtml_Index_1_17)

initial state [1](#chapter07_1.xhtml_chapter07_1_8), [2](#chapter07_1.xhtml_chapter07_1_19)

inner automorphism [1](#chapter08_2.xhtml_chapter08_2_13)

integer factorization [1](#chapter03_2.xhtml_chapter03_2_8)

–elliptic curves [1](#chapter05_2.xhtml_chapter05_2_9)

–Pollard’s p − [1](#chapter01_1.xhtml_chapter01_1_1) algorithm [2](#chapter03_2.xhtml_chapter03_2_11)

–Pollard’s ρ algorithm [1](#chapter03_2.xhtml_chapter03_2_11)

–quadratic sieve [1](#chapter03_2.xhtml_chapter03_2_13)

integer multiplication

–Karatsuba [1](#chapter03_2.xhtml_chapter03_2_27)

–Schönhage–Strassen [1](#chapter03_3.xhtml_chapter03_3_9)

integral domain [1](#chapter01_2.xhtml_chapter01_2_6)

interpolation [1](#chapter02_2.xhtml_chapter02_2_6)

introspective number [1](#chapter04.xhtml_chapter04_25)

inverse element [1](#chapter01_1.xhtml_chapter01_1_4), [2](#chapter01_1.xhtml_chapter01_1_5)

inversion [1](#chapter01_1.xhtml_chapter01_1_31)

invertible element [1](#chapter07_3.xhtml_chapter07_3_10)

irreducible normal form [1](#chapter08_1.xhtml_chapter08_1_22)

irreducible polynomial [1](#chapter01_3.xhtml_chapter01_3_12)

isomorphism [1](#chapter01_1.xhtml_chapter01_1_5)

–of rings [1](#chapter01_2.xhtml_chapter01_2_4)

isomorphism problem [1](#chapter08_1.xhtml_chapter08_1_1)

J

*J*-class [1](#chapter07_3.xhtml_chapter07_3_25)

Jacobi, C. G. J. [1](#chapter01_4.xhtml_chapter01_4_5)

Jacobi symbol [1](#chapter01_4.xhtml_chapter01_4_5)

K

Karatsuba, A. A. [1](#chapter03_2.xhtml_chapter03_2_27), [2](#chapter03_3.xhtml_chapter03_3_9)

Karatsuba’s algorithm [1](#chapter03_2.xhtml_chapter03_2_27)

Kayal, N. VI, [1](#chapter04.xhtml_chapter04_1)

Keller, R. M. [1](#chapter08_1.xhtml_chapter08_1_49)

Kerckhoffs, A. [1](#chapter02_1.xhtml_chapter02_1_5)

Kerckhoffs’ principle [1](#chapter02_1.xhtml_chapter02_1_5)

kernel [1](#chapter01_1.xhtml_chapter01_1_20), [2](#chapter01_2.xhtml_chapter01_2_4)

kernel of the Schreier graph [1](#chapter08_3.xhtml_chapter08_3_12)

key [1](#chapter02_1.xhtml_chapter02_1_3)

–private [1](#chapter02_1.xhtml_chapter02_1_21)

–public [1](#chapter02_1.xhtml_chapter02_1_21)

–secret [1](#chapter02_1.xhtml_chapter02_1_21)

key exchange [1](#chapter02_1.xhtml_chapter02_1_29), [2](#chapter05_2.xhtml_chapter05_2_4)

Kilian, J. J. [1](#chapter05_2.xhtml_chapter05_2_15), [2](#chapter05_2.xhtml_chapter05_2_17), [3](#chapter05_3.xhtml_chapter05_3_29)

Kleene, S. C. [1](#chapter07_1.xhtml_chapter07_1_1), [2](#chapter07_2.xhtml_chapter07_2_3), [3](#chapter07_2.xhtml_chapter07_2_8)

Kleene star [1](#chapter07_1.xhtml_chapter07_1_1)

Kleene’s theorem [1](#chapter07_2.xhtml_chapter07_2_8)

Klein, F. Chr. [1](#chapter01_1.xhtml_chapter01_1_30)

Klein four-group [1](#chapter01_1.xhtml_chapter01_1_30)

knapsack problem [1](#chapter02_2.xhtml_chapter02_2_12)

Knödel number [1](#chapter03_1.xhtml_chapter03_1_12)

Knödel, W. [1](#chapter03_1.xhtml_chapter03_1_12)

Koblitz, N. [1](#chapter05_3.xhtml_chapter05_3_9)

Krohn, K. B. VI, [1](#chapter01_1.xhtml_chapter01_1_2), [2](#chapter07_2.xhtml_chapter07_2_27), [3](#chapter07_2.xhtml_chapter07_2_39)

Krohn–Rhodes decomposition [1](#chapter07_2.xhtml_chapter07_2_27), [2](#chapter07_2.xhtml_chapter07_2_39)

Krohn–Rhodes theorem [1](#chapter07_2.xhtml_chapter07_2_39)

Kronecker delta [1](#chapter02_1.xhtml_chapter02_1_13)

Kronecker, L. [1](#chapter02_1.xhtml_chapter02_1_13)

Kruskal, J. B. [1](#chapter06.xhtml_chapter06_25), [2](#chapter06.xhtml_chapter06_28)

Kruskal’s tree theorem [1](#chapter06.xhtml_chapter06_28)

L

*L*-class [1](#chapter07_3.xhtml_chapter07_3_25)

label of a transition [1](#chapter07_1.xhtml_chapter07_1_19)

Lagrange interpolation [1](#chapter02_2.xhtml_chapter02_2_6)

Lagrange, J.-J. de [1](#chapter01_1.xhtml_chapter01_1_12)

Lagrange polynomial [1](#chapter02_2.xhtml_chapter02_2_6)

Lagrange’s theorem [1](#chapter01_1.xhtml_chapter01_1_12)

Lallement, G. [1](#chapter07_2.xhtml_chapter07_2_27)

Landau, E. G.H. [1](#chapter03_1.xhtml_chapter03_1_1)

language [1](#chapter07_1.xhtml_chapter07_1_1), [2](#chapter07_2.xhtml_chapter07_2_3), [3](#chapter07_4.xhtml_chapter07_4_10)

–accepted [1](#chapter07_4.xhtml_chapter07_4_15)

–at a state [1](#chapter07_1.xhtml_chapter07_1_11)

–deterministic [1](#chapter07_4.xhtml_chapter07_4_15)

–Dyck [1](#chapter08_1.xhtml_chapter08_1_29)

–formal [1](#chapter07_1.xhtml_chapter07_1_1)

–mirror [1](#chapter07_6.xhtml_chapter07_6_9)

–ω- [1](#chapter07_4.xhtml_chapter07_4_10)

–ω-rational [1](#chapter07_4.xhtml_chapter07_4_22)

–regular [1](#chapter07_2.xhtml_chapter07_2_3)

–reverse [1](#chapter07_6.xhtml_chapter07_6_9)

–star-free [1](#chapter07_2.xhtml_chapter07_2_20)

Laocoön [1](#chapter02_1.xhtml_chapter02_1_8)

law of quadratic reciprocity [1](#chapter01_4.xhtml_chapter01_4_8)

lcm see [least common multiple](#Index_1.xhtml_Index_1_23)

leading coefficient [1](#chapter01_2.xhtml_chapter01_2_27)

least common multiple [1](#chapter01_2.xhtml_chapter01_2_20), [2](#chapter04.xhtml_chapter04_11)

left-conjugate see [conjugate](#Index_1.xhtml_Index_1_8)

left coset [1](#chapter01_1.xhtml_chapter01_1_7)

left ideal [1](#chapter07_3.xhtml_chapter07_3_22)

left inverse [1](#chapter01_4.xhtml_chapter01_4_14)

left neutral [1](#chapter01_4.xhtml_chapter01_4_18)

Legendre, A.-M. [1](#chapter01_4.xhtml_chapter01_4_8)

Legendre symbol [1](#chapter01_4.xhtml_chapter01_4_8)

Lehmer, D.H. [1](#chapter03_3.xhtml_chapter03_3_23)

lemma

–Bézout [1](#chapter01_2.xhtml_chapter01_2_14)

–Dickson [1](#chapter06.xhtml_chapter06_20)

–Fine–Wilf [1](#chapter06.xhtml_chapter06_12)

–Green [1](#chapter07_4.xhtml_chapter07_4_1)

–Higman [1](#chapter06.xhtml_chapter06_20)

–Levi [1](#chapter06.xhtml_chapter06_30)

–periodicity [1](#chapter06.xhtml_chapter06_12)

–Zolotarev [1](#chapter01_4.xhtml_chapter01_4_5)

length of a word [1](#chapter06.xhtml_chapter06_1), [2](#chapter08_1.xhtml_chapter08_1_12)

length-lexicographic [1](#chapter08_1.xhtml_chapter08_1_12)

Lenstra, H., Jr. [1](#chapter05_2.xhtml_chapter05_2_9), [2](#chapter05_2.xhtml_chapter05_2_12)

letter [1](#chapter06.xhtml_chapter06_1), [2](#chapter08_1.xhtml_chapter08_1_12)

Levi, F. W. D. [1](#chapter06.xhtml_chapter06_30)

Levi’s lemma [1](#chapter06.xhtml_chapter06_30)

lexicographic order [1](#chapter06.xhtml_chapter06_30), [2](#chapter08_1.xhtml_chapter08_1_12)

Lindemann, C. L. F. von [1](#chapter01_1.xhtml_chapter01_1_1)

line [1](#chapter05_1.xhtml_chapter05_1_8)

linear Diophantine equation [1](#chapter03_3.xhtml_chapter03_3_23)

linear Diophantine system [1](#chapter07_5.xhtml_chapter07_5_22)

linear set [1](#chapter07_5.xhtml_chapter07_5_15)

Liouville, J. [1](#chapter01_1.xhtml_chapter01_1_1)

local divisor [1](#chapter07_2.xhtml_chapter07_2_20), [2](#chapter07_3.xhtml_chapter07_3_15)

local solution [1](#chapter02_1.xhtml_chapter02_1_5)

local submonoid [1](#chapter07_2.xhtml_chapter07_2_20)

locally confluent [1](#chapter08_1.xhtml_chapter08_1_17)

logic

–first-order [1](#chapter07_5.xhtml_chapter07_5_11)

–monadic second-order [1](#chapter07_4.xhtml_chapter07_4_10), [2](#chapter07_5.xhtml_chapter07_5_2)

Lucas, É [1](#chapter03_3.xhtml_chapter03_3_17), [2](#chapter03_3.xhtml_chapter03_3_23)

Lucas primality test [1](#chapter03_3.xhtml_chapter03_3_17)

Lucas–Lehmer primality test [1](#chapter03_3.xhtml_chapter03_3_23)

Lyndon factorization [1](#chapter06.xhtml_chapter06_36)

Lyndon, R. C. VII, [1](#chapter06.xhtml_chapter06_8), [2](#chapter06.xhtml_chapter06_36), [3](#chapter08_3.xhtml_chapter08_3_19)

Lyndon word [1](#chapter06.xhtml_chapter06_36)

Lyndon–Schützenberger theorem [1](#chapter06.xhtml_chapter06_8)

M

MacLane, S. [1](#chapter01_1.xhtml_chapter01_1_2)

man-in-the-middle attack [1](#chapter02_1.xhtml_chapter02_1_23)

marking algorithm [1](#chapter07_1.xhtml_chapter07_1_11)

master theorem [1](#chapter03_1.xhtml_chapter03_1_4)

master theorem II [1](#chapter03_3.xhtml_chapter03_3_17)

Matiyasevich, Yu. [1](#chapter07_5.xhtml_chapter07_5_21)

M-automaton see [automaton](#Index_1.xhtml_Index_1_5)

maximal ideal [1](#chapter01_2.xhtml_chapter01_2_4)

Mazurkiewicz, A. [1](#chapter08_1.xhtml_chapter08_1_49)

McKay, J.H. [1](#chapter01_1.xhtml_chapter01_1_16)

McKnight, D. J., Jr. [1](#chapter07_2.xhtml_chapter07_2_3)

McKnight’s theorem [1](#chapter07_2.xhtml_chapter07_2_3)

median [1](#chapter09_2.xhtml_chapter09_2_3)

Merkle, R. C. [1](#chapter02_1.xhtml_chapter02_1_37), [2](#chapter02_2.xhtml_chapter02_2_12)

Merkle–Damgård construction [1](#chapter02_1.xhtml_chapter02_1_37)

Merkle–Hellman cryptosystem [1](#chapter02_1.xhtml_chapter02_1_23), [2](#chapter02_2.xhtml_chapter02_2_12)

Mersenne, M. [1](#chapter03_3.xhtml_chapter03_3_17)

Mersenne number [1](#chapter03_3.xhtml_chapter03_3_17)

Mezei, J. [1](#chapter07_6.xhtml_chapter07_6_8)

Mezei’s theorem [1](#chapter07_6.xhtml_chapter07_6_8)

Miller, G. L. [1](#chapter03_1.xhtml_chapter03_1_19)

Miller–Rabin primality test [1](#chapter03_1.xhtml_chapter03_1_19)

minimal automaton [1](#chapter07_1.xhtml_chapter07_1_9)

minimal polynomial [1](#chapter01_4.xhtml_chapter01_4_29)

mirror language [1](#chapter07_6.xhtml_chapter07_6_9)

modular arithmetic [1](#chapter01_2.xhtml_chapter01_2_10)

modular group [1](#chapter08_4.xhtml_chapter08_4_12)

modulo [1](#chapter01_1.xhtml_chapter01_1_5), [2](#chapter01_1.xhtml_chapter01_1_20), [3](#chapter01_2.xhtml_chapter01_2_3)

modulus [1](#chapter01_1.xhtml_chapter01_1_5), [2](#chapter01_2.xhtml_chapter01_2_10)

monadic second-order logic [1](#chapter07_4.xhtml_chapter07_4_10), [2](#chapter07_5.xhtml_chapter07_5_2)

monadic semi-Thue system [1](#chapter08_3.xhtml_chapter08_3_1)

monoalphabetic cipher [1](#chapter02_1.xhtml_chapter02_1_8)

monoalphabetic substitution [1](#chapter02_1.xhtml_chapter02_1_8)

Monod, J. [1](#chapter05_1.xhtml_chapter05_1_8)

monoid [1](#chapter01_1.xhtml_chapter01_1_4)

–aperiodic [1](#chapter07_2.xhtml_chapter07_2_15)

–augmented [1](#chapter07_3.xhtml_chapter07_3_18)

–Brandt [1](#chapter07_4.xhtml_chapter07_4_4)

–cancellative [1](#chapter08_2.xhtml_chapter08_2_3)

–defining relations [1](#chapter08_1.xhtml_chapter08_1_22)

–divisor [1](#chapter07_2.xhtml_chapter07_2_39)

–finitely presented [1](#chapter08_1.xhtml_chapter08_1_27)

–flip–flop [1](#chapter07_2.xhtml_chapter07_2_39)

–free [1](#chapter06.xhtml_chapter06_1), [2](#chapter08_1.xhtml_chapter08_1_14)

–free partially commutative [1](#chapter08_1.xhtml_chapter08_1_49)

–group-free see [aperiodic](#Index_1.xhtml_Index_1_4)

–presentation [1](#chapter08_1.xhtml_chapter08_1_14)

–residually finite [1](#chapter08_1.xhtml_chapter08_1_12)

–syntactic [1](#chapter07_1.xhtml_chapter07_1_5)

–trace [1](#chapter08_1.xhtml_chapter08_1_49)

–transition [1](#chapter07_1.xhtml_chapter07_1_15)

Moore, E. F. [1](#chapter07_1.xhtml_chapter07_1_11)

Moore’s minimization algorithm [1](#chapter07_1.xhtml_chapter07_1_11)

morphism

–Frobenius [1](#chapter05_3.xhtml_chapter05_3_1)

–rational [1](#chapter05_3.xhtml_chapter05_3_1)

MSO see [monadic second-order logic](#Index_1.xhtml_Index_1_25)

multiple [1](#chapter01_1.xhtml_chapter01_1_5)

–least common [1](#chapter01_2.xhtml_chapter01_2_20), [2](#chapter04.xhtml_chapter04_11)

multiple exponent attack [1](#chapter02_2.xhtml_chapter02_2_27)

multiple root [1](#chapter01_3.xhtml_chapter01_3_9)

multiplication table [1](#chapter08_1.xhtml_chapter08_1_22)

multiplicative group [1](#chapter01_2.xhtml_chapter01_2_1)

multiplicity of a root [1](#chapter01_3.xhtml_chapter01_3_9), [2](#chapter05_1.xhtml_chapter05_1_21)

multi-prime RSA [1](#chapter02_2.xhtml_chapter02_2_27)

Myhill, J. R. [1](#chapter07_1.xhtml_chapter07_1_15)

Myhill–Nerode theorem [1](#chapter07_1.xhtml_chapter07_1_15)

N

Nair, M. [1](#chapter04.xhtml_chapter04_11)

Nash-Williams, C. St. J. A. [1](#chapter06.xhtml_chapter06_20), [2](#chapter06.xhtml_chapter06_30)

natural numbers [1](#chapter01_1.xhtml_chapter01_1_4)

Nerode, A. [1](#chapter07_1.xhtml_chapter07_1_15)

Neukirch, J. VII

Neumann, B.H. [1](#chapter08_2.xhtml_chapter08_2_21)

Neumann, H. [1](#chapter08_2.xhtml_chapter08_2_21)

neutral element [1](#chapter01_1.xhtml_chapter01_1_4), [2](#chapter01_1.xhtml_chapter01_1_5)

Newton, I., Sir [1](#chapter03_3.xhtml_chapter03_3_2)

Newton method [1](#chapter03_3.xhtml_chapter03_3_2)

NFA [1](#chapter07_2.xhtml_chapter07_2_13)

–ε- [1](#chapter07_2.xhtml_chapter07_2_13)

Nielsen, J. [1](#chapter08_3.xhtml_chapter08_3_5), [2](#chapter08_3.xhtml_chapter08_3_16), [3](#chapter08_3.xhtml_chapter08_3_22)

Nielsen transformation [1](#chapter08_3.xhtml_chapter08_3_22), [2](#chapter08_4.xhtml_chapter08_4_28)

Nielsen–Schreier theorem [1](#chapter08_3.xhtml_chapter08_3_16)

Noether, A. E. [1](#chapter01_1.xhtml_chapter01_1_2), [2](#chapter01_3.xhtml_chapter01_3_17)

Noetherian rewriting system [1](#chapter08_1.xhtml_chapter08_1_17)

Noetherian ring [1](#chapter01_3.xhtml_chapter01_3_17)

nondecreasing sequence [1](#chapter06.xhtml_chapter06_15)

nondeterministic automaton [1](#chapter07_1.xhtml_chapter07_1_19)

norm [1](#chapter05_1.xhtml_chapter05_1_19)

norm of a polynomial [1](#chapter05_2.xhtml_chapter05_2_18)

normal form

–Britton reduced [1](#chapter08_2.xhtml_chapter08_2_27)

–irreducible [1](#chapter08_1.xhtml_chapter08_1_22)

–Weierstrass [1](#chapter05_1.xhtml_chapter05_1_6), [2](#chapter05_3.xhtml_chapter05_3_9)

normal subgroup [1](#chapter01_1.xhtml_chapter01_1_20)

Novikov, P. S. [1](#chapter08_1.xhtml_chapter08_1_1)

number

–algebraic [1](#chapter01_1.xhtml_chapter01_1_1)

–Carmichael [1](#chapter03_1.xhtml_chapter03_1_12)

–coprime [1](#chapter01_1.xhtml_chapter01_1_5)

–Eulerian pseudoprime [1](#chapter03_1.xhtml_chapter03_1_31)

–Euler’s [1](#chapter01_1.xhtml_chapter01_1_1)

–Fermat [1](#chapter03_3.xhtml_chapter03_3_17)

–Fibonacci [1](#chapter08_4.xhtml_chapter08_4_28)

–introspective [1](#chapter04.xhtml_chapter04_25)

–Knödel [1](#chapter03_1.xhtml_chapter03_1_12)

–Mersenne [1](#chapter03_3.xhtml_chapter03_3_17)

–natural [1](#chapter01_1.xhtml_chapter01_1_4)

–pseudoprime [1](#chapter03_1.xhtml_chapter03_1_31)

–smooth [1](#chapter03_2.xhtml_chapter03_2_15), [2](#chapter03_2.xhtml_chapter03_2_25)

–Sophie Germain [1](#chapter02_1.xhtml_chapter02_1_29)

–square-free [1](#chapter03_1.xhtml_chapter03_1_16)

–strong pseudoprime [1](#chapter03_1.xhtml_chapter03_1_31)

–transcendental [1](#chapter01_1.xhtml_chapter01_1_1)

O

ω-language [1](#chapter07_4.xhtml_chapter07_4_10)

–deterministic [1](#chapter07_4.xhtml_chapter07_4_15)

–rational [1](#chapter07_4.xhtml_chapter07_4_22)

![](images/o.jpg)-notation [1](#chapter03_1.xhtml_chapter03_1_1)

ω-rational language [1](#chapter07_4.xhtml_chapter07_4_22)

ω-regular [1](#chapter07_4.xhtml_chapter07_4_15)

ω-word [1](#chapter07_4.xhtml_chapter07_4_10)

odd permutation [1](#chapter01_2.xhtml_chapter01_2_1)

one-time pad [1](#chapter02_1.xhtml_chapter02_1_18)

one-way function [1](#chapter02_1.xhtml_chapter02_1_34)

operation

–Abelian [1](#chapter01_1.xhtml_chapter01_1_4)

–associative [1](#chapter01_1.xhtml_chapter01_1_4)

–commutative [1](#chapter01_1.xhtml_chapter01_1_4)

–distributive [1](#chapter01_2.xhtml_chapter01_2_1)

–on elliptic curves [1](#chapter05_1.xhtml_chapter05_1_14), [2](#chapter05_2.xhtml_chapter05_2_2)

–on pseudocurves [1](#chapter05_2.xhtml_chapter05_2_6)

order

–length-lexicographic [1](#chapter08_1.xhtml_chapter08_1_12)

–lexicographic [1](#chapter06.xhtml_chapter06_30), [2](#chapter08_1.xhtml_chapter08_1_12)

–of a group [1](#chapter01_1.xhtml_chapter01_1_12)

–of a polynomial at P [1](#chapter05_1.xhtml_chapter05_1_21)

–of a rational function at P [1](#chapter05_3.xhtml_chapter05_3_1)

–of a root see [multiplicity](#Index_1.xhtml_Index_1_27)

–of an element [1](#chapter01_1.xhtml_chapter01_1_12)

–product [1](#chapter06.xhtml_chapter06_20)

–shortlex [1](#chapter08_1.xhtml_chapter08_1_12)

ordered tree [1](#chapter06.xhtml_chapter06_25)

Oscar [1](#chapter02_1.xhtml_chapter02_1_5)

overlap critical pair [1](#chapter08_1.xhtml_chapter08_1_24)

P

pair

–critical [1](#chapter08_1.xhtml_chapter08_1_24)

–factor critical [1](#chapter08_1.xhtml_chapter08_1_24)

–overlap critical [1](#chapter08_1.xhtml_chapter08_1_24)

partial homomorphism [1](#chapter07_2.xhtml_chapter07_2_41)

Pépin primality test [1](#chapter03_3.xhtml_chapter03_3_17)

Pépin, Th. [1](#chapter03_3.xhtml_chapter03_3_17)

perfect security [1](#chapter02_1.xhtml_chapter02_1_5), [2](#chapter02_1.xhtml_chapter02_1_15)

period of a word [1](#chapter06.xhtml_chapter06_12)

period of an element [1](#chapter07_3.xhtml_chapter07_3_22)

periodicity lemma [1](#chapter06.xhtml_chapter06_12)

permutation

–even [1](#chapter01_2.xhtml_chapter01_2_1)

–odd [1](#chapter01_2.xhtml_chapter01_2_1)

–sign [1](#chapter01_1.xhtml_chapter01_1_31)

Picard group [1](#chapter05_1.xhtml_chapter05_1_25)

plaintext [1](#chapter02_1.xhtml_chapter02_1_3)

Pocklington, H. C. [1](#chapter05_2.xhtml_chapter05_2_13), [2](#chapter05_2.xhtml_chapter05_2_15)

Pocklington’s theorem [1](#chapter05_2.xhtml_chapter05_2_13)

Poe, E. A. [1](#chapter02_1.xhtml_chapter02_1_10), [2](#chapter02_1.xhtml_chapter02_1_12)

Pohlig, S. [1](#chapter03_2.xhtml_chapter03_2_22)

Pohlig–Hellman algorithm [1](#chapter03_2.xhtml_chapter03_2_22)

point at infinity [1](#chapter05_1.xhtml_chapter05_1_2), [2](#chapter05_2.xhtml_chapter05_2_2)

pole of a rational function [1](#chapter05_3.xhtml_chapter05_3_1)

Pollard, J. M. [1](#chapter03_2.xhtml_chapter03_2_11), [2](#chapter03_2.xhtml_chapter03_2_20)

Pollard’s p − [1](#chapter01_1.xhtml_chapter01_1_1) algorithm [2](#chapter03_2.xhtml_chapter03_2_11)

Pollard’s ρ algorithm (factorization) [1](#chapter03_2.xhtml_chapter03_2_11)

Pollard’s ρ algorithm (logarithm) [1](#chapter03_2.xhtml_chapter03_2_20)

polyalphabetic cipher [1](#chapter02_1.xhtml_chapter02_1_10)

polynomial [1](#chapter01_2.xhtml_chapter01_2_27)

–constant [1](#chapter01_2.xhtml_chapter01_2_27)

–coprime [1](#chapter01_3.xhtml_chapter01_3_9)

–degree [1](#chapter01_2.xhtml_chapter01_2_27)

–derivative [1](#chapter01_3.xhtml_chapter01_3_3)

–irreducible [1](#chapter01_3.xhtml_chapter01_3_12)

–Lagrange [1](#chapter02_2.xhtml_chapter02_2_6)

–minimal [1](#chapter01_4.xhtml_chapter01_4_29)

–root of a [1](#chapter01_3.xhtml_chapter01_3_9)

–thin [1](#chapter01_4.xhtml_chapter01_4_27)

–zero [1](#chapter01_2.xhtml_chapter01_2_27)

–zero of a [1](#chapter01_3.xhtml_chapter01_3_9)

polynomial division [1](#chapter01_3.xhtml_chapter01_3_6)

polynomial method [1](#chapter04.xhtml_chapter04_31)

polynomial ring [1](#chapter01_2.xhtml_chapter01_2_27)

–over E(k) [1](#chapter05_1.xhtml_chapter05_1_17), [2](#chapter05_2.xhtml_chapter05_2_18)

Pomerance, C. B. [1](#chapter03_1.xhtml_chapter03_1_33)

power circuit [1](#chapter08_2.xhtml_chapter08_2_29)

power of a word [1](#chapter06.xhtml_chapter06_1)

power series [1](#chapter01_2.xhtml_chapter01_2_27)

powerset construction see [subset construction](#Index_2.xhtml_Index_2_17)

pragmatic security [1](#chapter02_1.xhtml_chapter02_1_8)

prefix [1](#chapter06.xhtml_chapter06_1)

Presburger arithmetic [1](#chapter07_5.xhtml_chapter07_5_11)

Presburger, M. [1](#chapter07_5.xhtml_chapter07_5_11), [2](#chapter07_5.xhtml_chapter07_5_19)

Presburger’s theorem [1](#chapter07_5.xhtml_chapter07_5_19)

presentation [1](#chapter08_1.xhtml_chapter08_1_14)

primality certificate [1](#chapter05_2.xhtml_chapter05_2_13)

–Goldwasser–Kilian [1](#chapter05_2.xhtml_chapter05_2_13)

–Pocklington [1](#chapter05_2.xhtml_chapter05_2_15)

primality test

–AKS [1](#chapter04.xhtml_chapter04_1)

–deterministic [1](#chapter04.xhtml_chapter04_1)

–Fermat [1](#chapter03_1.xhtml_chapter03_1_12)

–Goldwasser–Kilian [1](#chapter05_2.xhtml_chapter05_2_13)

–Lucas [1](#chapter03_3.xhtml_chapter03_3_17)

–Lucas–Lehmer [1](#chapter03_3.xhtml_chapter03_3_23)

–Miller–Rabin [1](#chapter03_1.xhtml_chapter03_1_19)

–Pépin [1](#chapter03_3.xhtml_chapter03_3_17)

–Pocklington [1](#chapter05_2.xhtml_chapter05_2_13)

–probabilistic [1](#chapter03_1.xhtml_chapter03_1_12)

–Solovay–Strassen [1](#chapter03_1.xhtml_chapter03_1_16)

prime field [1](#chapter01_2.xhtml_chapter01_2_6)

prime number

–Fermat [1](#chapter03_3.xhtml_chapter03_3_17)

–Mersenne [1](#chapter03_3.xhtml_chapter03_3_17)

–pseudo- [1](#chapter03_1.xhtml_chapter03_1_31)

–Sophie Germain [1](#chapter02_1.xhtml_chapter02_1_29)

primitive root [1](#chapter01_3.xhtml_chapter01_3_25), [2](#chapter03_3.xhtml_chapter03_3_4), [3](#chapter06.xhtml_chapter06_8)

–of a word [1](#chapter06.xhtml_chapter06_36)

primitive word [1](#chapter06.xhtml_chapter06_8), [2](#chapter06.xhtml_chapter06_36)

principal divisor [1](#chapter05_1.xhtml_chapter05_1_24)

principal ideal [1](#chapter01_2.xhtml_chapter01_2_3), [2](#chapter07_3.xhtml_chapter07_3_22)

principal root see [primitive root](#Index_2.xhtml_Index_2_4)

problem

–conjugacy [1](#chapter08_1.xhtml_chapter08_1_1)

–Diffie–Hellman [1](#chapter02_1.xhtml_chapter02_1_29), [2](#chapter05_2.xhtml_chapter05_2_6)

–discrete logarithm [1](#chapter03_2.xhtml_chapter03_2_18)

–extracting square roots [1](#chapter03_1.xhtml_chapter03_1_33)

–halting [1](#chapter08_1.xhtml_chapter08_1_27)

–Hilbert’s tenth [1](#chapter07_5.xhtml_chapter07_5_21)

–integer factorization [1](#chapter03_2.xhtml_chapter03_2_8)

–isomorphism [1](#chapter08_1.xhtml_chapter08_1_1)

–knapsack [1](#chapter02_2.xhtml_chapter02_2_12)

–word [1](#chapter08_1.xhtml_chapter08_1_1)

product

–amalgamated [1](#chapter08_2.xhtml_chapter08_2_15)

–direct [1](#chapter01_2.xhtml_chapter01_2_23)

–free [1](#chapter08_1.xhtml_chapter08_1_35)

–semidirect [1](#chapter08_2.xhtml_chapter08_2_13)

–wreath [1](#chapter07_2.xhtml_chapter07_2_39), [2](#chapter07_2.xhtml_chapter07_2_41)

product automaton [1](#chapter07_6.xhtml_chapter07_6_8)

product order [1](#chapter06.xhtml_chapter06_20)

projection [1](#chapter08_3.xhtml_chapter08_3_26)

pseudocurve [1](#chapter05_2.xhtml_chapter05_2_6)

–partially defined sum [1](#chapter05_2.xhtml_chapter05_2_6)

pseudoprime [1](#chapter03_1.xhtml_chapter03_1_31)

–Eulerian [1](#chapter03_1.xhtml_chapter03_1_31)

–strong [1](#chapter03_1.xhtml_chapter03_1_31)

pseudo-random sequence [1](#chapter03_2.xhtml_chapter03_2_11)

pseudovariety see [variety](#Index_2.xhtml_Index_2_22)

public-key cryptosystem [1](#chapter02_1.xhtml_chapter02_1_23)

Putnam, H. [1](#chapter07_5.xhtml_chapter07_5_22)

Q

Qin, J. [1](#chapter01_2.xhtml_chapter01_2_23)

quadratic reciprocity [1](#chapter01_4.xhtml_chapter01_4_8)

quadratic residue [1](#chapter01_4.xhtml_chapter01_4_3), [2](#chapter03_1.xhtml_chapter03_1_33)

quadratic sieve [1](#chapter03_2.xhtml_chapter03_2_13)

quasi-ordering [1](#chapter06.xhtml_chapter06_15)

–well- [1](#chapter06.xhtml_chapter06_15)

quotient group [1](#chapter01_1.xhtml_chapter01_1_20)

quotient of a language [1](#chapter07_1.xhtml_chapter07_1_9)

quotient ring [1](#chapter01_2.xhtml_chapter01_2_3)

R

ρ algorithm [1](#chapter03_2.xhtml_chapter03_2_11)

*R*-class [1](#chapter07_3.xhtml_chapter07_3_25)

RAAG see [right-angled Artin group](#Index_2.xhtml_Index_2_11)

Rabin cryptosystem [1](#chapter02_1.xhtml_chapter02_1_23), [2](#chapter02_1.xhtml_chapter02_1_26)

Rabin, M. O. [1](#chapter02_1.xhtml_chapter02_1_26), [2](#chapter03_1.xhtml_chapter03_1_19)

Ramsey, F. P. [1](#chapter06.xhtml_chapter06_17)

Ramsey’s theorem [1](#chapter06.xhtml_chapter06_17)

rank formula [1](#chapter08_3.xhtml_chapter08_3_16)

rank of a free group [1](#chapter08_1.xhtml_chapter08_1_27), [2](#chapter08_3.xhtml_chapter08_3_5)

rational expression [1](#chapter07_1.xhtml_chapter07_1_19)

rational function [1](#chapter05_2.xhtml_chapter05_2_18)

rational morphism [1](#chapter05_3.xhtml_chapter05_3_1)

rational set [1](#chapter07_1.xhtml_chapter07_1_19), [2](#chapter08_2.xhtml_chapter08_2_29)

reachable state [1](#chapter07_1.xhtml_chapter07_1_8)

reciprocity [1](#chapter01_4.xhtml_chapter01_4_3)

recognizable [1](#chapter07_1.xhtml_chapter07_1_2)

recognize [1](#chapter07_1.xhtml_chapter07_1_2), [2](#chapter07_4.xhtml_chapter07_4_29)

–strongly [1](#chapter07_4.xhtml_chapter07_4_29)

–weakly [1](#chapter07_4.xhtml_chapter07_4_29)

recurrence [1](#chapter03_1.xhtml_chapter03_1_1)

reduced word [1](#chapter08_3.xhtml_chapter08_3_11)

Rees, D. [1](#chapter01_4.xhtml_chapter01_4_18)

Rees sandwich semigroup [1](#chapter01_4.xhtml_chapter01_4_18)

regular class [1](#chapter07_4.xhtml_chapter07_4_6)

regular element [1](#chapter01_4.xhtml_chapter01_4_18)

regular expression see [rational expression](#Index_2.xhtml_Index_2_9)

regular language [1](#chapter07_2.xhtml_chapter07_2_3)

regular n-gon [1](#chapter01_1.xhtml_chapter01_1_26)

relation

–Green’s [1](#chapter07_3.xhtml_chapter07_3_25)

–independence [1](#chapter08_1.xhtml_chapter08_1_49)

relatively prime see [coprime](#Index_1.xhtml_Index_1_10)

remainder [1](#chapter01_2.xhtml_chapter01_2_14)

residually finite [1](#chapter08_1.xhtml_chapter08_1_12)

residue class [1](#chapter01_2.xhtml_chapter01_2_3)

–quadratic [1](#chapter01_4.xhtml_chapter01_4_3)

reverse language [1](#chapter07_6.xhtml_chapter07_6_9)

rewriting system [1](#chapter08_1.xhtml_chapter08_1_14)

–Church–Rosser [1](#chapter08_1.xhtml_chapter08_1_17)

–complete [1](#chapter08_1.xhtml_chapter08_1_17)

–confluent [1](#chapter08_1.xhtml_chapter08_1_17)

–convergent [1](#chapter08_1.xhtml_chapter08_1_17)

–locally confluent [1](#chapter08_1.xhtml_chapter08_1_17)

–Noetherian [1](#chapter08_1.xhtml_chapter08_1_17)

–semi-Thue [1](#chapter08_1.xhtml_chapter08_1_22)

–strongly confluent [1](#chapter08_1.xhtml_chapter08_1_17)

–terminating [1](#chapter08_1.xhtml_chapter08_1_17)

Rhodes, J. L. VI, [1](#chapter01_1.xhtml_chapter01_1_2), [2](#chapter07_2.xhtml_chapter07_2_27), [3](#chapter07_2.xhtml_chapter07_2_39)

Riemann, G. F. B. [1](#chapter04.xhtml_chapter04_1)

right-angled Artin group [1](#chapter08_1.xhtml_chapter08_1_54)

right-angled Coxeter group [1](#chapter08_2.xhtml_chapter08_2_8)

right coset [1](#chapter01_1.xhtml_chapter01_1_7)

right ideal [1](#chapter07_3.xhtml_chapter07_3_22)

right inverse [1](#chapter01_4.xhtml_chapter01_4_14)

right neutral [1](#chapter01_4.xhtml_chapter01_4_18)

right zero [1](#chapter07_3.xhtml_chapter07_3_5)

ring [1](#chapter01_1.xhtml_chapter01_1_4), [2](#chapter01_2.xhtml_chapter01_2_1)

–commutative [1](#chapter01_2.xhtml_chapter01_2_1)

–Noetherian [1](#chapter01_3.xhtml_chapter01_3_17)

–polynomial [1](#chapter01_2.xhtml_chapter01_2_27)

–zero [1](#chapter01_2.xhtml_chapter01_2_1)

ring homomorphism [1](#chapter01_2.xhtml_chapter01_2_3)

ring isomorphism [1](#chapter01_2.xhtml_chapter01_2_4)

Rivest, R.L. V, [1](#chapter02_1.xhtml_chapter02_1_24)

Robertson, G. N. [1](#chapter06.xhtml_chapter06_30)

Robinson, J. [1](#chapter07_5.xhtml_chapter07_5_22)

Rolle, M. [1](#chapter09_1.xhtml_chapter09_1_7)

Rolle’s theorem [1](#chapter09_1.xhtml_chapter09_1_7)

root

–of unity [1](#chapter01_3.xhtml_chapter01_3_25)

–primitive [1](#chapter01_3.xhtml_chapter01_3_25), [2](#chapter03_3.xhtml_chapter03_3_4), [3](#chapter06.xhtml_chapter06_8)

root of a polynomial [1](#chapter01_3.xhtml_chapter01_3_9)

–multiple [1](#chapter01_3.xhtml_chapter01_3_9)

–multiplicity of a [1](#chapter01_3.xhtml_chapter01_3_9)

–primitive [1](#chapter01_3.xhtml_chapter01_3_25)

–simple [1](#chapter01_3.xhtml_chapter01_3_9)

root of a rational function [1](#chapter05_3.xhtml_chapter05_3_1)

rose [1](#chapter08_3.xhtml_chapter08_3_30), [2](#chapter08_4.xhtml_chapter08_4_9)

Rosser, J. B. [1](#chapter08_1.xhtml_chapter08_1_14)

Rousseau, G. [1](#chapter01_4.xhtml_chapter01_4_14)

RSA cryptosystem [1](#chapter02_1.xhtml_chapter02_1_23), [2](#chapter02_1.xhtml_chapter02_1_24), [3](#chapter03_1.xhtml_chapter03_1_30)

–multiple exponent attack [1](#chapter02_2.xhtml_chapter02_2_27)

–multi-prime [1](#chapter02_2.xhtml_chapter02_2_27)

RSA signature [1](#chapter02_2.xhtml_chapter02_2_3)

Ruffini, P. [1](#chapter01_1.xhtml_chapter01_1_2), [2](#chapter01_2.xhtml_chapter01_2_1)

run [1](#chapter07_1.xhtml_chapter07_1_19), [2](#chapter07_1.xhtml_chapter07_1_26)

–accepting [1](#chapter07_1.xhtml_chapter07_1_19)

S

Saxena, N. VI, [1](#chapter04.xhtml_chapter04_1)

scattered subword see [subword](#Index_2.xhtml_Index_2_18)

scheme [1](#chapter05_3.xhtml_chapter05_3_9)

Schleimer, S. [1](#chapter08_3.xhtml_chapter08_3_22)

Schönhage, A. VI, [1](#chapter03_3.xhtml_chapter03_3_9)

Schönhage–Strassen multiplication [1](#chapter03_3.xhtml_chapter03_3_9)

Schoof, R. J. [1](#chapter05_2.xhtml_chapter05_2_17)

Schreier graph [1](#chapter08_3.xhtml_chapter08_3_11)

–complete [1](#chapter08_3.xhtml_chapter08_3_14)

–kernel [1](#chapter08_3.xhtml_chapter08_3_12)

Schreier, O. [1](#chapter08_3.xhtml_chapter08_3_5), [2](#chapter08_3.xhtml_chapter08_3_16)

Schupp, P. VII

Schützenberger group [1](#chapter07_4.xhtml_chapter07_4_1), [2](#chapter07_4.xhtml_chapter07_4_4)

Schützenberger, M.-P. VI, [1](#chapter06.xhtml_chapter06_8), [2](#chapter07_2.xhtml_chapter07_2_15), [3](#chapter07_2.xhtml_chapter07_2_21), [4](#chapter07_4.xhtml_chapter07_4_1), [5](#chapter08_3.xhtml_chapter08_3_19)

Schützenberger’s theorem [1](#chapter07_2.xhtml_chapter07_2_21)

secret sharing [1](#chapter02_2.xhtml_chapter02_2_4)

–Shamir [1](#chapter02_2.xhtml_chapter02_2_6)

–subset of keys [1](#chapter02_2.xhtml_chapter02_2_4)

security

–absolute see [perfect security](#Index_2.xhtml_Index_2_3)

–computational [1](#chapter02_1.xhtml_chapter02_1_5)

–perfect [1](#chapter02_1.xhtml_chapter02_1_5), [2](#chapter02_1.xhtml_chapter02_1_15)

–pragmatic [1](#chapter02_1.xhtml_chapter02_1_8)

–relative computational [1](#chapter02_1.xhtml_chapter02_1_8)

Selfridge, J. L. [1](#chapter03_1.xhtml_chapter03_1_33)

semidirect product [1](#chapter08_2.xhtml_chapter08_2_13)

semigroup [1](#chapter01_1.xhtml_chapter01_1_4)

–cyclic [1](#chapter07_6.xhtml_chapter07_6_8)

–Rees sandwich [1](#chapter01_4.xhtml_chapter01_4_18)

–syntactic [1](#chapter07_4.xhtml_chapter07_4_32)

semilinear set [1](#chapter07_5.xhtml_chapter07_5_15)

semi-Thue system [1](#chapter08_1.xhtml_chapter08_1_22)

–monadic [1](#chapter08_3.xhtml_chapter08_3_1)

sentence [1](#chapter07_5.xhtml_chapter07_5_5), [2](#chapter07_5.xhtml_chapter07_5_15)

separable endomorphism [1](#chapter05_3.xhtml_chapter05_3_7)

sequence

–bad [1](#chapter06.xhtml_chapter06_15)

–decreasing [1](#chapter06.xhtml_chapter06_15)

–good [1](#chapter06.xhtml_chapter06_15)

–nondecreasing [1](#chapter06.xhtml_chapter06_15)

–superincreasing [1](#chapter02_2.xhtml_chapter02_2_12)

Serre, J. P. VII, [1](#chapter08_2.xhtml_chapter08_2_27), [2](#chapter08_3.xhtml_chapter08_3_5)

set

–accepted [1](#chapter07_1.xhtml_chapter07_1_19)

–linear [1](#chapter07_5.xhtml_chapter07_5_15)

–rational [1](#chapter07_1.xhtml_chapter07_1_19), [2](#chapter08_2.xhtml_chapter08_2_29)

–recognizable [1](#chapter07_1.xhtml_chapter07_1_2)

–regular [1](#chapter07_2.xhtml_chapter07_2_3)

–semilinear [1](#chapter07_5.xhtml_chapter07_5_15)

–solution [1](#chapter07_5.xhtml_chapter07_5_28)

–star-free [1](#chapter07_2.xhtml_chapter07_2_20)

Seymour, P. D. [1](#chapter06.xhtml_chapter06_30)

Shallit, J. O. [1](#chapter06.xhtml_chapter06_12)

Shamir, A. V, [1](#chapter02_1.xhtml_chapter02_1_24), [2](#chapter02_2.xhtml_chapter02_2_6), [3](#chapter02_2.xhtml_chapter02_2_12), [4](#chapter02_2.xhtml_chapter02_2_17), [5](#chapter02_2.xhtml_chapter02_2_24)

Shamir’s attack [1](#chapter02_2.xhtml_chapter02_2_17)

Shamir’s secret sharing [1](#chapter02_2.xhtml_chapter02_2_6)

Shanks, D. [1](#chapter03_2.xhtml_chapter03_2_5), [2](#chapter03_2.xhtml_chapter03_2_18)

Shannon, C. E. [1](#chapter02_1.xhtml_chapter02_1_15)

shift cipher [1](#chapter02_1.xhtml_chapter02_1_8)

shortlex [1](#chapter08_1.xhtml_chapter08_1_12)

sign of a permutation [1](#chapter01_1.xhtml_chapter01_1_31)

signature

–digital [1](#chapter02_2.xhtml_chapter02_2_1)

–DSA [1](#chapter02_2.xhtml_chapter02_2_1)

–ElGamal [1](#chapter02_2.xhtml_chapter02_2_27)

–RSA [1](#chapter02_2.xhtml_chapter02_2_3)

simple group [1](#chapter07_2.xhtml_chapter07_2_39)

simple root [1](#chapter01_3.xhtml_chapter01_3_9)

skew field [1](#chapter01_2.xhtml_chapter01_2_1)

small cancellation group [1](#chapter08_1.xhtml_chapter08_1_44)

smooth number [1](#chapter03_2.xhtml_chapter03_2_15), [2](#chapter03_2.xhtml_chapter03_2_25)

Solitar, D. [1](#chapter08_1.xhtml_chapter08_1_35)

Solovay, R.M. [1](#chapter03_1.xhtml_chapter03_1_16)

Solovay–Strassen primality test [1](#chapter03_1.xhtml_chapter03_1_16)

solution set [1](#chapter07_5.xhtml_chapter07_5_28)

Sophie Germain prime [1](#chapter02_1.xhtml_chapter02_1_29)

source encoding [1](#chapter02_1.xhtml_chapter02_1_3), [2](#chapter02_1.xhtml_chapter02_1_13)

source of an edge [1](#chapter08_3.xhtml_chapter08_3_11)

spanning tree [1](#chapter08_3.xhtml_chapter08_3_12)

special linear group [1](#chapter08_1.xhtml_chapter08_1_12), [2](#chapter08_4.xhtml_chapter08_4_9)

spelling automaton [1](#chapter07_1.xhtml_chapter07_1_21), [2](#chapter07_2.xhtml_chapter07_2_13)

splitting field [1](#chapter01_3.xhtml_chapter01_3_22)

square [1](#chapter01_4.xhtml_chapter01_4_3), [2](#chapter03_1.xhtml_chapter03_1_33)

square root [1](#chapter01_4.xhtml_chapter01_4_3), [2](#chapter03_1.xhtml_chapter03_1_33)

square-free number [1](#chapter03_1.xhtml_chapter03_1_16)

Squier, C. C. [1](#chapter08_1.xhtml_chapter08_1_44)

stabilization index [1](#chapter07_6.xhtml_chapter07_6_8)

Stallings graph [1](#chapter08_3.xhtml_chapter08_3_5)

Stallings, J. R., Jr. VII, [1](#chapter08_3.xhtml_chapter08_3_5), [2](#chapter08_3.xhtml_chapter08_3_26)

star see [Kleene star](#Index_1.xhtml_Index_1_22)

star operation [1](#chapter07_1.xhtml_chapter07_1_1)

star-free expression [1](#chapter07_2.xhtml_chapter07_2_20)

star-free set [1](#chapter07_2.xhtml_chapter07_2_20)

state

–final [1](#chapter07_1.xhtml_chapter07_1_8), [2](#chapter07_1.xhtml_chapter07_1_19)

–initial [1](#chapter07_1.xhtml_chapter07_1_8), [2](#chapter07_1.xhtml_chapter07_1_19)

–reachable [1](#chapter07_1.xhtml_chapter07_1_8)

state elimination [1](#chapter07_1.xhtml_chapter07_1_26)

Steinitz, E. [1](#chapter01_1.xhtml_chapter01_1_2)

Strassen, V. VI, [1](#chapter03_1.xhtml_chapter03_1_16), [2](#chapter03_3.xhtml_chapter03_3_9)

string see [word](#Index_2.xhtml_Index_2_24)

string rewriting system see [semi-Thue system](#Index_2.xhtml_Index_2_14)

strong pseudoprime [1](#chapter03_1.xhtml_chapter03_1_31)

strongly confluent [1](#chapter08_1.xhtml_chapter08_1_17)

strongly recognize see [recognize](#Index_2.xhtml_Index_2_10)

subfield [1](#chapter01_2.xhtml_chapter01_2_3)

subgroup [1](#chapter01_1.xhtml_chapter01_1_7)

–index of a [1](#chapter01_1.xhtml_chapter01_1_12)

–normal [1](#chapter01_1.xhtml_chapter01_1_20)

submonoid [1](#chapter01_1.xhtml_chapter01_1_5)

–local [1](#chapter07_2.xhtml_chapter07_2_20)

subring [1](#chapter01_2.xhtml_chapter01_2_3)

subsemigroup [1](#chapter01_1.xhtml_chapter01_1_5)

subset automaton [1](#chapter07_2.xhtml_chapter07_2_8)

subset construction [1](#chapter07_2.xhtml_chapter07_2_8)

substitution

–monoalphabetic [1](#chapter02_1.xhtml_chapter02_1_8)

–polyalphabetic [1](#chapter02_1.xhtml_chapter02_1_10)

substructure [1](#chapter01_1.xhtml_chapter01_1_5)

–generated [1](#chapter01_1.xhtml_chapter01_1_5)

subtree [1](#chapter06.xhtml_chapter06_28)

subword [1](#chapter06.xhtml_chapter06_15), [2](#chapter06.xhtml_chapter06_20)

suffix [1](#chapter06.xhtml_chapter06_1)

Sun, T. [1](#chapter01_2.xhtml_chapter01_2_23)

superincreasing sequence [1](#chapter02_2.xhtml_chapter02_2_12)

symbol

–Jacobi [1](#chapter01_4.xhtml_chapter01_4_5)

–Legendre [1](#chapter01_4.xhtml_chapter01_4_8)

symmetric group [1](#chapter01_1.xhtml_chapter01_1_31)

symmetry group [1](#chapter01_1.xhtml_chapter01_1_29)

syntactic congruence [1](#chapter07_1.xhtml_chapter07_1_5), [2](#chapter07_4.xhtml_chapter07_4_32)

syntactic homomorphism [1](#chapter07_4.xhtml_chapter07_4_32)

syntactic monoid [1](#chapter07_1.xhtml_chapter07_1_5)

syntactic semigroup [1](#chapter07_4.xhtml_chapter07_4_32)

T

target of an edge [1](#chapter08_3.xhtml_chapter08_3_11)

Tartaglia, N. F. [1](#chapter01_1.xhtml_chapter01_1_1)

terminating rewriting system [1](#chapter08_1.xhtml_chapter08_1_17)

Theaitetos [1](#chapter01_1.xhtml_chapter01_1_1)

theorem

–Benois [1](#chapter08_3.xhtml_chapter08_3_5)

–binomial [1](#chapter01_2.xhtml_chapter01_2_8)

–Büchi [1](#chapter07_5.xhtml_chapter07_5_2), [2](#chapter07_5.xhtml_chapter07_5_6)

–Cauchy [1](#chapter01_1.xhtml_chapter01_1_16)

–chinese remainder [1](#chapter01_2.xhtml_chapter01_2_23)

–degree formula [1](#chapter01_2.xhtml_chapter01_2_28)

–Euler [1](#chapter01_2.xhtml_chapter01_2_23)

–Euler’s criterion [1](#chapter01_4.xhtml_chapter01_4_5)

–Fermat’s Last [1](#chapter05_1.xhtml_chapter05_1_6)

–Fermat’s little [1](#chapter01_2.xhtml_chapter01_2_10)

–Fine–Wilf [1](#chapter06.xhtml_chapter06_12)

–Gödel’s incompleteness [1](#chapter07_5.xhtml_chapter07_5_11), [2](#chapter07_5.xhtml_chapter07_5_21)

–Goldwasser–Kilian [1](#chapter05_2.xhtml_chapter05_2_15)

–Hasse [1](#chapter05_1.xhtml_chapter05_1_8)

–Hilbert’s basis [1](#chapter01_3.xhtml_chapter01_3_17)

–homomorphism (for groups) [1](#chapter01_1.xhtml_chapter01_1_23)

–homomorphism (for rings) [1](#chapter01_2.xhtml_chapter01_2_4)

–Kleene [1](#chapter07_2.xhtml_chapter07_2_8)

–Krohn–Rhodes [1](#chapter07_2.xhtml_chapter07_2_39)

–Kruskal’s tree [1](#chapter06.xhtml_chapter06_28)

–Lagrange [1](#chapter01_1.xhtml_chapter01_1_12)

–Lyndon–Schützenberger [1](#chapter06.xhtml_chapter06_8)

–master [1](#chapter03_1.xhtml_chapter03_1_4)

–master II [1](#chapter03_3.xhtml_chapter03_3_17)

–McKnight [1](#chapter07_2.xhtml_chapter07_2_3)

–Mezei [1](#chapter07_6.xhtml_chapter07_6_8)

–Myhill–Nerode [1](#chapter07_1.xhtml_chapter07_1_15)

–Nielsen–Schreier [1](#chapter08_3.xhtml_chapter08_3_16)

–Pocklington [1](#chapter05_2.xhtml_chapter05_2_13)

–Presburger [1](#chapter07_5.xhtml_chapter07_5_19)

–Ramsey [1](#chapter06.xhtml_chapter06_17)

–Rolle [1](#chapter09_1.xhtml_chapter09_1_7)

–Schützenberger [1](#chapter07_2.xhtml_chapter07_2_21)

–sums of two squares [1](#chapter08_5.xhtml_chapter08_5_1)

–Wedderburn [1](#chapter09_1.xhtml_chapter09_1_5)

Thompson construction [1](#chapter07_1.xhtml_chapter07_1_21)

Thompson, K. L. [1](#chapter07_1.xhtml_chapter07_1_21)

threshold of an element [1](#chapter07_3.xhtml_chapter07_3_22)

Thue, A. [1](#chapter06.xhtml_chapter06_1), [2](#chapter08_1.xhtml_chapter08_1_22)

Tietze transformation [1](#chapter08_1.xhtml_chapter08_1_38)

Tietze, H. F. F. [1](#chapter08_1.xhtml_chapter08_1_1), [2](#chapter08_1.xhtml_chapter08_1_38)

Tonelli, A. [1](#chapter03_2.xhtml_chapter03_2_3)

Tonelli’s algorithm [1](#chapter03_2.xhtml_chapter03_2_3)

torus [1](#chapter05_1.xhtml_chapter05_1_1)

totient function [1](#chapter01_2.xhtml_chapter01_2_23)

tower function [1](#chapter08_4.xhtml_chapter08_4_28)

trace monoid [1](#chapter08_1.xhtml_chapter08_1_49)

track [1](#chapter07_5.xhtml_chapter07_5_10), [2](#chapter07_5.xhtml_chapter07_5_16)

Trakhtenbrot, B. A. [1](#chapter07_5.xhtml_chapter07_5_6)

transcendental number [1](#chapter01_1.xhtml_chapter01_1_1)

transformation

–Nielsen [1](#chapter08_3.xhtml_chapter08_3_22), [2](#chapter08_4.xhtml_chapter08_4_28)

–Tietze [1](#chapter08_1.xhtml_chapter08_1_38)

transition [1](#chapter07_1.xhtml_chapter07_1_8), [2](#chapter07_1.xhtml_chapter07_1_19)

–ε- [1](#chapter07_1.xhtml_chapter07_1_24)

–elimination of ε- [1](#chapter07_1.xhtml_chapter07_1_24)

–final [1](#chapter09_4.xhtml_chapter09_4_3)

–label of a [1](#chapter07_1.xhtml_chapter07_1_19)

transition function [1](#chapter07_1.xhtml_chapter07_1_8)

transition monoid [1](#chapter07_1.xhtml_chapter07_1_15)

transposed elements [1](#chapter06.xhtml_chapter06_6)

transposition [1](#chapter01_1.xhtml_chapter01_1_34)

tree [1](#chapter06.xhtml_chapter06_25), [2](#chapter08_3.xhtml_chapter08_3_12)

–ordered [1](#chapter06.xhtml_chapter06_25)

–spanning [1](#chapter08_3.xhtml_chapter08_3_12)

–sub- [1](#chapter06.xhtml_chapter06_28)

trim automaton [1](#chapter07_6.xhtml_chapter07_6_2)

two-sided ideal [1](#chapter07_3.xhtml_chapter07_3_22)

U

ultimately periodic word [1](#chapter07_4.xhtml_chapter07_4_22)

unit [1](#chapter01_2.xhtml_chapter01_2_1), [2](#chapter07_3.xhtml_chapter07_3_10)

universal property [1](#chapter06.xhtml_chapter06_1)

unknown see [variable](#Index_2.xhtml_Index_2_21)

V

variable [1](#chapter01_2.xhtml_chapter01_2_27)

–first-order [1](#chapter07_5.xhtml_chapter07_5_5)

–free [1](#chapter07_5.xhtml_chapter07_5_15)

–monadic second-order [1](#chapter07_5.xhtml_chapter07_5_5)

variety [1](#chapter07_6.xhtml_chapter07_6_9)

Vernam, G. [1](#chapter02_1.xhtml_chapter02_1_18)

Vernam one-time pad [1](#chapter02_1.xhtml_chapter02_1_18)

vertical [1](#chapter05_1.xhtml_chapter05_1_8)

Vigenère, B. de [1](#chapter02_1.xhtml_chapter02_1_12)

Vigenère cipher [1](#chapter02_1.xhtml_chapter02_1_12)

Voltaire [1](#chapter02_1.xhtml_chapter02_1_1), [2](#chapter09_1.xhtml_chapter09_1_9)

W

Waack group [1](#chapter08_1.xhtml_chapter08_1_38)

Waack, S. [1](#chapter08_1.xhtml_chapter08_1_38)

Wagner, K. W. VII

Wagstaff, S. S., Jr. [1](#chapter03_1.xhtml_chapter03_1_33)

weakly recognize [1](#chapter07_4.xhtml_chapter07_4_29)

Wedderburn, J.H. M. [1](#chapter09_1.xhtml_chapter09_1_5)

Wedderburn’s theorem [1](#chapter09_1.xhtml_chapter09_1_5)

Weierstrass equation see [Weierstrass normal form](#Index_2.xhtml_Index_2_23)

Weierstrass, K. T. W. [1](#chapter05_1.xhtml_chapter05_1_6), [2](#chapter05_3.xhtml_chapter05_3_9)

Weierstrass normal form [1](#chapter05_1.xhtml_chapter05_1_6), [2](#chapter05_3.xhtml_chapter05_3_9)

Weil, A. [1](#chapter05_3.xhtml_chapter05_3_9)

Weil pairing [1](#chapter05_3.xhtml_chapter05_3_9)

well-quasi-ordering [1](#chapter06.xhtml_chapter06_15)

Whitehead automorphism [1](#chapter08_3.xhtml_chapter08_3_22)

Whitehead, J. H. C. VII, [1](#chapter08_3.xhtml_chapter08_3_22)

Wiener attack [1](#chapter02_1.xhtml_chapter02_1_24)

Wiener, M. J. [1](#chapter02_1.xhtml_chapter02_1_24)

Wiles, A. [1](#chapter05_1.xhtml_chapter05_1_6)

Wilf, H. S. [1](#chapter06.xhtml_chapter06_12)

Winograd, S. [1](#chapter07_1.xhtml_chapter07_1_5)

Witt, E. VII, [1](#chapter09_1.xhtml_chapter09_1_5)

word [1](#chapter06.xhtml_chapter06_1), [2](#chapter07_2.xhtml_chapter07_2_3), [3](#chapter08_1.xhtml_chapter08_1_12)

–alphabet of a [1](#chapter06.xhtml_chapter06_1)

–cyclically reduced [1](#chapter08_3.xhtml_chapter08_3_19)

–empty [1](#chapter06.xhtml_chapter06_1), [2](#chapter08_1.xhtml_chapter08_1_12)

–finite [1](#chapter06.xhtml_chapter06_1)

–infinite [1](#chapter07_4.xhtml_chapter07_4_10)

–length [1](#chapter06.xhtml_chapter06_1), [2](#chapter08_1.xhtml_chapter08_1_12)

–Lyndon [1](#chapter06.xhtml_chapter06_36)

–period [1](#chapter06.xhtml_chapter06_12)

–power [1](#chapter06.xhtml_chapter06_1)

–primitive [1](#chapter06.xhtml_chapter06_8), [2](#chapter06.xhtml_chapter06_36)

–reduced [1](#chapter08_3.xhtml_chapter08_3_11)

–ultimately periodic [1](#chapter07_4.xhtml_chapter07_4_22)

word problem [1](#chapter08_1.xhtml_chapter08_1_1), [2](#chapter08_1.xhtml_chapter08_1_14)

wreath product [1](#chapter07_2.xhtml_chapter07_2_39), [2](#chapter07_2.xhtml_chapter07_2_41)

wreath product principle [1](#chapter07_3.xhtml_chapter07_3_2)

Z

zero see [root of a polynomial](#Index_2.xhtml_Index_2_12)

–of a polynomial [1](#chapter01_3.xhtml_chapter01_3_9)

–of a rational function [1](#chapter05_3.xhtml_chapter05_3_1)

–right [1](#chapter07_3.xhtml_chapter07_3_5)

zero divisor [1](#chapter01_2.xhtml_chapter01_2_6)

zero element [1](#chapter01_1.xhtml_chapter01_1_4)

zero polynomial [1](#chapter01_2.xhtml_chapter01_2_27)

zero ring [1](#chapter01_2.xhtml_chapter01_2_1)

Zolotarev, Y. I. [1](#chapter01_4.xhtml_chapter01_4_5)

Zolotarev’s lemma [1](#chapter01_4.xhtml_chapter01_4_5)

# Footnotes

| [1](#chapter01_1.xhtml_chapter01_1_3) | By flip–flop we mean the three element monoid U2 = {1, a, b} with xy = y for y ≠ 1. |
| [2](#chapter02_1.xhtml_chapter02_1_2) | Historical sources do not entirely agree on the exact form. |
| [3](#chapter02_1.xhtml_chapter02_1_19) | The Vernam one-time pad was used on the red telephone which connected the White House to the Kremlin during the Cold War. |
| [4](#chapter02_2.xhtml_chapter02_2_10) | This scenario was taken from the lecture notes of a course taught by Holger Petersen at the University of Stuttgart in Summer Semester 2007. |
| [5](#chapter04.xhtml_chapter04_2) | The Gödel Prize is awarded annually for the best work in the field of theoretical computer science, published in the last 13 years. |
| [6](#chapter05_1.xhtml_chapter05_1_10) | According to Jacques Monod’s (1910–1976) book Le hasard et la nécessité. Essai sur la philosophie naturelle de la biologie moderne from 1970. |
| [7](#chapter06.xhtml_chapter06_4) | In the context of monoids, we use the symbol 1 for the empty word, too. Another standard notation for the empty word is λ. The symbol λ refers to the original work of Thue who published in German, where leeres Wort means empty word. |
| [8](#chapter07_5.xhtml_chapter07_5_29) | Given any rational set R of affine mappings the set { h(0) &#124; h ∈ R} is a semilinear set, but we do not need this fact here. |
| [9](#chapter08_1.xhtml_chapter08_1_30) | Dyck was enobled “Ritter” (“Knight”) in 1901, and in 1903 he became the first rector of the Technical University of Munich. |