
We start with the ipp.h header file.

```
1 #ifndef _IPP_H
2 #define _IPP_H
3
4 /*
5  * Defines parts of the IPP protocol between the scheduler
6  * and the printer.  Based on RFC2911 and RFC2910.
7  */
8
9 /*
10  * Status code classes.
11  */
12 #define STATCLASS_OK(x)    ((x) >= 0x0000 && (x) <= 0x00ff)
13 #define STATCLASS_INFO(x)  ((x) >= 0x0100 && (x) <= 0x01ff)
14 #define STATCLASS_REDIR(x) ((x) >= 0x0300 && (x) <= 0x03ff)
15 #define STATCLASS_CLERR(x) ((x) >= 0x0400 && (x) <= 0x04ff)
16 #define STATCLASS_SRVERR(x) ((x) >= 0x0500 && (x) <= 0x05ff)
17
18 /*
19  * Status codes.
20  */
21 #define STAT_OK            0x0000  /* success */
22 #define STAT_OK_ATTRIGN    0x0001  /* OK; some attrs ignored */
23 #define STAT_OK_ATTRCON    0x0002  /* OK; some attrs conflicted */
24 #define STAT_CLI_BADREQ    0x0400  /* invalid client request */
25 #define STAT_CLI_FORBID    0x0401  /* request is forbidden */
26 #define STAT_CLI_NOAUTH    0x0402  /* authentication required */
27 #define STAT_CLI_NOPERM    0x0403  /* client not authorized */
28 #define STAT_CLI_NOTPOS   0x0404  /* request not possible */
29 #define STAT_CLI_TIMOUT    0x0405  /* client too slow */
30 #define STAT_CLI_NOTFND    0x0406  /* no object found for URI */
31 #define STAT_CLI_OBJGONE   0x0407  /* object no longer available */
32 #define STAT_CLI_TOOBIG    0x0408  /* requested entity too big */
33 #define STAT_CLI_TOOLNG    0x0409  /* attribute value too large */
34 #define STAT_CLI_BADFMT    0x040a  /* unsupported doc format */
35 #define STAT_CLI_NOTSUP    0x040b  /* attributes not supported */
36 #define STAT_CLI_NOSCHM    0x040c  /* URI scheme not supported */
37 #define STAT_CLI_NOCHAR    0x040d  /* charset not supported */
38 #define STAT_CLI_ATTRCON   0x040e  /* attributes conflicted */
39 #define STAT_CLI_NOCOMP    0x040f  /* compression not supported */
40 #define STAT_CLI_COMPERR   0x0410  /* data can't be decompressed */
41 #define STAT_CLI_FMTERR    0x0411  /* document format error */
42 #define STAT_CLI_ACCERR    0x0412  /* error accessing data */
```

[1–14] We start the ipp.h header with the standard #ifndef to prevent errors when it is included twice in the same file. Then we define the classes of IPP status codes (see Section 13 in RFC 2911).

[15–39] We define specific status codes based on RFC 2911. We don't use these codes in the program shown here; their use is left as an exercise (See Exercise 21.1).

```
40  #define STAT_SRV_INTERN  0x0500 /* unexpected internal error */
41  #define STAT_SRV_NOTSUP  0x0501 /* operation not supported */
42  #define STAT_SRV_UNAVAIL 0x0502 /* service unavailable */
43  #define STAT_SRV_BADVER  0x0503 /* version not supported */
44  #define STAT_SRV_DEVERR  0x0504 /* device error */
45  #define STAT_SRV_TMPERR  0x0505 /* temporary error */
46  #define STAT_SRV_REJECT  0x0506 /* server not accepting jobs */
47  #define STAT_SRV_TOOBUSY 0x0507 /* server too busy */
48  #define STAT_SRV_CANCEL  0x0508 /* job has been canceled */
49  #define STAT_SRV_NOMULTI 0x0509 /* multi-doc jobs unsupported */

50  /*
51   * Operation IDs
52   */
53  #define OP_PRINT_JOB     0x02
54  #define OP_PRINT_URI     0x03
55  #define OP_VALIDATE_JOB  0x04
56  #define OP_CREATE_JOB    0x05
57  #define OP_SEND_DOC      0x06
58  #define OP_SEND_URI      0x07
59  #define OP_CANCEL_JOB    0x08
60  #define OP_GET_JOB_ATTR  0x09
61  #define OP_GET_JOBS      0x0a
62  #define OP_GET_PRINTER_ATTR 0x0b
63  #define OP_HOLD_JOB      0x0c
64  #define OP_RELEASE_JOB   0x0d
65  #define OP_RESTART_JOB   0x0e
66  #define OP_PAUSE_PRINTER 0x10
67  #define OP_RESUME_PRINTER 0x11
68  #define OP_PURGE_JOBS    0x12

69  /*
70   * Attribute Tags.
71   */
72  #define TAG_OPERATION_ATTR 0x01 /* operation attributes tag */
73  #define TAG_JOB_ATTR       0x02 /* job attributes tag */
74  #define TAG_END_OF_ATTR    0x03 /* end of attributes tag */
75  #define TAG_PRINTER_ATTR   0x04 /* printer attributes tag */
76  #define TAG_UNSUP_ATTR     0x05 /* unsupported attributes tag */
```

