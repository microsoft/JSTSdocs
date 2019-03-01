# Excessive CPU and/or memory usage
High CPU usage or memory usage by the Node.exe process that runs the JavaScript and TypeScript
language service is often caused by the amount of code loaded that needs to be analyzed. As a
first step, verify it is indeed the JavaScript/TypeScript language service process consuming the
resources. This is best done using Task Manager (most easily launched with Ctrl + Shift + Esc),
selecting "More details" in the bottom left if necessary, going to the "Details" tab, and adding
the "Command line" column (right click on the column headings and click on "Select columns"). The
language service process is the Node.exe process running the `tsserver.js` script, as shown below:

<img src="../../images/taskmanager.png" width="1600px"/>

If it is indeed the offending process, often the best way to reduce load is to reduce the amount
of source code analyzed, as shown below.

# Reducing the amount of source loaded

By default, without a `tsconfig.json` file present, a Visual Studio 2017 project will create
a TypeScript "context" that includes all the TypeScript files, and another for any JavaScript files. These
contexts may be controlled somewhat with TypeScript settings in the Visual Studio project file, however
for more control over the "contexts" and their settings, adding `tsconfig.json` files is recommended.

If one or more `tsconfig.json` files are present in a project, then a "context" will be created for
each `tsconfig.json` file, and any files not belonging to one of these contexts, will be placed into
a "Miscellaneous" context with default settings.

The language service works by statically analyzing the source code, and attempting to infer the shape
and types of the code; this is what powers the editor completion lists, signature help, goto definition, etc.
For TypeScript code, or JavaScript code with JsDoc annotations, this can be highly effective, however
for many JavaScript files - especially large libraries - this results in a lot of work, with often limited
results.

For some common JavaScript libraries, the langauge service can recognize the library files, and will
automatically fetch the type definitions for it rather than process the JavaScript code directly. For
some project structures however, this is insufficient, and assisting the language service via explicit
configuration can be highly beneficial.

The simpliest way to avoid loading large Javascript libraries, but still provide good IntelliSense, is to
have all such code under common directories which can be excluded from the context, and then listing the
libraries to fetch and include the type definitions for explicitly. For example, in the below configuration,
the large JavaScript libraries are included under the "js/lib" and "vendor" directories, so these have
been listed under the "exclude" setting. The "typeAcquisition" configuration is then provided to fetch and
include the definitions for the excluded libraries. (The other settings in this configuration file will be
explained further below).

**tsconfig.json**
```json
{
  "compilerOptions": {
    "allowJs": true,
    "noEmit": true,
    "disableSizeLimit": true,
    "skipLibCheck": true
  },
  "typeAcquisition": {
    "enable": true,
    "include": ["knockout", "underscore", "chartist"]
  },
  "exclude": [
      "node_modules",
      "js/lib",
      "vendor"
  ]
}
```

# Other optimizations to reduce overhead

## Project settings

The above `tsconfig.json` file contains several other options that may be beneficial, these are:

 - "disableSizeLimit": This will switch off the limit on the amount of JavaScript code loaded, which
 can cause the warning shown at the top of this page. Note however in doing so, there is a risk of
 "out of memory" errors in the language service if more code is loaded than can be processed.
 - "skipLibCheck": By default the language service will check the type definition files, ("*.d.ts" files).
 For a JavaScript only project, or projects using well-tested type definition files (such as
 those published via `@types` and fetched automatically), this can be of little value, so disabling
 this via this configuration option can be beneficial.
 - "noEmit": If the language service is not being used to "compile" the code (i.e. convert TypeScript
 into JavaScript, or convert ES2015 JavaScript into ES5 JavaScript), then this option should be set.

## Editor settings

Within Visual Studio 2017, the default behavior is to create the language service contexts for every
project in a solution. In VS2017 Update 3 an option was added to only create the contexts for projects
that have files open in the editor. This can significantly reduce memory usage, but does mean that
projects without files open may contain errors that will not show in the editor while editing. (Though
the errors will still be shown when performing a build).

To enable this option, select "Tools" / "Options" from the menu, navigate to "Text Editor" / "JavaScript/TypeScript"
 / "Project", and check the setting "Only analyze projects which contain files opened in the editor".

<img src="../../images/toolsoptionsproject.png" width="840px"/>

## Useful links

The below pages go over the configuration options in more detail:

 - https://www.typescriptlang.org/docs/handbook/tsconfig-json.html
 - https://www.typescriptlang.org/docs/handbook/compiler-options.html
 - https://www.typescriptlang.org/docs/handbook/declaration-files/consumption.html
