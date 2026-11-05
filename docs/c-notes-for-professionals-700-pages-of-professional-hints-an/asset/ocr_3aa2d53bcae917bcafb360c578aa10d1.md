```
}
#endregion

// <summary>Registers the type mappings with the Unity container.</summary>
// <param name="container">The unity container to configure.</param>
// <remarks>There is no need to register concrete types such as controllers or API controllers
(unless you want to
// change the defaults), as Unity allows resolving a concrete type even if it was not previously
registered.</remarks>
public static void RegisterTypes(IUnityContainer container)
{
    // NOTE: To load from web.config uncomment the line below. Make sure to add a
    Microsoft.Practices.Unity.Configuration to the using statements.
    // container.LoadConfiguration();

    // TODO: Register your types here
    // container.RegisterType<IProductRepository, ProductRepository>();

    container.RegisterType<ISanta, SantaAndHisReindeer>();
}
}
```

UnityMvcActivator - > also with nice comments which say that this class integrates Unity with ASP.NET MVC

```
using System.Linq;
using System.Web.Mvc;
using Microsoft.Practices.Unity.Mvc;

[assembly: WebActivatorEx.PreApplicationStartMethod(typeof(Vegan.WebUi.App_Start.UnityWebActivator), "Start")]
[assembly: WebActivatorEx.ApplicationShutdownMethod(typeof(Vegan.WebUi.App_Start.UnityWebActivator), "Shutdown")]

namespace Vegan.WebUi.App_Start
{
    // <summary>Provides the bootstrapping for integrating Unity with ASP.NET MVC.</summary>
    public static class UnityWebActivator
    {
        // <summary>Integrates Unity when the application starts.</summary>
        public static void Start()
        {
            var container = UnityConfig.GetConfiguredContainer();

            FilterProviders.Providers.Remove(FilterProviders.Providers.OfType<FilterAttributeFilterProvider>().First());
            FilterProviders.Providers.Add(new UnityFilterAttributeFilterProvider(container));

            DependencyResolver.SetResolver(new UnityDependencyResolver(container));

            // TODO: Uncomment if you want to use PerRequestLifetimeManager
            //
            Microsoft.Web.Infrastructure.DynamicModuleHelper.DynamicModuleUtility.RegisterModule(typeof(UnityPerRequestHttpModule));
        }
    }
```