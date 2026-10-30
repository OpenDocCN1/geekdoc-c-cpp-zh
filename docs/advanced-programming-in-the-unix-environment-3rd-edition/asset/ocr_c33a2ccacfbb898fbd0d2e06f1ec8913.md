# 21.6 Summary

This chapter has examined in detail two complete programs: a print spooler daemon that sends a print job to a network printer and a command that can be used to submit a job to be printed to the spooling daemon. This has given us a chance to see many features that we described in earlier chapters used in real programs: threads, I/O multiplexing, file I/O, reading directories, socket I/O, and signals.

# Exercises

+   21.1 Translate the IPP error code values listed in ipp.h into error messages. Then modify the print spooler daemon to log a message at the end of the printer_status function when the IPP header indicates a printer error.

+   21.2 Add support to the print command and the printed daemon to allow users to request double-sided printing. Do the same for landscape and portrait page orientation.

+   21.3 Modify the print spooler daemon so that when it starts, it contacts the printer to find out which features are supported by the printer so that the daemon doesn't request an option that isn't supported.

+   21.4 Write a command to report on the status of pending print jobs.

+   21.5 Write a command to cancel a pending print job. Use the job ID as the argument to the command to specify which job to cancel. How can you prevent one user from canceling another user's print jobs?

+   21.6 Add support for multiple printers to the printer spooler. Include a way to move print jobs from one printer to another.

+   21.7 In the printer daemon, explain why we don't need to prod the printer thread when the signal handling thread catches SIGHUP and sets reread to 1.

+   21.8 In the printer_status function, we search for the length of the IPP message by looking for the Content-Length HTTP attribute. This technique won't work with a printer that responds using a chunked transfer encoding. Check RFC 2616 to see how a chunked message is formatted and then modify printer_status to support this form of response as well.

+   21.9 In the update_jobno function, when the next job number wraps around from the maximum positive value to 1 (see get_newjobno to see how this can happen), we can write a smaller number over a larger one. This can result in the daemon reading an incorrect number when it restarts. What is a simple solution to this problem?