# Automatic Type Acquisition

## Overview

In Visual Studio and Visual Studio Code, type declarations for JavaScript libraries will automatically be downloaded.
These type declarations are used to populate completion lists, signature help, and documentation in JS files.
You can seamlessly write JS code and get great Intellisense for most commonly used JavaScript libraries.

These declaration files are provided by the DefinitelyTyped community effort.
Declarations may be incomplete or missing; always refer to your library's documentation as the final word.

## Acquisition Triggers

Visual Studio will only download types for libaries you're using in your project.
Detection of which libraries you're using occurs based on minified files in your project and imports in your code.

#### Minified Files

When a file named *something*.min.js is in your project, Visual Studio will exclude this file from code analysis and instead attempt to download types for the *something* library.
Most variants of common minified filenames (such as `jquery.5.2.min.js`) are recognized by this check.

#### Imports

When your code contains imports such as
```ts
var yargs = require('yargs');
```
or
```ts
import React from 'react';
```
Visual Studio will automatically download types for the imported libraries.

## Caveats

Automatic type acquisition works for almost every popular library, but there are some things to keep in mind.

 * The download process is not instantaneous. You may have to wait a few moments after importing a module before its types are available.
 * Not every library has types. Check https://aka.ms/types to see if a types package for a library exists. When a library doesn't have types, you'll see the default completion list, which is just a list of tokens in the current file.
 * Automatic type acquisition will always download the declaration file for the latest version of a library. If you're using a different version, there may be mismatches between what's shown in Intellisense and what's actually available at runtime
 * Declaration files are provided by the community and may not be 100% accurate or complete. Always refer to official documentation if you're unsure.

## Troubleshooting

If you're not seeing Intellisense features for a library, you might try one or more of the following troubleshooting procedures.

#### Reload the Solution

If the JavaScript language service encounters an error, it may fail to recognize new types.
Reloading the solution will typically fix the problem.

#### Clearing the Cache

In rare instances, the NPM installation of the local types cache may be corrupted.
Close any running instances of Visual Studio and delete the folder `%LOCALAPPDATA%\Microsoft\TypeScript`.

## Configuration

You can change how type acquisition works by including a `jsconfig.json` file in the root of the project.
See the [VS Code documentation](https://code.visualstudio.com/docs/languages/jsconfig) for more information on this file.
In your jsconfig, you can include a `typeAcqusition` property to change acquisition settings:
```json
{
    "typeAcquisition": {
        "enable": true,
        "include": ["react"],
        "exclude": ["leftpad"]
    }

}
```

#### `enable`

The default is `true`.
You can set `enable` to `false` to completely disable type acquisition.

#### `exclude`

If you need any libraries to not get types acquired automatically (for example, you may have a local version), you can add an entry to the `exclude` array.
Items in this list will not have their types acquired or included in the project.
However, minified files (as described above) will still be excluded from the project.

#### `include`

Conversely, `include` will add types to the project, even if they're not otherwise used.

