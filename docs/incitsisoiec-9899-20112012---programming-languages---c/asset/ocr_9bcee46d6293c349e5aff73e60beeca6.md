A multibyte character set may have a state-dependent encoding, wherein each sequence of multibyte characters begins in an initial shift state and enters other locale-specific shift states when specific multibyte characters are encountered in the sequence. In the initial shift state, all single-byte characters retain their usual interpretation and do not alter the shift state. The interpretation for subsequent bytes in the sequence is a function of the current shift state.

A byte with all bits zero shall be interpreted as a null character independent of shift state. Such a byte shall not occur as part of any multibyte character.

For source files, the following shall hold:

+   - An identifier, comment, string literal, character constant, or header name shall begin and end in the initial shift state.

+   - An identifier, comment, string literal, character constant, or header name shall consist of a valid multibyte characters.

# 5.2.2 Character display semantics

The active position is location on a display device where the next character output by the fputc function would appear. The intent of writing a printing character (as defined by the isprint function) to a display device is to display a graphic representation of that at the active position and advance the active position to the next position on the current line. The direction of writing is locale-specific. If the active position is at the final position of a line (if there is one), the behavior of the display device is unspecified.

Alphabetic escape sequences representing nongraphic characters in the execution character set are intended to produce actions on display devices as:

+   - \a (alert) Produces an audible or visible alert without changing the active position.

+   - \b (backspace) Moves the active position to the previous position on the current line. If the active position is at the initial position of a line, the behavior of the display device is unspecified.

+   - \f (form feed) Moves the active position to the initial position at the start of the next logical page.

+   - \n (new line) Moves the active position to the initial position of the next line.

+   - \r (carriage return) Moves the active position to the initial position of the current line.

+   - \t (horizontal tab) Moves the active position to the next horizontal tabulation position on the current line. If the active position is at or past the last defined horizontal tabulation position, the behavior of the display device is unspecified.

+   - \v (vertical tab) Moves the active position to the initial position of the next vertical tabulation position. If the active position is at or past the last defined vertical