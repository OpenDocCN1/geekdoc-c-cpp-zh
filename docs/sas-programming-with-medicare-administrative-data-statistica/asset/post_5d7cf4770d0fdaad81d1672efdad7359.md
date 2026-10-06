
# SAS® Programming with Medicare Administrative Data

![](img/ddfeb619b7009b6b3b96e48c6689ec7a_0_0.png)

Matthew Gillingham

The correct bibliographic citation for this manual is as follows: Gillingham, Matthew. 2014. SAS® Programming with Medicare Administrative Data. Cary, NC: SAS Institute Inc.

# SAS® Programming with Medicare Administrative Data

Copyright © 2014, SAS Institute Inc., Cary, NC, USA

ISBN 978-1-61290-322-4

All rights reserved. Produced in the United States of America.

For a hard-copy book: No part of this publication may be reproduced, stored in a retrieval system, or transmitted, in any form or by means, electronic, mechanical, photocopying, or otherwise, without the prior written permission of the publisher, SAS Institute Inc.

For a web download or e-book: Your use of this publication shall be governed by the terms established by the vendor at the time you acquire this publication.

The scanning, uplifting, and distribution of this document via the Internet or any other means without the permission of the publisher is illegal and punishable by law. Please use only authorized electronic editions and do not participate or encourage piracy of copyrighted materials. Your respect of others' rights is appreciated.

U.S. Government License Rights; Restricted Rights: The Software and its documentation developed at private expense and is provided with RESTRICTED RIGHTS to the United States Government. duplication or disclosure of the Software by the United States Government is subject to the license term of this Agreement pursuant to, as applicable, FAR 22.1212, DFAR 22.7202-1(a), DFAR 22.7202-3(a) and DFAR 22.7202-4(a), to the extent required by federal law, the minimum restricted rights as set out in FAR 52.22-19 (DEC 2007). If FAR 52.22-19 is applicable, this provision serves as notice under clause (c) thereof and no other notice is required to be affixed to the Software or its documentation. The Government's rights in Software and documentation shall be as set forth in this Agreement.

SAS Institute Inc., SAS Campus Drive, Cary, North Carolina 25313-2414.

April 2014

SAS provides a complete selection of books and electronic products to help customers SAS® software to its full potential. For more information about our offerings, visit support.sas.com/bookstore or call 1-800-727-3228.

SAS and all other SAS Institute Inc. product or service names are registered trademarks or trademarks of SAS Institute Inc. in the USA and other countries. ® indicates SAS registration.

Other brand and product names are trademarks of their respective companies.

## Contents

- About This Book ................................................................................... ix
- About The Author .............................................................................. xiii
- Acknowledgments ................................................................................... XV
- Chapter 1: Introduction ................................................................ 1
- Introduction and Purpose of This Book ............................................ 1
- Framework of This Book ................................................................. 2
- Our Programming Project ........................................................ 3
- Chapter Outline ............................................................................ 5
- How to Use This Book ................................................................ 6
- Disclaimer ................................................................................ 7
- Chapter Summary ................................................................. 8
- Chapter 2: An Introduction to the Medicare Program ........................ 9
- Introduction and Goals of the Chapter ............................................ 9
- An Introduction to the Medicare Program ...................................... 10
- What is Medicare? ................................................................ 10
- Medicare Enrollment and Eligibility ........................................ 11
- What Is Covered by Medicare? ............................................... 11
- What Is Not Covered by Medicare? ....................................... 12
- The Mechanics of Medicare ................................................ 13
- Chapter Summary ................................................................... 15
- Chapter 3: An Introduction to Medicare Data ............................ 17
- Introduction and Goals of This Chapter........................................... 17
- A Note on the Source and Structure of Our Claims Data ............... 18
- Part B Carrier Claims Data ................................................... 19
- Durable Medical Equipment (DME) Data ............................ 19
- Outpatient Claims Data ................................................................................ 20
- Inpatient Claims Data............................................................................................... 20
- Skilled Nursing Facility (SNF) Claims Data........................................................... 21
- Home Health Claims Data........................................................................................... 21
- Hospice Claims Data............................................................................................... 22
- Commonly Retained Elements in Administrative Claims Data................ 22
- Master Beneficiary Summary File........................................................................... 24
- Provider Data........................................................................................................... 24
- Example: Identification of Emergency Department (ED) Utilization......................... 25
- Example: Identification of Surgical Services........................................................... 26
- Chapter Summary.................................................................................................. 26
- Chapter 4: Planning the Research Programming Project......................................... 29
- Introduction and Goals of This Chapter.................................................................. 29
- Our Project's Plan: The SDLC............................................................................... 30
- Our Project's High-Level Requirements.................................................................... 32
- Our Project's Quality Assurance Plan....................................................................... 33
- Our Project's Flowchart............................................................................................... 33
- Our Project's Data Storage and LIBNAMES.............................................. 35
- Our Research Programming Technical Specifications................................................ 36
- Chapter Summary.................................................................................................. 37
- Chapter 5: Request, Receive, Load, and Transform Data....................................... 39
- Introduction........................................................................................................... 39
- Requesting Medicare Administrative Claims and Enrollment Data................ 40
- Sources of Medicare Claims and Enrollment Data....................................................... 40
- Data Available from CMS............................................................................... 41
- Our Project's Data Requirements and Request Specifications.................................. 42
- Contacting ResDAC and Completing Paperwork..................................................... 43
- Receiving, Decrypting, and Loading Medicare Administrative Claims and Enrollment Data.................................................................................................. 45
- Receiving Our Medicare Administrative Data........................................................... 45
- Decrypting Our Medicare Administrative Data....................................................... 46
- Loading Our Medicare Administrative Data into SAS Data Sets...Algorithms: Transforming Base Claim and Line Level Data Sets into Single Claim-Level
