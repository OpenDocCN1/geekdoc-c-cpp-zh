
| Instruction | Mnemonic | Format | OpCode |
|---|---|---|---|
| LOAD REVERSED (32) | LRVR | RRE | B91F |
| LOAD REVERSED (32) | LRV | RXV | B31B |
| LOAD REVERSED (64) | LRVGR | RRE | B90F |
| LOAD REVERSED (64) | LRVG | RXV | B30F |
| LOAD ROUNDED (extended to long BFP) | LXDBR | RRE | B345 |
| LOAD ROUNDED (extended to long HFP) | LDXR | RR | 25 |
| LOAD ROUNDED (extended to long HFP) | LDRR | RR | 25 |
| LOAD ROUNDED (extended to short BFP) | LXEBR | RRE | B346 |
| LOAD ROUNDED (extended to short HFP) | LEXR | RRE | B366 |
| LOAD ROUNDED (long to short BFP) | LEDBR | RRE | B344 |
| LOAD ROUNDED (long to short HFP) | LEDR | RR | 35 |
| LOAD ROUNDED (long to short HFP) | LRER | RR | 35 |
| LOAD USING REAL ADDRESS (32) | LURA | RRE | B24B |
| LOAD USING REAL ADDRESS (64) | LURAG | RRE | B905 |
| LOAD ZERO (extended) | LZXR | RRE | B376 |
| LOAD ZERO (long) | LZDR | RRE | B375 |
| LOAD ZERO (short) | LZSR | RRE | B374 |
| MODIFY STACKED STATE | MSTA | RRE | B247 |
| MODIFY SUBCHANNEL | MSCH | S C | B332 |
| MONITOR CALL | MC | SI | AF |
| MOVE (character) | MVC | SS | 02 |
| MOVE (immediate) | MVI | SI | 92 |
| MOVE (immediate) | MVII | SIY | B352 |
| MOVE INVERSE | MVCIN | SS | B4 |
| MOVE LONG | MVCL | RR C | 0E |
| MOVE LONG EXTENDED | MVCLE | RS C | A8 |
| MOVE LONG UNICODE | MVCLO | RST C | B68B |
| MOVE NUMERICS | MVN | SS | D1 |
| MOVE PAGE | MVPG | RRE C | B254 |
| MOVE STRING | MVST | RRE C | B255 |
| MOVE TO PRIMARY | MVCP | SS C | DA |
| MOVE TO SECONDARY | MVCS | SS C | DB |
| MOVE WITH DESTINATION KEY | MVCDK | SSE | E50F |
| MOVE WITH KEY | MVCK | SS C | D9 |
| MOVE WITH OFFSET | MVO | SS | F1 |
| MOVE WITH SOURCE KEY | MVCSK | SSE | E50E |
| MOVE ZONES | MVZ | SS | D3 |
| MULTIPLY (extended BFP) | MXDBR | RRE | B34C |
| MULTIPLY (extended HFP) | MXR | RR | 26 |
| MULTIPLY (long to extended BFP) | MXDBR | RRE | B307 |
| MULTIPLY (long to extended BFP) | MXDB | RXE | EDD07 |
| MULTIPLY (long to extended HFP) | MXDR | RR | 27 |
| MULTIPLY (long to extended HFP) | MXD | RX | 67 |
| MULTIPLY (long BFP) | MDBR | RRE | B31C |
| MULTIPLY (long BFP) | MDB | RXE | ED1C |

