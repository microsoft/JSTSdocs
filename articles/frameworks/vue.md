# Vue.js support

Visual Studio improved support for [Vue.js](https://vuejs.org/) framework, which enhances the experience when developing an application with Vue.js, JavaScript and TypeScript.

## Feature overview

In addition to the normal Visual Studio features when writing TypeScript or JavaScript, you'll see new behavior for Vue.js specific features:

* Supported Script, Style and Template blocks in .vue files.
* Recognize lang attribute on .vue files.

## Create a Vue.js project with the vue-cli

Vue.js provides and official CLI for quickly scaffolding projects. If you'll like to use it to create your application, follow the steps below to setup your developer environment.

> [!NOTE]
> This steps assumes you already have some knowledge about the Vue.js framework. If not, we suggest to visit [Vue.js](https://vuejs.org/) for details about it.

### Create a new Visual Studio project

We use an Empty ASP.NET Core Application (C#) for this example, but you can choose from a variety of projects and languages of your choice.

##### Create an Empty project:
1. Open Visual Studio and choose **File > New > Project** from the main menu.
1. Under **Visual C# > Web**, choose **ASP.NET Core Web Application** and click OK.
1. Select **Empty**, click OK.

##### Configure the project startup:
1. Open the file **./Startup.cs**, and add the following lines to the Configure method:

```c#
app.UseDefaultFiles() // Enables default file mapping on the web root.
app.UseStaticFiles(); // Marks files on the web root as servable.
```

### Install the vue-cli

To install the vue-cli, open a Command Prompt and type `npm install --g vue-cli` or `npm install -g @vue/cli` for version 3.0 (currently in beta).

#### Use the vue-cli to scaffold a new client application:
1. Go to your Command Prompt and change directory to your project root folder.
1. Type `vue init webpack ClientApp` and follow the additional questions.

##### Tweak the webpack config to output the built files to wwwroot:
1. Open the file **./ClientApp/config/index.js**, and change the `build.index` and `build.assetsRoot` to wwwroot path:

```js
// Template for index.html
index: path.resolve(__dirname, '../../wwwroot/index.html'),

// Paths
assetsRoot: path.resolve(__dirname, '../../wwwroot'),
```

##### Indicate the project to build the ClientApp everytime building is triggered:
1. Go to **Project properties > Build Events**
1. On **Pre-build event command line** type `npm --prefix ./ClientApp run build`.

##### Configure webpack's output module names:
1. Open the file **./ClientApp/build/webpack.base.conf.js**, and add the following properties to the output property:

```js
devtoolModuleFilenameTemplate: '[absolute-resource-path]',
devtoolFallbackModuleFilenameTemplate: '[absolute-resource-path]?[hash]'
```

#### Use the vue-cli 3.0 (currently in beta) with TypeScript
1. Go to your Command Prompt and change directory to your project root folder.
1. Type `vue create ClientApp` and choose **Manually select features**.
1. Choose Typescript and any other options desired.
1. Follow the additional questions.

##### Configure Vue.js-TypeScript project
1. Open the file **./ClientApp/tsconfig.json** and add to the compiler options `noEmit:true` for avoiding cluttering your project everytime you build on Visual Studio.
1. Create a vue.config.js file on ./ClientApp/ as below, for configuring webpack and setting the wwwroot folder:
```js
module.exports = {
	outputDir: '../wwwroot',

	configureWebpack: {
		output: {
			devtoolModuleFilenameTemplate: '[absolute-resource-path]',
			devtoolFallbackModuleFilenameTemplate: '[absolute-resource-path]?[hash]'
		}
	}
};
```

##### Building with vue-cli 3.0
There is an unknown issue with the vue-cli 3.0 that prevents automating the build process. Everytime you wish to refresh the wwwroot folder you will need to run the command `npm run build` on the ClientApp folder.

## Limitations

* Lang attribute only supports JavaScript and TypeScript languages.
* Lang attribute doesn't work with template or style tags.
* Debugging .vue files is not supported due to its preprocessed nature.
* .vue files are not recognized as modules. Shimming \*.vue files is necessary (vue-cli 3.0 template already includes this file).
* Running the command `npm run build` as a precompile task doesn't work when using vue-cli 3.0, for an unknown reason.

## Additional resources
* https://vuejs.org/v2/guide - Vue get started guide.
* https://github.com/vuejs/vue-cli - Vue CLI project.
* https://webpack.js.org/configuration/ - Webpack configuration documentation.
* https://github.com/madskristensen/vuepack2017 - Popular Vue.js extension for Visual Studio