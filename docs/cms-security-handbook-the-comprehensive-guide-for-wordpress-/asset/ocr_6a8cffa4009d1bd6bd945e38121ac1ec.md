```
SSLRequireSSL
SSLRequire %{HTTP_HOST} eq "domain.tld"
ErrorDocument 403 https://domain.tld

# require SSL without mod_ssl
RewriteCond %{HTTPS} !=on [NC]
RewriteRule ^.*$ https://%{SERVER_NAME}%{REQUEST_URI} [R,L]
```

# Deploying Custom Error Pages on Your Site

Replicate the following patterns to serve your own set of custom error pages. Simply replace the /errors/###.html with the correct path and filename. Also change the ### preceding the path to summon pages for other errors.

> **NOTE** Your custom error pages must be larger than 512 bytes in size, or they will be completely ignored by Internet Explorer.

Use the following to serve custom error pages:

```
ErrorDocument 400 /errors/400.html
ErrorDocument 401 /errors/401.html
ErrorDocument 403 /errors/403.html
ErrorDocument 404 /errors/404.html
ErrorDocument 500 /errors/500.html
Provide a Universal Error Document
```

Use the following to provide a universal error document:

```
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^.*$ /dir/error.php [L]
```

# Disable the Server Signature

Use the following to disable the server signature:

```
ServerSignature Off
```

# Limit Server Request Methods to Get and Put

Use the following to limit server request methods to GET and PUT:

```
Options -ExecCGI -Indexes -All
RewriteEngine on
RewriteCond %{REQUEST_METHOD} ^(TRACE|TRACK|OPTIONS|HEAD)
RewriteRule ^.* - [F]
```