| Instruction | Mnemonic | Format | OpCode |
|---|---|---|---|
| MULTIPLY (long HFP) | MDR | RR | 2C |
| MULTIPLY (long HFP) | MD | RX | 6C |
| MULTIPLY (short to long BFP) | MDBR | RRE | B30C |
| MULTIPLY (short to long BFP) | MDEB | RXE | BDDC |
| MULTIPLY (short to long HFP) | MDER | RR | 3C |
| MULTIPLY (short to long HFP) | MER | RR | 3C |
| MULTIPLY (short to long HFP) | MDE | RX | 7C |
| MULTIPLY (short to long HFP) | MB | RX | 7C |
| MULTIPLY (short BFP) | MEEBR | RRF | B317 |
| MULTIPLY (short BFP) | MEEB | RXE | B017 |
| MULTIPLY (short HFP) | MEER | RRF | B337 |
| MULTIPLY (short HFP) | MEE | RXE | B337 |
| MULTIPLY (64<32) | MR | RR | 1C |
| MULTIPLY (64<32) | M | RX | 5C |
| MULTIPLY AND ADD (long BFP) | MADBR | RRF | B31F |
| MULTIPLY AND ADD (long BFP) | MADB | RXF | B01F |
| MULTIPLY AND ADD (long BFP) | MADR | RRF | B33F |
| MULTIPLY AND ADD (long BFP) | MAD | RXF | B013F |
| MULTIPLY AND ADD (short BFP) | MAEBR | RRF | B30E |
| MULTIPLY AND ADD (short BFP) | MAEB | RXF | B12E |
| MULTIPLY AND ADD (short BFP) | MAER | RRF | B32E |
| MULTIPLY AND ADD (short BFP) | MAE | RXF | B02E |
| MULTIPLY AND SUBTRACT (long BFP) | MSDBR | RRF | B31F |
| MULTIPLY AND SUBTRACT (long BFP) | MSDB | RXF | B01F |
| MULTIPLY AND SUBTRACT (long HFP) | MSDR | RRF | B33F |
| MULTIPLY AND SUBTRACT (long HFP) | MSD | RXF | B013F |
| MULTIPLY AND SUBTRACT (short BFP) | MSEBR | RRF | B30F |
| MULTIPLY AND SUBTRACT (short BFP) | MSEB | RXF | B10F |
| MULTIPLY AND SUBTRACT (short HFP) | MSER | RRF | B32F |
| MULTIPLY AND SUBTRACT (short HFP) | MSE | RXF | B02F |
| MULTIPLY DECIMAL | MP | SS | FC |
| MULTIPLY HALFWORD (32) | MH | RX | 4C |
| MULTIPLY HALFWORD IMMEDIATE (32) | MHI | RI | A7C |
| MULTIPLY HALFWORD IMMEDIATE (64) | MGHI | RI | A7D |
| MULTIPLY LOGICAL (128<64) | MLGR | RRE | B986 |
| MULTIPLY LOGICAL (128<64) | MLG | RXE | B386 |
| MULTIPLY LOGICAL (64<32) | MLR | RRE | B996 |
| MULTIPLY LOGICAL (64<32) | ML | RXE | B396 |
| MULTIPLY SINGLE (32) | MSR | RRE | B252 |
| MULTIPLY SINGLE (32) | MS | RX | 71 |
| MULTIPLY SINGLE (32) | MSY | RXY | B251 |
| MULTIPLY SINGLE (64<32) | MSGFR | RRE | B91C |
| MULTIPLY SINGLE (64<32) | MSGF | RXE | B31C |
| MULTIPLY SINGLE (64) | MSGR | RRE | B90C |
| MULTIPLY SINGLE (64) | MSG | RXY | B30C |

| Instruction | Mnemonic | Format | OpCode |
|---|---|---|---|
| STORE CHARACTER | STCY | RXY | E372 |
| STORE CHARACTERS UNDER MASK (high) | STCMH | RXY | E82C |
| STORE CHARACTERS UNDER MASK (low) | STCM | RS | BE |
| STORE CHARACTERS UNDER MASK (low) | STCMY | RXY | E82D |
| STORE CLOCK | STCK | S C | B205 |
| STORE CLOCK COMPARATOR | STCKC | S | B207 |
| STORE CLOCK EXTENDED | STCKE | S C | B278 |
| STORE CONTROL (32) | STCTL | RS | B6 |
| STORE CONTROL (64) | STCTG | RXY | E825 |
| STORE CPU ADDRESS | STAP | S | B212 |
| STORE CPU ID | STIDF | S | B202 |
| STORE CPU TIMER | STPT | S | B209 |
| STORE FACILITY LIST | STFL | S | B1B1 |
| STORE FPC | STFPC | S | B39C |
| STORE HALFWORD | STH | RX | 40 |
| STORE HALFWORD | STHY | RXY | E370 |
| STORE MULTIPLE (32) | STM | RS | 90 |
| STORE MULTIPLE (32) | STMY | RXY | E890 |
| STORE MULTIPLE (64) | STMG | RSY | E824 |
| STORE MULTIPLE HIGH | STMH | RSY | E926 |
| STORE PAIR TO QUADWORD | STPQ | RXY | E1B8 |
| STORE PREFIX | STPX | S | B211 |
| STORE REAL ADDRESS | STRAG | SSE | B302 |
| STORE REVERSED (16) | STRVH | RXX | E313 |
| STORE REVERSED (32) | STRV | RXY | E33E |
| STORE REVERSED (64) | STRVG | RXY | E32F |
| STORE SUBCHANNEL | STSCH | S C | B234 |
| STORE SYSTEM INFORMATION | STSI | S C | B27D |
| STORE THEN AND SYSTEM MASK | STNSM | SI | AC |
| STORE THEN OR SYSTEM MASK | STOSM | SI | A0 |
| STORE USING REAL ADDRESS (12) | STURA | RRE | B246 |
| STORE USING REAL ADDRESS (64) | STURG | RRE | B325 |
| SUBTRACT (extended BFP) | SXBR | RRE C | B14B |
| SUBTRACT (long BFP) | SDBR | RRE C | B11B |
| SUBTRACT (long BFP) | SDB | RXE C | B01B |
| SUBTRACT (short BFP) | SEBR | RRE C | B30B |
| SUBTRACT (short BFP) | SEB | RXE C | B00B |
| SUBTRACT (32) | SR | RR C | 1B |
| SUBTRACT (32) | S | RX C | 5B |
| SUBTRACT (32) | SY | RXY C | E15B |
| SUBTRACT (64<32) | SGFR | RRE C | B919 |
| SUBTRACT (64<32) | SGF | RXY C | E319 |
| SUBTRACT (64) | SQR | RRE C | B909 |
| SUBTRACT (64) | SQ | RXY C | E309 |

