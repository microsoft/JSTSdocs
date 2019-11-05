# Troubleshooting TypeScript version issues

:warning: WORK IN PROGRESS :warning:

## Visual Studio picks the wrong version of TypeScript for IntelliSense

* If using the `<TypeScriptToolsVersion>` property confirm that the correct version of the SDK is installed
   * Tip: Using the Nuget package is preferred
* If using npm or nuget, confirm that the packages are restored
* Check the output window to confirm the version of TypeScript in use
  * Alternatively, check Task Manager (or PS command) to get the versions of running tsserver
* If there are multiple projects in the solution confirm that their selected TS versions match. Only one version of the language service can be loaded at a time, and the project with the highest version will be preferred.

## Visual Studio picks the wrong version of TypeScript for the build

* If using the `<TypeScriptToolsVersion>` property confirm that the correct version of the SDK is installed
   * Tip: Using the Nuget package is preferred
   
## Visual Studio picks the wrong version of TypeScript for compile-on-save

* Generally, the items under "[Visual Studio picks the wrong version of TypeScript for IntelliSense]()" should apply
* If the selected language service doesn't match the selected version for the build, compile-on-save is disabled to avoid conflicting code generation

## I am seeing Node processes in Task Manager that have different versions of TS running

* There is an instance of the tsserver process that powers syntactic features that's always on the latest TypeScript. This is by design.
