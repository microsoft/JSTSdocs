# Troubleshooting TypeScript version issues

:warning: WORK IN PROGRESS :warning:

## I want to know which version of TypeScript Visual Studio is using

To check the version of TypeScript that is used for the language service, which powers editor features such as IntelliSense and compile-on-save, check the IntelliSense section of the Output window for a message such as:

```
Using TypeScript 3.8 for IntelliSense.
```

To check the version of the TypeScript compiler that is used when you use the Build command in Visual Studio, or when you run MSBuild from the command line, check the MSBuild logs. The MSBuild logs can be seen in the Build section of the Output tab. Ensure your MSBuild log verbosity is set to Normal or higher, then look for the command line that invokes `tsc.js`.

```
<path_to_node_exe>\node.exe <path_to_nuget_packages>\microsoft.typescript.msbuild\3.8.2\tools\tsc\tsc.js  <command line arguments>
```

Note that the version of the compiler used may be different for each project in the solution.
 
Also note this method only works for projects that use the TypeScript SDK or NuGet package. Some Node.js project templates use the TypeScript npm module in the build. Check package.json to find out the version of the compiler that the project uses.

## Visual Studio picks the wrong version of TypeScript for IntelliSense

* The language service can be loaded from the TypeScript SDK, NuGet package or the npm package depending on how your project is configured.
* If using the `<TypeScriptToolsVersion>` property confirm that the correct version of the SDK is installed
   * Tip: Using the Nuget package is preferred
* If using npm or nuget, confirm that the packages are restored
* Check the output window to confirm the version of TypeScript in use
  * Alternatively, check Task Manager (or PS command) to get the versions of running tsserver
* If there are multiple projects in the solution confirm that their selected TS versions match. Only one version of the language service can be loaded at a time, and the project with the highest version will be preferred. For a consistent experience, it is recommended that you configure all projects in the solution to use the same version of TypeScript.

## Visual Studio picks the wrong version of TypeScript for the build

* If using the `<TypeScriptToolsVersion>` property confirm that the correct version of the SDK is installed
   * Tip: Using the Nuget package is preferred
   
## Visual Studio picks the wrong version of TypeScript for compile-on-save

* Generally, the items under "[Visual Studio picks the wrong version of TypeScript for IntelliSense]()" should apply
* If the selected language service doesn't match the selected version for the build, compile-on-save is disabled to avoid conflicting code generation

## I am seeing Node processes in Task Manager that have different versions of TS running

* There is an instance of the tsserver process that powers syntactic features that's always on the latest TypeScript. This is by design.
