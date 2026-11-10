
## Computational Intelligence Paradigms
### Theory and Applications Using MATLAB®

S. Sumathi  
Surekha P.

## Computational Intelligence in Database Management

James R.  
Jonathan  
Guy M. Lohman

## Computational Intelligence Paradigms
### Theory and Applications Using MATLAB®

![](img/d9a4cc12c48f7466f309cbd3c4549c73_6_0.png)

S. Sumathi  
Surekha P.

CRC Press  
Taylor & Francis Group  
Boca Raton London New York

CRC Press is an imprint of Taylor & Francis Group, an informa business  
A CHAPMAN & HALL BOOK

MATLAB® and Simulink® are trademarks of The MathWorks, Inc. and are used with permission. The MathWorks does not warrant the accuracy of the text or exercises in this book. This book's use or discussion of MATLAB® and Simulink® software or related products does not constitute endorsement or sponsorship by The MathWorks of a particular pedagogical approach or particular use of the MATLAB® and Simulink® software.

CRC Press  
Taylor & Francis Group  
6000 Broken Sound Parkway NW, Suite 300  
Boca Raton, FL 33487-2742  
© 2010 by Taylor and Francis Group, LLC  
CRC Press is an imprint of Taylor & Francis Group, an Informa business

No claim to original U.S. Government works

Printed in the United States of America on acid-free paper  
10 9 8 7 6 5 4 3 2 1

International Standard Book Number: 978-1-4398-0902-0 (Hardback)

This book contains information obtained from authentic and highly regarded sources. Reasonable efforts have been made to publish reliable data and information, but the author and publisher cannot assume responsibility for the validity of all materials or the consequences of their use. The authors and publishers have attempted to trace the copyright holders of all material reproduced in this publication and apologize to copyright holders if permission to publish in this form has not been obtained. If any copyright material has not been acknowledged please write and let us know so we may rectify in any future reprint.

Except as permitted under U.S. Copyright Law, no part of this book may be reprinted, reproduced, transmitted, or utilized in any form by any electronic, mechanical, or other means, now known or hereafter invented, including photocopying, microfilming, and recording, or in any information storage or retrieval system, without written permission from the publishers.

