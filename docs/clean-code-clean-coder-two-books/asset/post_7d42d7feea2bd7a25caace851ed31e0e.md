
- Producer-Consumer
- Readers-Writers
- Dining Philosophers
- **Beware Dependencies Between Synchronized Methods**
- **Keep Synchronized Sections Small**
- **Writing Correct Shut-Down Code Is Hard**
- **Testing Threaded Code**
  - Treat Spurious Failures as Candidate Threading Issues
  - Get Your Nonthreaded Code Working First
  - Make Your Threaded Code Pluggable
  - Make Your Threaded Code Tunable
  - Run with More Threads Than Processors
  - Run on Different Platforms
  - Instrument Your Code to Try and Force Failures
  - Hand-Coded
  - Automated
- **Conclusion**
- **Bibliography**

## Chapter 14: Successive Refinement

### Args Implementation

- How Did I Do This?

### Args: The Rough Draft

- So I Stopped
- On Incrementalism

### String Arguments

### Conclusion

## Chapter 15: JUnit Internals

### The JUnit Framework

### Conclusion

## Chapter 16: Refactoring SerialDate

### First, Make It Work
### Then Make It Right
### Conclusion
### Bibliography

## Chapter 17: Smells and Heuristics

### Comments

- C1: *Inappropriate Information*
- C2: *Obsolete Comment*
- C3: *Redundant Comment*
- C4: *Poorly Written Comment*
- C5: *Commented-Out Code*

### Environment

- E1: *Build Requires More Than One Step*
- E2: *Tests Require More Than One Step*

### Functions

- F1: *Too Many Arguments*
- F2: *Output Arguments*
- F3: *Flag Arguments*
- F4: *Dead Function*

### General

- G1: *Multiple Languages in One Source File*
- G2: *Obvious Behavior Is Unimplemented*
- G3: *Incorrect Behavior at the Boundaries*
- G4: *Overridden Safeties*
- G5: *Duplication*
- G6: *Code at Wrong Level of Abstraction*
- G7: *Base Classes Depending on Their Derivatives*
- G8: *Too Much Information*
- G9: *Dead Code*
- G10: *Vertical Separation*
- G11: *Inconsistency*
- G12: *Clutter*
- G13: *Artificial Coupling*
- G14: *Feature Envy*
- G15: *Selector Arguments*
- G16: *Obscured Intent*
- G17: *Misplaced Responsibility*
- G18: *Inappropriate Static*
- G19: *Use Explanatory Variables*
- G20: *Function Names Should Say What They Do*
- G21: *Understand the Algorithm*
- G22: *Make Logical Dependencies Physical*
- G23: *Prefer Polymorphism to If/Else or Switch/Case*
- G24: *Follow Standard Conventions*
- G25: *Replace Magic Numbers with Named Constants*
- G26: *Be Precise*
- G27: *Structure over Convention*
- G28: *Encapsulate Conditionals*
- G29: *Avoid Negative Conditionals*
- G30: *Functions Should Do One Thing*
- G31: *Hidden Temporal Couplings*
- G32: *Don’t Be Arbitrary*
- G33: *Encapsulate Boundary Conditions*
- G34: *Functions Should Descend Only One Level of Abstraction*
- G35: *Keep Configurable Data at High Levels*
- G36: *Avoid Transitive Navigation*

### Java

- J1: *Avoid Long Import Lists by Using Wildcards*
- J2: *Don’t Inherit Constants*
- J3: *Constants versus Enums*

### Names

- N1: *Choose Descriptive Names*
- N2: *Choose Names at the Appropriate Level of Abstraction*
- N3: *Use Standard Nomenclature Where Possible*
- N4: *Unambiguous Names*
- N5: *Use Long Names for Long Scopes*
- N6: *Avoid Encodings*
- N7: *Names Should Describe Side-Effects*

### Tests

- T1: *Insufficient Tests*
- T2: *Use a Coverage Tool!*
- T3: *Don’t Skip Trivial Tests*
- T4: *An Ignored Test Is a Question about an Ambiguity*
- T5: *Test Boundary Conditions*
- T6: *Exhaustively Test Near Bugs*
- T7: *Patterns of Failure Are Revealing*
- T8: *Test Coverage Patterns Can Be Revealing*
- T9: *Tests Should Be Fast*

