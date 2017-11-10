# Client-side debugging

Visual Studio provides debugging support for Chrome and Internet Explorer only. It will automatically attach breakpoints to JavaScript/TypeScript and embedded scripts on HTML files.

Dynamically generated files are not automatic though. See below to understand how the process works.

## Debugging JavaScript in dynamic files (using Razor)

Breakpoints on files generated with Razor syntax (cshtml, vbhtml) are not automatically attached when debugging. There are two approaches you can do in order to debug this kind of files:

1. **Place the `debugger;` statement where you want to break**: This will cause the dynamic script to stop execution and start debugging immediately while being created.
1. **Load the page and open the dynamic document on Visual Studio**: You'll need to open the dynamic file while debugging, place your breakpoint and refresh the page for this one to work. Depending if you're using Chrome or Internet Explorer you'll find the file using one of the following strategies:

   For Chrome, go to *Solution Explorer > Script Documents > YourPageName*. **Note**: When using Chrome you might get a screen indicating no source available between `script` tags. This is OK, just continue debugging.

   For Internet Explorer, go to *Solution Explorer > Script Documents > Windows Internet Explorer > YourPageName*.

Check more details on [Client-side debugging of ASP.NET projects in Google Chrome](https://blogs.msdn.microsoft.com/webdev/2016/11/21/client-side-debugging-of-asp-net-projects-in-google-chrome/).