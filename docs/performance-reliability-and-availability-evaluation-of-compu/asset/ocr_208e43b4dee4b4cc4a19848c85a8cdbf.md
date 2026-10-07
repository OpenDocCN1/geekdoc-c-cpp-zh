# 422 Performance Reliability, and Availability Evaluation of Computational Systems

# Command date

The command date is a widely used tool in Linux-based systems. Nevertheless, this command displays or sets the date and time of the system. Nevertheless there are many options for customizing its output, such as setting dates and times, presenting the information in various formats, calculating dates, and even setting the system clock. The standard syntax of the command is "date options format". The date command supports many options and output formats. For a detailed view of the available options and formats, please refer to "> man date". Here, we present some useful options that supports measuring duration or of events or between events. Hence, instead of introducing its options and then depicting some specific useful examples, and for them, we discuss the respective options and formats.

The command date without any options and arguments displays the current date and time, such as

```
Fri May 29 14:34:11 -03 2020
```

The output shows that it is Friday, May 29, 2020, and the command was executed on 14:34:11 PM, with a 24-hour format (hh:mm:ss)²⁰¹, and the time zone is GMT-2¹¹.

For the example, four which command display date and time in ISO 8601 format²², where "hours", "minutes", "seconds", or "ns" (nanoseconds) defines the precision.

```
> date --iso-8601-hours (command line)
> 2020-05-29T16:03:00 (output),
```

```
> date --iso-8601-minutes (command line)
> 2020-05-29T16:52:03 (output),
```

```
> date --iso-8601-seconds (command line)
> 2020-05-29T16:51:05-03 (output), and
```

```
> date --iso-8601=ns (command line)
> 2020-05-29T16:08:650258894-03 (output).
```

The next command displays date and time in RFC 3339 format²³³, where "ns" defines the precision.

> ²⁰ hour - mm - minutes, and seconds.

> ²¹¹ Greenwich Mean Time.

> ²²https://www.iso.org/iso-8601-date-and-time-format.html.

> ²³³https://tools.ietf.org/html/rfc3339.