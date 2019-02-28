---
title: Using a tsconfig.json file
author: uniqueiniquity
ms.author: belichtm
ms.date: 2/28/2019
ms.topic: article
ms.prod: .net
uid: tsconfig
---

# Using tsconfig.json for project configuration

The primary documentation concerning the `tsconfig.json` file can be found [on the TypeScript website](http://www.typescriptlang.org/docs/handbook/tsconfig-json.html).
There, you can find details on the file format, the available compiler options, and more.
Here, we will provide some tips for using the `tsconfig.json` file that commonly occur when using TypeScript in Visual Studio.

## JavaScript and tsconfig.json

By default, the set of files included in a project configured by a `tsconfig.json` file only includes TypeScript files. If you would also like JavaScript files to be included, then the `allowJs` option needs to be enabled. Furthermore, if you would like diagnostics to be reported in JavaScript files, then the `checkJs` option needs to be enabled.

To streamline this configuration, you can use a `jsconfig.json` file instead of a `tsconfig.json`. The two files are entirely the same, except that the `jsconfig.json` has `allowJs` set by default.

If your project only contains JavaScript source files, and you do not want to emit output files at all, you can set the `noEmit` compiler option and thereby prevent output files from being produced.

## Mixed TypeScript and JavaScript projects

When a single project uses includes some source files written in TypeScript and some source files written in JavaScript, it can be a little tricky to configure.
In particular, if `allowJs` is set to true and no output options are set (that is, `outFile` or `outDir`), the compiler will not be able to determine which JavaScript source files are intended to be source files and which are emitted files, and it will therefore produce an error.

In this scenario, if `outDir` or `outFile` cannot be used, it is reasonable to use a tsconfig.json without `allowJs` enabled to configure settings for the TypeScript files, and a `jsconfig.json` file (or a `tsconfig.json` file with `allowJs` enabled) to configure settings for the JavaScript files. Note that the latter configuration file should have `noEmit` set to resolve the error mentioned above. More details on this situation can be found [here](https://github.com/Microsoft/TypeScript/wiki/FAQ#why-am-i-getting-the-error-ts5055-cannot-write-file-xxxjs-because-it-would-overwrite-input-file-when-using-javascript-files).

## Settings to target the Node.js runtime

If you are targeting Node.js and not using a transpiler (such as TypeScript or Babel), make sure your `tsconfig.json` file has settings under the `compilerOptions` property to set the module type.

[!code-json[tsconfig](tsconfig.json?highlight=3)]

Note that this is done by default if you are targeting ES3 or ES5.
