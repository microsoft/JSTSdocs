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
|2.2.1|2420, 2720|[Implement interface members](#implement-interface-members)|
|2.2.1|2515, 2653|[Implement abstract members from base class](#implement-abstract-members-from-base-class)|
|2.2.1|2662, 2663|[Prepend `this.` to member access](#prepend-this-to-member-access)|
|2.2.1|2689|[Change `extends` to `implements`](#change-extends-to-implements)|
|2.2.1|17009|[Move `super()` call ahead of `this` access](#move-super-call-ahead-of-this-access)|
|2.3.0|All|[Suppress JS diagnostic](#suppress-js-diagnostic)|
|2.4.0|2551, 2552|[Correct misspelled name](#correct-misspelled-name)|
|2.4.1|6133, 6138|[Handle unused symbol](#handle-unused-symbol)|
|2.5.0|2713|[Rewrite as indexed access type](#rewrite-as-indexed-access-type)|
|2.5.0|8020|[Convert JSDoc type to TS type](#convert-jsdoc-type-to-ts-type)|
|2.6.1|1329|[Call decorator factory expression](#call-decorator-factory-expression)|
|2.6.1|7005, 7006, 7008, 7010, 7019, 7032, 7033, 7034|Annotate with inferred type|
|2.6.1|2307, 7016|Install @types for JS module|
|2.7.0|1219|[Set missing `experimentalDecorators` option](#set-missing-experimentaldecorators-option)|
|2.7.0|1308|[Add `async` modifier to function containing `await`](#add-async-modifier-to-function-containing-await)|
|2.9.0|2724|[Fix spelling of imported module](#fix-spelling-of-imported-module)|
|2.9.0|7027|[Remove unreachable code](#remove-unreachable-code)|
|2.9.0|80005|[Convert `require` call to `import`](#convert-require-call-to-import)|
|2.9.1|1340|[Add missing `typeof`](#add-missing-typeof)|
|2.9.1|7028|[Remove unused label](#remove-unused-label)|
|3.0.0|1337|[Convert to mapped object type](#convert-to-mapped-object-type)|
|3.2.1|2348|[Add missing new operator](#add-missing-new-operator)|
|3.2.1|2352|[Add convert to `unknown` for non-overlapping types](#add-convert-to-unknown-for-non-overlapping-types)|
|3.2.1|7051|[Add name to nameless parameter](#add-name-to-nameless-parameter)|

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

**After - Property**

```ts
class C {
    Prop2: number;
    Prop1: number;
}

const c = new C();
c.Prop2 = 1;
```

**After - Index Signature**

```ts
class C {
    [x: string]: number;
    Prop1: number;
}

const c = new C();
c.Prop2 = 1;
```

**Notes**

 * The receiver must have a class type.

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

 **Before - TS2662**
* For static members
```ts
class C {
    static m() { C.m(); }
    n() { m(); }
}
```

**After**

```ts
class C {
    static m() { C.m(); }
    n() { C.m(); }
}
```

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

#### Suppress JS Diagnostic

**Before**

```js
// @ts-check

x++;
```

**After - Suppress Single**

```js
// @ts-check

// @ts-ignore
x++;
```

**After - Suppress File**

```js
// @ts-nocheck


x++;
```

#### Correct Misspelled Name

**Before - TS2551**

```ts
class C {
    Prop1: number;
}

const c = new C();
c.Prop2 = 1; // TS2551
```

**After**

```ts
class C {
    Prop1: number;
}

const c = new C();
c.Prop1 = 1;
```

**Before - TS2552**

```ts
let variable1 = 1;
variable2++; //TS2552
```

**After**

```ts
let variable1 = 1;
variable1++;
```

**Notes**

 * There are restrictions on what counts as a misspelling - the lengths must match and be greater than 3, etc.

#### Handle Unused Symbol

**Before - TS6133**

```ts
// { "compilerOptions": { "noUnusedParameters": true } }
function F(x: number) { //TS6133
}
```

**After - Remove Declaration**

```ts
// { "compilerOptions": { "noUnusedParameters": true } }
function F() {
}
```

**After - Prepend Underscore**

```ts
// { "compilerOptions": { "noUnusedParameters": true } }
function F(_x: number) {
}
```

**Before - TS6138**

```ts
// { "compilerOptions": { "noUnusedLocals": true } }
class C {
    constructor(private x: number) { //TS6138
    }
}
```

**After - Remove Declaration**

```ts
// { "compilerOptions": { "noUnusedLocals": true } }
class C {
    constructor() {
    }
}
```

**After - Prepend Underscore**

```ts
// { "compilerOptions": { "noUnusedLocals": true } }
class C {
    constructor(private _x: number) {
    }
}
```

**Notes**

 * Prepending an underscore to a constructor parameter declaring a property doesn't fix the error.

#### Rewrite as Indexed Access Type

**Before - TS2713**

```ts
interface I {
    x: number;
}

let z: I.x; //TS2713
```

**After**

```ts
interface I {
    x: number;
}

let z: I["x"];
```

**Notes**

 * Presently, doesn't work for classes.

#### Convert JSDoc Type to TS Type

**Before - TS8020**

```ts
// { "compilerOptions": {"strictNullChecks": true} }

let x: ?number; //TS8020
```

**After - null**

```ts
// { "compilerOptions": {"strictNullChecks": true} }

let x: number | null;
```

**After - null, undefined**

```ts
// { "compilerOptions": {"strictNullChecks": true} }

let x: number | null | undefined;
```

**Notes**

 * Not offered in JS files.

#### Call Decorator Factory Expression

**Before - TS1329**

```ts
// { "compilerOptions": {"experimentalDecorators": true, "target": "es5"} }

function DecoratorFactory() {
    return function (target, propertyKey: string, descriptor: PropertyDescriptor) {
    }
}

class C {
    @DecoratorFactory //TS1329
    M() { }
}
```

**After**

```ts
// { "compilerOptions": {"experimentalDecorators": true, "target": "es5"} }

function DecoratorFactory() {
    return function (target, propertyKey: string, descriptor: PropertyDescriptor) {
    }
}

class C {
    @DecoratorFactory()
    M() { }
}
```

#### Set Missing `experimentalDecorators` Option

**Before - TS1219**

```ts
// @Filename: /dir/a.ts
declare const decorator: any;

class A {
    @decorator method() {};
};
```

```ts
// @Filename: /dir/tsconfig.json
{
    "compilerOptions": {
    }
}
```

**After**

```ts
// @Filename: /dir/a.ts
declare const decorator: any;

class A {
    @decorator method() {};
};
```

```ts
// @Filename: /dir/tsconfig.json
{
    "compilerOptions": {
        "experimentalDecorators": true,
    }
}
```

**Notes**
 * Experimental support for decorators is a feature that is subject to change in a future release.

#### Add `async` Modifier to Function Containing `await`

**Before - TS1308**

```ts
function f() {
    await Promise.resolve();
}
```

**After**

```ts
async function f() {
    await Promise.resolve();
}
```

#### Fix Spelling of Imported Module

 **Before - TS2724**

 ```ts
// @Filename: file1.ts
export const fooooooooo = 1;
 ```

 ```ts
// @Filename: file2.ts
import {fooooooooa} from "./file1"; fooooooooa;
 ```

 **After**

 ```ts
// @Filename: file1.ts
export const fooooooooo = 1;
 ```

 ```ts
// @Filename: file2.ts
import {fooooooooo} from "./file1"; fooooooooa;
 ```

#### Remove Unreachable Code

**Before - TS7027**

```ts
function f() {
    return 1;
    return 2;
}
```

**After**

```ts
function f() {
    return 1;
}
```

#### Convert `require` Call to `import`

**Before - TS80005**

```ts
const a = require("a");
```

**After**

```ts
import a = require("a");
```

#### Add Missing `typeof`

**Before - TS1340**

```ts
 declare module "foo" {
     const a = "foo"
     export = a
 }
 const x: import("foo") = import("foo");
```

**After**

```ts
 declare module "foo" {
     const a = "foo"
     export = a
 }
 const x: typeof import("foo") = import("foo");
```

#### Remove Unused Label

**Before - TS7028**

```ts
label1: while (1) {}
```

**After**

```ts
while (1) {}
```

#### Convert to Mapped Object Type

**Before - TS1337**

```ts
 type K = "foo" | "bar";
 interface SomeType {
     a: string;
     [prop: K]: any;
 }
```

**After**
```ts
 type K = "foo" | "bar";
 type SomeType = {
    [prop in K]: any;
} & {
    a: string;
};
```

#### Add Missing New Operator

**Before - TS2348**

```ts
class C {
}
var c = C();
```

**After**

```ts
class C {
}
var c = new C();
```

#### Add Convert to `unknown` for Non-Overlapping Types

**Before - TS2352**

```ts
const s1 = 1 as string;
const o1 = s + " word" as object;

const s2 = <string>2;
const o2 = <object>s2;
```

**After**

```ts
const s1 = 1 as unknown as string;
const o1 = s + " word" as unknown as object;

const s2 = <string><unknown>2;
const o2 = <object><unknown>s2;
```

#### Add Name to Nameless Parameter

**Before - TS7051**
```ts
var x: (number) => string;
```
**After**

```ts
var x: (arg0: number) => string;
```