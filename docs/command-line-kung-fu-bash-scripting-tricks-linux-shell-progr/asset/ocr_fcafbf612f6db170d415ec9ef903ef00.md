# Reset Your Terminal Emulator Display

```
```text
$ reset
```
```

Displaying binary files to your screen can cause your terminal to become unusable. To attempt to recover, type “reset” and press enter. Your terminal may be in such a state that you won't be able to see what you're typing, but you shell will still accept the input.

```
```text
$ cat blue-train.mp3
F...A....h...reset
$ 
```
```

# Search Wikipedia from the Command Line

```
```text
$ dig +short txt <string>.wp.dg.cx
$ host -t txt <string>.wp.dg.cx
```
```

If you need to quickly look up some information on a subject, you can search wikipedia using DNS. The name server returns wikipedia article summaries as TXT records.

```
```text
$ dig +short txt linux.wp.dg.cx
"Linux is a Unix-like computer operating system
assembled under the model of free and open source
software development and distribution. The defining
component of Linux is the Linux kernel, an operating
system kernel first released 5 October 1991 by Linus
Torvalds, http://en.wikipedia.org/wiki/Linux"
$ host -t txt bash_shell.wp.dg.cx
bash_shell.wp.dg.cx descriptive text "Bash is a Unix
```
```