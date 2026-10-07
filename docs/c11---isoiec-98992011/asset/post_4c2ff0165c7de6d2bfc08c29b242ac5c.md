
# INTERNATIONAL STANDARD
ISO/IEC 9899

Third edition
2011-12-15

# Information technology — Programming languages — C

Technologies de l'information — Langages de programmation — C

![](img/f7747faa567394efa3f5ee93366f36ff_0_0.png)

# ISO/IEC 9899:2011(E)

COPYRIGHT PROTECTED DOCUMENT
© ISO/IEC 2011
All rights reserved. Unless otherwise specified, no part of this publication may be reproduced or utilized in any form or by any means
electronic or mechanical, including photocopying and microfilm, without permission in writing from either ISO at the address below or
ISO's member body in the country of the requester.

ISO copyright official
Case posted: 96 - CH-1211 Geneva 20
Tel: +41 22 749 01 11
Fax : +41 22 749 09 47
E-mail : copyright@iso.org
Web : http://www.iso.org
Published in Switzerland

ISO/IEC 2011 – All rights reserved

Copyright International Organization for Standardization
Provided by IHS under license permitted with ISO
No reproduction or redistribution permitted without license from IHS

Not for Resale

# Contents

- Foreword ... xiii
- Introduction ... xvii
- 1. Scope ... 1
- 2. Normative references ... 2
- 3. Terms, definitions, and symbols ... 3
- 4. Conformance ... 8
- 5. Environment ... 10
- 5.1 Conceptual models ... 10
- 5.1.1 Translation environment ... 10
- 5.1.2 Execution environments ... 12
- 5.2 Environmental considerations ... 22
- 5.2.1 Character sets ... 22
- 5.2.2 Character display semantics ... 24
- 5.2.3 Signals and interrupts ... 25
- 5.2.4 Environmental limits ... 25
- 6. Language ... 35
- 6.1 Notation ... 35
- 6.2 Concepts ... 35
- 6.2.1 Scopes of identifiers ... 35
- 6.2.2 Linkages of identifiers ... 36
- 6.2.3 Name of identifiers ... 37
- 6.2.4 Storage durations of objects ... 38
- 6.2.5 Types ... 39
- 6.2.6 Representations of types ... 44
- 6.2.7 Compatible and composite type ... 47
- 6.2.8 Alignment of objects ... 48
- 6.2.9 Conversions ... 50
- 6.2.10 Arithmetic operands ... 50
- 6.2.11 Other operands ... 54
- 6.2.12 Lexical elements ... 57
- 6.2.13 Keywords ... 58
- 6.2.14 Identifiers ... 59
- 6.2.15 Universal character names ... 61
- 6.2.16 Constants ... 62
- 6.2.17 String literals ... 70
- 6.2.18 Punctuators ... 73
- 6.2.19 Header names ... 74
- 6.2.20 Comments ... 75
- 6.3 Expressions ... 76
- 6.3.1 Primary expressions ... 76
- 6.3.2 Postfix operators ... 78
- 6.3.3 Unary operators ... 79
- 6.3.4 Cast operators ... 88
- 6.3.5 Multiplicative operators ... 92
- 6.3.6 Additive operators ... 92
- 6.3.7 Bitwise shift operators ... 94
- 6.3.8 Relational operators ... 95
- 6.3.9 Equality operators ... 96
- 6.3.10 Bitwise AND operators ... 97
- 6.3.11 Bitwise exclusive OR operator ... 98
- 6.3.12 Bitwise inclusive OR operator ... 98
- 6.3.13 Logical AND operator ... 99
- 6.3.14 Logical OR operator ... 99
- 6.3.15 Conditional operator ... 100
- 6.3.16 Assignment operators ... 101
- 6.3.17 Comma operator ... 105
- 6.4 Constant expressions ... 106
- 6.5 Declarations ... 108
- 6.5.1 Storage-class specifiers ... 109
- 6.5.2 Type specifiers ... 111
- 6.5.3 Type qualifiers ... 121
- 6.5.4 Function specifiers ... 125
- 6.5.5 Alignment specifier ... 127
- 6.5.6 Declarators ... 128
- 6.5.7 Type names ... 136
- 6.5.8 Type definitions ... 137
- 6.5.9 Initialization ... 139
- 6.5.10 Static assertions ... 145
- 6.6 Statements and blocks ... 146
- 6.6.1 Labeled statements ... 146
- 6.6.2 Compound statement ... 147
- 6.6.3 Expression and null statements ... 147
- 6.6.4 Selection statements ... 148
- 6.6.5 Iteration statements ... 150
- 6.6.6 Jump statements ... 151
- 6.7 External definitions ... 155
- 6.7.1 Function definitions ... 156
- 6.7.2 External object definitions ... 158
- 6.8 Preprocessing directives ... 160
- 6.8.1 Conditional inclusion ... 162
- 6.8.2 Source file inclusion ... 164
- 6.8.3 Macro replacement ... 166
