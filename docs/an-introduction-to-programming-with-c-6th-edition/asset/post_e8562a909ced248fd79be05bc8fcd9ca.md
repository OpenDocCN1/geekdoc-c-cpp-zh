
# AN INTRODUCTION TO PROGRAMMING WITH C++

SIXTH EDITION

DIANE ZAK

# AN INTRODUCTION TO PROGRAMMING WITH C++

# AN INTRODUCTION TO PROGRAMMING WITH C++

DIANE ZAK

# COURSE TECHNOLOGY CENGAGE Learning™

An Introduction to Programming with C++, Sixth Edition
Diane Zak

Executive Editor: Marie Lee
Acquisitions Editor: Amy Jollymore
Freelance Product Manager: Tricia Co
Senior Content Manager: Jill Braiewa
Editorial Assistant: Zinaشرين
Art Director: Marissa Falco
Text Designer: Shawn Ginsberger
Print Buyer: Julio Esperas
Proofreader: Amy Smith, Green Pen QA
Indexer: Michael Brackney
Composer: Integra Software Services

© 2011 Cengage Learning ALL RIGHTS RESERVED. No part of this work covered by the copyright herein may be reproduced, transmitted, stored or used in any form or by any means—graphic, electronic, or mechanical, including but not limited to photocopying, recording, digital taping, Web distribution, information networks, or information storage and retrieval systems, except as permitted under Section 107 or 108 of the 1976 United States Copyright Act—without prior written permission of the publisher.

For information and technology assistance, contact us at
Cengage Learning Customer & Services, 1-800-354-9076
For permission to use this material from this text or product,
submit all requests at cengage.com/permissions
Further requests can be emailed to
permissionrequest@cengage.com

Library of Congress Control Number: 2009941969
ISBN-13: 9-78-0538-46652-3
ISBN-10: 0-538-46652-9

Course Technology
20 Channel Center Street
Boston, MA 02210
USA

Some of the product names and company names used in this book have been used for identification purposes only and may be trademarks or registered trademarks of their respective manufacturers and sellers.

Course Technology, a part of Cengage Learning, reserves the right to revise this publication and make changes from time to time in its content without notice.

Cengage Learning is a provider of customized learning solutions with office locations around the globe, including Singapore, the United Kingdom, Australia, Mexico, Brazil, and Japan. Locate your local office at:
www.cengage.com/global

Cengage Learning products are represented in Canada by Nelson Education, Ltd.

To learn more about Course Technology, visit
www.cengage.comsetetechnology

Purchase any of your products at your local college store or at your preferred online store: www.CengageBrain.com

Printed in the United States of America
1 2 3 4 5 6 7 8 16 15 14 13 12 11 10

# Brief Contents

- Preface . . . . . . . . . . . . . . . . . . . xiv
- CHAPTER 1 An Introduction to Programming . . . . . . . . . . . 1
- CHAPTER 2 Beginning the Problem-Solving Process. . . . . . . 22
- CHAPTER 3 Variables and Constants . . . . . . . . . . . 51
- CHAPTER 4 Completing the Problem-Solving Process . . . 77
- CHAPTER 5 The Selection Structure . . . . . . . . . . 119
- CHAPTER 6 More on the Selection Structure. . . . . 163
- CHAPTER 7 The Repetition Structure . . . . . . . . . . 213
- CHAPTER 8 More on the Repetition Structure . . . . . 264
- CHAPTER 9 Value-Returning Functions . . . . . . . . 308
- CHAPTER 10 Void Functions . . . . . . . . . . . 370
- CHAPTER 11 One-Dimensional Arrays . . . . . 419
- CHAPTER 12 Two-Dimensional Arrays . . . . . . 486
- CHAPTER 13 Strings. . . . . . . . . . . . . . . . 524
- CHAPTER 14 Sequential Access Files . . . . . 582
- APPENDIX A Answers to Mini-Quizzes and Labs . . . 626
- APPENDIX B C++ Keywords . . . . . . . . . . . 690
- APPENDIX C ASCII Codes . . . . . . . . . . . . . . . . . . 691
- APPENDIX D How to Use Microsoft Visual C++ . . . . . . . . 693
- APPENDIX E How to Use Dev-C++ . . . . . . . . . . . . . . . 694
- APPENDIX F Classes and Objects . . . . . . . . . . . . 695
- Index . . . . . . . . . . . . . . . . . . . . . 721

# Contents

Preface ................................................................. . . . . . . . . . .xiv

