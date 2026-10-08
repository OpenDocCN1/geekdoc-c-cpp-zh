# Embedded C Coding Standard

# 6 Procedure Rules

# 6.1 Naming Conventions

Rules:

+   a. No procedure shall have a name that is a keyword of any standard version of the C or C++ programming language. Restricted names include interrupt, inline, class, true, false, public, private, friend, and many others.

+   b. No procedure shall have a name that overlaps a function in the C Standard Library. Examples of such names include strlen, atoi, and memset.

+   c. No procedure shall have a name that begins with an underscore.

+   d. No procedure name shall be longer than 31 characters.

+   e. No function name shall contain any uppercase letters.

+   f. No macro name shall contain any lowercase letters.

+   g. Underscores shall be used to separate words in procedure names.

+   h. Each procedure's name should be descriptive of its purpose. Note that procedures benefit from the use of verbs in their names (e.g., adc_read()); this “noun-verb” word ordering is recommended. Alternatively, procedures may be named according to the question they answer (e.g., led_is_on()).

+   i. The names of all public functions shall be prefixed by their module name and an underscore (e.g., sensor_read()).

**Example:** Append D.

**Reasoning:** Good function names make reviewing and maintaining code easier (and thus cheaper). The data (variables) in programs are nouns. Functions manipulate data and are thus verbs. The use of module prefixes is in keeping with the important goal of encapsulation and helps avoid procedure name overlaps.

![](bbox=[0.793, 0.213, 0.856, 0.263])

![](bbox=[0.793, 0.323, 0.856, 0.373])