---
title: JavaScript Linting in Visual Studio
author: uniqueiniquity
ms.author: belichtm
ms.date: 6/14/2018
ms.topic: article
ms.prod: .net
uid: linting
---
# Linting

In order to enforce style concerns or help ensure correctness, you may want to use a linter. Here, we will discuss support in Visual Studio for linting JavaScript and TypeScript code.

## ESLint

Visual Studio natively supports ESLint for linting JavaScript, TypeScript, JSX and TSX files. By default, Visual Studio installs ESLint 6 and uses it to lint all open .js, .ts, .jsx and .tsx files. The set of rules that are used to lint your files is configured by default using the global ESLint configuration file (.eslintrc) in the User Home folder. Files are linted as you type, and results are shown in the error list and as squiggles in the editor. Information concerning ESLint rules and usage can be found in [the ESLint documentation](https://eslint.org/docs/user-guide/configuring).

### Configuration

Visual Studio offers several ways that you can configure its support for ESLint.

#### Configuring rules enforced by ESLint

As mentioned above, by default, ESLint will provide results based on the global ESLint configuration file, and you can configure your results by editing this file. However, if you would like to use a specific ESLint configuration for a particular directory, you can add a configuration file to that directory, and all files contained in that folder or any subdirectory will use that configuration file instead of the global one. More details can be found in [the ESLint documentation](https://eslint.org/docs/user-guide/configuring#using-configuration-files).

#### Configuring the version of ESLint

Visual Studio will use its installation of ESLint 6 by default. However, if you would like to use a different version, Visual Studio will pick up a local installation of ESLint and use it instead. In particular, if any parent directory of the file you want to be linted contains a `package.json` that lists ESLint as a dependency, as well as a `node_modules` folder with an installation of ESLint, then it will use that copy of the linter. Visual Studio is designed to be backwards compatible to ESLint 2.

> :warning:
> Before version 4, ESLint did not provide full location information for its results. Therefore, if you are using a version of ESLint earlier than 4, squiggles will appear under the first character of any error location, rather than underneath the whole error.

#### Configuring files to be ignored

Since Visual Studio now lints all files in your project or solution, you may want to choose some files or directories for it to ignore. To do so, Visual Studio supports the `.eslintignore` file. When such a file is located in a project's root directory, ESLint will use it to exclude the requested files or directories from linting. More information on usage of the `.eslintignore` file can be found in [the ESLint documentation](https://eslint.org/docs/user-guide/configuring#ignoring-files-and-directories).

> :pushpin:
> When using a `jsconfig.json` file, or when using a `tsconfig.json` file with `allowJS` enabled, the location of that file is considered to be the project root. Otherwise, the location of the project file (e.g., a `.csproj` file) is considered to be the project root. In scenarios without such a file, such as when using Open Folder or when the rooting `tsconfig.json` does not have `allowJS` enabled, an `.eslintignore` file in the User Home folder will be recognized.

> :pushpin:
> Since ASP.NET Core projects frequently include JavaScript libraries in the `wwwroot\lib` directory, files in that directory will not be linted by default. If you do want these files to be linted, you can re-include that directory or any file or subdirectory it contains by using an `.eslintignore` file.

### Settings
ESLint support can be enabled or disabled under Tools -> Options -> Text Editor -> JavaScript/TypeScript -> Linting. Here, you can also reset the global ESLint configuration file to the default recommended by Visual Studio.

Additionally, you can choose to lint your whole project or solution (as opposed to only open files) by selecting "Lint all files included in project, even closed files" under Tools -> Options -> Text Editor -> JavaScript/TypeScript -> Linting.

## TypeScript and ESLint
Visual Studio uses the [@typescript-eslint/parser](https://github.com/typescript-eslint/typescript-eslint/tree/master/packages/parser) to enable linting for TypeScript files. 

### Rules that require type information
The global ESLint configuration file includes some rules for TypeScript from [@typescript-eslint/plugin](https://github.com/typescript-eslint/typescript-eslint/tree/master/packages/eslint-plugin), but does not include any of the rules that require type information. Enabling these rules requires a `tsconfig.json` that is specified in the ESLint configuration file (search for the term **parserOptions** [here](https://github.com/typescript-eslint/typescript-eslint/tree/master/packages/eslint-plugin)). If you would like to use these rules, we recommend you set up a local installation of ESLint as described above. 