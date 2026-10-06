We'll print out the string from $text so that we can see exactly what we'll be matching against, and then proceed onto our regex.

To not unfamiliar with regular expressions, with this line:
$text~ m/ ((0-9a-f]{2} [-]){5} ([0-9a-f]{2})/i;

might seem a bit confusing and largely like random gibberish characters. The m before the first forward slash / is the match operator. The characters between the two forward slashes are actually the pattern we use to find the MAC address that is part of the line stored in $text. In the pattern, we have two sections: the first deals with the first five bytes of the MAC address, and the second deals with the last byte.

The first section, ([0-9a-f]{2} [-]){5}, says to look for a pattern that starts with two characters in the range of 0-9 or a-f, with these followed by a colon : a dash -, and to look for repetitions of this pattern, accounting for the first five bytes of our MAC address. The sixth byte does not end in a colon, so we need to change the pattern slightly. For the sixth byte, we match against [0-9a-f]{2}, meaning two characters in the range of 0-9 or a-f.

We wrap the entire set of the pattern in parentheses () and add the /i regex, to make our pattern case-insensitive. This is not a completely perfect regex, but it will match properly the vast majority of the time. We might find a corner case where we have a similar pattern that mixes colons and dashes, for instance, and accidentally match, but this will likely be a corner case for most applications to which we would put this type of script.

The last line of our script, print "the mac is %s\n", prints the MAC address we found using our regex. This line is relatively clear, other than the use of a special variable $, which will contain the string that was found in the most recent pattern match performed in our script, namely our MAC address.

There are a number of other character designators for matching patterns that we use in our regexes. Table 3.2 lists a few of them.

# Table 3.2

# Regex Pattern Characters