
# COMBINATORIAL
# MAPS

Efficient Data Structures for
Computer Graphics and Image Processing

![](img/6ba3cf72cbe3568e76a174448323bb33_0_0.png)

![](img/6ba3cf72cbe3568e76a174448323bb33_0_1.png)

Guillaume Damiand

Pascal Lienhardt

CRC Press
Taylor & Francis Group

# COMBINATORIAL
# MAPS

Efficient Data Structures for
Computer Graphics and Image Processing

This page intentionally left blank

# COMBINATORIAL MAPS

Efficient Data Structures for
Computer Graphics and Image Processing

Guillaume Damiand
Pascal Lienhardt

CRC Press
Taylor & Francis Group
6000 Broken Sound Parkway NW, Suite 300
Boca Raton, FL 33487-2742

© 2015 by Taylor & Francis Group, LLC
CRC Press is an imprint of Taylor & Francis Group, an Informa business

No claim to original U.S. Government works
Version Date: 20140724

International Standard Book Number-13: 978-1-4822-0653-1 (eBook - PDF)

This book contains information obtained from authentic and highly regarded sources. Reasonable efforts have been made to publish reliable data and information, but the author and publisher cannot assume responsibility for the validity of all materials or the consequences of their use. The authors and publishers have attempted to trace the copyright holders of all material reproduced in this publication and apologize to copyright holders if permission to publish in this form has not been obtained. If any copyright material has not been acknowledged please write and let us know so we may rectify in any future reprint.

Except as permitted under U.S. Copyright Law, no part of this book may be reprinted, reproduced, transmitted, or utilized in any form by any electronic, mechanical, or other means, now known or hereafter invented, including photocopying, microfilming, and recording, or in any information storage or retrieval system, without written permission from the publishers.

