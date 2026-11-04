+   - Enter the following line to the end of the file:

```
    * * * * * /home/pi/myscript.sh
```

+   - Exit nano by entering:

```
    Ctrl+X
    Y
    <Enter>
```

+   - The commands in the **myscript.sh** will now be executed every minute and the output will be sent to **myfile**. We can verify that the commands are executed by looking at the contents of **myfile** after a few minutes:

```
    pi@raspberrypi:~ $ cat myfile
    Wed 13 May 16:27:01 BST 2020
    Wed 13 May 16:28:01 BST 2020
    Wed 13 May 16:29:01 BST 2020
    pi@raspberrypi:~ $
```

+   - You can stop the scheduling by deleting the line entered by command **crontab -e**

The **crontab -l** command displays a list of the scheduled tasks (if there are any):

```
    pi@raspberrypi:~ $ crontab -l
```

All scheduled tasks can be deleted (if there are any) using the **crontab -r** command:

```
    pi@raspberrypi:~ $ crontab -r
    pi@raspberrypi:~ $ crontab -l
    no crontab for pi
    pi@raspberrypi:~ $
```

The -i option can be added to the delete command to confirm the delete action.

# ### Crontab generator

An online tool called Crontab Generator (available free of charge on the internet) can be used to easily generate crontab entries. This tool is available on the following website:

[https://crontab-generator.org/](https://crontab-generator.org/)

Figure 16.2 shows part of the Crontab Generator. An example is given to show how to use this tool.