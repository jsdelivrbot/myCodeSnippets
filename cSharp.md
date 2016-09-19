## Documentation
- C# Styling *https://github.com/dotnet/corefx/blob/master/Documentation/coding-guidelines/coding-style.md*
- Nancy Documentataion: *https://github.com/NancyFx/Nancy/wiki/Documentation*
- Razor Documentation: *http://haacked.com/archive/2011/01/06/razor-syntax-quick-reference.aspx/*

## Creating a Csharp Program
Make a file that ends with .cs.  M(ake sure a runtime is loaded on computer, like Mono).  Here is basics needed for each file.
```csharp
using System;

class Goodbye
{
  static void Main()
  {
    //Everything godes here, like:
    Console.WriteLine("Goodbye World");
  }
}
```

## Creating a C# project with Nancy
You may need to check for the last version 
```console
$ dnvm install latest
$ dnvm upgrade
```
Common starting folders
```console
Modules
Views
Content
Tests
Objects
> Startup.cs
> project.json
> readme.md

> Modules \ HomeModule.cs
> Objects \ ProjectObjects.cs
> Views \ index.cshtml
> Tests \ Tests.cs
> Content \ styles.css
> Content \ scripts.js
```
Small reminders
```cs
using System.Data;
using System.Data.SqlClient;
@Model.
using System.Collections.Generic;
Request.Form[""];
public static List<Contact> DisplayAll()  //Remember that the object is List<Contact>

//Remember that creating a method that is the same as the class is called a constructor and it's a key activity. 

```


### SetUp
To start a c# program using Nancy (as set up by Epicodus), you need to create a json file that pass a set of dependencies.  The name for this file is **project.json.**  When **> dnu restore** is typed into the command line, it will create a larger json file necessary for the compiler.  This includes telling the program to find the Startup.cs and provides a set of namespaces.   
```json
{
  "dependencies": {
    "Microsoft.AspNet.Server.Kestrel": "1.0.0-*",
    "Microsoft.AspNet.Owin": "1.0.0-*",
    "Nancy": "1.3.0",
    "Nancy.ViewEngines.Razor": "1.3.0",
    "xunit": "2.1.0",
    "xunit.runner.dnx": "2.1.0-rc1-*"
  },
  "commands": {
    "kestrel": "Microsoft.AspNet.Hosting --server Microsoft.AspNet.Server.Kestrel --server.urls http://localhost:5004",
    "test": "xunit.runner.dnx"
  },
  "frameworks": {
    "dnx451": {
      "frameworkAssemblies": {
        "System.Data": "4.0.0.0"
      }
    }
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
  public static class DBConfiguration
  {
    public static string ConnectionString = "Data Source=(localdb)\\mssqllocaldb;Initial Catalog=todo;Integrated Security=SSPI;";
  }
}
```

Additionally, the HomeModule.cs with Nancy should have the code.  The beauty of Nancy is the ease of loading a "View", as seen below. Please note that a index.cshtml file is needed.  
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
Then ready a tests folder
```c#
using System;
using Xunit;
using Inventory.Objects;
using System.Collections.Generic;
using System.Data;
using System.Data.SqlClient;

namespace Testing
using System;
using Xunit;
using Inventory.Objects;
using System.Collections.Generic;
using System.Data;
using System.Data.SqlClient;

namespace Tests
{
  public class Testing : IDisposable
  {
    public ToDoTest()
    {
      DBConfiguration.ConnectionString = "Data Source=(localdb)\\mssqllocaldb;Initial Catalog=todo_test;Integrated Security=SSPI;";
    }
    [Fact]
    public void Item_TestingCreatorMethod_true()
    {
      Item newItem = new Item("My Computer");
      Assert.Equal("My Computer", newItem.GetDescription() );
    }

    public void Dispose()
    {
      Item.DeleteAll();
    }
  }
}

```

## Background on cSharp

From Epicodus LEsson cSharp.
> To have access to C#, we need to install an implementation of the .NET Framework. This will give us and what is called the Common Language Runtime. We recommend using Mono. It's open-source and even better, it's cross-platform.

> C#, pronounced see sharp, began development in the late 90's. Released as a part of the .NET Framework initiative in July 2000, C# is part of a family of computer languages which evolved out of the C/C++ Programming Language, which originated in the late 60's at Bell Labs.

> Today, C# is the object-oriented component of the ASP.NET Framework. Microsoft Chief Architect and C# team leader Anders Hejlsberg described it as an iteration and improvement of the C++ language. Hejlsberg touted C# as "the first component-oriented language in the C/C++ family." As a result, it is " a simple, modern, general-purpose, object-oriented programming language" and to be "economical with regard to memory and processing power requirements".

From Wikipedia
> The Common Language Runtime (CLR), the virtual machine component of Microsoft's .NET framework, manages the execution of .NET programs. A process known as just-in-time compilation converts compiled code into machine instructions which the computer's CPU then executes.[1] The CLR provides additional services including memory management, type safety, exception handling, garbage collection, security and thread management. All programs written for the .NET framework, regardless of programming language, are executed by the CLR. All versions of the .NET framework include CLR.

> A compiler is a computer program (or a set of programs) that transforms source code written in a programming language (the source language) into another computer language (the target language), with the latter often having a binary form known as object code.

## Methods to Remember

```csharp

//char
char = 

// strings
string phrase = "Programming is AWESOME";
phrase.ToUpper();
phrase.ToLower();
phrase.Contains(phraseTwo);
string phrase3 = phrase.Replace("hello", "goodbye")
int number = 56;  number.ToString();
" Hi ".Trim();

//ints
string num = "32";
int newNum = int.Parse(num);

//bools
string phrase = "Gosh";
bool answer = phrase.StartsWith("g");
bool answer1 = phrase.EndsWith("o");

//Dictionary
Dictionary<string, string> myDictionary = new Dictionary<string, string>() { {"A", "apple"}, {"B", "bear"} };
```


