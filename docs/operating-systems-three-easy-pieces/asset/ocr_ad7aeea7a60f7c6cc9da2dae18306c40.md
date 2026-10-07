# MECHANISM: ADDRESS TRANSLATION

| OS @ run (kernel mode) | Hardware | Program (user mode) |

To start process A: allocate entry in process table alloc memory for process set base/bound registers return-from-trap (into A)

restore registers of A move to user mode jump to A's (initial) PC

Process A runs Fetch instruction

translate virtual address perform fetch

Execute instruction

if explicit load/store: ensure address is legal translate virtual address perform load/store

(A runs...)

Timer interrupt move to kernel mode jump to handler

Handle timer decide: stop A, run B call switch() routine save regs(A) to proc-struct(A) (including base/bounds) restore regs(B) from proc-struct(B) (including base/bounds) return-from-trap (into B)

restore registers of B move to user mode jump to B's PC

Process B runs Execute bad load

Load is out-of-bounds: move to kernel mode jump to trap handler

Handle the trap decide to kill process B deallocate B's memory free B's entry in process table

Figure 15.6: Limited Direct Execution (Dynamic Relocation) @ Runtime