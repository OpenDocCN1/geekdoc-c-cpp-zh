
| 指令 | 助记符 | 格式 | 操作码 |
|---|---|---|---|
| 将 UTF-16 转换为 UTF-32 | CU24 | RRE C | B9B1 |
| 将 UTF-16 转换为 UTF-8 | CU21 | RRE C | B2A6 |
| 将 UTF-32 转换为 UTF-16 | CU42 | RRE C | B9B3 |
| 将 UTF-32 转换为 UTF-8 | CU41 | RRE C | B9B2 |
| 将 UTF-8 转换为 Unicode | CUTFU | RRE C | B2A7 |
| 将 UTF-8 转换为 UTF-16 | CU12 | RRE C | B2A7 |
| 将 UTF-8 转换为 UTF-32 | CU14 | RRE C | B9B0 |
| 复制访问 | CPIA | RRE | B24D |
| 诊断 |  |  | 93 |
| 除法（扩展 BFP） | DXBR | RRE | B34D |
| 除法（扩展 HFP） | DXR | RRE | B22D |
| 除法（长 BFP） | DDBR | RRE | B31D |
| 除法（长 BFP） | DDB | RXE | E01D |
| 除法（长 HFP） | DDR | RR | 2D |
| 除法（长 HFP） | DD | RX | 6D |
| 除法（短 BFP） | DESBR | RRE | B30D |
| 除法（短 BFP） | DEBR | RXE | E00D |
| 除法（短 HFP） | DER | RR | 1D |
| 除法（短 HFP） | DE | RX | 7D |
| 除法（32<64） | DR | RR | 1D |
| 除法（32<64） | D | RX | 5D |
| 十进制除法 | DP | SS | FD |
| 逻辑除法（32<64） | DLR | RRE | B997 |
| 逻辑除法（32<64） | DL | RXY | E397 |
| 逻辑除法（64<128） | DLGR | RRE | B987 |
| 逻辑除法（64<128） | DLG | RXY | E187 |
| 单精度除法（64<32） | DSGR | RRE | B91D |
| 单精度除法（64<32） | DSG | RXY | E31D |
| 单精度除法（64） | DSGR | RRE | B90D |
| 单精度除法（64） | DSG | RXY | E30D |
| 单精度除法（64） | DSG | RXY | E30D |
| 除法取整（长 BFP） | DIDBR | RRF C | B35B |
| 除法取整（短 BFP） | DIESBR | RRF C | B353 |
| 编辑 | ED | SS C | DE |
| 编辑并标记 | EDMK | SS C | DF |
| 异或（字符） | XC | SS C | D7 |
| 异或（立即数） | XI | SI C | 97 |
| 异或（立即数） | XIY | SIY C | E857 |
| 异或（32） | XR | RR C | 17 |
| 异或（32） | X | RX C | 57 |
| 异或（32） | XY | RXY C | E357 |
| 异或（64） | XGR | RRE C | B992 |
| 异或（64） | XG | RXY C | E382 |
| 执行 | EX | RX | 44 |
| 提取访问 | EAR | RRE | B24F |
| 提取并设置扩展权限 | ESEA | RRE | B99D |
| 提取 EPC | EEPC | RRE | B3C8 |
| 提取主 ASN | EPAR | RRE | B226 |
| 提取主 ASN 及实例 | EPAIR | RRE | B99A |
| 提取 PSW | EPSW | RRE | B98D |
| 提取次要 ASN | ESAR | RRE | B227 |
| 提取次要 ASN 及实例 | ESAIR | RRE | B99B |
| 提取暂存寄存器（32） | EREG | RRE | B249 |
| 提取堆栈寄存器（64） | EREGG | RRE | B90E |
| 提取堆栈状态 | ESTA | RRE C | B24A |
| 停止 SIE 指令 | HSCH | S C | B231 |
| 减半（长 HFP） | HDR | RR | 24 |
| 减半（短 HFP） | HSR | RR | 34 |
| 插入地址空间控制 | IAC | RRE C | B224 |
| 插入字符 | IC | RR | 43 |
| 插入字符 | ICY | RXY | E373 |
| 按掩码插入字符（高） | ICMH | RSY C | EB80 |
| 按掩码插入字符（低） | ICM | RSY C | BF |
| 按掩码插入字符（低） | ICMY | RSY C | EB81 |
| 插入立即数（高高） | IIHH | RI | A50 |
| 插入立即数（高低） | IIHL | RI | A51 |
| 插入立即数（低高） | IILH | RI | A52 |
| 插入立即数（低低） | IILL | RI | A53 |
| 插入程序掩码 | IPM | RRE | B222 |
| 插入 PSW 键 | IPK | S | B208 |
| 插入扩展存储键 | ISKE | RRE | B229 |
| 插入虚拟存储键 | ISVK | RRE | B223 |
| 使 DAT 表项无效 | IDTE | RRE | B98E |
| 使页表项无效 | IPTE | RRE | B221 |
| 加载（扩展） | LXR | RRE | B365 |
| 加载（长） | LDR | RR | 28 |
| 加载（长） | LD | RX | 68 |
| 加载（长） | LDY | RXY | ED65 |
| 加载（短） | LER | RR | 38 |
| 加载（短） | LE | RX | 78 |
| 加载（短） | LEY | RXY | ED64 |
| 加载（32） | LR | RR | 18 |
| 加载（32） | L | RX | 58 |
| 加载（32） | LY | RXY | E358 |
| 加载（64） | LGFR | RRE | B914 |
| 加载（64←32） | LGF | RXY | E314 |
| 加载（64←32） | LGR | RRE | B904 |
| 加载（64） | LG | RXY | E304 |
| 多重加载访问 | LAM | RS | 9A |
| 多重加载访问 | LAMY | RSY | EB9A |
| 加载地址 | LA | RX | 41 |
| 加载地址 | LAY | RXY | E371 |
| 加载扩展地址 | LAE | RX | 51 |
| 加载相对长地址 | LARL | RIL | C000 |
| 加载地址空间参数 | LASP | SSE C | E500 |
| 加载并测试（扩展 BFP） | LTXBR | RRE C | B342 |
| 加载并测试（扩展 HFP） | LTXBR | RRE C | B362 |
| 加载并测试（长 BFP） | LTDBR | RRE C | B312 |
| 加载并测试（长 HFP） | LTOR | RR C | 22 |
| 加载并测试（短 BFP） | LTESBR | RRE C | B302 |
| 加载并测试（短 HFP） | LTER | RR C | 32 |
| 加载并测试（32） | LTR | RR C | 12 |
| 加载并测试（64<->32） | LTOFR | RRE C | B912 |
| 加载并测试（64） | LTGR | RRE C | B902 |
| 加载字节（32） | LB | RXY | E376 |
| 加载字节（64） | LGB | RXY | E377 |
| 加载补码（扩展 BFP） | LCXBR | RRE C | B343 |
| 加载补码（扩展 HFP） | LCXBR | RRE C | B263 |
| 加载补码（长 BFP） | LCDBR | RRE C | B313 |
| 加载补码（长 HFP） | LCDR | RR C | 23 |
| 加载补码（短 BFP） | LCEBR | RRE C | B303 |
| 加载补码（短 HFP） | LCER | RR C | 33 |
| 加载补码（32） | LCR | RR C | 1B3 |
| 加载补码（64<->32） | LCGFR | RRE C | B913 |
| 加载补码（64） | LCGR | RRE C | B003 |
| 加载控制（32） | LCTL | RS | 07 |
| 加载控制（64） | LCTLG | RSY | E92F |
| 加载 FP 整数（扩展 BFP） | FIXBR | RRF | D247 |
| 加载 FP 整数（扩展 HFP） | FIXBR | RRE | D267 |
| 加载 FP 整数（长 BFP） | FIDBR | RRF | D35F |
| 加载 FP 整数（长 HFP） | FIDBR | RRE | B37F |
| 加载 FP 整数（短 BFP） | FIEDBR | RRF | B357 |
| 加载 FP 整数（短 HFP） | FIER | RRE | B377 |
| 加载 FPC | LFPC | S | B290 |
| 加载半字（32） | LH | RX | 48 |
| 加载半字（32） | LHY | RXY | E378 |
| 加载半字（64） | LGH | RXY | E315 |
| 加载半字立即数（32） | LHI | RI | A78 |
| 加载半字立即数（64） | LGHI | RI | A79 |
| 加载扩展（长到扩展 BFP） | LXDBR | RRE | B305 |
| 加载扩展（长到扩展 BFP） | LXDB | RXE | E005 |
| 加载扩展（长到扩展 HFP） | LXDR | RRE | B325 |
| 加载扩展（长到扩展 HFP） | LXD | RXE | E025 |
| 加载扩展（短到扩展 BFP） | LXEBR | RRE | B306 |
| 加载扩展（短到扩展 BFP） | LXEB | RXE | E006 |
| 加载扩展（短到扩展 HFP） | LXER | RRE | B326 |
| 加载扩展（短到扩展 HFP） | LXE | RXE | E026 |
| 加载扩展（短到长 BFP） | LDER | RRE | B104 |
| 加载扩展（短到长 BFP） | LDEB | RRE | E004 |
| 加载扩展（短到长 HFP） | LDER | RRE | B124 |
| 加载扩展（短到长 HFP） | LDE | RXE | E024 |
| 逻辑加载（64<32） | LLGFR | RRF | B916 |
| 逻辑加载（64<32） | LLGPR | RXY | E316 |
| 逻辑加载字符 | LLGC | RXY | E390 |
| 逻辑加载半字 | LLGH | RXY | E391 |
| 逻辑加载立即数（高高） | LLIHH | RI | A5C |
| 逻辑加载立即数（高低） | LLIHL | RI | A5D |
| 逻辑加载立即数（低高） | LLILH | RI | A5E |
| 逻辑加载立即数（低低） | LLILL | RI | A5F |
| 加载逻辑三十一位 | LLOTR | RRE | B917 |
| 加载逻辑三十一位 | LLOT | RXY | E317 |
| 多重加载（32） | LM | RS | 98 |
| 多重加载（32） | LMY | RSY | E898 |
| 多重加载（64） | LMG | RSY | EB04 |
| 不相交多重加载 | LMD | SS | EF |
| 高多重加载 | LMH | RSY | E896 |
| 加载负数（扩展 BFP） | LNXR | RRE C | B341 |
| 加载负数（扩展 HFP） | LNXR | RRE C | B361 |
| 加载负数（长 BFP） | LNDBR | RRE C | B311 |
| 加载负数（长 HFP） | LNDR | RR C | 21 |
| 加载负数（短 BFP） | LNEBR | RRE C | B301 |
| 加载负数（短 HFP） | LNER | RR C | 31 |
| 加载负数（32） | LNR | RR C | 11 |
| 加载负数（64<32） | LNGFR | RRE C | B911 |
| 加载负数（64） | LNGR | RRE C | B901 |
| 从四字加载对 | LPQ | RXY | B3F0 |
| 加载正数（扩展 BFP） | LPXBR | RRE C | B340 |
| 加载正数（扩展 HFP） | LPXFR | RRE C | B360 |
| 加载正数（长 BFP） | LPDBR | RRE C | B310 |
| 加载正数（长 HFP） | LPDR | RR C | 20 |
| 加载正数（短 BFP） | LPEBR | RRE C | B300 |
| 加载正数（短 HFP） | LPER | RR C | 30 |
| 加载正数（32） | LPR | RR C | 10 |
| 加载正数（64<32） | LPGFR | RRE C | B910 |
| 加载正数（64） | LPGR | RRE C | B900 |
| 加载 PSW | LPSW | S | 82 |
| 加载扩展 PSW | LPSWE | S | B2B2 |
| 加载实地址（32） | LRA | RX C | B1 |
| 加载实地址（32） | LRA | RXY C | B113 |
| 加载实地址（64） | LRAG | RXY C | B303 |
| 加载反转（16） | LVRH | SXY | E11F |
