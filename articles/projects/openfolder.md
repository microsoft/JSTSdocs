# Open Folder projects in JavaScript and TypeScript 

Visual Studio 2017 introduces the ability to [develop code without without projects or solutions](https://docs.microsoft.com/en-us/visualstudio/ide/develop-code-in-visual-studio-without-projects-or-solutions), 
which enables you to open a folder of source files and immediatly start coding with support for IntelliSense,
browsing, refactoring, debugging, etc. In addition to these features, the Node Tools workload adds support
for building TypeScript files, managing npm packages, and running npm scripts.

To use open folder, select _Open Folder_ from the Start Page, or select _File | Open | Folder_ from 
the main menu. The Solution Explorer will immediatly display all the files in the folder, and you can open
any to begin editing. In the background Visual Studio will index the files to enable the npm, build, and debug 
functionality.

## npm Integration

If the folder you opened contains a `package.json` file, right-clicking that file will show a npm specific menu item. 

![npm menu in solution explorer](../../images/node/solution-explorer-npm-ctx.png) 

In the menu you can manage the packages installed by npm in the same way you 
[manage npm packages](../nodejs/npm.md) when using a project file. In addition the menu also allows
you to run scripts defined in the scripts element in `package.json`. These scripts will use the version of 
Node.js available on the `PATH`, and run in a new window.

## Build and Debug

### package.json
If the `package.json` in the folder specifies a `main` element, Debug will be available on the menu. 
Clicking this will start `node.exe` with the specifed script as it's argument.

### JavaScript files
JavaScript files can be debugged by right-clicking them, and selecting Debug from the menu. This will start 
`node.exe` with that script as it's argument.

### TypeScript files and tsconfig.json
If there is no `tsconfig.json` present in the folder, right-clicking a TypeScript file will you give you the
option to Build and Debug that file using `tsc.exe` with default options. 
(You need to build the file before you can debug.)

> [!Note]
> For building TypeScript code we use the newest version installed in 
`C:\Program Files (x86)\Microsoft SDKs\TypeScript`

If there is a `tsconfig.json` file present in the folder, right-clicking a TypeScript file will give you the 
option to Debug that TypeScript file, only if there is no `outFile` specified. If an `outFile` is specified you 
can Debug that file by right-clicking on the `tsconfig.json` file. The `tsconfig.json` file will also give you a
Build option to allow you specify compiler options.

> [!Note]
> More information about `tsconfig.json` can be found in the 
[tsconfig.json TypeScript Handbook page](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html).
