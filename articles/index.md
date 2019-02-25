# JavaScript in Visual Studio 2017

## Overview

Visual Studio 2017 provides rich support for JavaScript development, both via JavaScript directly, and via
the [TypeScript programming language](http://www.typescriptlang.org), which was developed to provide a more
productive and enjoyable JavaScript development experience - especially when developing projects at scale.

The language service underlying the JavaScript experience is all new for Visual Studio 2017, and is based
the same engine that provides TypeScript support. This provides for a level of feature support, richness,
and integration that was not possible with the previous JavaScript language service.

> :warning: With the new JavaScript language service, while many new features were enabled, some features 
> were also removed. In particular, [IntelliSense extensions](https://msdn.microsoft.com/en-us/library/hh874692.aspx)
> based on the prior language service will not run in the new language service, and the
> [XML documentation comments](https://msdn.microsoft.com/en-us/library/hh524453.aspx) format is no longer recognized.
> See the [JsDoc](types/jsdoc.md) topic for alternatives.

The below provides a high-level overview of various feature areas, with links to more in-depth documentation.

## Broad project support

While JavaScript or TypeScript files can be directly added to many project types, several project types
provide an enhanced experience via preconfigured new project templates, rich build support, integrated
debuggers, etc. These include ASP.NET & ASP.NET Core projects for web development, Node.js project support,
Cordova for mobile development, and features to support UWP applications.

## Custom configuration

Detailed configuration information may be provided for JavaScript & TypeScript either directly in the 
project property pages, or via the addition of a `tsconfig.json` file. Configuration details can include
settings such as which version of the language specification to target, which common libraries to provide
IntelliSense for, configuration settings for source-map support, settings to control type checking, etc.

Since Visual Studio 2017 Update 2, side-by-side versions of the language service are supported. This enables
different projects to target different versions of the language.

## Advanced editing features

The JavaScript and TypeScript languages use the same [Roslyn](https://github.com/dotnet/roslyn)-powered
editor in Visual Studio 2017 that is used for languages such as C#, Visual Basic, etc. This provides a
rich and consistent experience in which to view, edit, and navigate code.

## Rich type information

One of the key benefits of TypeScript is the volume and quality of "type definitions" for common
JavaScript frameworks that have been authored [by the community](https://github.com/DefinitelyTyped/DefinitelyTyped).

Using these type definitions, or type definitions from elsewhere (including your own), IntelliSense
can provide rich and accurate suggestions, and type checking can catch errors in code. For JavaScript projects,
by default, many of the type definitions needed can be automatically detected and added to the project.

## First class Node.js support

Visual Studio 2017 includes a "Node.js" workload, and when installed, project templates for creating
Node.js applications with either JavaScript or TypeScript are installed. Integrated into Visual Studio
are also features such as NPM package management, debugger support for various Node.js runtimes, unit 
testing support, and an Interactive Window.

See the [Node.js](nodejs/index.md) documentation for more information.

## Support for popular JavaScript frameworks

The JavaScript ecosystem is a vibrant and ever evolving landscape. There are a number of JavaScript projects
that have had an outsized impact on the community, among them React, Angular, Vue, WebPack, and Gulp -
to name a few. Visual Studio 2017 provides direct support for a number of these, with others support
via easily configured extensions.

## Integrated debugging for multiple platforms

Integrated into Visual Studio 2017 is support for debugging several JavaScript engines; among these
are Edge, Chrome, Internet Explorer, UWP and Node.js (both via the _legacy_ pre-Node.js 8.0 debugger, and 
the new post-Node.js 8.0 debugger).

These debuggers also have various levels of support for consuming "source-maps", which provide a format
and mechanism to map from one set of source code to another. For example, from the original TypeScript
code the author wrote, to the minified JavaScript output by WebPack that a debugger consumes.

## Integrated build environment

JavaScript and TypeScript are integrated directly into the Visual Studio build environment, which provides
for compiling either TypeScript or JavaScript code to an output location, along with build errors on
failure, publishing artifacts on success, etc. The Visual Studio editor also provides a 'compile-on-save'
feature, enabling the output to stay up-to-date as the developer works, without the need for a full build.

Beyond the MSBuild support provided by the installation
of Visual Studio, there is also a [TypeScript NuGet package](https://www.nuget.org/packages/Microsoft.TypeScript.MSBuild/)
to provide for cross-platform build.
