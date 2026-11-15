```
fileout_name = ajStrNewC("outfile");
buffin_name = ajStrNewC("bufffile");
dirin_name = ajDirNewPath("./dirin");
dirout_name = ajDirNewPath("./dirout");

filein = ajFileNewInNameC("infile");
fileout = ajOutfileNewNameS(fileoutname);
datain = ajDatafileNewInNameC("datafile");
buffin = ajFilebuffNewNameS(buffname);
dirin = ajDirNewPath(dirin_name);
dirout = ajDiroutNewPath(dirout_name);

/* The objects are instantiated and ready for use */
```

# 6.14.7.2 Default object destruction

You must free the memory for any object once you are finished with them. All the default destructor functions take the address of the object being freed:

```
/* File object destructor */
void ajFileClose (AjPFile* Pfile);

/* Output file object destructor */
void ajOutfileClose (AjPOutfile* Pfile);

/* Buffered file object constructor */
void ajFilebuffDel (AjPFilebuff* Pfile);

/* Directory destructor */
void ajDirDel (AjPDir* Pdir);
```

The destructor functions close the file (if appropriate) and free memory for the file or directory object. Following from the example above:

```
ajFileClose(&filein);
ajOutfileClose(&fileout);
ajFilebuffDel(&buffin);
ajDirDel(&dirin);
ajDirDel(&dirout);
```

For a list of files (filelist or dirlist) it is necessary to free the list of filenames (which are stored as strings), once you are done with them, by calling ajListstrFreeData:

```
AjPList files   = NULL;
AjPList filelist = NULL;
AjIList iter    = NULL;
AjPFile infile  = NULL;
AjPStr filename = NULL;

files   = ajAcdGetFilelist("files");
filelist = ajAcdGetDirlist("directory");

/* both lists are filenames as strings */
```