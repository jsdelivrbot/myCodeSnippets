##Creating a C# project witn Nancy
You may need to check for the last version 
```console
$ dnvm install latest
$ dnvm upgrade
```
Small points to remember
```html
@Model. 
```
#### Documentation
- Nancy Documentataion: *https://github.com/NancyFx/Nancy/wiki/Documentation*
- Razor Documentation: *http://haacked.com/archive/2011/01/06/razor-syntax-quick-reference.aspx/*
To start a c# program using Nancy (as set up by Epicodus), you need to create a json file that pass a set of dependencies.  The name for this file is **project.json.**  When **> dnu restore** is typed into the command line, it will create a larger json file necessary for the compiler.  This includes telling the program to find the Startup.cs and provides a set of namespaces.   
```json
{
  "dependencies": {
    "Microsoft.AspNet.Server.Kestrel": "1.0.0-*",
    "Microsoft.AspNet.Owin": "1.0.0-*",
    "Nancy": "1.3.0",
    "Nancy.ViewEngines.Razor": "1.3.0"
  },
  "commands": {
    "kestrel": "Microsoft.AspNet.Hosting --server Microsoft.AspNet.Server.Kestrel --server.urls http://localhost:5004"
  },
  "frameworks": {
    "dnx451": {}
  }
}
```

When making a project with Nancy, Nancy looks for a file called **Startup.cs** .  This file will use these namespaces in Startup.cs.  
```cs
using System.Collections.Generic;
using System.IO;
using Microsoft.AspNet.Builder;
using Nancy;
using Nancy.Owin;
using Nancy.ViewEngines.Razor;
```

In the file **Startup.cs** and inside the "primary" project namespace, you will need to add Startup class  Do not forget to put this inside a namespace!

```cs
namespace ProjectCore
{
  public class Startup
  {
    public void Configure(IApplicationBuilder app)
    {
      app.UseOwin(x => x.UseNancy());
    }
  }
  public class CustomRootPathProvider : IRootPathProvider
  {
    public string GetRootPath()
    {
      return Directory.GetCurrentDirectory();
    }
  }
  public class RazorConfig : IRazorConfiguration
  {
    public IEnumerable<string> GetAssemblyNames()
    {
      return null;
    }

    public IEnumerable<string> GetDefaultNamespaces()
    {
      return null;
    }

    public bool AutoIncludeModelNamespace
    {
      get { return false; }
    }
  }
}
```

Additionally, the first module with Nancy should have the code.  The beauty of Nancy is the ease of loading a "View", as seen below. Please note that a index.cshtml file is needed.  
```csharp
using Nancy;
namespace ProjectCore
{
  public class HomeModule : NancyModule
  {
    public HomeModule()
    {
      Get["/"] = _ => {return View["index.cshtml"];};
    }
  }
}

```
From here it is common to create an objects folder with a cs folder of objects
```csharp
namespace ProjectCore.Objects
{
  public class ProjectCore
  {
    private string _name;

    public string GetName()
    {
      return _name;
    }

    public void SetName(string newName)
    {
      _name = newName;
    }
  }
}
```
