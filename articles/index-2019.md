# JavaScript and TypeScript in Visual Studio 2019

## Overview
Visual Studio 2019 provides rich support for JavaScript development, both via JavaScript directly, and via
the [TypeScript programming language](http://www.typescriptlang.org), which was developed to provide a more
productive and enjoyable JavaScript development experience - especially when developing projects at scale. You can write JavaScript or TypeScript code in Visual Studio for many application types and services.


## JavaScript Language Service
The JavaScript experience in Visual Studio 2019 is powered by the same engine that provides TypeScript support. This gives you better feature support, richness, and integration immediately out-of-the-box.

The option to restore to the legacy JavaScript language service is no longer available. Users will now have the new JavaScript language service out-of-the-box. The new language service is solely based on the TypeScript language service, which is powered by static analysis. This enables us to provide you with better tooling, so your JavaScript code can benefit from richer IntelliSense based on type definitions. The new service is lightweight and consumes less memory than the legacy service, providing you with better performance as your code scales. We have also improved performance of the language service to handle larger projects.

The corresponding version of the language service will now be automatically loaded in projects that have the TypeScript NuGet package (with TypeScript 3.2 and up) or npm package (with TypeScript 2.1 and up) installed.


## Building TypeScript

In Visual Studio 2017 and 2019, there are three ways of building TypeScript files in a VS project:

1.	Install the TypeScript NuGet package and use MSBuild to build

2.	Install the TypeScript SDK and use MSBuild to build.

3.	Install the TypeScript npm package and use a separate build tool

> The “TypeScript SDK” refers to the component that comes bundled with VS 2017 as well as a standalone download from the Download Center / VS Marketplace (INSERT LINK TO TS 3.3 FROM MARKETPLACE). The component includes the TypeScript compiler and the language service.

For projects developed in Visual Studio 2019, we encourage you to use the TypeScript NuGet and npm packages for greater portability across different platforms and environments.

## Projects
UWP JavaScript apps are no longer supported in Visual Studio 2019. You cannot create or open JavaScript UWP projects (files with extension .jsproj). You can learn more via our documentation (NEED LINK) on creating Progressive Web Apps (PWAs) that run well on Windows.


## Debugging 

Launch Google Chrome with custom arguments and debug your JavaScript applications all within the Visual Studio IDE.
Debug unit tests in Node.js projects. 


## Editor
We no longer show diagnostics of closed JavaScript/TypeScript files in the error list by default in order to get you faster performance and show you relevant errors. If you do choose to enable it in closed files, you can go to Tools > Options > Text Editor > JavaScript/TypeScript > Project and uncheck the option to "Only report diagnostics for files opened in the editor".

