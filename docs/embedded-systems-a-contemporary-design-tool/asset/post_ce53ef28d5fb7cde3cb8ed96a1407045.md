
![](img/679b8d2d47f1bf86e17aca48f596f5cc_0_0.png)

## Fully revised and updated

## Second Edition

## EMBEDDED SYSTEMS

## A CONTEMPORARY DESIGN TOOL

JAMES K. PECKOL

with website

WILEY

## Embedded Systems

## Embedded Systems
A Contemporary Design Tool

Second Edition

James K. Peckol, Ph.D.
University of Washington

WILEY

This edition first published 2019
© 2019 John Wiley & Sons Ltd

Edition History
1st Edition:
Embedded systems : a contemporary design tool / James K. Peckol.
ISBN 978-0-471-72180-2
(cloth)

All rights reserved. No part of this publication may be reproduced, stored in a retrieval system, or transmitted, in any form or by any means, electronic, mechanical, photocopying, recording or otherwise, except as permitted by law. Advice on how to obtain permission to reuse material from this title is available at http://www.wiley.com/go/permissions.

The right of James K. Peckol to be identified as the author of this work has been asserted in accordance with law.

Registered Offices
John Wiley & Sons, Inc., 111 River Street, Hoboken, NJ 07030, USA
John Wiley & Sons Ltd, The Atrium, Southern Gate, Chichester, West Sussex, PO19 8SQ, UK

Editorial Office
The Atrium, Southern Gate, Chichester, West Sussex, PO19 8SQ, UK

For details of our global editorial offices, customer services, and more information about Wiley products visit us at www.wiley.com.

Wiley also publishes its books in a variety of electronic formats and by print-on-demand. Some content that appears in standard print versions of this book may not be available in other formats.

Limit of Liability/Disclaimer of Warranty
While the publisher and authors have used their best efforts in preparing this work, they make no representations or warranties with respect to the accuracy or completeness of the contents of this work and specifically disclaim all warranties, including without limitation any implied warranties of merchantability or fitness for a particular purpose. No warranty may be created or extended by sales representatives, written sales materials or promotional statements for this work. The fact that an organization, website, or product is referred to in this work as a citation and/or a potential source of further information does not mean that the publisher and the authors endorse the information or services the organization, website, or product may provide or recommendations it may make. This work is sold with the understanding that the publisher is not engaged in rendering professional services. The advice and strategies contained herein may not be suitable for your situation. You should consult with a specialist where appropriate. Further, readers should be aware that websites listed in this work may have changed or disappeared between when this work was written and when it is read. Neither the publisher nor authors shall be liable for any loss of profit or any other commercial damages, including but not limited to special, incidental, consequential, or other damages.

Library of Congress Cataloging-in-Publication Data
Name: Peckol, James K., author.
Title: Embedded systems : A Contemporary Design Tool / James K. Peckol, Ph.D., University of Washington.
Description: Second edition. | Hoboken, NJ : John Wiley & Sons, Inc., 2019. |
Includes bibliographical references and index.
Identifiers: LCCN 2018039258 (print) | LCCN 2018045459 (ebook) | ISBN 9781119455747 (Adobe PDF) | ISBN 9781119455758 (ePub) | ISBN 9781119457503 (hardcover)
Subjects: LCSH: Embedded computer systems | Object-oriented methods
Classification: LCC TK7895.E42 (ebook) | LCC TK7895.E42 P43 2019 (print) | DDC 006.22--dc23
LC record available at https://lccn.loc.gov/2018039258
Cover Design: Wiley
Cover Image: © HWYARDS/Stock.com/Getty Images Plus
Set in 10/12 TimesLTstd by SPI Global, Chennai, India
Printed and bound by CPI Group (UK) Ltd, Croydon, CR0 4YY
10 9 8 7 6 5 4 3 2 1

To my family: Near and Extended, Close and Distant,
Present and Departed, So Similar,
So Different, So Known, So Surprising ...
especially to our youngest brother Karl,
taken from us out of season during the last voyage
of the Edmund Fitzgerald.

## Contents

- About the Author xxxiii
- Foreword xxxv
- Preface xlix
- Acknowledgment lix
- About the Companion Website lxi

## Part 1 Hardware and Software Infrastructure

