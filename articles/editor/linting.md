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

Visual Studio natively supports ESLint for linting JavaScript files, JSX files, and JavaScript contained in script blocks in HTML files. By default, Visual Studio installs ESLint 4 and uses it to lint all open .js files, .jsx files, and files containing JavaScript code in script blocks. The set of rules that are used to lint your files is configured by default using the global ESLint configuration file (.eslintrc) in the User Home folder. Files are linted as you type, and results are shown in the error list and as squiggles in the editor. Information concerning ESLint rules and usage can be found in [the ESLint documentation](https://eslint.org/docs/user-guide/configuring).

### Configuration

Visual Studio offers several ways that you can configure its support for ESLint.

#### Configuring rules enforced by ESLint

As mentioned above, by default, ESLint will provide results based on the global ESLint configuration file, and you can configure your results by editing this file. However, if you would like to use a specific ESLint configuration for a particular directory, you can add a configuration file to that directory, and all files contained in that folder or any subdirectory will use that configuration file instead of the global one. More details can be found in [the ESLint documentation](https://eslint.org/docs/user-guide/configuring#using-configuration-files).

#### Configuring the version of ESLint

Visual Studio will use its installation of ESLint 4 by default. However, if you would like to use a different version, Visual Studio will pick up a local installation of ESLint and use it instead. In particular, if any parent directory of the file you want to be linted contains a `package.json` that lists ESLint as a dependency, as well as a `node_modules` folder with an installation of ESLint, then it will use that copy of the linter. Visual Studio is designed to be backwards compatible to ESLint 2.

> [!WARNING]
> Before version 4, ESLint did not provide full location information for its results. Therefore, if you are using a version of ESLint earlier than 4, squiggles will appear under the first character of any error location, rather than underneath the whole error.

#### Configuring files to be ignored

Since Visual Studio now lints all files in your project or solution, you may want to choose some files or directories for it to ignore. To do so, Visual Studio supports the `.eslintignore` file. When such a file is located in a project's root directory, ESLint will use it to exclude the requested files or directories from linting. More information on usage of the `.eslintignore` file can be found in [the ESLint documentation](https://eslint.org/docs/user-guide/configuring#ignoring-files-and-directories).

> [!NOTE]
> When using a `jsconfig.json` file or a `tsconfig.json` file, the location of that file is considered to be the project root. Otherwise, the location of the project file (e.g., a `.csproj` file) is considered to be the project root. In scenarios without such a file, such as when using Open Folder, an `.eslintignore` file in the User Home folder will be recognized.

> [!NOTE]
> Since ASP.NET Core projects frequently include JavaScript libraries in the `wwwroot\lib` directory, files in that directory will not be linted by default. If you do want these files to be linted, you can re-include that directory or any file or subdirectory it contains by using an `.eslintignore` file.

### Settings
ESLint support can be enabled or disabled under Tools -> Options -> Text Editor -> JavaScript/TypeScript -> Linting. Here, you can also reset the global ESLint configuration file to the default recommended by Visual Studio.

Additionally, you can choose to lint your whole project or solution (as opposed to only open files) by selecting "Lint all files included in project, even closed files" under Tools -> Options -> Text Editor -> JavaScript/TypeScript -> Linting.

## TSLint
Currently, TSLint is not supported directly by Visual Studio. However, there are extensions available, or it can be used as a command-line tool.