For permission to photocopy or use material electronically from this work, please access www.copyright.com (http://www.copyright.com/) or contact the Copyright Clearance Center, Inc. (CCC), 222 Rosewood Drive, Danvers, MA 01923, 978-750-8400. CCC is a not-for-profit organization that provides licenses and registration for a variety of users. For organizations that have been granted a photocopy license by the CCC, a separate system of payment has been arranged.

Trademark Notice: Product or corporate names may be trademarks or registered trademarks, and are used only for identification and explanation without intent to infringe.

| Library of Congress Cataloging-in-Publication Data |
|---|
| Sumathi, S., 1968- |
| Computational intelligence paradigms : theory & applications using MATLAB / S. Sumathi and Surekha Paneerselvam. |
| p. cm. |
| Includes bibliographical references and index. |
| ISBN 978-1-4398-0902-0 (hardback : alk. paper) |
| 1. Computational intelligence. 2. MATLAB. I. Paneerselvam, Surekha, 1980- II. Title. |
| QA342 .S94 2010 |
| 006.3--dc22 |
| 2009022113 |

Visit the Taylor & Francis Web site at  
http://www.taylorandfrancis.com  
and the CRC Press Web site at  
http://www.crcpress.com

## Contents

- Preface ... xvii
- 1 Computational Intelligence ... 1
    - 1.1 Introduction ... 1
    - 1.2 Primary Classes of Problems for CI Techniques ... 5
        - 1.2.1 Optimization ... 5
        - 1.2.2 NP-Complete Problems ... 6
    - 1.3 Neural Networks ... 7
        - 1.3.1 Feed Forward Neural Networks ... 8
    - 1.4 Fuzzy Systems ... 9
        - 1.4.1 Fuzzy Sets ... 9
        - 1.4.2 Fuzzy Controllers ... 11
    - 1.5 Evolutionary Computing ... 12
        - 1.5.1 Genetic Algorithms ... 13
        - 1.5.2 Genetic Programming ... 14
        - 1.5.3 Evolutionary Programming ... 15
        - 1.5.4 Evolutionary Strategies ... 15
    - 1.6 Swarm Intelligence ... 16
    - 1.7 Other Paradigms ... 17
        - 1.7.1 Granular Computing ... 18
        - 1.7.2 Chaos Theory ... 20
        - 1.7.3 Artificial Immune Systems ... 21
    - 1.8 Hybrid Approaches ... 22
    - 1.9 Relationship with Other Paradigms ... 23
    - 1.10 Challenges To Computational Intelligence ... 25
    - Summary ... 26
    - Review Questions ... 27
- 2.3.3 Implementation of Artificial Neuron Electronically ... 35
- 2.3.4 Operations of Artificial Neural Network ... 37
- 2.3.5 Training an Artificial Neural Network ... 40
- 2.3.6 Comparison between Neural Networks, Traditional Computing, and Expert Systems ... 44
- 2.4 Neural Network Components ... 46
    - 2.4.1 Teaching an Artificial Neural Network ... 52
    - 2.4.2 Learning Rates ... 54
    - 2.4.3 Learning Laws ... 55
    - 2.4.4 MATLAB Implementation of Learning Rules ... 61
- Summary ... 67
- Review Questions ... 67
- 3 Artificial Neural Networks - Architectures and Algorithms ... 69
    - 3.1 Introduction ... 69
    - 3.2 Layered Architectures ... 71
        - 3.2.1 Single-Layer Networks ... 71
        - 3.2.2 Multilayer Networks ... 73
    - 3.3 Prediction Networks ... 75
        - 3.3.1 The Perceptron ... 75
        - 3.3.2 MATLAB Implementation of a Perceptron Network ... 79
        - 3.3.3 Feedforward Back-Propagation Network ... 83
        - 3.3.4 Implementation of BPN Using MATLAB ... 91
        - 3.3.5 Delta Bar Delta Network ... 95
        - 3.3.6 Extended Delta Bar Delta ... 97
        - 3.3.7 Directed Random Search Network ... 100
        - 3.3.8 Functional Link Artificial Neural Network (FLANN) or Higher-Order Neural Network ... 102
    - Summary ... 106
    - Review Questions ... 106
- 4 Classification and Association Neural Networks ... 109
    - 4.1 Introduction ... 109
    - 4.2 Neural Networks Based on Classification ... 109
        - 4.2.1 Learning Vector Quantization ... 110
        - 4.2.2 Implementation of LVQ in MATLAB ... 115
        - 4.2.3 Counter-Propagation Network ... 116
        - 4.2.4 Probabilistic Neural Network ... 123
        - 4.2.5 Implementation of the Probabilistic Neural Net Using MATLAB ... 128
    - 4.3 Data Association Networks ... 129
        - 4.3.1 Hopfield Network ... 130
        - 4.3.2 Implementation of Hopfield Network in MATLAB ... 133
        - 4.3.3 Boltzmann Machine ... 134
        - 4.3.4 Hamming Network ... 137
        - 4.3.5 Bi-Directional Associative Memory ... 141
    - 4.4 Data Conceptualization Networks ... 146
        - 4.4.1 Adaptive Resonance Network ... 146
        - 4.4.2 Implementation of ART Algorithm in MATLAB ... 151
        - 4.4.3 Self-Organizing Map ... 153
    - 4.5 Applications Areas of ANN ... 158
        - 4.5.1 Language Processing ... 159
        - 4.5.2 Character Recognition ... 160
        - 4.5.3 Data Compression ... 160
        - 4.5.4 Pattern Recognition ... 160
        - 4.5.5 Signal Processing ... 161
        - 4.5.6 Financial ... 161
    - Summary ... 162
    - Review Questions ... 162
- 5 MATLAB Programs to Implement Neural Networks ... 165
    - 5.1 Illustration 1: Coin Detection Using Euclidean Distance (Hamming Net) ... 165
    - 5.2 Illustration 2: Learning Vector Quantization - Clustering Data Drawn from Different Regions ... 171
    - 5.3 Illustration 3: Character Recognition Using Kohonen SOM Network ... 174
    - 5.4 Illustration 4: The Hopfield Network as an Associative Memory ... 182
    - 5.5 Illustration 5: Generalized Delta Learning Rule and Back-Propagation of Errors for a Multilayer Network ... 187
    - 5.6 Illustration 6: Classification of Heart Disease Using Learning Vector Quantization ... 189
    - 5.7 Illustration 7: Neural Network Using MATLAB Simulink ... 198
    - Summary ... 200
    - Review Questions ... 200
- 6 MATLAB-Based Fuzzy Systems ... 203
    - 6.1 Introduction ... 203
    - 6.2 Imprecision and Uncertainty ... 205
    - 6.3 Crisp and Fuzzy Logic ... 205
    - 6.4 Fuzzy Sets ... 207
