# Branch if Minus or Plus – SREG N Flag

# BRMI (Branch if Minus)

Equivalent to BRBS SREG_N,k where k is the constant relative address to branch to.

# BRPL (Branch if Plus)

Equivalent to BRBC SREG_N,k where k is the constant relative address to branch to.

# Branch if Greater or Equal, or Less Than Signed – SREG S Flag

# BRGE (Branch if Greater or Equal (Signed))

Equivalent to BRBC SREG_S,k where k is the constant relative address to branch to.

# BRLT (Branch if Less Than (Signed))

Equivalent to BRBS SREG_S,k where k is the constant relative address to branch to.

# Branch if Half Carry Flag Set or Cleared – SREG H Flag

# BRHS (Branch if Half Carry Flag is Set)

Equivalent to BRBS SREG_H,k where k is the constant relative address to branch to.

# BRHC (Branch if Half Carry Flag is Cleared)

Equivalent to BRBC SREG_H,k where k is the constant relative address to branch to.

# Branch if T Bit Set or Cleared – SREG T Flag

# BRTS (Branch if the T Bit is Set)

Equivalent to BRBS SREG_T,k where k is the constant relative address to branch to.

# BRTC (Branch if the T Bit is Cleared)

Equivalent to BRBC SREG_T,k where k is the constant relative address to branch to.

# Branch if Overflow Flag Set or Cleared – SREG V Flag

# BRVS (Branch if Overflow Set)

Equivalent to BRBS SREG_V,k where k is the constant relative address to branch to.

# BRVC (Branch if Overflow Cleared)

Equivalent to BRBC SREG_V,k where k is the constant relative address to branch to.

# Branch if Interrupt Enabled or Disabled – SREG I Flag

# BRIE (Branch if Global Interrupt is Enabled)

Equivalent to BRBS SREG_I,k where k is the constant relative address to branch to.

# BRID (Branch if Global Interrupt is Disabled)

Equivalent to BRBC SREG_I,k where k is the constant relative address to branch to.