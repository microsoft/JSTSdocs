# Refactoring & Quick fixes

## Availability

### Refactorings

Refactorings are supported as of Visual Studio 2017 version 15.4.0.

| TS Version | Effects |
|-|-|
|2.4.0|Convert to ES6 class|
|2.5.0|Extract function|
|2.6.0|Extract local|
|2.6.1|Annotate with type from JSDoc|
|2.6.1|Install @types for JS module|
|TBD|Convert to default import|


### Code Fixes

Code fixes are supported as of Visual Studio 2017 version 15.0.0.

| TS Version | Error Codes | Effects |
|-|-|-|
|2.1.4|2304, 2503, 2552, 2686|Add an appropriate import (?)|
|2.2.1|2339, 2551|Add missing member|
|2.2.1|2377|Synthesize missing `super()` call|
|2.2.1|2420|Implement interface members|
|2.2.1|2515, 2653|Implement abstract members from base class|
|2.2.1|2663|Prepend `this.` to member access|
|2.2.1|2689|Change `extends` to `implements`|
|2.2.1|17009|Move `super()` call ahead of `this` access|
|2.3.0|All|Suppress JS diagnostics by adding `// @ts-nocheck`|
|2.4.0|2551, 2552|Correct misspelled name|
|2.4.1|6133, 6138|Handle unused symbol (e.g. by deleting or prefixing with underscore)|
|2.5.0|2713|Rewrite as the indexed access type (?)|
|2.5.0|8020|Convert JSDoc type to TS type (?)|
|2.6.1|1329|Call decorator expression (?)|
|2.6.1|7005, 7006, 7008, 7010, 7019, 7032, 7033, 7034|Annotate with inferred type|
|2.6.1|7016|Install @types for JS module|
