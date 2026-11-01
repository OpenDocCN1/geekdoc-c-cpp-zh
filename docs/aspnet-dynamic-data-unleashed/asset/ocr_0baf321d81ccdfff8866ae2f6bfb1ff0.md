Having access denied by default forces you to modify the Web.config for every new entity you want to access through the dynamically generated web pages. In other words, if you decide to enable dynamic pages for the Customer entity, you have to create authorization rules for it in the Web.config before you can test it in the browser.

# Limitations of Configuration-Based Rules

Web configuration files allow you to implement a complete authorization system for Dynamic Data applications. You can configure access rules based on entities, actions, users, and roles. However, there are several significant drawbacks associated with this approach as well. On one hand, configuring a set of rules for a sizable entity model is often very verbose. You must create a separate <location/> element for every entity and potentially for every action that needs different authorization rules. With at least seven lines of XML configuration for every location element, the size of configuration can quickly reach hundreds of lines.

A bigger problem with configuration-based approach is that enforcing access rules at the page level is often not granular enough. Take a dynamic search page for the Product entity as an example. Suppose you want all your customers and even unauthenticated users to browse the product catalog. However, you also want to restrict access to Suppliers so that only employees of your company can see them. To enforce these rules, you could try implementing the following authorization rules in the Web.config file:

```
```xml
<location path="Products">
    <system.web>
        <authorization>
            <allow users="*"/>
        </authorization>
    </system.web>
</location>
<location path="Suppliers">
    <system.web>
        <authorization>
            <allow roles="Manager,Employee"/>
            <deny users="*"/>
        </authorization>
    </system.web>
</location>
```
```

These authorization rules prevent customers from seeing the Suppliers page itself. However, they can still see supplier names on the dynamic Products page. The Product entity has a navigation property, Supplier, and Dynamic Data automatically generates a foreign key field template for it. Figure 14.2 shows an example.