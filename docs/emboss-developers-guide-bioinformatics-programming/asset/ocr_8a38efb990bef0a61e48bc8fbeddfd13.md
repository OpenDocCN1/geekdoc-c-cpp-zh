```
set path= (/home/auser/emboss/emboss/emboss $path)
rehash
```

Or if you are using an sh style shell then type the following commands:

```
export PATH=/home/auser/emboss/emboss/emboss:$PATH
```

If, however, you installed using make install rather than just a make then the commands will be different (you must set the PATH to where you installed the executables). For a csh style shell:

```
set path= (/home/auser/emboss/bin $path)
rehash
```

For a sh style shell:

```
export PATH=/home/auser/emboss/bin:$PATH
```

# 1.2.6 Testing all is well

To test all is well with your installation you can run:

```
embossversion
```

and check that the EMBOSS version number is reported.

You could also try using the seqret application to retrieve some sequences from the test databases that come bundled with the EMBOSS distribution. Before you can do this however you need to set up the databases for use with EMBOSS.

# 1.2.7 Database setup

> **Note**
> Database setup is covered in the *EMBOSS Administrator's Guide*; only the bare essentials are covered below.

The EMBOSS distribution comes bundled with some test databases. They are, for example, located in: