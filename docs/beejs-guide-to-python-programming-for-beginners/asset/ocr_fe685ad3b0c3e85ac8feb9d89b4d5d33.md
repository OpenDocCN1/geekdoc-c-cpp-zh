We just have to plan it out.

# Problem-solving step: Devising a Plan

Here’s where we start digging. Start skimming the docs, and take note of anything that sounds remotely like what you want to do. Ignore anything you don’t understand. We want to get information about the contents of the ZIP file.

Keep your eyes peeled for example code.

Let’s skim!

I want you to come up with a list of functions or data in the docs that sound promising. As we learned earlier in this chapter, it can pay to skim the entire document so you don’t miss anything.

Go for it.

I’ll wait.

I’m about to share my list of candidates, now, so run get yours to see how it compares.

Spoiler alert!

Here are things that I thought sounded like they might get me my table of contents for the ZIP file.

Here are the first few I found. As I go, I’m keeping track in my head about which one sounds the most promising:

```
ZipInfo        # Class containing info about a ZIP file member
ZipFile.getinfo()   # Return a ZipInfo object for a file member
ZipFile.infolist()  # Return ZipInfo objects for all file members
ZipFile.namelist()  # Return list of file members by name
```

Let’s keep looking.

```
ZipFile.open()      # Access member of the archive
ZipFile.printdir()  # Print a table of contents to sys.stdout (!!!!)
```

Now that sounds promising.

sys.stdout is a file stream that represents what we call standard output. For now, when you hear stdout or standard output, replace it with "the screen".

So printdir() prints the table of contents to the screen, which sounds exactly like what we’re after.

But let’s keep looking, just to be sure.

```
ZipFile.read()      # Read bytes from a member of the archive
ZipFile.filename    # Name of the ZIP file
```

```
ZipInfo.filename    # Name of an archive member
ZipInfo.date_time   # Modification time of an archive member
ZipInfo.file_size   # File size of an archive member
```

And that’s the end of my skim. How did it compare with your list?

Now… Those last three look interesting. If we could get the ZipInfo object for each item in the archive, we could use those attributes to print out our directory listing.

But that sounds like it’s just going to get us what the printdir() function would do, and printdir() looks easier to use.

Maybe we’re wrong, but let’s pursue printdir(), and if it doesn’t pan out, we can go to Plan B and try the ZipInfo fields.

So… How do we use it? Let’s read the docs again.

```
{ .py } ZipFile.printdir()

Print a table of contents for the archive to sys.stdout.
```