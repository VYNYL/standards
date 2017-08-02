# Typescript Styling Guidelines

Guidelines for Typescript language

## Names
1. Use PascalCase for type names.
2. Do not use "I" as a prefix for interface names.
3. Use PascalCase for enum values.
4. Use camelCase for function names.
5. Function names should start with a verb (get, set, update, put, send, is...)
6. Use camelCase for property names and local variables.
7. Do not use "_" as a prefix for private properties.
8. Use whole words in names when possible.
9. Single letter variables are discouraged except for cases where definition can be inferred (e.g. i = index).

## null and undefined
1. use undefined, do not use null.

## Flags
1. More than 2 related boolean properties on a type shoudl be turned into a flag.

## Comments
1. Use of [JSDoc](https://github.com/shri/JSDoc-Style-Guide) style comments for functions, interfaces, enums and classes is encouraged.
2. In line comments shall be used sparingly, code should be easily readable and logic flow should be apparent.

## Strings
1. Use Single quotes for strings.
2. Prefer template strings over concat strings eg ``My name is ${name}`` vs `'My Name is ' + name`

## Diagnostic and Error Messages
1. Use a period at the end of a sentence.
2. Use indfinite articles for indefinite entities.
3. Definite entities should be named ("User was not updated", "Role could not be applied to User").
4. When stating a rule, the subject should be in the singular ("A password cannot be shorter than 3 characters" instead of "Passwords cannot be ...")
5. Use present tense.

## General Constructs
1. Do not use for..in statements; instead use `ts.forEach`.
2. Try to use `ts.forEach`, `ts.map`, and `ts.filter` instead of loops when it is not strongly inconvenient.

## Style
1. Use arrow functions over anonymous function expressions.
2. Only surround arrow functions parameters when necessary.
3. Always surround loop and conditional bodies with curly braces (tsLint forces this by default as well).
4. Open curly braces always go on the same line as whatever necessitates them.
5. Parenthesized constructs should have no surrounding whitespace.
6. Use a single declaration per variable statement (`var x = 1; var y = 3;` over `var x = 1, y = 2`).
7. Else goes on the same line as the closing curly brace.
8. Four(4) spaces per indentation.
9. Classes end with new line character.
10. Ternary operators never fail or succeed to another ternary eg `true ? '1' : true2 ? '2' : ''`
11. If you need to drop to a new line, operators will stay on previous line eg 

        ```
            this.isTrue(true) ?
                true :
                false

            return this && this.isTrue() &&
                !this.isFalse()
        ```
