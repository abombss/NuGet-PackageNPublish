# NuGet-PackageNPublish

This project creates a Visual Studio extension (VISX) containing Project templates and a packaging MSBuild targets
file to allow easier Package&#39;n&#39;Publish integration with TFS (or other CI) builds.

It was presented at Developer! Developer! Developer! South West 4 (http://www.dddsouthwest.com) on 26th May 2012, and
in an updated form at DDDNorth 2 on 13th October 2012.

## Requirements

- Visual Studio 2012 SP1.
- Visual Studio 2012 SP1 SDK.
- NuGet Package Manager 1.8 or above.

## Getting Started

There's a handy screencast demonstrating how to get started on YouTube:
- http://www.youtube.com/watch?v=R6e4kV5dfIQ

### How to create a NuGetPackage using the NuGet.Package'n'Publish extension

- Install the extension into Visual Studio 
 - EITHER from a pre-built .visx file
 - OR by building the **NuGet.PackageNPublish.sln** solution (and then installing the generated .visx file)
- Add a new **NuGet.PackageNPublish** project to your solution. 
 - Give the project sensible name ending in .NuGetPackage 
  - If named like this, then the assembly from the packaging project is removed from the package automatically.
- Add references to the assemblies you want to include in your package
 - Any assembly ending in **.Silverlight.dll** will be put in the **lib/SL40** folder within the package.
 - Any other assembly will be put in the **lib/Net40** folder within the package.
 - Any assembly with **CopyLocal=false** will be skipped and **NOT** included in the package.
- Add dependencies on other NuGet packages
 - Don't forget to set the assemblies added by other NuGetPackages to **CopyLocal=False**!
- Set the **AssemblyTitle**, **AssemblyFileVersion** and **AssemblyDescription** in **Properties\AssemblyInfo.cs**
- Build the solution

- You now have NuGet (.npkg) and a Symbols (.symbols.nupkg) packages built in your project directory!

### How to publish a package using the NuGet.Package'n'Publish extension

- Build your solution with the **/p:PublishNuGetPackage=true** msbuild switch
 - To change the target repository from the default (http://nuget.org) use the **/p:PublishNuGetPackageTarget="http://myrepo.org"** switch
 - If you've not cached the API key for your custom repository, use the **/p:PublishNuGetPackageTargetKey="MySecretAPIKey"** switch

### How to publish a Symbols package using the NuGet.Package'n'Publish extension

- Build your solution with the **/p:PublishSymbolPackage=true** msbuild switch
 - To change the target repository from the default (http://symbolsource.org) use the **/p:PublishSymbolPackageTarget="http://mysymbolserver.org"** switch
 - If you've not cached the API key for your custom repository, use the **/p:PublishSymbolPackageTargetKey="MySecretAPIKey"** switch

## Still to do

Lots!

- A project template for "meta" packages (i.e. those that only contain dependencies on other NuGet packages)
- Documentation! Documentation! Documentation!

## Get Involved

Fork it... Fix it... Generate Pull requests... Use it!

For general chat about the NuGet.PackageNPublish tooling, there's also the JabbR channel - http://jabbr.net/#/rooms/NuGetPackageNPublish

## Thanks

Thanks have to go to my company, Landmark Information Group (http://www.landmark.co.uk / @LandmarkUK) for allowing this
tooling to be open-sourced under the Apache 2.0 license.