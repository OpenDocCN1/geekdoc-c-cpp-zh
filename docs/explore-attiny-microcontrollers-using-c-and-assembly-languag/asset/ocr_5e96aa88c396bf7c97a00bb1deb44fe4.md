# Calculating the Maximum Delay Time of the Subroutine....................238

# Posing Value Limits in Assembly Language....................................240

# Number Size Limits in the Assembler Program...............................243

# Solution to Flagging Out of Range Upper Values...........................246

# Flagging Out of Range High and Low Values.................................247

# 10.2.4 Passing a Value to a Subroutine.....................................251

# 10.2.4.1 Simplest Way to Pass a Value......................................251

# 10.2.4.2 Improved Way to Pass a Value.....................................253

# **10.3 Calling an Assembly Subroutine from C Code..........................261**

# 10.3.1 Passing a Value to an Assembly Subroutine from C..................261

# 10.3.1.1 Testing the wait_ms_c Project Code..............................263

# 10.3.1.2 How the wait_ms_c Project Code Works............................264

# 10.3.2 Returning a Value from an Assembly Subroutine in C................266

# **10.4 Polled Timer Delay....................................................268**

# 10.4.1 Timer/Counter0 Registers............................................268

# 10.4.1.1 Timer/Counter0 Register Addresses...............................269

# 10.4.1.2 Using Counter/Timer0 as a Timer.................................270

# 10.4.2 Polled Timer Assembly Program.....................................271

# 10.4.2.1 The IFNDF Directive...............................................271

# 10.4.2.2 Left Shift Operator...............................................272

# 10.4.2.3 Register Write or Read-Modify-Write.............................273

# 10.4.2.4 Initializing Timer 0..............................................273

# 10.4.2.5 Polling Timer 0...................................................275

# 10.4.2.6 Running the Code in the Simulator...............................276

# 10.4.3 Polled Timer C Program..............................................276

# **10.5 Timer Interrupt Delay.................................................277**

# 10.5.1 How Interrupt Work..................................................278

# 10.5.2 The Interrupt Vector Table..........................................278

# 10.5.3 Assembly Program Timer Interrupt....................................279

# 10.5.3.1 ATtiny13(A) Timer Interrupt Project...............................279

# The Interrupt Vector Table...................................................280

# Main Program Code............................................................282

# Interrupt Service Routine Code.............................................282

# Running the Timer Interrupt Code...........................................283

# 10.5.3.2 ATtiny25/45/85 Timer Interrupt Project............................283

# 10.5.3.3 Universal Timer Interrupt Project.................................285