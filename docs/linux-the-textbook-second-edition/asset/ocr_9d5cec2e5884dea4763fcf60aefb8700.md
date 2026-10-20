```
>   echo "These are the machines on the network: "
>   uptime | cut -f1 -d' ' | more
> }
$ ./machines
Thu Jul 31 20:23:28 PKT 2014
These are the machines on the network: upibm0
...
upsun1
...
upsun29
$
```

We now enhance the dext script described in Section 13.3 so that it can take multiple names at the command line. The enhanced version also uses a function OutputData to display one or more output records (i.e., lines in the directory) for every name passed as the command line argument. In the case of multiple lines for a name, this function displays them in sorted order. A few sample runs are shown following the script.

```
$ cat dext
#!/bin/bash
# File Name:    ~/linux2e/chaper13/bash/dext
# Author:       Syed Mansoor Sarwar
# Written:      August 1999
# Modified:     August 28, 2004; July 29, 2014; April 9, 2017

if [ $# = 0 ]
    then
        echo "Usage: $0 name"
        exit 1
fi
OutputData()
{
    echo "Infomation about $user_input"
    (grep -i "$user_input"| sort) << DIRECTORY

    John Doe      555.232.0000    johnd@somedomain.com
    Jenny Great   444.6565.11111  jg@new.somecollege.edu
    David Nice    999.111.3333    david_nice@xyz.org
    Don Carr      555.111.3333    dcarr@old.hoggie.edu
    Masood Shah   666.010.9820    shah@Garments.com.pk
    Jim Davis     777.000.9999    davis@great.adviser.edu
    Art Pohm      333.000.8888    art.pohm@great.professor.edu
    David Carr    777.999.2222    dcarr@net.net.gov

DIRECTORY
    echo      # A blank line between two records
}

# As long as there is at least one command line argument (name), take the
# first name, call the OutputData function to search the DIRECTORY and
# display the line(s) containing the name, shift this name left by one
# position, and repeat the process.

while [ $# != 0 ]
do
    user_input="$1"    # Get the next command line argument (name)
    OutputData          # Display info about the next name
    shift               # Get the following name
done
exit 0
$ ./dext john
```