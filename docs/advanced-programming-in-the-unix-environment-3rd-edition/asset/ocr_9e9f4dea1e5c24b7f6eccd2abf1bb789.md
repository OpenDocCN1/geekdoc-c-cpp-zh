```
64  /*
65   * Return the host name running the print server or NULL on error.
66   *
67   * LOCKING: none.
68   */
69  char *
70  get_printserver(void)
71  {
72      return(scan_configfile("printserver"));
73  }
74  
75  /*
76   * Return the address of the network printer or NULL on error.
77   *
78   * LOCKING: none.
79   */
80  struct addrinfo *
81  get_printaddr(void)
82  {
83      int             err;
84      char            *p;
85      struct addrinfo *ailist;
86  
87      if ((p = scan_configfile("printer")) != NULL) {
88          if ((err = getaddrlist(p, "ipp", &ailist)) != 0) {
89              log_msg("no address information for %s", p);
90              return(NULL);
91          }
92          return(ailist);
93      }
94      log_msg("no printer address specified");
95      return(NULL);
96  }
```

[64–73] The get_printserver function is simply a wrapper function that calls scan_configfile to find the name of the computer system where the printer spooling daemon is running.

[74–94] We use the get_printaddr function to get the address of the network printer. It is similar to the previous function except that when we find the name of the printer in the configuration file, we use the name to find the corresponding network address.

Both get_printserver and get_printaddr call scan_configfile. If it can't open the printer configuration file, scan_configfile calls log_sys to print an error message and exit. Although get_printserver is meant to be called from a client command and get_printaddr is meant to be called from the daemon, having both call log_sys is OK, because we can arrange for the log functions to print to the standard error instead of to the log file by setting a global variable.