[40–49] We continue to define status codes. The ones in the range 0x500 to 0x5ff are server error codes. All codes are described in Sections 13.1.1 through 13.1.5 in RFC 2911.

[50–68] We define the various operation IDs next. There is one ID for each task defined by IPP (see Section 4.4.15 in RFC 2911). In our example, we will use only the print-job operation.

[69–76] The attribute tags delimit the attribute groups in the IPP request and response messages. The tag values are defined in Section 3.5.1 of RFC 2910.

```
77 /*
78  * Value Tags.
79  */
80 #define TAG_UNSUPPORTED 0x10 /* unsupported value */
81 #define TAG_UNKNOWN     0x12 /* unknown value */
82 #define TAG_NONE        0x13 /* no value */
83 #define TAG_INTEGER     0x21 /* integer */
84 #define TAG_BOOLEAN     0x22 /* boolean */
85 #define TAG_ENUM        0x23 /* enumeration */
86 #define TAG_OCTSTR      0x30 /* octetString */
87 #define TAG_DATETIME    0x31 /* dateTime */
88 #define TAG_RESOLUTION  0x32 /* resolution */
89 #define TAG_INTRANGE    0x33 /* rangeOfInteger */
90 #define TAG_TEXTWLANG   0x35 /* textWithLanguage */
91 #define TAG_NAMEWLANG   0x36 /* nameWithLanguage */
92 #define TAG_TEXTWOLANG  0x41 /* textWithoutLanguage */
93 #define TAG_NAMEWOLANG  0x42 /* nameWithoutLanguage */
94 #define TAG_KEYWORD     0x44 /* keyword */
95 #define TAG_URI         0x45 /* URI */
96 #define TAG_URISCHEME   0x46 /* uriScheme */
97 #define TAG_CHARSET     0x47 /* charset */
98 #define TAG_NATULANG    0x48 /* naturalLanguage */
99 #define TAG_MIMETYPE    0x49 /* mimeMediaType */

100 struct ipp_hdr {
101   int8_t major_version; /* always 1 */
102   int8_t minor_version; /* always 1 */
103   union {
104     int16_t op; /* operation ID */
105     int16_t st; /* status */
106   } u;
107   int32_t request_id;  /* request ID */
108   char _attr_group[1]; /* start of optional attributes group */
109   /* optional data follows */
110 };

111 #define operation u.op
112 #define status u.st

113 #endif /* _IPP_H */
```

[77–99] The value tags indicate the format of individual attributes and parameters. They are defined in Section 3.5.2 of RFC 2910.

[100–113] We define the structure of an IPP header. Request messages start with the same header as response messages, except that the operation ID in the request is replaced by a status code in the response.

We end the header file with a #endif to match the #ifdef at the start of the file.

The next file is the print.h header.

```
1 #ifndef _PRINT_H
2 #define _PRINT_H
3
4 /*
5  * Print server header file.
6  */
7 #include <sys/socket.h>
8 #include <arpa/inet.h>
9 #include <netdb.h>
10 #include <errno.h>
11
12 #define CONFIG_FILE "/etc/printer.conf"
13 #define SPOOLDIR "/var/spool/printer"
14 #define JOBFILE "jobno"
15 #define DATADIR "data"
16 #define REQDIR "reqs"
17
18 #if defined(BSD)
19 #define LPName "daemon"
20 #elif defined(MACOS)
21 #define LPName "_lp"
22 #else
23 #define LPName "lp"
24 #endif
```

[1–9] We include all header files that an application might need if it included this header. This makes it easy for applications to include print.h without having to track down all the header dependencies.

[10–14] We define the files and directories for the implementation. The configuration file containing the host names of the printer spooling daemon and the network-attached printer is /etc/printer.conf. Copies of the files to be printed will be stored in the directory /var/spool/printer/data and control information for each request will be stored in the directory /var/spool/printer/reqs. The file containing the next job number is /var/spool/printer/jobno.

The directories must be created by an administrator and be owned by the same user account under which the printer spooling daemon runs. The daemon won’t try to create these directories if they don’t exist, because the daemon would need root privileges to create directories in /var/spool. We design the daemon to do as little as possible while running as root to minimize the chance of creating a security hole.

[15–21] Next, we define the account name under which the printer spooling daemon will run. On Linux and Solaris, this name is lp. On Mac OS X, the name is _lp. FreeBSD, however, doesn’t define a separate account for the printer spooling daemon, so we use the account reserved for system daemons.
