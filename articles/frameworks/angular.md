# Angular support

You can use Visual Studio to edit Angular projects.
With the Angular Language Service plugin installed, you can use Visual Studio in Angular projects to:
 * Navigate between templates and code
 * See Intellisense information in inline templates and template files
 * Get immediate error feedback for errors in Angular syntax
 * Write JavaScript or TypeScript code

See the sample repo at https://github.com/Microsoft/angular2-in-visual-studio for setup instructions and a complete walkthrough.

Note that your project should use the `.ngml` file extension rather than `.html`. Angular will understand templates with any extension and this convention allows VS to load custom Angular behavior for these files.

## Feature Overview

In addition to the normal Visual Studio features when writing TypeScript or JavaScript, you'll see new behavior for Angular code in both kinds of tempaltes.

### Inline Templates

You'll see Intellisense, including errors, Quick Info, and completion lists for inline template strings:
```ts
@Component({
  selector: 'app',
  template: '<span>{{prop1.toLowerCase()}}</span>',
})
export class InlineComponent {
  prop1 = 'hello';
  prop2 = 'world';
}
```

### Template Files

The same features in inline templates will work in `.ngml` template files:
```html
<h3>
  Angular 2 Seed
</h3>
<nav>
	<a [routerLink]="['/']" title={{prop1}}>
    Home
  </a>
  |
	<a [routerLink]="['/about']">
    About
  </a>
  |
	<a [routerLink]="['/github', 'angular']">
```

## Additional Resources

Note that some of these examples use `.html` files instead of `.ngml` and don't include instructions on setting up the Angular language service plugin.
Refer to [the Visual Studio Angular 2](https://github.com/Microsoft/angular2-in-visual-studio) repo for information on how to modify your `tsconfig.json` appropriately.

 * https://angular.io/guide/quickstart - Angular quick start guide
 * https://github.com/RyanCavanaugh/angular2-ngml-seed - Angular seed project using NGML files
 * https://adrientorris.github.io/aspnet-core/how-setup-angular-2-typescript-project-visual-studio-2017.html - Tutorial
 * http://www.mithunvp.com/angular-2-in-asp-net-5-typescript-visual-studio-2015/ - Another walkthrough
