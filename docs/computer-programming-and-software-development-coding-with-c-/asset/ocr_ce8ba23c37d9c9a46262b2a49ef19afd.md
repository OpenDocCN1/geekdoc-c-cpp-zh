![](bbox=[0.12, 0.07, 0.905, 0.41])

Let's try to add the footnote parameter to the query string. Now, let's take a look if we can use it to inject an XSS payload. The attack, once again, was successful. We can use this vector to exfiltrate the secret token. Luckily, fixing this vulnerability is extremely simple. The EJS syntax that we have applied here doesn't automatically apply HTML escaping.