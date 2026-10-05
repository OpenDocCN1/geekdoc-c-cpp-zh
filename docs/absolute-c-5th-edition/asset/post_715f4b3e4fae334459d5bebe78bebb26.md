
# ABSOLUTE C++

FIFTH EDITION

Walter Savitch

# ABSOLUTE 5TH EDITION C++

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_4_0.png)

# Walter Savitch
University of California, San Diego
Contributor

# Kenrick Mock
University of Alaska Anchorage

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_4_1.png)

Boston Columbus Indianapolis New York San Francisco Upper Saddle River Amsterdam Cape Town Dubai London Madrid Milan Munich Paris Montréal Toronto Delhi Mexico City São Paulo Sydney Hong Kong Seoul Singapore Taipei Tokyo

Vice President and Editorial Director, ECS:
Marcia Horton
Executive Director: Matt Goldstein
Editorial Assistants: Chelsea Kharakozova/Emma Snider
Vice President Marketing: Patrice Jones
Marketing Manager: Yes Alayan
Marketing Coordinator: Kathryn Ferranti
Vice President and Director of Production:
Vince O'Brien
Managing Editor: Jeff Holcomb
Senior Project Manager: Marilyn Loudv
Manufacturing Manager: Nick Skylitis
Operations Specialist: Lisa McDowell
Test Designer: Joyce CentOS Wells
Cover Designer: Anthony Gemmellaro
Cover Image: © Shutterstock
Media Editor: Dan Sandin
Manager, Rights and Permissions: Michael Joyce
Test Permissions--assessment: Dana Weightman
Test Permissions--clearance: Nicole Coiffeauer/Creative Compliance
Full-Service Vendor: GEX Publishing Services
Project Management: GEX Publishing Services
Printer/Binder: Edwards Brothers
Cover Printer: Lehigh-Phonix Color

This book was composed in InDesign. Base font is Adobe Garamond 10/12. Display font is Open LT Ltd.

Credits and acknowledgments from other sources and reproduced, with permission, in this textbook appear on the appropriate page within

Copyright © 2013, 2010, 2008, 2006, 2004 by Pearson Education, Inc., publishing as Addison-Wesley. All rights reserved. Manufactured in the United States of America. This publication is protected by Copyright, and permission should be obtained from the publisher prior to any prohibited reproduction, storage in a retrieval system, or in any form or by any electronic, mechanical, photocopying, recording, or likewise. To obtain(s) to use material from this work, please submit a written request to Pearson Education, Inc., Permissions Department, One Lake Street, Upper River, New Jersey 07548, or you may fax your request to 201-236-3290.

Many of the designations by manufacturers and sellers to distinguish their products are claimed as trademarks. Where those designations appear in this book, and the publisher was aware of a trademark claim, the designs have been printed in initial caps or all caps.

# Library of Congress Cataloging-in-Publication Data

Savitch, Walter
Absolute C++ / Walter Savitch ; contributor, Kenrick Mock. -- 5th ed.
pcm.
Includes bibliographical references and index.
ISBN 978-0-13-283071-3 (all. paper)
1. C++ (Computer program language) I. Mock, Kenrick. II. Title.
QA76.73.C153279 2010
005.13'-dc23
201201325

1 2 3 4 5 6 7 8 9 10—EB—15 14 13 12

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_5_0.png)

ISBN-10: 0-13-283071-X
ISBN-13: 978-0-13-283071-3

# Preface

This book is designed to be a textbook and reference for programming in the C++ language. Although it includes programming techniques, it is organized around the features of the C++ language, rather than any particular curriculum of techniques. The main audience I had in mind is undergraduate students who have not de extensive programming experience with the C++ language. As such, this book is a suitable C++ text or reference for a wide range of users. The introductory chapters are written at a level that is accessible to beginners, the boxed sections of these chapters to introduce more experienced programmers to basic C++ syntax. Later chapters are also understandable to beginners, but are written at a level suitable for those who have progressed to more advanced topics. Absolute C++ is also suitable for anyone learning the C++ language on their own. (For those who want a textbook with more pedagogical material and on very basic programming, try my Problem Solving with C++, Eighth Edition, Pearson Education).

The C++ coverage in this book goes well what a beginner needs to know. In particular, it has extensive coverage of inheritance, polymorphism, exception handling, and the Standard Template Library (STL), as well as basic coverage of patterns and the unified modeling language (UML).

# CHANGES IN THIS EDITION

This fifth edition presents the same programming philosophy as the fourth edition. For instructors, you can teach the same course, presenting the same topics in the same order with no changes in the material covered or the chapters assigned. Changes include:

- Chapter 1 includes a short introduction to the string class and Chapter 12 includes a section on using `iostream` to convert strings and other types.
- New self-test exercises have been added along with twenty-five Chapter 13 briefly describes recursion.
- Several errors that were found in the fourth edition have been corrected.
- Fifteen new VideoNotes have been added to the book (www.pearsonhigher.com/savitch) for a total of forty-six. These VideoNotes walk through the process of problem solving and coding to reinforce key concepts. An icon appears in the margin of the book when a video is available.

# ANSI/ISO C++ STANDARD

This edition is fully compatible with compilers that meet the latest ANSI/ISO standard.

# STANDARD TEMPLATE LIBRARY

The Standard Template Library (STL) is an extensive collection of preprogrammed structure classes and algorithms. The STL is perhaps as big a topic as the core language, so I have included a substantial introduction to STL. There is a full chapter on the general topic of templates and a chapter on the particulars of STL, as well as other material, or related to, at other points in the text.

# OBJECT-ORIENTED PROGRAMMING

This book is organized around the structure of C++. As such, the early chapters cover aspects of C++ that are common to high-level programming languages but not particularly oriented toward object-oriented programming (OOP). For a reference book—and for a book for learning second language—this makes sense. However, I consider C++ to be an OOP language. If you are programming in C++ and not C, you must be using the OOP features of C++. This offers extensive coverage of encapsulation, inheritance, and polymorphism as realized in the C++ language. Chapter 20, on patterns and UML, gives additional coverage of OOP-related material.

# FLEXIBILITY IN TOPIC ORDERING

This book allows instructors wide latitude in reordering the material. This is important if a book is to serve as a reference. This is also in keeping with my philosophy of accommodating the instructor's style, rather than tying the instructor to my own personal preference of topic ordering. Each chapter introduction explains what material must already have covered before each section of the chapter can be covered.

# ACCESSIBLE TO STUDENTS

It is not enough for a book to present the right topics in the right order. It is not enough for it to be correct and clear to an instructor. The material also needs to be presented in a way that is accessible to the novice. Like my other textbooks, which proved to be very popular with students, this book was written to be friendly and accessible to the student.

# SUMMARY BOXES

Each major point is summarized in a boxed section. These boxed sections are spread throughout each chapter. They serve as summaries of the material, as a quick reference source, and as a quick way to learn the C++ syntax for a feature you know about in general but for which you do not know the particulars.

# SELF-TEST EXERCISES

Each chapter contains numerous self-test exercises. Complete answers for all the self-test exercises are given at the end of each chapter.