### Conclusion

### Bibliography

## Appendix A: Concurrency II

### Client/Server Example

- The Server
- Adding Threading
- Server Observations
- Conclusion

### Possible Paths of Execution

- Number of Paths
- Digging Deeper
- Pacing Yourself
- Being Late
- Help
- Bibliography

## Chapter 5. Test Driven Development

### The Jury Is In

### The Three Laws of TDD

### What TDD Is Not

### Bibliography

## Chapter 6. Practicing

### Some Background on Practicing

### The Coding Dojo

### Broadening Your Experience

### Conclusion

### Bibliography

## Chapter 7. Acceptance Testing

### Communicating Requirements

### Acceptance Tests

### Conclusion

## Chapter 8. Testing Strategies

### QA Should Find Nothing

### The Test Automation Pyramid

### Conclusion

### Bibliography

## Chapter 9. Time Management

### Meetings

### Degrees of Failure

### Mentoring

### Apprenticeship

### Craftsmanship

### Conclusion

## Appendix A. Tooling

### Tools

### Source Code Control

### IDE/Editor

### Issue Tracking

### Continuous Build

### Unit Testing Tools

### Component Testing Tools

### Integration Testing Tools

### UML/MDA

### Conclusion

## Index

## Footnotes

## Clean Code

*A Handbook of Agile Software Craftsmanship*

### The Object Mentors:

Robert C. Martin
Michael C. Feathers Timothy R. Ottinger
Jeffrey J. Langr Brett L. Schuchert
James W. Grenning Kevin Dean Wampler
Object Mentor Inc.

> Writing clean code is what you must do in order to call yourself a professional. There is no reasonable excuse for doing anything less than your best.

![](img/d3848357ae109884a140c7b3662e0e30_21_0.png)

Upper Saddle River, NJ • Boston • Indianapolis • San Francisco
New York • Toronto • Montreal • London • Munich • Paris • Madrid
Capetown • Sydney • Tokyo • Singapore • Mexico City

Many of the designations used by manufacturers and sellers to distinguish their products are claimed as trademarks. Where those designations appear in this book, and the publisher was aware of a trademark claim, the designations have been printed with initial capital letters or in all capitals.

The authors and publisher have taken care in the preparation of this book, but make no expressed or implied warranty of any kind and assume no responsibility for errors or omissions. No liability is assumed for incidental or consequential damages in connection with or arising out of the use of the information or programs contained herein.

The publisher offers excellent discounts on this book when ordered in quantity for bulk purchases or special sales, which may include electronic versions and/or custom covers and content particular to your business, training goals, marketing focus, and branding interests. For more information, please contact:

U.S. Corporate and Government Sales
(800) 382-3419
[corpsales@pearsontechgroup.com](mailto:corpsales@pearsontechgroup.com)

For sales outside the United States please contact:

International Sales
[international@pearsoned.com](mailto:international@pearsoned.com)

Visit us on the Web: informit.com/ph

### *Library of Congress Cataloging-in-Publication Data*

Martin, Robert C.
Clean code : a handbook of agile software craftsmanship / Robert C. Martin.
p. cm.
Includes bibliographical references and index.
ISBN 0-13-235088-2 (pbk. : alk. paper)
1. Agile software development. 2. Computer software—Reliability. I. Title.

QA76.76.D47M3652 2008
005.1—dc22

2008024750

Copyright © 2009 Pearson Education, Inc.

All rights reserved. Printed in the United States of America. This publication is protected by copyright, and permission must be obtained from the publisher prior to any prohibited reproduction, storage in a retrieval system, or transmission in any form or by any means, electronic, mechanical, photocopying, recording, or likewise. For information regarding permissions, write to:

Pearson Education, Inc
Rights and Contracts Department
501 Boylston Street, Suite 900
Boston, MA 02116
Fax: (617) 671-3447

ISBN-13: 978-0-13-235088-4
ISBN-10: 0-13-235088-2

Text printed in the United States on recycled paper at Courier in Stoughton, Massachusetts.

Ninth printing April, 2011
