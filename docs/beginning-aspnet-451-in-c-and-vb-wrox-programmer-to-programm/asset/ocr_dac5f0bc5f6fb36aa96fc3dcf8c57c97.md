```
<add key="ToAddress" value="planetwrox-production@example.com"
xdt:Transform="SetAttributes" xdt:Locator="Match(key)" />
</appSettings>
..
<system.web>
```

The <add /> elements are added to the source file, except for exclusion of the xdt attributes.

+   5. Right-click Web.to local disk.config again and choose Preview Transformation. Because the e-mail addresses are different, they will be highlighted as well.

+   6. Next, add the following section above <settings> tag to modify the connection strings. Update the connectionString attributes with a connection string that your host expects. You find more information about connection strings later in this chapter and in Appendix B. Also, your host is likely to provide you with relevant details you need to enter here.

```
<connectionStrings>
<name="PlanetWroxConnectionString" connectionString="removed to save space"
xdt:Transform="SetAttributes" xdt:Locator="Match(name)" />
<name="PlanetWroxAttributes" connectionString="removed to save space"
xdt:Transform="SetAttributes" xdt:Locator="Match(name)" />
</connectionStrings>
<appSettings>
```

Note that the Locator uses name to find the correct connection string by its name, whereas the appSettings you saw in step 4 used key.

+   7. Below the <compilation> element within the <system.web> element, add the following code to turn custom errors in the production site:

```
<customErrors mode="On" xdt:Transform="SetAttributes" />
```

+   8. Finally, below the <system.web> element, add the following element to configure the main mail server:

```
<system.web>
<mailSettings xdt:Transform="Replace">
<smtp deliveryMethod="Network" server="Planet Wrox &amp;planetwrox@example.com&gt;">
<network host="your host" />
</smtp>
</mailSettings>
</system.web>
```

+   9. Update the code inside the network element to match the requirements for your production server. Refer to Chapter 9 to learn more about the different settings, and consult your server's administrator for the exact details you must supply here.

+   10. Request a preview of the transformation once and verify that the file looks exactly as you want. If your transformation file contains any errors, they’ll be listed in the Output window.

+   11. When you’re done, close the .config file, as you're done with it now.