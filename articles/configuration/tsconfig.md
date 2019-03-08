---
title: Using a tsconfig.json file
author: uniqueiniquity
ms.author: belichtm
ms.date: 2/28/2019
ms.topic: article
ms.prod: .net
uid: tsconfig
---

# Using `tsconfig.json` for project configuration

The primary documentation concerning the `tsconfig.json` file can be found [on the TypeScript website](http://www.typescriptlang.org/docs/handbook/tsconfig-json.html).
There, you can find details on the file format, the available compiler options, and more.
Here, we will provide some tips for using the `tsconfig.json` file that might be helpful when using TypeScript in Visual Studio.

## Configuring JavaScript using a `jsconfig.json` file

Generally, you can edit JavaScript files in Visual Studio without needing a configuration file. Most of the options that are commonly used can be changed using the Visual Studio user interface. However, if you need to change one or more of the features that are not exposed, you can use a `jsconfig.json` file to configure your project. This file acts like a `tsconfig.json` file, but with some defaults that are specific to JavaScript development. In particular, these defaults are as follows:

- `allowJs` is enabled
- `maxNodeModuleJsDepth` is set to 2
- `skipLibCheck` is enabled
- `noEmit` is enabled

If you have a significant number of JavaScript files in your project and are experiencing performance issues related to editing JavaScript files, it can sometimes be advantageous to use a `jsconfig.json` file to specify the source files that constitute your project (as opposed to libraries that may be checked in and included in your solution). This will limit the number of files that Visual Studio is processing and may improve performance.

## Mixed TypeScript and JavaScript projects

By default, the set of files included in a project configured by a `tsconfig.json` file only includes TypeScript files. If you would also like JavaScript files to be included, then the `allowJs` option needs to be enabled. Furthermore, if you would like diagnostics to be reported in JavaScript files, then the `checkJs` option needs to be enabled.

When a single project includes some source files written in TypeScript and some source files written in JavaScript, it can be a little tricky to configure.
In particular, if `allowJs` is set to true and no output options are set (that is, `outFile` or `outDir`), the compiler will not be able to determine which JavaScript source files are intended to be source files and which are emitted files, and it will therefore produce an error.

In this scenario, if `outDir` or `outFile` cannot be used, it is reasonable to use a `tsconfig.json` without `allowJs` enabled to configure settings for the TypeScript files, and a `jsconfig.json` file (or a `tsconfig.json` file with `allowJs` and `noEmit` enabled) to configure settings for the JavaScript files. More details on this situation can be found [here](https://github.com/Microsoft/TypeScript/wiki/FAQ#why-am-i-getting-the-error-ts5055-cannot-write-file-xxxjs-because-it-would-overwrite-input-file-when-using-javascript-files).
