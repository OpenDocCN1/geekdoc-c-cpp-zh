# # Sentences Containing Specific Terms

An array of strings can be searched for sentences that contain given words. This code sample prints two of the sentences:

```
$TestArray[0] = "The earth is alive with care.";
$TestArray[1] = "The earth is teeming with care.";
$TestArray[2] = "The earth is pulsating with care.";

for($iv = 0; $iv < 3; $iv++) {
    if($TestArray[$iv] =~ m/(alive|pulsating)/) {
        print "$NL Found $TestArray[$iv] $NL";
    }
}
```

Here is the output of Example 4 in Listing15_07:
Found The earth is alive with care.
Found The earth is pulsating with care.

Note that with the use of the group, the match is returned as soon as the first match occurs. In the following, the match is with c, not with the whole word:
$Word = "cats";
print "$NL $Word (cat) found." if($Word =~ m/(c|ca|cat|cats)/);

Here is the output of Example 5 in Listing15_07:
cats (cat) found.

# # Conclusion

This chapter provided what should be regarded as an introduction to regular expressions. Since every operating system and many programming languages (Java, JavaScript, and C#, to name a few) offer some form of regular expression capability, your work with Perl regular expressions can prove useful regardless of what direction you take as a programmer. Likewise, regular expressions prove essential to working with Unix/Linux systems.

Generally, this chapter has emphasized the basics of working with matching and substitution as they might be applied to standard programming activities restricted to making selection statements or controlling repetition statements. You can easily extend this beginning in many directions, including the creation of files that help you work with file IO.