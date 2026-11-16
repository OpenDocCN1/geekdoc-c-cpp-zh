
## Formalized Probability Theory and Applications Using Theorem Proving

Osman Hasan and Sofiène Tahar

## Formalized Probability Theory and Applications Using Theorem Proving

Osman Hasan
National University of Sciences and Technology, Pakistan

Sofiène Tahar
Concordia University, Canada

![](img/0e284aa46fa831bc38a68343fef110e3_1_0.png)

Managing Director: Lindsay Johnston
Managing Editor: Austin DeMarco
Director of Intellectual Property & Contracts: Jan Travers
Acquisitions Editor: Kayla Wolfe
Production Editor: Christina Henning
Typesetter: Amanda Smith
Cover Design: Jason Mull

Published in the United States of America by
Information Science Reference (an imprint of IGI Global)
701 E. Chocolate Avenue
Hershey PA 17033
Tel: 717-533-8845
Fax: 717-533-8661
E-mail: cust@igi-global.com
Web site: http://www.igi-global.com

Copyright © 2015 by IGI Global. All rights reserved. No part of this publication may be reproduced, stored or distributed in any form or by any means, electronic or mechanical, including photocopying, without written permission from the publisher.
Product or company names used in this set are for identification purposes only. Inclusion of the names of the products or companies does not indicate a claim of ownership by IGI Global of the trademark or registered trademark.

Library of Congress Cataloging-in-Publication Data
Hasan, Osman, 1975-
Formalized probability theory and applications using theorem proving / by Osman Hasan and Sofiène Tahar.
pages cm
Includes bibliographical references and index.
ISBN 978-1-4666-8315-0 (hardcover) — ISBN 978-1-4666-8316-7 (ebook) 1. Computer systems—Evaluation. 2. Automatic theorem proving. 3. Stochastic analysis—Data processing. I. Tahar, Sofiène, 1966- II. Title.
QA76.9.E95H37 2015
004.029—dc23
2015006750

British Cataloguing in Publication Data
A Cataloguing in Publication record for this book is available from the British Library.

All work contributed to this book is new, previously-unpublished material. The views expressed in this book are those of the authors, but not necessarily of the publisher.

## To our Families.

## Table of Contents

Preface .................................................................... viii
Acknowledgment ........................................................ xii

## Chapter 1
Probabilistic Analysis .................................................... 1

### 1.1 MOTIVATION ........................................................ 2
### 1.2 RANDOMIZED MODELS ............................................ 2
### 1.3 PROBABILISTIC PROPERTIES .................................... 3
### 1.4 STATISTICAL PROPERTIES ....................................... 4
### 1.5 TRADITIONAL PROBABILISTIC ANALYSIS METHODS ......... 6
### 1.6 CONCLUSION ........................................................ 8

## Chapter 2
Formal Verification Methods ...................................... 10

### 2.1 INTRODUCTION .................................................... 11
### 2.2 MODEL CHECKING ................................................ 12
### 2.3 THEOREM PROVING ............................................... 14
### 2.4 CONCLUSION ........................................................ 18

## Chapter 3
Probabilistic Analysis Using Theorem Proving ............... 21

### 3.1 METHODOLOGY .................................................... 22
### 3.2 HOL4 THEOREM PROVER ........................................ 25
### 3.3 CONCLUSION ........................................................ 28

## Chapter 4
Measure Theory and Lebesgue Integration Theories ......... 29

### 4.1 FORMALIZATION OF EXTENDED REAL NUMBERS ............ 30
### 4.2 FORMALIZATION OF MEASURE THEORY ........................ 33
### 4.3 FORMALIZATION OF LEBESGUE INTEGRATION IN HOL ....... 41
### 4.4 CONCLUSION ........................................................ 45

## Chapter 5
Probability Theory ........................ 47

### 5.1 FORMALIZATION OF PROBABILITY THEORY ........................ 48
### 5.2 FORMALIZATION OF STATISTICAL PROPERTIES ........................ 50
### 5.3 HEAVY HITTER PROBLEM ........................ 52
### 5.4 FORMALIZATION OF CONDITIONAL PROBABILITIES ........................ 57
### 5.5 CONCLUSION ........................ 62

## Chapter 6
Discrete-Time Markov Chains in HOL ........................ 65

