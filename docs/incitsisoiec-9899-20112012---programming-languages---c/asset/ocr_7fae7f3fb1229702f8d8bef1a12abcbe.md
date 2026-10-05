# # Annex J
(informative)
Portability issues

This annex collects some information about portability that appears in this International Standard.

# ## J.1 Unspecified behavior

The following are unspecified:

+   - The manner and timing of static initialization (5.1.2).
- The termination status returned to the hosted environment if the return type of **main** is not compatible with int (5.1.2.2.3).
- The values of objects that are neither lock-free atomic objects nor of type **volatile sig_atomic_t** and the state of the floating-point environment, when the processing of the abstract machine is interrupted by receipt of a signal (5.1.2.3).
- The behavior of the display device if a printing character is written when the active position is at the final position of a line (5.2.2).
- The behavior of the display device if a backspace character is written when the active position is at the initial position of a line (5.2.2).
- The behavior of the display device if a horizontal tab character is written when the active position is at or past the last defined horizontal tabulation position (5.2.2).
- The behavior of the display device if a vertical tab character is written when the active position is at or past the last defined vertical tabulation position (5.2.2).
- How an extended source character that does not correspond to a universal character name counts toward the significant initial characters in an external identifier (5.2.4.1).
- Many aspects of the representations of types (6.2.6).
- The value of padding bytes when storing values in structures or unions (6.2.6.1).
- The values of bytes that correspond to union members other than the one stored into (6.2.6.1).
- The representation used when storing a value in an object that has more than one object representation for that value (6.2.6.1).
- The values of any padding bits in integer representations (6.2.6.2).
- Whether certain operators can generate zeros and whether a negative zero becomes a normal zero stored in an object (6.2.6.2).