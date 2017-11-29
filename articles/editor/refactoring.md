# Refactoring & Quick fixes

## Availability

### Refactorings

Refactorings are supported as of Visual Studio 2017 version 15.4.0.

| TS Version | Effects |
|-|-|
|2.4.0|[Convert to ES6 class](#convert-to-es6-class)|
|2.5.0|[Extract function](#extract-function)|
|2.6.0|[Extract constant](#extract-constant)|
|2.6.1|[Annotate with type from JSDoc](#annotate-with-type-from-jsdoc)|
|2.6.1|[Install @types for JS module](#install-types-for-js-module)|
|TBD|[Convert to default import](#convert-to-default-import)|


### Code Fixes

Code fixes are supported as of Visual Studio 2017 version 15.0.0.

| TS Version | Error Codes | Effects |
|-|-|-|
|2.1.4|2304, 2503, 2552, 2686|Add an appropriate import (?)|
|2.2.1|2339, 2551|[Add missing member](#add-missing-member)|
|2.2.1|2377|[Synthesize missing `super()` call](#synthesize-missing-super-call)|
|2.2.1|2420|[Implement interface members](#implement-interface-members)|
|2.2.1|2515, 2653|[Implement abstract members from base class](#implement-abstract-members-from-base-class)|
|2.2.1|2663|[Prepend `this.` to member access](#prepend-this-to-member-access)|
|2.2.1|2689|[Change `extends` to `implements`](#change-extends-to-implements)|
|2.2.1|17009|[Move `super()` call ahead of `this` access](#move-super-call-ahead-of-this-access)|
|2.3.0|All|Suppress JS diagnostics by adding `// @ts-nocheck`|
|2.4.0|2551, 2552|Correct misspelled name|
|2.4.1|6133, 6138|Handle unused symbol (e.g. by deleting or prefixing with underscore)|
|2.5.0|2713|Rewrite as the indexed access type (?)|
|2.5.0|8020|Convert JSDoc type to TS type (?)|
|2.6.1|1329|Call decorator expression (?)|
|2.6.1|7005, 7006, 7008, 7010, 7019, 7032, 7033, 7034|Annotate with inferred type|
|2.6.1|7016|Install @types for JS module|

## Examples

### Refactorings

#### Convert to ES6 Class

**Before**

```js
function cls() {
    this.x = 10;
}
cls.prototype.method = function () {
    return 3;
}
```

**After**

```js
class cls
{
    constructor()
    {
        this.x = 10;
    }
    method()
    {
        return 3;
    }
}
```

**Notes**

 * Only applies in JavaScript files.
 * The caret must be on an occurrence of the class name.

#### Extract Function

**Before**

```ts
function F(x: number)
{
    /*start*/return x + 1;/*end*/
}
```

**After - Nested Function**

```ts
function F(x: number)
{
    return newFunction();

    function newFunction()
    {
        return x + 1;
    }
}
```

**After - Top-Level Function**

```ts
function F(x: number)
{
    return newFunction(x);
}
function newFunction(x: number)
{
    return x + 1;
}
```

**Notes**

 * Extraction is best-effort - the resulting code may not compile or may behave subtly differently.
 * After the refactoring, the caret should be at the beginning of the call to the extracted function.

#### Extract Constant

**Before**

```ts
const PI = 3.141;
class Circle {
    readonly radius = 3;

    Area() {
        return /*start*/PI * (this.radius ** 2)/*end*/;
    }
}
```

**After - Local**

```ts
const PI = 3.141;
class Circle {
    readonly radius = 3;

    Area() {
        const newLocal = PI * (this.radius ** 2);

        return newLocal;
    }
}
```

**After - Property**

```ts
const PI = 3.141;
class Circle {
    readonly radius = 3;

    private readonly newProperty = PI * (this.radius ** 2);

    Area() {
        return this.newProperty;
    }
}
```

**Notes**

 * The extracted range must be an expression (exception
 * Extraction is best-effort - the resulting code may not compile or may behave subtly differently.  In particular, evaluation order may change.
 * After the refactoring, the caret should be at the beginning of the call to the extracted constant/property.

#### Annotate with Type from JSDoc

**Before**

```ts
/** @type {number} */
var x;
```

**After**

```ts
/** @type {number} */
var x: number;
```

**Notes**

 * The caret must be on the name of the declaration to be annotated.

#### Install @types for JS Module

**Before**

```ts
import "left-pad";
```

**After**

```ts
import "left-pad";
```

**Notes**

 * The caret must be on the name of module being imported.
 * No change is made to the source.  Instead, the corresponding @types module for the module being imported is installed in the project.
 * The refactoring will not be offered if no corresponding @types module is available.
 * If there is an error, the corresponding code fix will be offered instead.

#### Convert to Default Import

**Before**

```ts
// @Filename: /a.d.ts
declare const x: number;
export = x;
```

```ts
// @Filename: /b.ts
import * as a from "./a";
```

```ts
// @Filename: /c.ts
import a = require("./a");
```

**After**

```ts
// @Filename: /a.d.ts
declare const x: number;
export = x;
```

```ts
// @Filename: /b.ts
import a from "./a";
```

```ts
// @Filename: /c.ts
import a from "./a";
```

**Notes**

 * Currently this will only activate if `--allowSyntheticDefaultImports` is enabled.
 * The caret must be on the name of the module being imported.

### Code Fixes

#### Add Missing Member

**Before - TS2339**

```ts
class C {
}

const c = new C();
c.P = 1; // TS2339
```

**After - Property**

```ts
class C {
    P: number;
}

const c = new C();
c.P = 1;
```

**After - Index Signature**

```ts
class C {
    [x: string]: number;
}

const c = new C();
c.P = 1;
```

**Before - TS2551**

```ts
class C {
    Prop1: number;
}

const c = new C();
c.Prop2 = 1; // TS2551
```

**After - Correct Spelling**

```ts
class C {
    Prop1: number;
}

const c = new C();
c.Prop1 = 1;
```

**Notes**

 * The receiver must have a class type.
 * There are restrictions on what counts as a mispelling - the lengths must match and be greater than 3, etc.

#### Synthesize Missing `super()` Call

**Before - TS2377**

```ts
class Base {
}

class Derived extends Base {
    constructor() { //TS2377
    }
}
```

**After**

```ts
class Base {
}

class Derived extends Base {
    constructor() {
        super();
    }
}
```

**Notes**

 * Always calls `super()` without arguments.

#### Implement Interface Members

**Before - TS2420**

```ts
interface I {
    X: number
}

class C implements I { //TS2420
}
```

**After**

```ts
interface I {
    X: number
}

class C implements I {
    X: number;
}
```

#### Implement Abstract members from Base Class

**Before - TS2515**

```ts
abstract class A {
    abstract M();
}

class C extends A { //TS2515
}
```

**After**

```ts
abstract class A {
    abstract M();
}

class C extends A {
    M() {
        throw new Error("Method not implemented.");
    }
}
```

**Before - TS2563**

```ts
abstract class A {
    abstract M();
}

const c = class C extends A { //TS2563
}
```

**After**

```ts
abstract class A {
    abstract M();
}

const c = class C extends A {
    M() {
        throw new Error("Method not implemented.");
    }
}
```

#### Prepend `this.` to Member Access

**Before - TS2663**

```ts
class C {
    private x: number;
    Increment() {
        x++; //TS2663
    }
}
```

**After**

```ts
class C {
    private x: number;
    Increment() {
        this.x++;
    }
}
```

#### Change `extends` to `implements`

**Before - TS2689**

```ts
interface I {
}

class C extends I { //TS2689
}
```

**After**

```ts
interface I {
}

class C implements I {
}
```

#### Move `super()` Call Ahead of `this` Access

**Before - TS17009**

```ts
class Base {
}

class Derived extends Base {
    private x: number;
    constructor() {
        this.x = 1; //TS17009
        super();
    }
}
```

**After**

```ts
class Base {
}

class Derived extends Base {
    private x: number;
    constructor() {
        super();
        this.x = 1;
    }
}
```