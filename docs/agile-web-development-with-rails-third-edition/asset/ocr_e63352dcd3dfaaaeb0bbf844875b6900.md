# 27.6 Avoid Session Fixation Attacks

If you know someone's session id, then you could create HTTP requests that use it. When Rails receives those requests, it thinks they're associated with the original user and so will let you do whatever that user can do.

Rails goes a long way toward preventing people from guessing other people's session ids, because it constructs these ids using a secure hash function. In effect, they're very large random numbers. However, there are ways of achieving almost the same effect.

In a session fixation attack, the bad guy gets a valid session id from our application and then passes this on to a third party in such a way that the third party will use this same session. If that person uses the session to log in to our application, the bad guy, who also has access to that session id, will also be logged in.⁴

A couple of techniques help eliminate session fixation attacks. First, you might find it helpful to keep the IP address of the request that created the session in the session data. If this changes, you can cancel the session. This will penalize users who move their laptops across networks and home users whose IP addresses change when PPPOE leases expire.

Second, you should consider creating a new session via reset_session every time someone logs in. That way, the legitimate user will continue with their use of the application while the bad guy will be left with an orphaned session id.

# 27.7 File Uploads

Some community-oriented websites allow their participants to upload files for other participants to download. Unless you're careful, these uploaded files could be used to attack your site.

For example, imagine someone uploading a file whose name ended with .rhtml or .cgi (or any other extension associated with executable content on your site). If you link directly to these files on the download page, when the file is selected, your web server might be tempted to execute its contents, rather than simply download it. This would allow an attacker to run arbitrary code on your server.

The solution is never to allow users to upload files that are subsequently made accessible directly to other users. Instead, upload files into a directory that is not accessible to your web server (outside the DocumentRoot in Apache terms). Then provide a Rails action that allows people to view these files.

> 4. Session fixation attacks are described in great detail in a document from ACROS Security, available at http://www.secinft.net/uplarticle/11/session_fixation.pdf.