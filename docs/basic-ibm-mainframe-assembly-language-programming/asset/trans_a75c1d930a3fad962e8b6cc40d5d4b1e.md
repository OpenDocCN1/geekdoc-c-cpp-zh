
| 指令 | 助记符 | 格式 | 操作码 |
|---|---|---|---|
| 反向加载 (32) | LRVR | RRE | B91F |
| 反向加载 (32) | LRV | RXV | B31B |
| 反向加载 (64) | LRVGR | RRE | B90F |
| 反向加载 (64) | LRVG | RXV | B30F |
| 舍入加载（扩展到长 BFP） | LXDBR | RRE | B345 |
| 舍入加载（扩展到长 HFP） | LDXR | RR | 25 |
| 舍入加载（扩展到长 HFP） | LDRR | RR | 25 |
| 舍入加载（扩展到短 BFP） | LXEBR | RRE | B346 |
| 舍入加载（扩展到短 HFP） | LEXR | RRE | B366 |
| 舍入加载（长到短 BFP） | LEDBR | RRE | B344 |
| 舍入加载（长到短 HFP） | LEDR | RR | 35 |
| 舍入加载（长到短 HFP） | LRER | RR | 35 |
| 使用实地址加载 (32) | LURA | RRE | B24B |
| 使用实地址加载 (64) | LURAG | RRE | B905 |
| 装零（扩展） | LZXR | RRE | B376 |
| 装零（长） | LZDR | RRE | B375 |
| 装零（短） | LZSR | RRE | B374 |
| 修改堆栈状态 | MSTA | RRE | B247 |
| 修改子通道 | MSCH | S C | B332 |
| 监视器调用 | MC | SI | AF |
| 移动（字符） | MVC | SS | 02 |
| 移动（立即） | MVI | SI | 92 |
| 移动（立即） | MVII | SIY | B352 |
| 逆向移动 | MVCIN | SS | B4 |
| 长移动 | MVCL | RR C | 0E |
| 扩展长移动 | MVCLE | RS C | A8 |
| Unicode 长移动 | MVCLO | RST C | B68B |
| 移动数字 | MVN | SS | D1 |
| 移动页 | MVPG | RRE C | B254 |
| 移动字符串 | MVST | RRE C | B255 |
| 移动到主存储 | MVCP | SS C | DA |
| 移动到次存储 | MVCS | SS C | DB |
| 带目标键移动 | MVCDK | SSE | E50F |
| 带键移动 | MVCK | SS C | D9 |
| 带偏移移动 | MVO | SS | F1 |
| 带源键移动 | MVCSK | SSE | E50E |
| 移动区域 | MVZ | SS | D3 |
| 乘法（扩展 BFP） | MXDBR | RRE | B34C |
| 乘法（扩展 HFP） | MXR | RR | 26 |
| 乘法（长到扩展 BFP） | MXDBR | RRE | B307 |
| 乘法（长到扩展 BFP） | MXDB | RXE | EDD07 |
| 乘法（长到扩展 HFP） | MXDR | RR | 27 |
| 乘法（长到扩展 HFP） | MXD | RX | 67 |
| 乘法（长 BFP） | MDBR | RRE | B31C |
| 乘法（长 BFP） | MDB | RXE | ED1C |

