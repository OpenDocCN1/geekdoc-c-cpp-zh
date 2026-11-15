+   - Places where you do something out of the ordinary (this will help others to debug the code)
+   - Places where you do something particularly clever (the technique might be useful for others).

Properties of code should only be commented if they are not obvious. By contrast, even seemingly obvious global properties and invariants may need to be made explicit. However, this doesn't have to be through comments. The assert() macro is an excellent executable comment. There are a few guidelines when writing comments:

+   - If your code needs a comment to be understood then you should look for ways to rewrite it so that it’s clearer.
+   - Comments should be comprehensible to other people, not just yourself.
+   - Never write comments that might become incorrect or out of date. An inaccurate or misleading comment is worse than no comment at all.
+   - The size of a comment should be proportional to the size of the code that it refers to.
+   - All comments should be correctly formatted (see Appendix C, C coding standards).

# D.3 Application code documentation

The application code documentation includes:

+   - General comments (see above)
+   - Standard header including the GPL
+   - Documentation of main() function
+   - Structured comments for datatypes
+   - Structured comments for functions.

# D.3.1 Standard header

The application source file must begin with a standard header that includes the General Public License (GPL) statement, which should be used where possible. The header is shown below. The first few lines are specific to each source file, the remainder are constant:

```
/********************************************************************
 * @source ApplicationName
 ***
 * ShortDescription
 ***
 * @author Copyright (C) Year AuthorName
 * @version VersionNumber description of version
 * @modified EditDate EditorName description of edit
 * @@@
 **
 ** This program is free software; you can redistribute it and/or
 ** modify it under the terms of the GNU General Public License
 ** as published by the Free Software Foundation; either version 2
 ** of the License, or (at your option) any later version.
```