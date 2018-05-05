### please check out the [orginal post on Cooldown.io](https://cooldown.io/topic/16-getting-started-with-blazor-and-electronnet/)

# **Getting started with [Blazor](https://github.com/aspnet/Blazor) and [Electron.NET](https://github.com/ElectronNET/Electron.NET)**

## **Background Information:**

*   **What is Blazor?**
    *   From the [Blazor Github](https://github.com/aspnet/Blazor), Blazor is "an experimental .NET web framework using C#/Razor and HTML that runs in the browser via WebAssembly"
*   **What is Electron.NET?**
    *   From the [Electron.NET Github](https://github.com/ElectronNET/Electron.NET), "Electron.NET is a **wrapper** around a "normal" Electron application with an embedded ASP.NET Core application".

## **Perquisites:**

*   So that this article does not get dated with irreverent information quickly I will be using information from other resources.
*   [getting started for blazor](https://blazor.net/docs/get-started.html) 
*   node.js v8.6.0+
*   electron-packager --global

## **Sample Project Github:**

*   If you do not want to follow the steps below, or just want to check out the code I reproduced the following steps in a repo. Besure you all the required perquisites 

## **Setting up a simple project:**

1.  If you have not done so, check out the [getting started for blazor](https://blazor.net/docs/get-started.html) to install perquisites for this tutorial 
2.  Create a new **Blazor (ASP.NET Core hosted)** project
3.  Install ElectronNET.API
```
PM> Install-Package ElectronNET.API
```
       
4.  In %projectname%.Server/Program.cs change BuildWebHost to use Electron
```csharp
public static IWebHost BuildWebHost(string[] args) =>
            WebHost.CreateDefaultBuilder(args)
                .UseElectron(args)
                .UseStartup<Startup>()
                .Build();
```
    
5.  In %projectname%.Server/Startup.cs change Configure to open Electron
```csharp
app.UseBlazor<Client.Program>();
Task.Run(async () => await Electron.WindowManager.CreateWindowAsync());
``` 
6.  Add cli tooling to %projectname%.Server
```html
<ItemGroup>
    <DotNetCliToolReference  Include="ElectronNET.CLI"  Version="0.0.9"  />         
</ItemGroup>
**Note at the time the current version is 0.0.9**
```
```
dotnet restore
```

7.  Install electron packager
```
sudo npm install electron-packager --global
```
        
8.  Init and Run
```
dotnet electronize init
dotnet electronize start
```
        
## **Credits:**

I claim none of this work as my own and proudly support the work of both the aspnet team on Blazor and the team developing Electron.NET, this post is intended to raise awareness of some of the possibilities for a **prototype**. Most of the "Setting up a simple project" is directly from both Electron.NET's and Blazor's githubs.