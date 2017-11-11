# Refactoring & Quick fixes

## Availability

### Refactorings

| TS Version | VS Version | Effects |
|-|-|-|
|2.6.?|?|Annotate with type from JSDoc|
|2.4.?|?|Convert to ES6 class|
|2.5.?|?|Extract function|
|2.6.?|?|Extract local|
|2.6.?|?|Install @types for JS module|
|2.7.?|?|Convert to default import|

### Code Fixes

| TS Version | VS Version | Error Codes | Effects |
|-|-|-|-|
|2.6.?|?|1329|Call decorator expression (?)|
|2.5.?|?|2713|Rewrite as the indexed access type (?)|
|2.3.?|?|All|Suppress JS diagnostics by adding `// @ts-nocheck`|
|2.2.?|?|2339, 2551|Add missing member|
|2.6.?|?|7016|Install @types for JS module|
|2.2.?|?|2515, 2653|Implement abstract members from base class|
|2.2.?|?|2420|Implement interface members|
|2.2.?|?|17009|Move `super()` call ahead of `this` access|
|2.2.?|?|2377|Synthesize missing `super()` call|
|2.2.?|?|2689|Change `extends` to `implements`|
|2.2.?|?|2663|Prepend `this.` to member access|
|2.5.?|?|8020|Convert JSDoc type to TS type (?)|
|2.4.?|?|2551, 2552|Correct misspelled name|
|2.4.?|?|6133, 6138|Handle unused symbol (e.g. by deleting or prefixing with underscore)|
|2.1.?|?|2304, 2503, 2552, 2686|Add an appropriate import (?)|
|2.6.?|?|7005, 7006, 7008, 7010, 7019, 7032, 7033, 7034|Annotate with inferred type|
