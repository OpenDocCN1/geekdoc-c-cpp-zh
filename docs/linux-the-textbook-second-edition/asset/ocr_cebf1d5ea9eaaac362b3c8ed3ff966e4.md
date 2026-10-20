**Syntax:**
`command << [-] input_marker`
`... input data ...`
`input_marker`

**Purpose:** To execute command with its input coming from the here document—data between the input start and end markers input_marker

The input_marker is a string that you choose to wrap the input data in for command. The closing marker must be on a line by itself and cannot be surrounded by any spaces. The command and variable substitutions are performed before the here document data is directed to stdin of the command. Quotes can be used to prevent these substitutions or to enclose any quotes in the here document. input_marker can be enclosed in quotes to prevent any substitutions in the entire document, as in

```
command <<'Marker'
...
'Marker'
```

A hyphen (-) after << can be used to remove leading tabs (not spaces) from the lines in the here document and the marker that ends the here document. This feature allows the here document and the delimiting marker to conform to the indentation of the script. The following session illustrates this point:

```
while [ ... ]
do
    grep ... <<- DIRECTORY
        John Doe ...
        ...
        Art Pohm ... DIRECTORY
...
done
```

One last, but very important point: output and error redirections of the command that uses the here document must be specified in the command line, not following the marker that ends the here document. The same is true of connecting the standard output of the command with other commands via a pipeline, as shown in the following session. Note that the grep ... <<- DIRECTORY 2> errorfile | sort command can be replaced by (grep ... 2> errorfile | sort) <<- DIRECTORY.

```
while [ ... ]
do
    grep ... <<- DIRECTORY 2> errorfile | sort John Doe ...
        ...
        Art Pohm ... DIRECTORY
        ...
done
```

We can illustrate the use of the here document feature with a simple instance of redirecting stdin of the cat command from the here document. The script in the heredoc_demo file is used to display a message for the user and then send a message to the person whose e-mail address is passed as a command line argument. In the following session, we use two here documents: one begins with << DataTag and ends with DataTag; and the other begins with << WRAPPER and ends with WRAPPER. Note that the Linux mail utility must have been installed before you can use this script.

```
$ cat heredoc_demo
#!/bin/bash

cat << DataTag
This is a simple use of the here document. This data is the
input to the cat command.
```