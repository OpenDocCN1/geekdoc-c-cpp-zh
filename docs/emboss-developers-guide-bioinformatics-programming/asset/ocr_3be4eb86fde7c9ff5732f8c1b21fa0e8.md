# 7.2.1.13 FC [<=] NumberLines

For the test to pass, the number of lines (NumberLines) may be checked as follows:

+   = There must be NumberLines lines
+   < There must be more than NumberLines lines
+   > There must be less than NumberLines lines

# 7.2.1.14 FP count / regexp /

For the test to pass the Perl regular expression regexp given between forward-slashes must be found in the preceding FI file. The expression may be preceded by an optional integer (count) to check the exact number of the pattern.

This record can be used to check stderr (which often contains the user prompts) for the absence of exception messages (warning, error or fatal).

# 7.2.1.15 FZ [<=] FileSize

For the test to pass, the size (FileSize) of the file may be checked as follows:

+   = File must be exactly FileSize
+   < File must be bigger than FileSize
+   > File must be smaller than FileSize

There is an implicit test that stdout and stderr must be of size zero unless otherwise stated.

# 7.2.1.16 IC text

This is annotation (text) for the input and is used by makeexample.pl when creating the HTML documentation files. The information is not used in QA testing.

# 7.2.1.17 IN UserInput

The value UserInput will be used. If there is nothing on the line then an empty line is input to the application which will use the default value for the option (if defined). Care is needed where options are conditionally prompted for.

# 7.2.1.18 OC text

This is annotation (text) for the output and is used by makeexample.pl when creating the HTML documentation files. The information is not used in QA testing.

# 7.2.1.19 PP command

This is a command executed (by /bin/sh) before the test is run. Each PP line defines a single command: long commands may not be concatenated over multiple lines as is allowed for the CL records.