### 6.1 FORMALIZATION OF DISCRETE-TIME MARKOV CHAIN ........................ 66
### 6.2 FORMAL VERIFICATION DTMC PROPERTIES ........................ 69
### 6.3 FORMALIZATION OF STATIONARY DISTRIBUTIONS ........................ 73
### 6.4 FORMALIZATION OF STATIONARY PROCESS ........................ 75
### 6.5 BINARY COMMUNICATION MODEL ........................ 77
### 6.6 AMQM PROTOCOL ........................ 80
### 6.7 CONCLUSION ........................ 85

## Chapter 7
Classified Discrete-Time Markov Chains ........................ 87

### 7.1 FORMALIZATION OF CLASSIFIED STATES ........................ 88
### 7.2 FORMAL VERIFICATION OF CLASSIFIED DTMCs ........................ 90
### 7.3 FORMAL VERIFICATION OF LONG-TERM PROPERTIES ........................ 91
### 7.4 APPLICATIONS ........................ 95
### 7.5 CONCLUSION ........................ 113

## Chapter 8
Formalization of Hidden Markov Model ........................ 116

### 8.1 DEFINITION OF HMM ........................ 117
### 8.2 HMM PROPERTIES ........................ 119
### 8.3 PROOF AUTOMATION ........................ 122
### 8.4 APPLICATION: DNA SEQUENCE ANALYSIS ........................ 123
### 8.5 CONCLUSION ........................ 127

## Chapter 9
Information Measures ........................ 129

### 9.1 FORMALIZATION OF RADON-NIKODYM DERIVATIVE ........................ 130
### 9.2 FORMALIZATION OF KULLBACK-LEIBLER DIVERGENCE ........................ 132
### 9.3 FORMALIZATION OF MUTUAL INFORMATION ........................ 133
### 9.4 ENTROPY ........................ 134
### 9.5 FORMALIZATION OF CONDITIONAL MUTUAL INFORMATION ........................ 135
### 9.6 FORMALIZATION OF QUANTITATIVE ANALYSIS OF INFORMATION ........................ 137
### 9.7 CONCLUSION ........................ 140

## Chapter 10
Formal Analysis of Information Flow Using Min-Entropy and Belief Min-Entropy

### 10.1 INFORMATION FLOW ANALYSIS ........................ 143
### 10.2 FORMALIZATION OF MIN-ENTROPY AND BELIEF MIN-ENTROPY ............ 144
### 10.3 FORMAL ANALYSIS OF INFORMATION FLOW .................... 149
### 10.4 APPLICATION: CHANNELS IN CASCADE ....................... 153
### 10.5 CONCLUSION ........................................... 156

## Chapter 11
Applications of Formalized Information Theory....................... 159

### 11.1 DATA COMPRESSION .................................... 160
### 11.2 ANONYMITY-BASED SINGLE MIX .......................... 167
### 11.3 ONE-TIME PAD ........................................ 171
### 11.4 CONCLUSION .......................................... 176

## Chapter 12
Reliability Theory ....................................... 179

### 12.1 LIFETIME DISTRIBUTIONS .............................. 180
### 12.2 CUMULATIVE DISTRIBUTION FUNCTION .................... 181
### 12.3 SURVIVAL FUNCTION ................................... 183
### 12.4 RELIABILITY BLOCK DIAGRAMS .......................... 185
### 12.5 APPLICATIONS ........................................ 197
### 12.6 CONCLUSION .......................................... 205

## Chapter 13
Scheduling Algorithm for Wireless Sensor Networks .............. 208

### 13.1 COVERAGE-BASED RANDOMIZED SCHEDULING ALGORITHM ...... 209
### 13.2 FORMAL ANALYSIS OF THE K-SET RANDOMIZED SCHEDULING .... 210
### 13.3 FORMAL ANALYSIS OF WSN FOR FOREST FIRE DETECTION .... 218
### 13.4 CONCLUSION .......................................... 225

## Chapter 14
Formal Probabilistic Analysis of Detection Properties in Wireless Sensor Networks .................................................... 228

### 14.1 DETECTION OF A WIRELESS SENSOR NETWORK .............. 228
### 14.2 DETECTION PROPERTIES ................................ 231
### 14.3 WSN FOR BORDER SURVEILLANCE ......................... 247
### 14.4 CONCLUSION .......................................... 256
