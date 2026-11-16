
## GAME PROGRAMMING GEMS 5

![](img/672fe9a2d008ba627b1991e15d70f43e_0_0.png)

Charles River Media

Edited by Kim Pallister

LIVERPOOL
JOHN MOORES UNIVERSITY
AVRIL ROBERTS LRC
TITHEBARN STREET
LIVERPOOL L2 2ER
TEL 0151 231 4022

| Liverpool John Moores University | | |
|---|---|---|
| LEARNING & INFO SERVICES | | |
| Accession Number 13297665 W | | |
| Class Number 794.48152 PA | | |
| Site | A | M | V |

CD-ROM to accompany this book available from Library Issue Desk

Books are to be returned on or before the last date below.

29 MAR 2006

LIVERPOOL JOHN MOORES UNIVERSITY AVRIL ROBERTS LRC TITHEBARN STREET LIVERPOOL L2 2ER TEL 0151 231 4022

LIBREX-

# WITHDRAWN

LIVERPOOL JOHN MOORES UNIVERSITY AVRIL ROBERTS LRC TITHEBARN STREET LIVERPOOL L2 2ER TEL 0151 231 4022

LIVERPOOL JMU LIBRARY 3 1111 01142 5905

## Game Programming Gems 5

## LIMITED WARRANTY AND DISCLAIMER OF LIABILITY

THE CD-ROM THAT ACCOMPANIES THE BOOK MAY BE USED ON A SINGLE PC ONLY. THE LICENSE DOES NOT PERMIT THE USE ON A NETWORK (OF ANY KIND). YOU FURTHER AGREE THAT THIS LICENSE GRANTS PERMISSION TO USE THE PRODUCTS CONTAINED HEREIN, BUT DOES NOT GIVE YOU RIGHT OF OWNERSHIP TO ANY OF THE CONTENT OR PRODUCT CONTAINED ON THIS CD-ROM. USE OF THIRD-PARTY SOFTWARE CONTAINED ON THIS CD-ROM IS LIMITED TO AND SUBJECT TO LICENSING TERMS FOR THE RESPECTIVE PRODUCTS.

CHARLES RIVER MEDIA, INC. ("CRM") AND/OR ANYONE WHO HAS BEEN INVOLVED IN THE WRITING, CREATION, OR PRODUCTION OF THE ACCOMPANYING CODE ("THE SOFTWARE") OR THE THIRD-PARTY PRODUCTS CONTAINED ON THE CD-ROM OR TEXTUAL MATERIAL IN THE BOOK, CANNOT AND DO NOT WARRANT THE PERFORMANCE OR RESULTS THAT MAY BE OBTAINED BY USING THE SOFTWARE OR CONTENTS OF THE BOOK. THE AUTHOR AND PUBLISHER HAVE USED THEIR BEST EFFORTS TO ENSURE THE ACCURACY AND FUNCTIONALITY OF THE TEXTUAL MATERIAL AND PROGRAMS CONTAINED HEREIN. WE HOWEVER, MAKE NO WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, REGARDING THE PERFORMANCE OF THESE PROGRAMS OR CONTENTS. THE SOFTWARE IS SOLD "AS IS" WITHOUT WARRANTY (EXCEPT FOR DEFECTIVE MATERIALS USED IN MANUFACTURING THE DISK OR DUE TO FAULTY WORKMANSHIP).

THE AUTHOR, THE PUBLISHER, DEVELOPERS OF THIRD-PARTY SOFTWARE, AND ANYONE INVOLVED IN THE PRODUCTION AND MANUFACTURING OF THIS WORK SHALL NOT BE LIABLE FOR DAMAGES OF ANY KIND ARISING OUT OF THE USE OF (OR THE INABILITY TO USE) THE PROGRAMS, SOURCE CODE, OR TEXTUAL MATERIAL CONTAINED IN THIS PUBLICATION. THIS INCLUDES, BUT IS NOT LIMITED TO, LOSS OF REVENUE OR PROFIT, OR OTHER INCIDENTAL OR CONSEQUENTIAL DAMAGES ARISING OUT OF THE USE OF THE PRODUCT.

THE SOLE REMEDY IN THE EVENT OF A CLAIM OF ANY KIND IS EXPRESSLY LIMITED TO REPLACEMENT OF THE BOOK AND/OR CD-ROM, AND ONLY AT THE DISCRETION OF CRM.

THE USE OF "IMPLIED WARRANTY" AND CERTAIN "EXCLUSIONS" VARIES FROM STATE TO STATE, AND MAY NOT APPLY TO THE PURCHASER OF THIS PRODUCT.

## Game Programming Gems 5

Edited by Kim Pallister

![](img/672fe9a2d008ba627b1991e15d70f43e_6_0.png)

CHARLES RIVER MEDIA, INC.
Hingham, Massachusetts

Copyright 2005 by CHARLES RIVER MEDIA, INC.
All rights reserved.

