# C# Style Guide

A general style guide for C#.

## Table of Contents

1. [Spacing](#spacing)
1. [Naming Conventions](#naming-conventions)
1. [Commas](#commas)
1. [Comments](#comments)
1. [Booleans](#booleans)
1. [Conditional Operator](#conditional-operator)
1. [Class vs Struct](https://github.com/dotnet/docs/blob/master/docs/standard/design-guidelines/choosing-between-class-and-struct.md#choosing-between-class-and-struct)
1. [If Statements](#if-statements)
1. [No Else Return](#no-else-return)
1. [Sort Imports](#sort-imports)
1. [Magic Numbers](#magic-numbers)
1. [Yoda Conditions](#yoda-conditions)
1. [Partial Classes](#partial-classes)
1. [Ordering](#ordering)
1. [Further Reading](#further-reading)
1. [License](#license)

## Spacing

- Use _spaces_ over _tabs_.
- Use four (4) spaces.
- `if`, `else`, `switch`, `while`, etc. must have a space before the brackets.

```csharp
// good
if (isValid)
{
    // Do something.
}

// bad
if(isValid)
{
    // Do something.
}
```

## Naming Conventions

### PascalCasing

Use PascalCasing for the following:

- _Classes_
- _Structs_
- _Functions_
- _Methods_
- _Enums_

Examples:

- `PropertyDescriptor`
- `HtmlTag`

The exception being for two-letter acronyms in which both letters are capitalized, for example; `IOStream`.

### camelCasing

Use camelCasing for the following:

- _variables_
- _arguments_

**[↑ back to top](#table-of-contents)**

## Commas

```csharp
// bad
var sentences = new List<string>() {
      "Lorem ipsum dolor sit amet, consectetur adipiscing elit."
    , "Duis volutpat consectetur ante, nec accumsan nunc blandit quis."
    , "Nunc hendrerit lacinia lectus, quis ultricies augue."
};

// good
var sentences = new List<string> {
    "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
    "Duis volutpat consectetur ante, nec accumsan nunc blandit quis.",
    "Nunc hendrerit lacinia lectus, quis ultricies augue."
};

// also good
var sentences = new List<string> {
    "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
    "Duis volutpat consectetur ante, nec accumsan nunc blandit quis.",
    "Nunc hendrerit lacinia lectus, quis ultricies augue.",
};
```

If you choose to adopt the trailing comma, be consistent with it and use it everywhere.

**[↑ back to top](#table-of-contents)**

## Comments

Add a space after your double slash comments.

```csharp
//bad comment

// Good comment.
```

Wrap long comments.

```csharp
// This is a very long comment so we will wrap it to a new line after it
// it surpasses 80 characters.
```

[Source<sup>1</sup>](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/inside-a-program/coding-conventions#commenting-conventions)

**[back to top](#table-of-contents)**

## Booleans

- Prefer to prefix your Booleans with _is_, _has_, _should_, _can_, or _was_.
- Prefer affirmative phrases e.g. `CanSeek` instead of `CantSeak`.

```csharp
// bad
public bool Enabled { get; set; }

// good
public bool IsEnabled { get; set; }
```

[Source<sup>1</sup>](https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/names-of-type-members#names-of-properties)

**[back to top](#table-of-contents)**

## Conditional Operator

The conditional operator, also known as the ternary conditional operator, should wrap to multiple lines if it is very long.

```csharp
// good
var foo = (a > b) ? value1 : value2;

// good
var food = (aLongValueName > anotherLongValueName)
    ? aLongValueName
    : anotherLongValueName;
```

**[back to top](#table-of-contents)**

## `If` Statements

- Avoid negated `if` statements when possible.

```csharp
// bad
if (!isValid)
{
    // This is false.
}
else
{
    // This is true.
}

// good
if (isValid)
{
    // This is true.
}
else
{
    // This is false.
}
```

- Consider avoiding nested code blocks in `if` statements.

```csharp
// okay
void DoSomething()
{
    if (isValid)
    {
        // Many
        // lines
        // of
        // code.
    }
}

// better
void DoSomething()
{
    if (!isValid)
    {
      return;
    }

    // Many
    // lines
    // of
    // code.
}
```

- Prefer using a single descriptive boolean variable instead of long or complex `if` evaluations.

```csharp
// bad
if (a >= 100 && b != 13 && c)
{
    // Do something.
}

// good
var isSomethingToDo = a >= 100 && b != 13 && c;

if (isSomethingToDo)
{
    // Do something.
}
```

> Why? This improves readability by clarifying when we should enter the `if` statement.

**[↑ back to top](#table-of-contents)**

## No Else Return

If an `if` block contains a return statement, the else block becomes unnecessary. Its contents can be placed outside of the block.

```csharp
// bad
function Foo()
{
    if (x)
    {
        return y;
    }
    else
    {
        return z;
    }
}

// good
function Foo()
{
    if (x)
    {
        return y;
    }

    return z;
}
```

[Source<sup>1</sup>](https://eslint.org/docs/2.0.0/rules/no-else-return)

**[↑ back to top](#table-of-contents)**

## Sort Imports

- Sort your `using` statements alphabetically.

```csharp
// bad
using System.Linq;
using System.Collection;
using System;

// good
using System;
using System.Collection;
using System.Linq;
```

**[↑ back to top](#table-of-contents)**

## Magic Numbers

- Magic numbers are generally defined as unnamed constants. Avoid magic numbers at all costs.

```csharp
// bad
var total = price + (price * 0.25M);

// good
const decimal TAX = 0.25M;
...
var total = price + (price * TAX);
```

The same principals can also be applied to strings:

```csharp
// bad
var output = "Success \u2714";

// good
private const string CHECKMARK = "\u2714";

...

var output = $"Success {CHECKMARK}";
```

**[↑ back to top](#table-of-contents)**

## Yoda Conditions

- Avoid Yoda conditions.

Yoda conditions are so named because the literal value of the condition comes first while the variable comes second. For example, the following is a Yoda condition:

```csharp
// bad
if ("red" == colour)
{
    // ...
}
```

This is called a Yoda condition because it reads as, "red is the color", similar to the way the Star Wars character Yoda speaks. Compare to the other way of arranging the operands:

```csharp
// good
if (colour == "red")
{
    // ...
}
```

[Source<sup>1</sup>](https://eslint.org/docs/2.0.0/rules/yoda)

**[↑ back to top](#table-of-contents)**

## Partial Classes

- Partial classes should use dot _._ notation in the file names.

e.g.

```csharp
MyClass.cs
MyClass.Foo.cs
MyClass.Bar.cs
```

> When should I use partial classes?

Partial classes should be considered if your classes are becoming very large (exceeding 1,000 lines) and cannot be broken up into multiple classes.
You may also use partial classes if a portion of your class is programmatically generated from an external source.

[Source<sup>1</sup>](https://stackoverflow.com/questions/1478610/naming-conventions-for-partial-class-files#answer-1478628)

**[↑ back to top](#table-of-contents)**

## Ordering

Within a _class_, _struct_ or _interface_:

- Constant Fields
- Fields
- Constructors
- Finalizers (Destructors)
- Delegates
- Events
- Enums
- Interfaces
- Properties
- Indexers
- Methods
- Structs
- Classes

Within each of these groups order by access:

- public
- internal
- protected internal
- protected
- private

Within each of the access groups, order by static, then non-static:

- static
- non-static

Within each of the static/non-static groups of fields, order by readonly, then non-readonly:

- readonly
- non-readonly

[Source<sup>1</sup>](http://stylecop.soyuz5.com/Ordering%20Rules.html), [Source<sup>2</sup>](https://stackoverflow.com/questions/150479/order-of-items-in-classes-fields-properties-constructors-methods#answer-310967)

**[↑ back to top](#table-of-contents)**

## Further Reading

- [Microsoft - Guidelines and Best Practices](https://docs.microsoft.com/en-us/dotnet/framework/wcf/guidelines-and-best-practices)
- [Microsoft - Coding Conventions](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/inside-a-program/coding-conventions)
- [Language Specification](https://www.microsoft.com/en-us/download/details.aspx?id=7029)

## License

(The MIT License)

Copyright (c) 2018

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the 'Software'), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
