# Intellisense

Intellisense is a general term used for a number of code completion features including member completion lists, parameter and signature help, and quick info. The TypeScript language service powers both JavaScript and TypeScript Intellisense. The language service uses type information from declaration files, JSDoc (JavaScript) and type annotations (TypeScript) along with its own type inference to give suggestions to help developers be more productive. [Look here](https://docs.microsoft.com/en-us/visualstudio/ide/javascript-intellisense?view=vs-2019) to learn more about these sources for type information.

## Completion lists

When you are trying to access members of an object with a known type, Intellisense will help by showing a list of applicable members that can be used. For example, here we show all the members that `console` has:

We can do this because the `console` object has been declared in `lib.dom.d.ts` as having a type with all these members. Also, based on the characters typed we can narrow the list of members to those that start with the same characters. Above, we see that typing `l` has automatically brought us to the `log` member. Hitting `Tab` will insert the highlighted member into your code. 

More information about completion lists can be found [here](https://docs.microsoft.com/en-us/visualstudio/ide/using-intellisense?view=vs-2017#list-members).

## Signature help

When calling a function or method it might be helpful to know the type for parameters, especially if there are many overloads. Here is an example of calling a function that has multiple overloads:

Signature help shows that given that we chose `"img"` as the first parameter, the next parameter is optional and should be of type `ElementCreationOptions`. Also, for the same reason, the return type is now inferred to be `HTMLImageElement`. This function is also declared in `lib.dom.d.ts` which allows the language service to provide the extra detail about it including documentation. More information on parameter help can be found [here](https://docs.microsoft.com/en-us/visualstudio/ide/using-intellisense?view=vs-2017#parameter-info).

## Quick info

Hovering over an identifier in your code will give you the declaration and documentation of it if it can. Similarly, selecting an item in the completion list will also invoke quick info. For more information, [see here](https://docs.microsoft.com/en-us/visualstudio/ide/using-intellisense?view=vs-2017#quick-info).
