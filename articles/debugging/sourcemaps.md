# Using Source Maps

Visual Studio has the capability to use and generate source maps on JavaScript source files. This is often required if your source is minified or created by a transpiler like TypeScript. By defailt it will generate it for you.

> [!NOTE]
> We're going to assume you already know about source maps. If not, we suggest to read the page [Introduction to JavaScript Source Maps](https://www.html5rocks.com/en/tutorials/developertools/sourcemaps/).

See below if you'll like to know how to configure more advance settings. You can use either a tsconfig.json or the project settings, but not both.

## Configure source maps using tsconfig.json file
By adding a *tsconfig.json* file to your project you will indicate that the directory root is a TypeScript project. Just right right click *project > Add > New Item > Web > Scripts > TypeScript JSON Configuration File* to generate a file like below:

tsconfig.json:
```json
{
  "compilerOptions": {
    "noImplicitAny": false,
    "noEmitOnError": true,
    "removeComments": false,
    "sourceMap": true,
    "target": "es5"
  },
  "exclude": [
    "node_modules",
    "wwwroot"
  ]
}
```

### tsconfig compiler options
- **inlineSourceMap**: Emit a single file with source maps instead of having a separate file.
- **inlineSources**: Emit the source alongside the sourcemaps within a single file; requires *inlineSourceMap* or *sourceMap* to be set.
- **mapRoot**: Specifies the location where debugger should locate map files instead of generated locations. Use this flag if the .map files will be located at run-time in a different location than the .js files. The location specified will be embedded in the sourceMap to direct the debugger where the map files will be located.
- **sourceMap**: Generates corresponding .map file.
- **sourceRoot**: Specifies the location where debugger should locate TypeScript files instead of source locations. Use this flag if the sources will be located at run-time in a different location than that at design-time. The location specified will be embedded in the sourceMap to direct the debugger where the source files will be located.

For more details about the compiler options check the page [Compiler Options](https://www.typescriptlang.org/docs/handbook/compiler-options.html) on the TypeScript Handbook.

## Configure source maps using project settings
You can also configure the souce map settings on the project properties by right click *Project > Properties > TypeScript Build > Debugging*.

### Project settings
- **Generate source maps** (sourceMap tsconfig.json equivalent): Generates corresponding .map file.
- **Specify root directory of source maps** (mapRoot tsconfig.json equivalent): Specifies the location where debugger should locate map files instead of generated locations. Use this flag if the .map files will be located at run-time in a different location than the .js files. The location specified will be embedded in the sourceMap to direct the debugger where the map files will be located.
- **Specify root directory of TypeScript files** (sourceRoot tsconfig.json equivalent): Specifies the location where debugger should locate TypeScript files instead of source locations. Use this flag if the sources will be located at run-time in a different location than that at design-time. The location specified will be embedded in the sourceMap to direct the debugger where the source files will be located.