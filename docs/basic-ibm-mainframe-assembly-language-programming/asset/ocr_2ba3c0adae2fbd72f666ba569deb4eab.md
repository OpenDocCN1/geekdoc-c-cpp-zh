| OpCode | Type | 1st Operand | 2nd Operand | Result | Operation |
|---|---|---|---|---|---|
| L | RX | 32 bit register | 32 bit memory | 32 bit register | 2nd operand is loaded unchanged into the first operand except for the LGFR and LGF where the result is sign extended. |
| LR | RR | 32 bit register | 32 bit register | 32 bit register |  |
| LGR | RRE | 64 bit register | 64 bit register | 64 bit register |  |
| LGFR | RRE | 64 bit register | 32 bit memory | 64 bit register |  |
| LY | RXY | 32 bit register | 16 bit immediate | 32 bit register |  |
| LG | RXY | 64 bit register | 64 bit register | 64 bit register |  |
| LGF | RXY | 64 bit register | 32 bit memory | 64 bit register |  |
| LPQ | RXY | 2 64 bit registers | 128 bit memory | 2 64 bit registers |  |
|  |  |  | Load Address |  |  |
| LA | RX | 64 bit register | 21/31/64 bits | 64 bit register | Address computed by 2nd operand loaded into 1st operand. |
| LAY | RXY | 64 bit register | 21/31/64 bits | 64 bit register |  |
|  |  |  | Load and Test |  |  |
| LTR | RR | 32 bit register | 32 bit register | 32 bit register | 2nd operand loaded into 1st operand to set Condition Code |
| LTGR | RRE | 64 bit register | 64 bit register | 64 bit register |  |
| LTGFR | RRE | 64 bit register | 32 bit register | 64 bit register |  |
|  |  |  | Load Complement |  |  |
| LCR | RR | 32 bit register | 32 bit register | 32 bit register | 2s complement of 2nd operand loaded into 1st operand. |
| LCGR | RRE | 64 bit register | 64 bit register | 64 bit register |  |
| LCGFR | RRE | 64 bit register | 64 bit register | 64 bit register |  |
|  |  |  | Load Multiple |  |  |
| LM | RS | 32 bit register(s) | 32 bit memory word(s) | 32 bit register(s) | One or more registers are loaded from locations in memory. For LM and LMY, the high |
| LMY | RSY | 32 bit register(s) | 32 bit memory word(s) | 32 bit register(s) |  |
| LMG | RSY | 64 bit register(s) | 64 bit memory word(s) | 64 bit register(s) |  |