```
```csharp
public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    // ... other configurations
    app.UseRouting(); // Enable routing
    app.UseEndpoints(endpoints =>
    {
        endpoints.MapControllerRoute(
            name: "default",
            pattern: "{controller=Home}/{action=Index}/{id?}");
    });
    // ... other configurations
}
```
```

This configures the default routing convention, mapping requests to controllers and actions based on their names.

+   3. **Configure Static Files:**

```
```csharp
public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    // ... other configurations
    app.UseStaticFiles(); // Enable serving static files from the wwwroot folder
    // ... other configurations
}
```
```