## CHAPTER 1 An Introduction to Programming . . . . . . . . . . . 1
Programming a Computer . . . . . . . . . . . . . . . . 2
The Programmer's Job . . . . . . . . . . . . . . . . . 2
Do I Have What It Takes to Be a Programmer? . . . 3
Employment Opportunities . . . . . . . . . . . . . . . . 4
A Brief History of Programming Languages . . . . 4
Machine Languages . . . . . . . . . . . . . . . . . 4
Assembly Languages . . . . . . . . . . . . . . . . . 4
High-Level Languages. . . . . . . . . . . . . . . . . 4
Control Structures . . . . . . . . . . . . . . . . . . . 6
The Sequence Structure . . . . . . . . . . . . . . . . . 6
The Selection Structure . . . . . . . . . . . . . . . . . 7
The Repetition Structure . . . . . . . . . . . . . . . . . . . 9
Summary . . . . . . . . . . . . . . . . . . . . . . . . 12
Key Terms . . . . . . . . . . . . . . . . . . . . . . . . 12
Review Questions . . . . . . . . . . . . . . . . . . . 13
Exercises . . . . . . . . . . . . . . . . . . . . . . 15

## CHAPTER 2 Beginning the Problem-Solving Process. . . . 22
Problem Solving . . . . . . . . . . . . . . . . . . . . . . . 23
Everyday Problems . . . . . . . . . . . . . . . . 23
Creating Computer Solutions to Problems . . . . . . . 24
Step 1—Analyze the Problem . . . . . . . . . . . . . . . . 25
Step 2—Plan the Algorithm . . . . . . . . . . . . . . . . 27
Step 3—Desk-Check the Algorithm . . . . . . . . 31
The Mileage Problem. . . . . . . . . . . . . . . . . 34
Summary . . . . . . . . . . . . . . . . . . . . . . . . 43
Key Terms . . . . . . . . . . . . . . . . . . . . . . . 44
Review Questions . . . . . . . . . . . . . . . . . . . . 44
Exercises . . . . . . . . . . . . . . . . . . . . . . 46

## CHAPTER 3 Variables and Constants . . . . . . . . . . . 51
Beginning Step 4 in the Problem-Solving Process . . . 52
Internal Memory . . . . . . . . . . . . . . . . . . . . . . 52
Selecting a Name for a Memory Location . . . . . . . . . . . . . 53
Revisiting the Treyson Mobley Problem . . . . . . . . . . . . . . 54
Selecting a Data Type for a Memory Location . . . . . . . . . . . . 55
How Data Is Stored in Internal Memory . . . . . . . . . . . . . . . 57
Selecting an Initial Value for a Memory Location . . . . . . . . 60
Declaring a Memory Location . . . . . . . . . . . . . . . 62
Summary . . . . . . . . . . . . . . . . . . . . . . . . 69
Key Terms . . . . . . . . . . . . . . . . . . . . . . . 69
Review Questions . . . . . . . . . . . . . . . . . . . . 71
Exercises . . . . . . . . . . . . . . . . . . . . . . 73

## CHAPTER 4 Completing the Problem-Solving Process . . . 77
Finishing Step 4 in the Problem-Solving Process . . . . 78
Getting Data from the Keyboard . . . . . . . . . . . . . . . 79
Displaying Messages on the Computer Screen . . . . 81
Arithmetic Operators in C++ . . . . . . . . . . . . 83
Type Conversions in Arithmetic Expressions . . . . . 84
The static_cast Operator . . . . . . . . . . . . . . . . . 86
Assignment Statements . . . . . . . . . . . . . . . . 87
Step 5—Desk-Check the Program . . . . . 90
Step 6—Evaluate and Modify the Program . . . . 92
Arithmetic Assignment Operators . . . . . . . . . . . 97
Summary . . . . . . . . . . . . . . . . . . . . . . . . 103
Key Terms . . . . . . . . . . . . . . . . . . . . . . . 105
Review Questions . . . . . . . . . . . . . . . . . . . . 107
Exercises . . . . . . . . . . . . . . . . . . . . . . 109

## CHAPTER 5 The Selection Structure . . . . . . . 119
Making Decisions . . . . . . . . . . . . . . . . . . . 120
Flowcharting a Selection Structure . . . . . . . . 123
Coding a Selection Structure in C++ . . . . . . . 125
Comparison Operators . . . . . . . . . . . . . . . 127
Swapping Numeric Values . . . . . . . . . . . . 128
Displaying the Sum or Difference . . . . . . . . . . 130
Logical Operators . . . . . . . . . . . . . . 132
Using the Truth Tables . . . . . . . . . . . 134
Calculating Gross Pay . . . . . . . . . . . . 135
Pass/Fail Program . . . . . . . . . . . . . . . 137
Converting a Character to Uppercase or Lowercase . . 140
Formatting Numeric Output . . . . . . . . . 141
Summary . . . . . . . . . . . . . . . . . . . . . . . . 150
Key Terms . . . . . . . . . . . . . . . . . . . . . . . 151
Review Questions . . . . . . . . . . . . . . . . . . . . 152
Exercises . . . . . . . . . . . . . . . . . . . . . . 154

## CHAPTER 6 More on the Selection Structure. . . . . 163
Making Decisions . . . . . . . . . . . . . . . . . . . . 164
Flowcharting a Nested Selection Structure . . . 168
Coding a Nested Selection Structure . . . . . 170
