# Vue.js support

Visual Studio improved support for [Vue.js](https://vuejs.org/) framework, which enhances the experience when developing an application with Vue.js, JavaScript and TypeScript.

## Feature overview

In addition to the normal Visual Studio features when writing TypeScript or JavaScript, you'll see new behavior for Vue.js specific features:

* Supported Script, Style and Template blocks in .vue files.
* Recognize lang attribute on .vue files.
* Preconfigured Vue.js project and file templates.

## Using the Vue.js project and file templates

Visual Studio comes preconfigured with basic Vue.js templates. To use them you need to have installed the Node.js workload. If you don't have it installed yet, follow the steps localed on [Node.js requirements](../nodejs/requirements.md).

#### Create a basic Vue.js project
1. Open Visual Studio and choose **File > New > Project** from the main menu.
1. Under **JavaScript > Node.js** or **TypeScript > Node.js**, choose **Basic Vue.js Web Application** and click OK.

#### Adding a .vue file
1. Right click on any folder on **Solution Explorer > Add > New Item**.
2. Select either **JavaScript Vue Single File Component** or **TypeScript Vue Single File Component**, click Add.

#### Building and debugging
The Vue.js project template uses the build npm script by configuring a post build event. If you wish to modify this setting, open the project file and locate the line below:
```xml
<PostBuildEvent>npm run build</PostBuildEvent>
```
Debugging runs `node_modules\@vue\cli-service\bin\vue-cli-service.js serve`. You can see and modify this settings on the project properties.

## Create a Vue.js project with ASP.NET Core and the vue-cli

Vue.js provides an official CLI for quickly scaffolding projects. If you would like to use it to create your application, follow the steps below to setup your development environment.

> [!NOTE]
> This steps assumes you already have some knowledge about the Vue.js framework. If not, we suggest to visit [Vue.js](https://vuejs.org/) for details about it.

### Create a new ASP.NET Core project

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

* Lang attribute only supports JavaScript and TypeScript languages. The accepted values are: js, jsx, ts and tsx.
* Lang attribute doesn't work with template or style tags.
* Debugging script blocks in .vue files is not supported due to its preprocessed nature.
* TypeScript doesn't recognize .vue files as modules. A file like below is needed to tell TypeScript what a .vue files look like (vue-cli 3.0 template already includes this file).
```js
// ./ClientApp/vue-shims.d.ts
declare module "*.vue" {
    import Vue from "vue";
    export default Vue;
}
```
* Running the command `npm run build` as a pre-build event on the project properties doesn't work when using vue-cli 3.0.

## Additional resources
* https://vuejs.org/v2/guide - Vue get started guide.
* https://github.com/vuejs/vue-cli - Vue CLI project.
* https://webpack.js.org/configuration/ - Webpack configuration documentation.