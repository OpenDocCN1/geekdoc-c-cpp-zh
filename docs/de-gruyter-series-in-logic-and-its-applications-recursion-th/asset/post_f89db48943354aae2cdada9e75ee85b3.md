

Chi Tat Chong, Liang Yu

## Recursion Theory

Computational Aspects of Definability

### De Gruyter Series in Logic and Its Applications

Editors

- Wilfried A. Hodges, University of London, United Kingdom
- Menachem Magidor, The Hebrew University of Jerusalem, Israel
- Anand Pillay, University of Notre Dame, USA

### Volume 8

### AMS subject classification (2010)

03-01, 03-02, 03C0, 03E

### Authors

- Prof. Dr. Chi Tat Chong
  National University of Singapore
  Department of Mathematics
  10 Lower Kent Ridge Road
  119076 Singapore
  chongct@math.nus.edu.sg

- Prof. Dr. Liang Yu
  Nanjing University
  Institute of Mathematical Science
  210093 Nanjing
  People's Republic of China
  yuliang.nju@gmail.com

- ISBN 978-3-11-027555-1
- e-ISBN (PDF) 978-3-11-027564-3
- e-ISBN (EPUB) 978-3-11-038129-0
- Set-ISBN 978-3-11-027565-0
- ISSN 1438-1893

### Library of Congress Cataloging-in-Publication Data

A CIP catalog record for this book has been applied for at the Library of Congress.

### Bibliographic information published by the Deutsche Nationalbibliothek

The Deutsche Nationalbibliothek lists this publication in the Deutsche Nationalbibliografie; detailed bibliographic data are available on the Internet at http://dnb.dnb.de.

© 2015 Walter de Gruyter GmbH, Berlin/Boston
Typesetting: FIT Berlin, Prota TX-Produktion GmbH
Printing and binding: CPI books GmbH, Leck
Printed on acid-free paper
Printed in Germany
www.degruyter.com

Chi Tat Chong dedicates this book to the memory of his parents;

Liang Yu dedicates it to Li Zhang.

## Preface

> ... logic is about definability.
> - Gerald E. Sacks [124]

The above quote underlines the authors’ view that recursion theory is anchored on the notion of definability. Although classically the theory began with Turing’s conception of effective computability (of various types of objects), it soon took on a much broader perspective. A fundamental theorem states that a set of natural numbers is computable if and only if it is \(\Delta^1_1\)-definable in first order arithmetic. This sets the stage for a general study of sets of natural numbers and their syntactic classes.

The view on definability does not conflict with the fact that computation is the heart of recursion theory. Indeed a definability problem naturally translates into one about (possibly relativized) computation and vice versa. Kleene’s characterization of the \(\Delta^1_1\)-sets of numbers as precisely those that are hyperarithmetic, and the corresponding theorem of Spector and Gandy that these are all the reals in \(L_{\omega_1^{CK}}\), is a case in point. Once the syntax (the language of first and second order arithmetic) and the structure in which to interpret members of \(\omega\) and its subsets are specified, definability naturally takes its place. Tools and construction techniques have been introduced to study problems concerning computability for syntactic classes over \(\omega\), \(2^\omega\) and even the power set of \(2^\omega\) or \(\omega^\omega\). Post’s problem for the recursively enumerable sets, the Gandy basis theorem for \(\Sigma^1_1\)-sets of reals, characterization of \(\Delta^1_1\)-sets in terms of hyperarithmetic, the definability of the jump operator, are immediate examples. Indeed it is hard to find a problem in the area that has little to do with definability. The title of this book is chosen to reflect this point.

The idea of writing a book in recursion theory, focusing on the computational aspects of the set of reals and its subsets, evolved over a period of time. The subject was established by Kleene who introduced the notion of hyperarithmetic hierarchy relative to a real and its associated ordinals. It grew in the hands of Spector, Gandy, Kreisel and Sacks. These were major developments in what one now calls higher recursion theory. The theory was a subject of intensive study for almost thirty years beginning in the 1950s, but seemed to lose momentum in the 1980s. In an interview reproduced in the Appendix, Sacks remarked: “I tended over the years to keep predicting the immediate end of recursion theory, but I have been wrong every time.” Despite the rather pessimistic pronouncement by one of the founders of the field, recursion theory is alive and well. However, higher recursion theory in the grand tradition of the pioneers received only occasional attention since, even though a number of highly significant contributions to the subject, such as Slaman and Woodin’s theorem on the rigidity of the hyperdegrees, were made towards the end of the last century, and many interesting as well as challenging problems remain. Indeed Sacks himself bade farewell to higher recursion theory in 1998. Today the subject is not pursued with as much vigor or zeal as it deserves. We view this as rather unfortunate since in it one sees a beautiful illustration of the unity of mathematical logic, where ideas and tools from set theory and model theory are fruitfully applied to study problems about computability. It was a tempting proposition to write another book (following Sacks's *Higher Recursion Theory* [123]) to exhibit this interplay. Recent advances in the study of the global theory of Turing and hyperdegrees, and the emergence of higher randomness as a subject of investigation, provided the impetus for us to turn the idea into reality. It is hoped that the reader would agree, at the end of it, that the enterprise of generalizing recursion theory that began more than half a century ago has been mathematically rewarding, and that the subject is both attractive and highly challenging, with many deep and elegant theorems.

This book consists of four main parts. The first six chapters constitute Part I and develop the fundamental theory of $\Pi^1_1$-sets and fine structure theory of the constructible universe, the ramified analytical hierarchy, and set theory. They lay the groundwork for the rest of the book. Part II focuses on the structure of Turing degrees. Here we discuss classification of the jump operator in relation to Martin's conjecture and the construction of $\Pi^1_1$-sets, as well as degree-theoretic independence results. We turn our attention to hyperdegrees in Part III. In particular, we prove the rigidity of the structure of the hyperdegrees and its biinterpretability with second order arithmetic. We also include a chapter on basis/antibasis theorems as well as perfect subsets in $L$. Part IV is devoted to the study of higher randomness, a subject which is naturally linked to the topics covered in the first three parts. Exercises are sprinkled throughout the chapters. Many of them are intended to supplement the topics covered. The most challenging ones are labelled with a *.

The book ends with an interview with Gerald Sacks (in Appendix B) conducted in 2009. We think that it is fitting to conclude the book with a tribute to one whose work has arguably substantially shaped the development of recursion theory, both classical and higher, in the last century.

A word about prerequisites: While this book attempts to cover as much background material as possible, it is not intended to be encyclopedic. The reader is assumed to be familiar with basic logic and set theory, including classical recursion theory, basic set theory (including forcing) and algorithmic randomness. A number of the results are used in proofs, sometimes without explicit mention. In line with our preference and taste, some of the proofs of theorems in set theory presented are discernibly recursion-theoretic in flavor. These proofs are not necessarily the simplest. Our aim is to offer the reader a different perspective to these theorems by highlighting the effective content that is not immediately apparent. Hopefully these provide additional insights to the ideas that went behind the proofs.

The materials in the first two chapters closely follow Sacks's *Higher Recursion Theory* [123]. Mansfield and Weitkamp's monograph *Recursive Aspects of Descriptive Set Theory* [88] was also one of our key references. Of course one should not fail to mention Hartley Rogers's classic *Theory of Recursive Functions and Effective Computability*

