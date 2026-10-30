```
48  /*
49   * Structure describing a print request.
50   */
51  struct printreq {
52      uint32_t size;              /* size in bytes */
53      uint32_t flags;             /* see below */
54      char usernm[USERNM_MAX];    /* user's name */
55      char jobnm[JOBNM_MAX];      /* job's name */
56  };
57  /*
58   * Request flags.
59   */
60  #define PR_TEXT    0x01    /* treat file as plain text */
61  /*
62   * The response from the spooling daemon to the print command.
63   */
64  struct printr esp {
65      uint32_t retcode;           /* 0=success, 10=error code */
66      uint32_t jobid;             /* job ID */
67      char msg[MSGLEN_MAX];       /* error message */
68  };
69  #endif /* _PRINT_H */
```

[48–69] The printreq and printr esp structures define the protocol between the print command and the printer spooling daemon. The print command sends a printreq structure specifying the size of the job in bytes, job characteristics, the user name, and the job name to the printer spooling daemon. The daemon responds with a printr esp structure containing a return code, the job ID, and an error message if the request failed.

The PR_TEXT job characteristic indicates that the file being printed should be treated as plaintext (instead of PostScript). We define a bitmask of flags instead of defining a separate field for each flag. Although only one flag value is currently defined, we could extend the protocol in the future to add more characteristics. For example, we could add a flag to request double-sided printing. We have room for 31 additional flags without requiring that we change the size of the structure. Changing the size of the structure means that we might introduce a compatibility problem between the client and the server unless we upgrade both at the same time. An alternative approach is to add a version number to the messages to allow the structures to change with each version.

Note that we define all integers in the protocol structures with an explicit size. This helps avoid misaligned structure elements when a client has a different long integer size than the server.