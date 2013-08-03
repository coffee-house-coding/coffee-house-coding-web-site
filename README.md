Coffee House Coding Web Site
============================

The Coffee House Coding Web Site is an ASP.Net MVC 4 application which is built using Mono and publicly accessible NuGet packages.  The solution is developed with Xamarin Studio and runs on Mod_Mono on Apache 2.

Our local environment is:

Xamarin Studio v4.0.10
Mono v3.2.0
GTK 2.24.20
GTK# 2.12.0.0
NuGet Extension 0.5 using NuGet 2.6
Mac OS X 10.8.4

In order to use NuGet with Xamarin Studio, please install the NuGet extension. For installation details click here, https://github.com/mrward/monodevelop-nuget-addin. Scroll down to the README.md file and look for the installation section.  Follow the directions.

The source code in GitHub does not contain the NuGet packages. These will be downloaded from the NuGet feed upon first build if you have have Xamarin Studio configured to "Restore NuGet Packages".  To do this open the "Preferences" for Xamarin Studio and under "Projects/Build" check the box next to "Compile projects using MSBuild/XBuild".  Then on the sidebar click "NuGet/General" and check the box next to "Enable package restore".  Finally, open the file "NuGet.targets" under the ".nuget" project.  Check the following line:

<RestorePackages Condition="  '$(RestorePackages)' == '' ">true</RestorePackages>

Make sure it says true. Then build and the packages should be downloaded.  It is recommended to change the value to false for subsequent builds after you have the packages as enabling NuGet restore does slow down the build process.

On a Mac, we needed to do one other thing to make XBuild work correctly...

If you get an error like this after enabling XBuild...

could not import "$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v10.0\WebApplications\Microsoft.WebApplication.targets" (CoffeeHouseCodingWebSite)

... then you need to do the following ...

cd /Library/Frameworks/Mono.framework/Versions/Current/lib/mono/xbuild/Microsoft/VisualStudio
sudo ln -s v9.0/ v10.0

This will enable XBuild to find the Visual Studio 10.0 Microsoft.WebApplication.targets.  Such a solution will probably work for Linux too if you run into a similar problem.  We have not tried to run Xamarin Studio with NuGet on Windows.

