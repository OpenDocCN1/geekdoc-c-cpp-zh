# ## 10.5 Iterating Through Files

I've talked about iteration before and we'll talk about it in later chapters. Iteration is simply performing an operation on data in a sequential fashion, usually through the *for* loop. With files, iteration can be used to read the information in the file and process it in an orderly manner. It also limits the amount of memory taken up when a file is read, which not only reduces system resource use but can also improve performance.

Say you have a file of tabular information, e.g. a payroll file. You want to read the file and print out each line, with “pretty” formatting so it is easy to read. Here's an example of how to do that. (We're assuming that the information has already been put in the file. Also, the normal Python interpreter prompts aren't visible because you would actually write this as a full-blown program, as we'll see later. Finally, the print statements are not compatible with Python 3.x.)

> Listing 10.5: Inputting tabular data

```
	try:
		file = open("payroll", "r")
	except IOError:
		print "The file doesn't exist. Check filename."

	individuals = file.readlines()
	print "Account".ljust(10), #comma prevents newline
	print "Name".ljust(10),
	print "Amount".rjust(10)
	for record in individuals:
		columns = record.split()
		print columns[0].ljust(10)
		print columns[1].ljust(10)
		print columns[2].rjust(10)
	file.close()
```

Here is how the output should be displayed on the screen (or on paper if sent to a printer).