Key Concepts  558

Summary  558

Review Questions  559

Programming Exercises  561

# 13  File Input/Output  565

Communicating with Files  565

What Is a File?  566

The Text Mode and the Binary Mode  566

Levels of I/O  568

Standard Files  568

Standard I/O  568

Checking for Command-Line Arguments  569

The fopen() Function  570

The getc() and putc() Functions  572

End-of-File  572

The fclose() Function  574

Pointers to the Standard Files  574

A Simple-Minded File-Condensing Program  574

File I/O: fprintf(), fscanf(), fgets(), and fputs()  576

The fprintf() and fscanf() Functions  576

The fgets() and fputs() Functions  578

Adventures in Random Access: fseek() and ftell()  579

How fseek() and ftell() Work  580

Binary Versus Text Mode  582

Portability  582

The fgetpos() and fsetpos() Functions  583

Behind the Scenes with Standard I/O  583

Other Standard I/O Functions  584

The int ungetc(int c, FILE *fp) Function  585

The int fflush() Function  585

The int setvbuf() Function  585

Binary I/O: fread() and fwrite()  586

The size_t fwrite() Function  588

The size_t fread() Function  588

The int feof(FILE *fp) and int ferror(FILE *fp) Functions  589

An fread() and fwrite() Example  589