For permission to photocopy or use material electronically from this work, please access www.copyright.com (http://www.copyright.com/) or contact the Copyright Clearance Center, Inc. (CCC), 222 Rosewood Drive, Danvers, MA 01923, 978-750-8400. CCC is a not-for-profit organization that provides licenses and registration for a variety of users. For organizations that have been granted a photocopy license by the CCC, a separate system of payment has been arranged.

**Trademark Notice:** Product or corporate names may be trademarks or registered trademarks, and are used only for identification and explanation without intent to infringe.

**Visit the Taylor & Francis Web site at**
**http://www.taylorandfrancis.com**

**and the CRC Press Web site at**
**http://www.crcpress.com**

to Jean Françon and Yves Bertrand

This page intentionally left blank

## Contents

+ Acknowledgements xi
+ List of Algorithms xiii
+ List of Figures xvii
+ 1 Introduction 1
+ 1.1 Subdivisions of Geometric Objects 1
+ 1.1.1 Subdivided Objects 1
+ 1.1.2 Different Subdivisions 4
+ 1.2 Explicit Representations of Subdivisions 5
+ 1.2.1 Why Explicit Representations? 5
+ 1.2.2 Some Interests of Explicit Representations 6
+ 1.3 Numerous Structures 7
+ 1.3.1 Why Numerous Structures? 9
+ 1.3.2 Some Interests of Many Structures 11
+ 1.4 Cellular Structures 11
+ 1.4.1 Some Historical Milestones 13
+ 1.4.2 Outline 14
+ 2 Preliminary Notions 17
+ 2.1 Basic Topological Notions 17
+ 2.1.1 Basic Elements 17
+ 2.1.2 Continuous Map, Homeomorphism 19
+ 2.2 Paper Surfaces 22
+ 2.2.1 Basic Elements 22
+ 2.2.2 Basic Construction Operation: Identification of Edges 23
+ 2.3 Classification of Paper Surfaces 28
+ 2.3.1 Topological Surfaces 28
+ 2.3.2 Constructing any Subdivision of Any Surface 34
+ 2.4 Manifolds, Quasi-manifolds, Pseudo-manifolds, Complexes 36
+ 2.5 Discrete Structures 42
+ 2.5.1 Discrete Mappings 43
+ 2.5.2 Hypermaps, Group of Permutations, Orbits 47
+ 2.5.3 Partial Functions, Partial Permutations, Partial Involutions and Related Notions 48
+ 2.6 Incidence Graphs 50

## 3 Intuitive Presentation 53

+ 3.1 *n*-maps 53
+ 3.1.1 Objects without Boundary 53
+ 3.1.2 Objects with Boundary 62
+ 3.1.3 Generalization in Any Dimension 68
+ 3.2 *n*-Gmaps 69
+ 3.2.1 Objects without Boundary 70
+ 3.2.2 Objects with Boundary 76
+ 3.2.3 Generalization in Any Dimension 79

## 4 *n*-Gmaps 83

+ 4.1 Basic Definitions 83
+ 4.2 Basic Operations 87
+ 4.2.1 Basic Tools 88
+ 4.2.2 Sew Operations 90
+ 4.2.3 Unsew Operations 96
+ 4.3 Completeness, Multi-Incidence 97
+ 4.3.1 Construction by Increasing Dimensions 97
+ 4.3.2 Construction Directly in a Given Dimension 100
+ 4.3.3 Completeness 104
+ 4.3.4 Multi-Incidence 105
+ 4.4 Data Structures, Iterators and Algorithms 108
+ 4.4.1 Data Structures 108
+ 4.4.2 Iterators 111
+ 4.4.3 Basic Tools 115
+ 4.4.4 Sew/Unsew Operations 119
+ 4.5 Complements 123
+ 4.5.1 Boundary Map 123
+ 4.5.2 Duality 125
+ 4.5.3 Orientability 127
+ 4.5.4 Classification of 2-Gmaps 130

## 5 *n*-maps 133

+ 5.1 Basic Definitions 133
+ 5.2 Basic Operations 138
+ 5.2.1 Basic Tools 139
+ 5.2.2 Sew Operations 141
+ 5.2.3 Unsew Operations 146
+ 5.3 Completeness, Multi-Incidence 147
+ 5.3.1 Construction by Increasing Dimensions 148
+ 5.3.2 Construction Directly in a Given Dimension 151
+ 5.3.3 Completeness 153
+ 5.3.4 Multi-Incidence 154
+ 5.4 Data Structures, Iterators and Algorithms 158
+ 5.4.1 Data Structures 158
+ 5.4.2 Iterators 161
+ 5.4.3 Basic Tools 165
+ 5.4.4 Sew/Unsew Operations 171
+ 5.5 Complements 174
+ 5.5.1 Boundary Map 175
+ 5.5.2 Links between *n*-maps and *n*-Gmaps 178
+ 5.5.3 Classification of 2-maps 181
+ 5.5.4 Duality 182

## Contents

+ 5.4.2 Iterators 161
+ 5.4.3 Basic Tools 165
+ 5.4.4 Sew/Unsew Operations 171
+ 5.5 Complements 174
+ 5.5.1 Boundary Map 175
+ 5.5.2 Links between *n*-maps and *n*-Gmaps 178
+ 5.5.3 Classification of 2-maps 181
+ 5.5.4 Duality 182

## 6 Operations 185

+ 6.1 Closure 185
+ 6.1.1 For *n*-Gmaps 186
+ 6.1.2 For *n*-maps 192
+ 6.2 Removal 198
+ 6.2.1 For *n*-Gmaps 199
+ 6.2.2 For *n*-maps 205
+ 6.3 Contraction 214
+ 6.3.1 For *n*-Gmaps 214
+ 6.3.2 For *n*-maps 219
+ 6.4 Insertion 224
+ 6.5 Expansion 230
+ 6.6 Chamfering 233
+ 6.7 Extrusion 240
+ 6.8 Triangulation 245

## 7 Embedding for Geometric Modeling and Image Processing 251

+ 7.1 Embedding 251
+ 7.2 Geometric Modeling 255
+ 7.2.1 Embedding of *n*-Gmaps in ℝᵈ 255
+ 7.2.2 Geometric Operations 258
+ 7.2.3 Example of Modeling of an Object 263
+ 7.3 Image Processing 272
+ 7.3.1 Preliminary Notions 272
+ 7.3.2 2D Topological Map 273
+ 7.3.3 Operations 277

## 8 Cellular Structures as Structured Simplicial Structures 295

+ 8.1 Simplicial Structures 297
+ 8.1.1 Abstract Simplicial Complexes 297
+ 8.1.2 Semi-Simplicial Sets 302
+ 8.1.3 Conversions of Simplicial Structures 307
+ 8.2 Numbered Simplicial Structures and Cellular Structures 308
+ 8.2.1 Numbered Simplicial Structures 308
+ 8.2.2 Simplicial Interpretation of *n*-Gmaps 313
+ 8.2.3 Simplicial Interpretation of Incidence Graphs 320
