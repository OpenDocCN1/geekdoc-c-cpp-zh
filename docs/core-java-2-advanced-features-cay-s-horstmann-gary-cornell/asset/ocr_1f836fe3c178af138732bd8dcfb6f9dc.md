# java.util.regex.Pattern 1.4 (Continued)

+   - Matcher matcher(CharSequence input)
+     returns a matcher object that you can use to locate the matches of the pattern in the input.
+   - String[] split(CharSequence input)
+   - String[] split(CharSequence input, int limit)
+   - Stream<String> splitAsStream(CharSequence input) 8
+     splits the input string into tokens, where the pattern specifies the form of the delimiters. Returns an array or stream of tokens. The delimiters are not part of the tokens.
+     *Parameters:* input The string to be split into tokens
+     limit The maximum number of strings to produce. If limit - 1 matching delimiters have been found, then the last entry of the returned array contains the remaining unsplit input. If limit is ≤ 0, then the entire input is split. If limit is 0, then trailing empty strings are not placed in the returned array.

# java.util.regex.Matcher 1.4

+   - boolean matches()
+     returns true if the input matches the pattern.
+   - boolean lookingAt()
+     returns true if the beginning of the input matches the pattern.
+   - boolean find()
+   - boolean find(int start)
+     attempts to find the next match and returns true if another match is found.
+     *Parameters:* start The index at which to start searching
+   - int start()
+   - int end()
+     returns the start or past-the-end position of the current match.
+   - String group()
+     returns the current match.