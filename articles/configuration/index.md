# Project configuration

We have configured, external, and inferred project types. Whoop whoop!

> [!warning]
> Configured projects cannot include content in script blocks

## External projects
The MSBuild default, with all the goodness of XML

```xml
<TypeScriptToolsVersion>2.5</TypeScriptToolsVersion>
```

## Configured projects
Just add a `tsconfig.json` file, e.g.

```json
{
	"compilerOptions": {
		"target": "es5",
		"module": "commonjs"
	}
}
```

## Inferred projects
The leftovers will appear in the Virtual Projects node as:

<img src="../../images/virtualproject.png" width="375px"/>
