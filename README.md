# RavenDB.AspNetCore.DependencyInjection
Dependency Injection package for using RavenDB with ASP.NET Core.

[![Docker Stars](https://img.shields.io/nuget/v/RavenDB.AspNetCore.DependencyInjection.svg?style=flat)](https://www.nuget.org/packages/RavenDB.AspNetCore.DependencyInjection/)
[![Docker Pulls](https://img.shields.io/nuget/vpre/RavenDB.AspNetCore.DependencyInjection.svg?style=flat)](https://www.nuget.org/packages/RavenDB.AspNetCore.DependencyInjection/)

This package handles the injection of DocumentSession( or AsyncDocumentSession) for you and while keeping track and managing the DocumentStore(s) for you.

## Getting Started:
Install the [RavenDB.AspNetCore.DependencyInjection](https://www.nuget.org/packages/RavenDB.AspNetCore.DependencyInjection) library through [NuGet](https://nuget.org).
```
    Install-Package RavenDB.AspNetCore.DependencyInjection
    
    Or
    
    Install-Package RavenDB.AspNetCore.DependencyInjection -Pre
```    

## Usage:   
Add this to your Startup.cs:
```csharp
public IServiceProvider ConfigureServices(IServiceCollection services)
{
...
	
  services.AddRavenManager(
      options =>
      {
          options.DefaultServer = "Main";
          options.AddServer("Main", new RavenServerOptions()
          {
              Url = "{server url}",
              DefaultDatabase = "{default database}"
          });
      }).AddScopedAsyncSession();
	
...
}
```

Now you can use the standard injection syntax to get you're session or the raven manager:
```csharp
public class HomeController
      : Controller
  {
      private readonly IAsyncDocumentSession _session;
      private readonly IRavenManager _ravenManager;

      public HomeController(
          IAsyncDocumentSession session,
          IRavenManager ravenManager)
      {
          _session = session;
          _ravenManager = ravenManager;
      }
  }
```

# User Feedback

## Issues

If you have any problems with or questions about this image, please contact us through a [GitHub issue](https://github.com/FriendlyAgent/RavenDB.AspNetCore.DependencyInjection/issues).