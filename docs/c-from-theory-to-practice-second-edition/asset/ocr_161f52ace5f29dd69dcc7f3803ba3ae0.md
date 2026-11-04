```
```c
pkt[23] = port & 0xFF;
pkt[33] = 2; /* SYN bit. */
pkt[34] = 0xFF; /* The maximum value for the Window field is all
16 bits set to 1. */
pkt[35] = 0xFF;
/* The values of the CheckSum and Urgent Pointer are set in positions
36-40, therefore the total length of the IP packet is 40 bytes. */
pkt[2] = 0; /* IP Total Length. */
pkt[3] = 40;

Save_Pkt(pkt, 40);
}

void Save_Pkt(BYTE pkt[], int len)
{
FILE *fp;
char name[100];
int i;

printf("Enter file name: ");
read_text(name, sizeof(name), 1);

fp = fopen(name, "w");
if(fp == NULL)
{
printf("Error: fopen() failed\n");
exit(EXIT_FAILURE);
}
for(i = 0; i < len; i++)
{
if(i%16 == 0)
{
putc('\n', fp);
}
fprintf(fp, "%02X ", pkt[i]);
}
fclose(fp);
}
```
```

**Comments:** Do you have any idea about what this program really does? This program is an oversimplified version of a popular application, almost certainly installed in your computer, the firewall. Like this program, a firewall may prevent communication to specific IP addresses and specific applications (e.g., web servers listen to TCP port 80). In fact, the main part of a firewall is nothing more than a sequence of if-else statements.

In a real networking application, this IP packet is encapsulated in a MAC frame (see C.11.38), the hardware of the network card encodes the bits of the frame in digital signals (e.g., two different voltage levels to represent 0 and 1) and forwards the frame to the connected router. The router checks the IP destination address, finds the best path to that destination, and forwards the frame to the next router. Yes, we understand, it is all Greek to you, we just tried to introduce you to the fascinating world of computer networking.

C.20.6 Suppose that 20 firms participate in a contest. Each firm rates the other firms with a grade in [1, 20]. Write a program that reads their names (less than 100 characters) and the