No part of this publication may be reproduced in any way, stored in a retrieval system of any type, or transmitted by any means or media, electronic or mechanical, including, but not limited to, photocopying, recording, or scanning, without prior permission in writing from the publisher.

Publisher: Jenifer Niles
Cover Design: The Printed Image
Cover Image: © Sammy Studios, Inc.

CHARLES RIVER MEDIA, INC.
10 Downer Avenue
Hingham, Massachusetts 02043
781-740-0400
781-740-8816 (FAX)
info@charlesriver.com
www.charlesriver.com

This book is printed on acid-free paper.

Kim Pallister, Game Programming Gems 5.
ISBN: 1-58450-352-1.

All brand names and product names mentioned in this book are trademarks or service marks of their respective companies. Any omission or misuse (of any kind) of service marks or trademarks should not be regarded as intent to infringe on the property of others. The publisher recognizes and respects all marks used by companies, manufacturers, and developers as a means to distinguish their products.

Library of Congress Cataloging-in-Publication Data

Game programming gems 5 / Kim Pallister, editor.— 1st ed.
p. cm.
Includes bibliographical references and index.
ISBN 1-58450-352-1 (hardcover with cd-rom : alk. paper)
1. Computer games—Programming. 2. Computer graphics. 1. Pallister, Kim.
QA76.6.C6723645 2005
794.8'1526—dc22
2004026858

Printed in the United States of America
05 7 6 5 4 3 2 First Edition

CHARLES RIVER MEDIA titles are available for site license or bulk purchase by institutions, user groups, corporations, etc. For additional information, please contact the Special Sales Department at 781-740-0400.

Requests for replacement of a defective CD-ROM must be accompanied by the original disc, your mailing address, telephone number, date of purchase, and purchase price. Please state the nature of the problem, and send the information to CHARLES RIVER MEDIA, Inc., 10 Downer Avenue, Hingham, Massachusetts 02043. CRM’s sole obligation to the purchaser is to replace the disc, based on defective materials or faulty workmanship, but not on the operation or functionality of the product.

## Contents

- Foreword .................................................... xi
- Preface .................................................... xv
- About the Cover Image .................................... xix
- Contributor Bios ......................................... xxi

## SECTION 1 GENERAL PROGRAMMING ........................ 1

- Introduction ................................................ 3
- William E. Damon III

- 1.1 Context-Sensitive HUDs for Editors.................... 5
- Adam Martin, Grex Games

- 1.2 Parsing Text Data in Games ........................... 17
- Aurelio Reis

- 1.3 Component Based Object Management .................. 25
- Bjarne Rene, Circle Studio Ltd

- 1.4 Using Templates for Reflection in C++ .............. 39
- Dominic Filion, Artificial Mind & Movement

- 1.5 Sphere Trees for Speedy BSPs ....................... 55
- Dominic Filion, Artificial Mind & Movement

- 1.6 Improved Frustum Culling ........................... 65
- Frank Puig Placeres

- 1.7 Generic Pager ........................................ 79
- Ignacio Incerra Cruz

- 1.8 Large-Scale Stack-Based State Machines.............. 93
- James Boer

- 1.9 CSG Construction Using BSP Trees ................... 103
- Octavian Marius Chincisan

- 1.10 Building Lua into Games ........................... 115
- Matthew Harmon, eV Interactive Corporation

- 1.11 Improving Freelists with Policy Based Design .................................... 129
- Nathan Mefford

- 1.12 A Real-Time Remote Debug Message Logger .................................... 143
- Patrick Duquette, Microods Canada Inc.

- 1.13 A Transparent Class Saving and Loading Trick ................................ 149
- Patrick Meehan

- 1.14 An Effective Cache-Oblivious Implementation of the ABT Tree ............ 159
- Sébastien Schertenleib, Swiss Federal Institute of Technology (EPFL),
  Virtual Reality Lab (VRLab)

- 1.15 Visual Design of State Machines .................................................... 169
- Scott Jacobs

- 1.16 A Generic Component Library ........................................................ 177
- Warrick Buchanan

- 1.17 Choose Your Path—A Menu System ................................................ 189
- Wendy Jones

## SECTION 2 MATHEMATICS .................................................................... 197

- Introduction ............................................................................................ 199
- Eric Lengyel, Naughty Dog Inc.

- 2.1 Using Geometric Algebra for Computer Graphics .............................. 201
- Chris Lomont

- 2.2 Minimal Acceleration Hermite Curves .............................................. 225
- Tony Barrera, Barrera Kristiansen AB; Anders Hast, Creative Media Lab,
  University of Gävle; and Ewert Bengtsson, Centre for Image Analysis,
  Uppsala University

- 2.3 Spline-Based Time Control for Animation ........................................ 233
- James M. Van Verth, Red Storm Entertainment

- 2.4 Faster Quaternion Interpolation Using Approximations .................... 247
- Andy Thomason

- 2.5 Minimax Numerical Approximation .................................................. 269
- Christopher Tremblay

- 2.6 Oblique View Frustums for Mirrors and Portals ................................ 281
- Eric Lengyel
