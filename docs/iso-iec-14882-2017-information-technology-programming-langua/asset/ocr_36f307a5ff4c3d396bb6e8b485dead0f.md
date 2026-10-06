# ISO/IEC 14882:2017(E)

+   1. Preprocessing number tokens lexically exclude all integer literal tokens (5.13.2) and all floating literal tokens (5.13.4).

+   2. A preprocessing number does not have a type or a value; it acquires both after a successful conversion to an integer literal or a floating literal token.

# 5.10 Identifiers [lex.name]

```
identifier:
identifier-nondigit
identifier-nondigit
identifier digit

identifier-nondigit:
nondigit
unnivers-character-name

nondigit: one of
 a b c d e f g h i j k l m
 o p q r s t u v w x y z
 B C D E F G H I J K L M
 O P Q R S T U W X Y _

digit: one of
0 1 2 3 4 5 6 7 8 9
```

An identifier is an arbitrarily long sequence of letters and digits. Each universal-character-name in an identifier shall designate a character encoding in ISO 10646 falls into one of ranges specified in Table 2. The initial element shall not be one of ranges specified in Table 3. Upper- and lower-case letters are different. All characters are significant.

> Table 2 — Ranges of characters allowed

| 00AB | 00AA | 00C0–00D6 | 00D8–00F6 | 00B2–00FF |
|---|---|---|---||
| 00B7–00AB | 008C–00B5 | 1681–18FF | | 00F8–00FF |
| 0100–167F | 202A–202E | 203F–206A | 2776–2793 | 2060–206F |
| 200B–200D | 3021–302F | 2054 | 2C00–2CFF | 2E80–2FFFF |
| 2070–218F | 2460–246F | 3031–3D7F | | |
| 3004–3007 | | | | |
| F900–F3D3 | FD40–FDCF | FDE0–FE44 | FE47–FFFF | |
| 10000–1FFFF | 20000–2FFF | 30000–3FFF | 40000–4FFFF | 50000–5FFFF |
| 60000–6FFFF | 70000–7FFFF | 80000–8FFFF | 90000–9FFFF | A0000–AFFFF |
| B0000–FFFF | C0000–CFFF | D0000–DFFFF | | |

> Table 3 — Ranges of characters initialized (combining characters)

| 0300–036F | 1DC0–1DFF | 20B0–20FF | FE20–FE2F |

On systems where it cannot accept extended characters, an encoding of the universal-character-name may be in forming valid identifiers. For example, otherwise unused character or sequence of characters may be used to encode the \u in a universal-character-name. Extended characters may produce a long identifier, but C++ does not place a translation limit on significant characters for external identifiers. In C++, upper- and lower-case letters are considered different for all identifiers, including external identifiers.

§ 5.10  ©ISO/IEC 2017 — All rights reserved  27