## 25. EBCDIC Table

| Dec | Hex | Code |
|---:|:---:|:---|
| 0 | 00 | NUL |
| 1 | 01 | SOH |
| 2 | 02 | STX |
| 3 | 03 | ETX |
| 4 | 04 | PF |
| 5 | 05 | HT |
| 6 | 06 | LC |
| 7 | 07 | DEL |
| 8 | 08 |  |
| 9 | 09 |  |
| 10 | 0A | SMM |
| 11 | 0B | VT |
| 12 | 0C | FF |
| 13 | 0D | CR |
| 14 | 0E | SO |
| 15 | 0F | SI |
| 16 | 10 | DLE |
| 17 | 11 | DC1 |
| 18 | 12 | DC2 |
| 19 | 13 | TM |
| 20 | 14 | RES |
| 21 | 15 | NL |
| 22 | 16 | BS |
| 23 | 17 | IL |
| 24 | 18 | CAN |
| 25 | 19 | EM |
| 26 | 1A | CC |
| 27 | 1B | CU1 |
| 28 | 1C | IFS |
| 29 | 1D | IGS |
| 30 | 1E | IRS |
| 31 | 1F | IUS |
| 32 | 20 | DS |
| 33 | 21 | SOS |
| 34 | 22 | FS |
| 35 | 23 |  |
| 36 | 24 | BYP |
| 37 | 25 | LF |
| 38 | 26 | PTB |
| 39 | 27 | ESC |
| 40 | 28 |  |
| 41 | 29 |  |
| 42 | 2A | SM |
| 43 | 2B | CU2 |
| 44 | 2C |  |
| 45 | 2D | ENQ |
| 46 | 2E | ACK |
| 47 | 2F | BEL |
| 48 | 30 |  |
| 49 | 31 |  |
| 50 | 32 | SYN |
| 51 | 33 |  |
| 52 | 34 | PN |
| 53 | 35 | RS |
| 54 | 36 | UC |
| 55 | 37 | EOT |
| 56 | 38 |  |
| 57 | 39 |  |
| 58 | 3A |  |
| 59 | 3B | CU3 |
| 60 | 3C | DC4 |
| 61 | 3D | NAK |
| 62 | 3E |  |
| 63 | 3F | SUB |
| 64 | 40 | SP |
| 65 | 41 |  |
| 66 | 42 |  |
| 67 | 43 |  |
| 68 | 44 |  |
| 69 | 45 |  |
| 70 | 46 |  |
| 71 | 47 |  |
| 72 | 48 |  |
| 73 | 49 |  |
| 74 | 4A | ¢ |
| 75 | 4B | . |
| 76 | 4C | < |
| 77 | 4D | ( |
| 78 | 4E | + |
| 79 | 4F | | |
| 80 | 50 | ° |
| 81 | 51 |  |
| 82 | 52 |  |
| 83 | 53 |  |
| 84 | 54 |  |
| 85 | 55 |  |
| 86 | 56 |  |
| 87 | 57 |  |
| 88 | 58 |  |
| 89 | 59 |  |
| 90 | 5A | ! |
| 91 | 5B | $ |
| 92 | 5C | * |
| 93 | 5D | ) |
| 94 | 5E | ? |
| 95 | 5F | ~ |
| 96 | 60 | - |
| 97 | 61 | / |
| 98 | 62 |  |
| 99 | 63 |  |
| 100 | 64 |  |
| 101 | 65 |  |
| 102 | 66 |  |
