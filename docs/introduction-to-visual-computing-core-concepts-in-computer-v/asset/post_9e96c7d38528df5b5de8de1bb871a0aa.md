
## Introduction to VISUAL COMPUTING

Core Concepts in Computer Vision, Graphics, and Image Processing

Aditi Majumder
University of California, Irvine, USA

M. Gopi
University of California, Irvine, USA

CPD CERTIFIED
The CPD Certification Service

CRC Press
Taylor & Francis Group
A CHAPMAN & HALL BOOK

CRC Press
Taylor & Francis Group
6000 Broken Sound Parkway NW, Suite 300
Boca Raton, FL 33487-2742

© 2018 by Taylor & Francis Group, LLC
CRC Press is an imprint of Taylor & Francis Group, an Informa business

No claim to original U.S. Government works

Printed on acid-free paper
Version Date: 20180112

International Standard Book Number-13: 978-1-4822-4491-5 (Hardback)

This book contains information obtained from authentic and highly regarded sources. Reasonable efforts have been made to publish reliable data and information, but the author and publisher cannot assume responsibility for the validity of all materials or the consequences of their use. The authors and publishers have attempted to trace the copyright holders of all material reproduced in this publication and apologize to copyright holders if permission to publish in this form has not been obtained. If any copyright material has not been acknowledged please write and let us know so we may rectify in any future reprint.

Except as permitted under U.S. Copyright Law, no part of this book may be reprinted, reproduced, transmitted, or utilized in any form by any electronic, mechanical, or other means, now known or hereafter invented, including photocopying, microfilming, and recording, or in any information storage or retrieval system, without written permission from the publishers.

For permission to photocopy or use material electronically from this work, please access www.copyright.com (http://www.copyright.com/) or contact the Copyright Clearance Center, Inc. (CCC), 222 Rosewood Drive, Danvers, MA 01923, 978-750-8400. CCC is a not-for-profit organization that provides licenses and registration for a variety of users. For organizations that have been granted a photocopy license by the CCC, a separate system of payment has been arranged.

Trademark Notice: Product or corporate names may be trademarks or registered trademarks, and are used only for identification and explanation without intent to infringe.

Visit the Taylor & Francis Web site at
http://www.taylorandfrancis.com

and the CRC Press Web site at
http://www.crcpress.com

## Contents

- Preface ........................................................ xi
- I Fundamentals .................................................. 1
  - 1 Data ............................................................ 3
    - 1.1 Visualization ............................................. 4
    - 1.2 Discretization ............................................ 4
      - 1.2.1 Sampling ............................................ 5
      - 1.2.2 Quantization ........................................ 7
    - 1.3 Representation ............................................ 8
      - 1.3.1 Geometric Data ...................................... 11
    - 1.4 Noise ..................................................... 15
    - 1.5 Conclusion ................................................ 16
    - Bibliography ................................................... 17
    - Summary ......................................................... 18
    - Exercises ....................................................... 19
  - 2 Techniques ...................................................... 21
    - 2.1 Interpolation ............................................. 21
      - 2.1.1 Linear Interpolation ................................ 22
      - 2.1.2 Bilinear Interpolation .............................. 23
    - 2.2 Geometric Intersections ................................... 26
    - 2.3 Conclusion ................................................ 29
    - Bibliography ................................................... 29
    - Summary ......................................................... 30
    - Exercises ....................................................... 31
- II Image Based Visual Computing .................................. 33
  - 3 Convolution ..................................................... 35
    - 3.1 Linear Systems ................................................ 35
      - 3.1.1 Response of a Linear System ........................... 36
      - 3.1.2 Properties of Convolution ............................. 40
    - 3.2 Linear Filters .............................................. 41
      - 3.2.1 All, Low, Band and High Pass Filters .................. 43
      - 3.2.2 Designing New Filters ................................... 51
      - 3.2.3 2D Filter Separability .................................. 54
      - 3.2.4 Correlation and Pattern Matching ...................... 56
    - 3.3 Implementation Details .................................... 60
    - 3.4 Conclusion ................................................. 61
    - Bibliography ................................................... 62
    - Summary ........................................................ 63
    - Exercises ...................................................... 64
  - 4 Spectral Analysis ............................................ 67
    - 4.1 Discrete Fourier Transform ............................... 67
      - 4.1.1 Why Sine and Cosine Waves? ............................ 73
    - 4.2 Polar Notation ............................................. 74
      - 4.2.1 Properties .............................................. 76
      - 4.2.2 Example Analysis of Signals ........................... 77
    - 4.3 Periodicity of Frequency Domain .......................... 80
    - 4.4 Aliasing ................................................... 81
    - 4.5 Extension for 2D Interpretation .......................... 83
      - 4.5.1 Effect of Periodicity .................................. 85
      - 4.5.2 Notch Filter ............................................ 85
      - 4.5.3 Example of Aliasing .................................... 87
    - 4.6 Duality .................................................... 89
    - 4.7 Conclusion ................................................. 92
    - Bibliography ................................................... 93
    - Summary ........................................................ 94
    - Exercises ...................................................... 95
  - 5 Feature Detection ............................................ 99
    - 5.1 Edge Detection ............................................. 100
      - 5.1.1 Edgel Detectors ......................................... 100
      - 5.1.2 Multi-Resolution Edge Detection ....................... 111
      - 5.1.3 Aggregating Edgels ..................................... 113
    - 5.2 Feature Detection ......................................... 116
    - 5.3 Other Non-Linear Filters .................................. 118
    - 5.4 Conclusion ................................................. 120
    - Bibliography ................................................... 120
    - Summary ........................................................ 121
    - Exercises ...................................................... 122
- III Geometric Visual Computing  125
  - 6 Geometric Transformations  127
    - 6.1 Homogeneous Coordinates  127
    - 6.2 Linear Transformations  129
    - 6.3 Euclidean and Affine Transformations  131
      - 6.3.1 Translation  131
      - 6.3.2 Rotation  132
      - 6.3.3 Scaling  134
      - 6.3.4 Shear  135
      - 6.3.5 Some Observations  136
    - 6.4 Concatenation of Transformations  136
      - 6.4.1 Scaling About the Center  137
      - 6.4.2 Rotation About an Arbitrary Axis  138
    - 6.5 Coordinate Systems  141
      - 6.5.1 Change of Coordinate Systems  142
    - 6.6 Properties of Concatenation  145
      - 6.6.1 Global vs Local Coordinate System  146
    - 6.7 Projective Transformation  146
    - 6.8 Degrees of Freedom  148
    - 6.9 Non-Linear Transformations  149
    - 6.10 Conclusion  151
    - Bibliography  151
    - Summary  152
    - Exercises  153
  - 7 The Pinhole Camera  157
    - 7.1 The Model  157
      - 7.1.1 Camera Calibration  161
      - 7.1.2 3D Depth Estimation  163
      - 7.1.3 Homography  164
    - 7.2 Considerations in the Practical Camera  168
    - 7.3 Conclusion  172
    - Bibliography  172
    - Summary  173
    - Exercises  174
  - 8 Epipolar Geometry  177
    - 8.1 Background  177
    - 8.2 Correspondences in Multi-View Geometry  179
    - 8.3 Fundamental Matrix  182
      - 8.3.1 Properties  183
      - 8.3.2 Estimating Fundamental Matrix  184
