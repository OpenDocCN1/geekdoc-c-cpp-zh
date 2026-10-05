
## C# GAME PROGRAMMING COOKBOOK for UNITY 3D
Jeff W. Murray

![](img/041dca164b58875f4f1a64abb3328f5c_0_0.png)

CRC Press
Taylor & Francis Group
AN A.K PETERS BOOK

# C# GAME PROGRAMMING COOKBOOK for

BARNFIELD COLLEGE LRC LIBRARY
New Bedford Road, Luton LU2 7BF
Tel: 01582 569588
Please return on or before the last date stamped below.

![](img/041dca164b58875f4f1a64abb3328f5c_2_0.png)

## C# GAME PROGRAMMING COOKBOOK for UNITY 3D
Jeff W. Murray

CRC Press
Taylor & Francis Group
Boca Raton London New York
CRC Press is an imprint of the
Taylor & Francis Group, an Informa business
AN K. PETERS BOOK

## C# GAME PROGRAMMING COOKBOOK for UNITY 3D
Jeff W. Murray

![](img/041dca164b58875f4f1a64abb3328f5c_6_0.png)

CRC Press
Taylor & Francis Group
Boca Raton London New York
CRC Press is an imprint of the
Taylor & Francis Group, an Informa business
AN K. PETERS BOOK

# MIX Paper from responsible sources
FSC
FSC® C014174
www.fsc.org

# EAST HERTS COLLEGE

CRC & Francis Group
Taylor & Broken Sound Parkway NW, Suite 300
Boca Raton, FL 33487-2742

© 2014 by Taylor & Francis Group, LLC
CRC Press is an imprint of Taylor & Francis Group, an Informa business

No claim to original U.S. government works

Printed on acid-free paper
Date: 201400213

Standard Book Number: 978-1-4665-8140-1 (Paperback)

This book contains information obtained from authentic and highly regarded sources. Reasonable efforts have been made to publish reliable data and information, but the author and publisher cannot assume responsibility for the validity of all materials or the consequences of them. The authors and publisher have attempted to trace the copyright holders of all material referenced in this publication and apologize to copyright holders if permission to publish in this form has not been obtained. If any error is found, the publisher would appreciate being notified.

Except permitted under U.S. Copyright Law, no part of this book may be reprinted, reproduced, transmitted, or utilized in any form electronic, mechanical, or other means, without prior written approval invented, including photocopying, microfilming, and recording, or in any form of storage or retrieval system, without written permission from the publisher.

For permission to use material electronically from this work, please access (http://www.copyright.com/) or contact the Copyright Clearance Center, Inc. (CCC), 222 Rosemary Drive, Davenport, MA 01923, 978-750-8400. CCC is a for-profit organization that provides licenses and registration for a variety of users. For organizations who have been granted a license by the CCC, a separate system of payment has been arranged.

Trademark: Product or corporate names may be trademarks or registered trademarks, and are used only for identification and without intent to infringe.

# Library of Cataloging-in Publication Data

Murray, Jeff
C# game programming handbook for 3D Unity / Jeff J.W. Murray.

- + pages
Includes indexes.
ISBN 978-1-4665-8140-1 (paperback)
1. Computer games programming. 2. C# (Computer program language) 3. Unity (Electronic resource) 4. Three-dimensional display systems. 1. Title.

QA76.C67*M868 2014
794.8/1526—c23

2013048921

Visit the Taylor & Francis Web site at
http://www.taylorfrancis.com
and the CRC Press Web site at
http://www.crcpress.com

> This book is dedicated to my boys,
Ethan and William.
Be nice to the cat.

## Contents

- Acknowledgments ................................................................................ xiii
- Introduction .................................................................................................... xv
- 1. Making Games the Modular Way ................................................................ I
    - 1.1 Important Programming Concepts ........................................................ 2
        - 1.1.1 Manager and Controller Scripts ........................................................ 2
        - 1.1.2 Script Communication ....................................................................... 3
        - 1.1.3 Using the Singleton Pattern in Unity ................................................ 5
        - 1.1.4 Inheritance ................................................................................... 6
        - 1.1.5 Where to Now? ................................................................................ 8
- 2. Building the Core Game Framework ............................................................ 9
    - 2.1 Controllers and Managers ....................................................................... 11
        - 2.1.1 Controllers ................................................................................... 11
        - 2.1.2 Managers ...................................................................................... 11
    - 2.2 Building the Core Framework Scripts ................................................... 11
        - 2.2.1 BaseGameController.cs ................................................................ 12
            - 2.2.1.1 Script Breakdown ................................................................ 14
            - 2.2.2 Scene Manager Script Breakdown ................................................................... 17
            - 2.2.2.1 ExtendedCustomMonoBehavior.cs ........................................................ 17
        - 2.2.3 ExtendedUserManager.cs ................................................................ 19
        - 2.2.4 BaseUserManager.cs ....................................................... 20
            - 2.2.4.1 Script Breakdown ................................................................ 22
            - 2.2.4.2 BasePlayerManager.cs ................................................................ 22
        - 2.2.5 Script Breakdown ................................................... 23
            - 2.2.5.1 Script Breakdown ................................................................ 23
        - 2.2.6 BaseInputController.cs ................................................... 24
            - 2.2.6.1 Script Breakdown ................................................................ 24

## 3. Player Structure 29
- 3.1 Game-Specific Player Controller ........................................ 31
- 3.2 Dealing with Input ................................................................ 32
- 3.3 Player Manager ................................................................... 35
    - 3.3.1 Script Breakdown ................................................................ 36
- 3.4 User Data Manager (Dealing with Player Stats Such as Health, Lives, etc.) 37
    - 3.4.1 Script Breakdown ................................................................ 39

## 4. Recipes: Common Components 41
- 4.1 Introduction ................................................................... 41
- 4.2 The Timer Class ................................................................ 43
    - 4.2.1 Script Breakdown ........................................................ 45
- 4.3 Spawns ...................................................................... 48
    - 4.3.1 A Simple Spawn Controller ........................................ 49
        - 4.3.1.1 Script Breakdown ................................................ 52
    - 4.3.2 Trigger Spawner ...................................................... 56
    - 4.3.3 Path Spawner ........................................................ 57
        - 4.3.3.1 Script Breakdown ................................................ 61
- 4.4 Set Gravity ........................................................ 66
    Pretend Friction-Friction Simulation to Prevent Slipping Around 66
- 4.5.1 Script Breakdown ................................................... 68
- 4.6 Cameras ................................................................... 68
    - 4.6.1 Third-Person Camera ........................................ 69
        - 4.6.1.1 Script Breakdown ...................................... 71
    - 4.6.2 Top-Down Camera ......................................... 74
        - 4.6.2.1 Script Breakdown ................................ 74
- 4.7 Input Scripts ........................................ 75
    - 4.7.1 Mouse Input ........................................ 75
        - 4.7.1.1 Script Breakdown ...................... 76
    - 4.7.2 Single Axis Keyboard Input ................... 78
- 4.8 Automatic Self-Destruction Script ................... 79
    - 4.8.1 Script Breakdown ................................... 79
- 4.9 Automatic Object Spinner ................... 79
    - 4.9.1 Script Breakdown ........................ 80