- 1 The Hardware Side – Part 1: An Introduction 1
- 1.1 Introduction 1
- 1.2 The Hardware Side – Getting Started 3
- 1.3 The Core Level 3
- 1.3.1 The Microprocessor 6
- 1.3.2 The Microcomputer 7
- 1.3.3 The Microcontroller 7
- 1.3.4 The Digital Signal Processor 7
- 1.4 Representing Information 8
- 1.4.1 Word Size 9
- 1.5 Understanding Numbers 9
- 1.5.1 Resolution 10
- 1.5.2 Propagation of Error 11
- 1.5.2.1 Addition 11
- 1.5.2.2 Multiplication 12
- 1.6 Addresses 13
- 1.7 Instructions 14
- 1.8 Registers – A First Look 16
- 1.9 Embedded Systems – An Instruction Set View 18
- 1.9.1 Instruction Set – Instruction Types 18
- 1.9.2 Data Transfer Instructions 18
- 1.9.2.1 Addressing Modes 20
- 1.9.3 Execution Flow 26
- 1.9.3.1 Sequential Flow 26
- 1.9.3.2 Branch 27
- 1.9.3.3 If-else Construct 28
- 1.9.3.4 Loop 28
- 1.9.3.5 Procedure or Function Call 29
- 1.9.3.6 Arithmetic and Logic 32
- 1.10 Embedded Systems – A Register View 34
- 1.10.1 The Basic Register 35
- 1.10.2 Register Operations 35
- 1.10.2.1 Write to a Register 36
- 1.10.2.2 Read from a Register 36
- 1.11 Register Transfer Language 36
- 1.12 Register View of a Microprocessor 38
- 1.12.1 The Datapath 38
- 1.12.2 Processor Control 39
- 1.12.2.1 Fetch 39
- 1.12.2.2 Decode 40
- 1.12.2.3 Execute 40
- 1.12.2.4 Next 41
- 1.13 Summary 45
- 1.14 Review Questions 45
- 1.15 Thought Questions 46
- 1.16 Problems 47

## 2 The Hardware Side – Part 2: Combinational Logic – A Practical View 55

- 2.1 Introduction 55
- 2.2 A Look at Real-World Gates – Part 1: Signal Levels 56
- 2.2.1 Logic Levels 57
- 2.2.2 A First Look Inside the Logic Gate 59
- 2.2.3 Fan-In and Fan-Out 60
- 2.3 A Look at Real-World Gates – Part 2: Time 64
- 2.3.1 Rise and Fall Times 65
- 2.3.2 Propagation Delay 65
- 2.3.3 Race Conditions and Hazards 67
- 2.3.3.1 Static Hazard 67
- 2.3.3.2 Dynamic Hazard 69
- 2.4 A Look at Real-World Gates – Part 3: Signal Behavior in the Real World – the Legacy of Early Physicists 70
- 2.5 Look For the Guilty – A First Look at Signal Quality 71
- 2.5.1 Resistors 71
- 2.5.1.1 A Discrete Component First-Order Resistor Model 72
- 2.5.2 Capacitors 74
- 2.5.2.1 Discrete Component First-Order Capacitor Model 76
- 2.5.3 Inductors 78
- 2.5.3.1 Magnetic Field Lines – The First Principle 78
- 2.5.3.2 Magnetic Field Lines – The Second Principle 79
- 2.5.3.3 Magnetic Field Lines – The Third Principle 80
- 2.6 Inductance in Action 81
- 2.6.1 Wires and Conductors 82
- 2.7 Logic Circuit Models and Parasitic Components 84
- 2.7.1 First-Order RC Circuit Model 84
- 2.7.2 First-Order RL Circuit Model 86
- 2.7.3 Second-Order Series RLC Circuit Model 87
- 2.7.4 Tristate Drivers 89
- 2.7.4.1 Open Gate Inputs 90
- 2.8 Testing Combinational Circuits – Introduction and Philosophy 91
- 2.9 Modeling, Simulation, and Tools 92
- 2.10 Structural Faults 93
- 2.10.1 Stuck-at Faults 93
- 2.10.1.1 Stuck-at-Zero Faults 94
- 2.10.1.2 Stuck-at-One Faults 95
- 2.10.2 Open Circuit Faults 96
- 2.10.3 Bridging Faults 96
- 2.10.3.1 Nonfeedback Bridge Faults 97
- 2.10.3.2 Feedback Bridge Faults 99
- 2.11 Functional Faults 99
- 2.11.1 Hazards and Race Conditions 100
- 2.12 Summary 101
- 2.13 Review Questions 101
- 2.14 Thought Questions 102
- 2.15 Problems 104

## 3 The Hardware Side – Part 3: Storage Elements and Finite-State Machines – A Practical View 111

- 3.1 Introduction 111
- 3.2 The Concepts of State and Time 112
- 3.2.1 Time 112
- 3.2.2 State 112
- 3.2.3 State Changes 113
- 3.3 The State Diagram 113
- 3.4 Finite-State Machines – A Theoretical Model 114
- 3.5 Designing Finite-State Machines – Part 1: Registers 116
- 3.5.1 Storage Registers 116
- 3.5.2 Shift Registers 117
- 3.5.2.1 Shift Right Shift Register 117
- 3.5.2.2 Parallel In/Serial Out – Serial In/Parallel Out Left Shift Registers 121
- 3.5.3 Linear Feedback Shift Registers 122
- 3.6 Designing Finite-State Machines – Part 2: Counting and Dividing 124
- 3.6.1 Dividers 124
- 3.6.1.1 Divide by Two 124
- 3.6.2 Asynchronous Dividers and Counters 125
- 3.6.3 Synchronous Dividers and Counters 127
- 3.6.4 Johnson Counters 128
- 3.6.4.1 Two-Stage Johnson Counter 129
- 3.6.4.2 Three- or Greater Stage Johnson Counter 130
- 3.7 Practical Considerations – Part 1: Timing in Latches and Flip-Flops 131
- 3.7.1 Gated Latches 131
- 3.7.2 Flip-Flops 132
- 3.7.3 Propagation Delays 132
- 3.7.4 Timing Margin 133
- 3.8 Practical Considerations – Part 2: Clocks and Clock Distribution 135

