
## Linux
### The Textbook

Syed Mansoor Sarwar • Robert M. Koretsky

## Linux

## Linux
### The Textbook, Second Edition

Syed Mansoor Sarwar and Robert M. Koretsky

CRC Press
Taylor & Francis Group
Boca Raton London New York
CRC Press is an imprint of the Taylor & Francis Group, an informa business
A CHAPMAN & HALL BOOK

CRC Press
Taylor & Francis Group
6000 Broken Sound Parkway NW, Suite 300
Boca Raton, FL 33487-2742

© 2019 by Taylor & Francis Group, LLC
CRC Press is an imprint of Taylor & Francis Group, an Informa business

No claim to original U.S. Government works

Printed on acid-free paper
International Standard Book Number-13: 978-1-138-71008-5 (Hardback)

This book contains information obtained from authentic and highly regarded sources. Reasonable efforts have been made to publish reliable data and information, but the author and publisher cannot assume responsibility for the validity of all materials or the consequences of their use. The authors and publishers have attempted to trace the copyright holders of all material reproduced in this publication and apologize to copyright holders if permission to publish in this form has not been obtained. If any copyright material has not been acknowledged please write and let us know so we may rectify in any future reprint.

Except as permitted under U.S. Copyright Law, no part of this book may be reprinted, reproduced, transmitted, or utilized in any form by any electronic, mechanical, or other means, now known or hereafter invented, including photocopying, microfilming, and recording, or in any information storage or retrieval system, without written permission from the publishers.

For permission to photocopy or use material electronically from this work, please access www.copyright.com (http://www.copyright.com/) or contact the Copyright Clearance Center, Inc. (CCC), 222 Rosewood Drive, Danvers, MA 01923, 978-750-8400. CCC is a not-for-profit organization that provides licenses and registration for a variety of users. For organizations that have been granted a photocopy license by the CCC, a separate system of payment has been arranged.

**Trademark Notice:** Product or corporate names may be trademarks or registered trademarks, and are used only for identification and explanation without intent to infringe.

## Library of Congress Cataloging-in-Publication Data

- Names: Sarwar, Syed Mansoor, author. | Koretsky, Robert, author.
- Title: Linux : the textbook / Syed Mansoor Sarwar, Robert M Koretsky.
- Description: Second edition. | Boca Raton : Taylor & Francis, CRC Press, 2018. | Includes index.
- Identifiers: LCCN 2018019196 | ISBN 9781138710085 (hardback : alk. paper)
- Subjects: LCSH: Linux. | Operating systems (Computers)
- Classification: LCC QA76.774.L46 S37 2018 | DDC 005.4/46--dc23
- LC record available at https://lccn.loc.gov/2018019196

Visit the Taylor & Francis Web site at
http://www.taylorandfrancis.com

and the CRC Press Web site at
http://www.crcpress.com

To Abbujee with love

SMS

To my family

RMK

- Preface
- Acknowledgments
- Authors
- 1 Overview of Operating Systems
- 1.1 Introduction
- 1.2 What Is an Operating System?
- 1.3 Operating System Services
- 1.4 Character (Command Line) versus Graphical User Interfaces
- 1.5 Types of Operating Systems
- 1.6 The Linux Distribution Families
- 1.7 The Linux Software Architecture
- 1.7.1 Device Driver Layer
- 1.7.2 Linux Kernel
- 1.7.2.1 Process Management
- 1.7.2.2 File Management
- 1.7.2.3 Main Memory Management
- 1.7.2.4 Disk Management
- 1.7.3 System Call Interface
- 1.7.4 Language Libraries
- 1.7.5 Linux Shell
- 1.7.6 Applications
- 1.8 Historical Development of the Linux Operating System
- 1.8.1 Beginnings
- 1.8.2 The History of Shells
- 1.8.3 Future Developments
- 1.9 A Basic Comparison of Linux System Distributions
- 1.9.1 Linux System Standardization
- Summary
- Questions and Problems
- Advanced Questions and Problems
- 2 “Quick Start” into the Linux Operating System
- 2.1 Introduction
- 2.2 The Structure of a Linux Command
- 2.3 Logging On and Logging Off
- 2.3.1 Stand-Alone Login Connection to Linux
- 2.3.1.1 Graphical Login and Logout Procedures
- 2.3.2 Connecting via PuTTY from a Microsoft Windows Computer
- 2.3.2.1 Login and Logout Procedures
- 2.3.3 Connecting via an SSH Client between Linux Machines
- 2.3.3.1 Login and Logout Procedures
- 2.4 File Maintenance Commands and Help on Linux Command Usage
- 2.4.1 File and Directory Structure
- 2.4.2 Viewing the Contents of Files
- 2.4.3 Creating, Deleting, and Managing Files 27
- 2.4.4 Creating, Deleting, and Managing Directories 30
- 2.4.5 Obtaining Help with the man Command 34
- 2.4.6 Other Methods of Obtaining Help 36
- 2.5 Utility Commands 37
- 2.5.1 Examining System Setups 37
- 2.5.2 Printing and General Utility Commands 38
- 2.5.3 Communication Commands 39
- 2.6 Command Aliases 41
- 2.7 Introduction to Linux Shells 42
- 2.8 Various Linux Shells 44
- 2.8.1 Shell Programs 45
- 2.8.2 Which Shell Suits Your Needs? 46
- 2.8.3 Ways to Change Your Shell 46
- 2.8.4 Shell Start-Up Files and Environment Variables 48
- 2.9 Shell Metacharacters 49
- 2.10 The sudo and su Commands 50
- Summary 50
- Questions and Problems 51
- Advanced Questions and Problems 52
- Projects 54
