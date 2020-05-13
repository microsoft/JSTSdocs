# Formatting

Use the **Formatting** page of the **Options** dialog box to set options for formatting code in the Code Editor. To access this page, on the menu bar, choose **Tools**, **Options**, and then expand **Text Editor**, **JavaScript**, and **Formatting**.

## General

These options determine when formatting occurs in Source view.

| Option | Description |
| --- | --- |
| **Format completed line on Enter** | Checkbox - When enabled, the Code Editor automatically formats the line when you choose the Enter key. |
| **Format completed statement on ;** | Checkbox - When enabled, the Code Editor automatically formats the line when you choose the semicolon key. |
| **Format opened block on {** | Checkbox - When enabled, the Code Editor automatically formats the line when you choose the opening brace key. |
| **Format completed block on }** | Checkbox - When enabled, the Code Editor automatically formats the line when you choose the closing brace key. |
| **Format on paste** | Checkbox - When enabled, the Code Editor reformats code when you paste it into the editor. The editor uses the currently defined formatting rules. If this option is not selected, the editor uses the original formatting of the pasted-in code. |

### Completions

| Option | Description |
| --- | ---|
| **Include auto imports from other modules in completion list** | Checkbox - When enabled, suggestions from other modules are included in the completion list. Selecting an imported suggestion will add an import statement for the relevant module to the document. |

| Option | Description |
| --- | ---|
| **Replace "." with "?." on completion in strictNullChecks mode** | Checkbox - When enabled and in strictNullChecks mode, suggestions for items which may be null or undefined are included in the completion list. Selecting one of these items will replace the preceding "." with the optional chaining operator "?.". Requires TS 3.7 or later. |

### Module Quote Preference

This option determines the quote style to be used for auto import completions and quick fixes.

| Option | Description |
| --- | ---|
| **Infer from existing imports** | Radio Button - When selected, the quote style for completions will be determined from those already existing in the document. Defaults to double.  |
| **Single (')** | Radio Button - When selected, single quotation marks will be used for completions. |
| **Double (")** | Radio Button - When selected, double quotation marks will be used for completions. |

### Module Specifier Preference

This option determines the path style to be used for auto import completions.

| Option | Description |
| --- | ---|
| **Use unqualified module names if possible** | Radio Button - When selected, import paths will be based on the `baseUrl` specified in your configuration file. |
| **Always use relative paths** | Radio Button - When selected, import paths will be relative to the file location. |

### Semicolon Preference

This option determines handling of optional semicolons.
| Option | Description |
| --- | ---|
| **Do not insert or remove any semicolons** | Radio Button - When selected, semicolons will not be inserted or removed.  |
| **Insert semicolons at statement ends** | Radio Button - When selected, semicolons will be inserted at statement ends. |
| **Remove unnecessary semicolons** | Radio Button - When selected, unnecessary semicolons will be removed. |

## New Lines
These options determine whether the Code Editor puts an open brace for functions and control blocks on a new line.

### Braces

| Option | Description |
| --- | ---|
| **Place open brace on new line for functions** | Checkbox - When enabled, the Code Editor moves the open brace associated with a function to a new line. |
| **Place open brace on new line for control blocks** | Checkbox - When enabled, the Code Editor moves the open brace associated with a control block (for example, `if` and `while` control blocks) to a new line. |

## Spacing

These options determine how spaces are inserted in Source view.

| Option | Description |
| --- | ---|
| **Insert space after comma delimiter** | Checkbox - When enabled, the Code Editor adds a space after comma delimiters. |
| **Insert space after semicolon in `for` statements** | Checkbox - When enabled, the Code Editor adds a space after each semicolon in the first line of a `for` loop. |
| **Insert space before and after binary operators** | Checkbox - When enabled, the Code Editor adds a space before and after binary operators (for example, +, -, &&, ||). |
| **Insert space after keywords in control flow statements** | Checkbox - When enabled, the Code Editor adds a space after JavaScript keywords in control flow statements. |
| **Insert space after `function` keyword for anonymous functions** | Checkbox - When enabled, the Code Editor adds a space after the `function` keyword for anonymous functions. |
| **Insert space after opening and before closing non-empty parenthesis** | Checkbox - When enabled, the Code Editor adds a space after the opening parenthesis and before the closing parenthesis if non-empty characters are present within the parentheses. |

## Formatting a selection

Formatting can be manaully invoked on both the document and selection levels.

### Format Document

Code formatting can be manually invoked on a document by choosing **Edit > Advanced > Format Document**, or by using the shortcut `Ctrl + K`, `Ctrl + D`.

For example:
```javascript
function CheckEquality(a,b)
{
    if (a===b)
    {
        return true;
    }
    return false;
}
```
becomes
```javascript

function CheckEqual(a, b) {
    if (a === b) {
        return true;
    }
    return false;
}
```

when document formatting is performed. In this example, the formatting options **Insert space after comma delimiter**, **Insert space before and after binary operators**, **Place open brace on new line for functions**, and **Place open brace on new line for control blocks were used**. Any options which have been disabled or changed in the settings menu will be respected.

### Format Selection 

Formatting can also be invoked on a specific block of code. To do so, select or highlight the code to format, and choose **Edit > Advanced > Format Selection**, or use the shortcut `Ctrl + K`, `Ctrl + F`. 

For example, by selecting *only* the inner `if` control block in the following code,

```javascript
function CheckEquality(a,b)
{
    if (a===b)
    {
        return true;
    }
    return false;
}
```
becomes
```javascript

function CheckEqual(a,b)
{
    if (a === b) {
        return true;
    }
    return false;
}
```

when selection formatting is performed. This time, only **Insert space before and after binary operators** and **Place open brace on new line for control blocks were used** were used. Notice in particular that the inner opening brace was formatted, while the outer brace was not.