| 指令 | 助记符 | 格式 | 操作码 |
|---|---|---|---|
| 乘法（长 HFP） | MDR | RR | 2C |
| 乘法（长 HFP） | MD | RX | 6C |
| 乘法（短到长 BFP） | MDBR | RRE | B30C |
| 乘法（短到长 BFP） | MDEB | RXE | BDDC |
| 乘法（短到长 HFP） | MDER | RR | 3C |
| 乘法（短到长 HFP） | MER | RR | 3C |
| 乘法（短到长 HFP） | MDE | RX | 7C |
| 乘法（短到长 HFP） | MB | RX | 7C |
| 乘法（短 BFP） | MEEBR | RRF | B317 |
| 乘法（短 BFP） | MEEB | RXE | B017 |
| 乘法（短 HFP） | MEER | RRF | B337 |
| 乘法（短 HFP） | MEE | RXE | B337 |
| 乘法（64<32） | MR | RR | 1C |
| 乘法（64<32） | M | RX | 5C |
| 乘加（长 BFP） | MADBR | RRF | B31F |
| 乘加（长 BFP） | MADB | RXF | B01F |
| 乘加（长 BFP） | MADR | RRF | B33F |
| 乘加（长 BFP） | MAD | RXF | B013F |
| 乘加（短 BFP） | MAEBR | RRF | B30E |
| 乘加（短 BFP） | MAEB | RXF | B12E |
| 乘加（短 BFP） | MAER | RRF | B32E |
| 乘加（短 BFP） | MAE | RXF | B02E |
| 乘减（长 BFP） | MSDBR | RRF | B31F |
| 乘减（长 BFP） | MSDB | RXF | B01F |
| 乘减（长 HFP） | MSDR | RRF | B33F |
| 乘减（长 HFP） | MSD | RXF | B013F |
| 乘减（短 BFP） | MSEBR | RRF | B30F |
| 乘减（短 BFP） | MSEB | RXF | B10F |
| 乘减（短 HFP） | MSER | RRF | B32F |
| 乘减（短 HFP） | MSE | RXF | B02F |
| 十进制乘法 | MP | SS | FC |
| 半字乘法 (32) | MH | RX | 4C |
| 半字立即乘法 (32) | MHI | RI | A7C |
| 半字立即乘法 (64) | MGHI | RI | A7D |
| 逻辑乘法 (128<64) | MLGR | RRE | B986 |
| 逻辑乘法 (128<64) | MLG | RXE | B386 |
| 逻辑乘法 (64<32) | MLR | RRE | B996 |
| 逻辑乘法 (64<32) | ML | RXE | B396 |
| 单精度乘法 (32) | MSR | RRE | B252 |
| 单精度乘法 (32) | MS | RX | 71 |
| 单精度乘法 (32) | MSY | RXY | B251 |
| 单精度乘法 (64<32) | MSGFR | RRE | B91C |
| 单精度乘法 (64<32) | MSGF | RXE | B31C |
| 单精度乘法 (64) | MSGR | RRE | B90C |
| 单精度乘法 (64) | MSG | RXY | B30C |

| 指令 | 助记符 | 格式 | 操作码 |
|---|---|---|---|
| 存储字符 | STCY | RXY | E372 |
| 按掩码存储字符（高） | STCMH | RXY | E82C |
| 按掩码存储字符（低） | STCM | RS | BE |
| 按掩码存储字符（低） | STCMY | RXY | E82D |
| 存储时钟 | STCK | S C | B205 |
| 存储时钟比较器 | STCKC | S | B207 |
| 扩展存储时钟 | STCKE | S C | B278 |
| 存储控制 (32) | STCTL | RS | B6 |
| 存储控制 (64) | STCTG | RXY | E825 |
| 存储 CPU 地址 | STAP | S | B212 |
| 存储 CPU ID | STIDF | S | B202 |
| 存储 CPU 定时器 | STPT | S | B209 |
| 存储设施列表 | STFL | S | B1B1 |
| 存储 FPC | STFPC | S | B39C |
| 存储半字 | STH | RX | 40 |
| 存储半字 | STHY | RXY | E370 |
| 存储多个 (32) | STM | RS | 90 |
| 存储多个 (32) | STMY | RXY | E890 |
| 存储多个 (64) | STMG | RSY | E824 |
| 高位存储多个 | STMH | RSY | E926 |
| 存储对到四字 | STPQ | RXY | E1B8 |
| 存储前缀 | STPX | S | B211 |
| 存储实地址 | STRAG | SSE | B302 |
| 反向存储 (16) | STRVH | RXX | E313 |
| 反向存储 (32) | STRV | RXY | E33E |
| 反向存储 (64) | STRVG | RXY | E32F |
| 存储子通道 | STSCH | S C | B234 |
| 存储系统信息 | STSI | S C | B27D |
| 存储后与系统掩码 | STNSM | SI | AC |
| 存储后或系统掩码 | STOSM | SI | A0 |
| 使用实地址存储 (12) | STURA | RRE | B246 |
| 使用实地址存储 (64) | STURG | RRE | B325 |
| 减法（扩展 BFP） | SXBR | RRE C | B14B |
| 减法（长 BFP） | SDBR | RRE C | B11B |
| 减法（长 BFP） | SDB | RXE C | B01B |
| 减法（短 BFP） | SEBR | RRE C | B30B |
| 减法（短 BFP） | SEB | RXE C | B00B |
| 减法 (32) | SR | RR C | 1B |
| 减法 (32) | S | RX C | 5B |
| 减法 (32) | SY | RXY C | E15B |
| 减法 (64<32) | SGFR | RRE C | B919 |
| 减法 (64<32) | SGF | RXY C | E319 |
| 减法 (64) | SQR | RRE C | B909 |
| 减法 (64) | SQ | RXY C | E309 |

## 25. EBCDIC 表

| 十进制 | 十六进制 | 代码 |
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
