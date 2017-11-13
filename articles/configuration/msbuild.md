---
uid: msbuild
---

# MSBuild configuration

## TypeScript Tools Version
Since a particular machine may have multiple versions of TypeScript installed, MSBuild allows you to set the TypeScriptToolsVersion property in your project file to specify which version to use.
If this property is not set, MSBuild defaults to using the newest version of TypeScript that is installed. However, if you are using the TypeScript NuGet package instead, its version will override any setting in the project file.

## Props and Targets

There are two different sources of information that tell MSBuild how to handle TypeScript. The first, `Microsoft.TypeScript.Default.props`, establishes some default TypeScript compilation settings. The second, `Microsoft.TypeScript.targets`, gives instructions on how to handle TypeScript files as part of the building and cleaning processes. To include these in your project, you will need to (in most cases) import `Microsoft.TypeScript.Default.props` at the beginning of your project file and `Microsoft.TypeScript.targets` at the end, as shown [in the TypeScript handbook](http://www.typescriptlang.org/docs/handbook/integrating-with-build-tools.html#msbuild).

> [!NOTE]
> ASP.NET Core projects implicitly include these files, so an ASP.NET Core project file will not need to import them.

## Compilation Scenarios
There are two ways that files can be recognized by and therefore built with the project: either by the project file itself or by way of a tsconfig.json file.
### With TSConfig
One option for allowing MSBuild to recognize what TypeScript files are part of your project is by way of a tsconfig.json file. This configuration file can either be explicitly associated with your .csproj in the Content item list, or it can be simply included as part of the directory tree rooted at the directory containing your project file. Note that in the latter case, configuration files within a folder titled "node_modules", "bower_components", or "platforms" will not be considered in order to avoid duplicate symbol errors.

The tsconfig.json can either explicitly enumerate the files intended to be compiled (in the "includes" property) or it can exclude files that should not be compiled (in the "excludes" property). The file also allows you to set compile options that will override those set in the TypeScript Build page of your project's Properties. For more details, refer to [the discussion of tsconfig.json files](xref:tsconfig).

### Without TSConfig

If there is no discoverable tsconfig.json, MSBuild relies on the project file to determine what files to include. For this scenario, TypeScript files must be included using the TypeScriptCompile item list.

## Incremental Build

The `Inputs` and `Outputs` attributes of certain targets, such as `CompileTypeScript` or `CompileTypeScriptWithTSConfig` allow MSBuild to determine whether or not to skip the target. For targets that have these attributes defined, MSBuild compares the timestamps of the files specified by `Inputs` with those specified by `Outputs`. Since there is not always a one-to-one mapping between input files and output files (e.g., if `--outFile` is specified), MSBuild will rebuild all output files if at least one of the input files has been updated.

## Compilation Options

Similar to how the set of files to be compiled is specified, there are two ways to specify settings for the compiler. If a `tsconfig.json` exists, then it will specify the compilation settings. Otherwise, settings can be specified in the project file itself (between the imports of the props and targets files), as shown [in the TypeScript handbook](http://www.typescriptlang.org/docs/handbook/integrating-with-build-tools.html#msbuild). These settings are documented [in the handbook](http://www.typescriptlang.org/docs/handbook/compiler-options-in-msbuild.html) as well.