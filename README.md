# CoffeeScript Style Guide

This guide presents a collection of best-practices and coding conventions for the [CoffeeScript][coffeescript] programming language.

This guide is intended to be community-driven, and contributions are highly encouraged.

## Inspiration

The details in this guide have been very heavily inspired by several existing style guides and other resources. In particular:

- [PEP-8][pep8]: Style Guide for Python Code
- Bozhidar Batsov's [Ruby Style Guide][ruby-style-guide]
- [Google's JavaScript Style Guide][google-js-styleguide]
- [Common CoffeeScript Idioms][common-coffeescript-idioms]
- Thomas Reynolds' [CoffeeScript-specific Style Guide][coffeescript-specific-style-guide]
- Jeremy Ashkenas' [code review][spine-js-code-review] of [Spine][spine-js]
- The [CoffeeScript FAQ][coffeescript-faq]
- [Apiary's Coffeescript style guide][apiary-guide]

## Table of Contents

* [The CoffeeScript Style Guide](#guide)
    * [Code Layout](#code_layout)
        * [Tabs or Spaces?](#tabs_or_spaces)
        * [Maximum Line Length](#maximum_line_length)
        * [Blank Lines](#blank_lines)
        * [Trailing Whitespace](#trailing_whitespace)
        * [Optional Commas](#optional_commas)
        * [Encoding](#encoding)
    * [Module Imports](#module_imports)
    * [Whitespace in Expressions and Statements](#whitespace)
    * [Comments](#comments)
        * [Block Comments](#block_comments)
        * [Inline Comments](#inline_comments)
    * [Naming Conventions](#naming_conventions)
    * [Functions](#functions)
    * [Strings](#strings)
    * [Conditionals](#conditionals)
    * [Looping and Comprehensions](#looping_and_comprehensions)
    * [Extending Native Objects](#extending_native_objects)
    * [Exceptions](#exceptions)
    * [Annotations](#annotations)
    * [Miscellaneous](#miscellaneous)

<a name="code_layout"/>
## Code layout

<a name="file_endings"/>
### File Endings

Files should be terminated with a newline character.

UNIX line endings should always be used.

<a name='align_characters'/>
### Align Characters

Align similar characters.  Where readability is improved align characters which
appear in subsequent lines such as `=`, keywords such as `and` or `is`, `{`,
`[`, etc. Spacing should allow all values to be completed and include a single
padding whitespace character (see elephant example below).

```coffeescript
switch value
  when 1   then console.log 'one'
  when 'b' then console.log 'B'
  else          console.log 'no match'

a     = 1
b     = 2
c     = 25
apple = 'banana'

if animal in   heavy_animals and
   animal in   blue_animals  and
   animal in   mammals       and
   animal in   large_animals and
   animal isnt whale
  console.log 'elephant'
```

<a name="tabs_or_spaces"/>
### Tabs or Spaces?

Use **spaces only**, with **2 spaces** per indentation level. Never mix tabs and spaces.

<a name="maximum_line_length"/>
### Maximum Line Length

Limit all lines to a maximum of 80 characters.

<a name='object_braces'/>
### Object Braces

Omit object braces unless value is in an array, or it improves readability.

```coffeescript
inline = value: 56

example = [
  { sample: 'value' }
  { other : 'test'  }
]
```

<a name="blank_lines"/>
### Blank Lines

Separate top-level function and class definitions with a single blank line.

Separate method definitions inside of a class with a single blank line.

Use a single blank line within the bodies of methods or functions in cases where this improves readability (e.g., for the purpose of delineating logical sections).

<a name="trailing_whitespace"/>
### Trailing Whitespace

Do not include trailing whitespace on any lines.

<a name="optional_commas"/>
### Optional Commas

Avoid the use of commas before newlines when properties or elements of an Object or Array are listed on separate lines.

```coffeescript
# Yes
foo = [
  'some'
  'string'
  'values'
]
bar:
  label: 'test'
  value: 87

# No
foo = [
  'some',
  'string',
  'values'
]
bar:
  label: 'test',
  value: 87
```

<a name="encoding"/>
### Encoding

`UTF-8` is the preferred source file encoding.

<a name="module_imports"/>
## Module Imports

If using a module system (CommonJS Modules, AMD, etc.), `require` statements should be placed on separate lines.

```coffeescript
require 'lib/setup'

Backbone = require 'backbone'
```
These statements should be grouped in the following order:

1. Standard library imports _(if a standard library exists)_
2. Third party library imports
3. Local imports _(imports specific to this application or library)_

Each section should be separated by one blank line.

<a name="whitespace"/>
## Whitespace in Expressions and Statements

Avoid extraneous whitespace in the following situations:

- Immediately inside parentheses, brackets or braces

    ```coffeescript
       ($ 'body')    # Yes
       "#{ sample }" # Yes
       ( $ 'body' )  # No
       "#{sample}"   # No
    ```

- Immediately before a comma

    ```coffeescript
       console.log x, y  # Yes
       console.log x , y # No
    ```


- Always surround these binary operators with a single space on either side.
Additional spaces may be used on the left side to align operators for better readability.

    - assignment: `=`

        - _Note that this also applies when indicating default parameter value(s) in a function declaration_

           ```coffeescript
            test: (param    = null,
                   otherArg = 14) -> # Yes
            test: (param=null,
                   otherArg=14) ->   # No
           ```

    - augmented assignment: `+=`, `-=`, etc.
    - comparisons: `==`, `<`, `>`, `<=`, `>=`, `unless`, etc.
    - arithmetic operators: `+`, `-`, `*`, `/`, etc.

        ```coffeescript
           # Yes
           x       = 1
           y       = 1
           fooBar  = 3
           sample += 4
           test    * 0.5

           # No
           x = 1
           y = 1
           fooBar = 3
           sample += 4
           test * 0.5
        ```

<a name="comments"/>
## Comments

If modifying code that is described by an existing comment, update the comment such that it accurately reflects the new code.

The first word of the comment should be capitalized, unless the first word is an identifier that begins with a lower-case letter.

Comments should aim to explain the 'why' behind a piece of code and should be
written with proper punctuation unless very small.

Where possible and makes sense align comments for better readability (comments on their own line
should always be aligned to the current indent where code would go):

```coffeescript
value = Math.floor(29 * arg) # Note about accounting for edge case
console.log(value)           # continuation of note.
```


<a name="block_comments"/>
### Block Comments

Block comments apply to the block of code that follows them.

Each line of a block comment starts with a `#` and a single space, and should be indented at the same level of the code that it describes. A block comment should be padded by one empty row on top and bottom.

Paragraphs inside of block comments are separated by a line containing a single `#`.

```coffeescript
  #
  # This is a block comment. Note that if this were a real block
  # comment, we would actually be describing the proceeding code.
  #
  # This is the second paragraph of the same block comment. Note
  # that this paragraph was separated from the previous paragraph
  # by a line containing a single comment character.
  #

  init()
  start()
  stop()
```

<a name="inline_comments"/>
### Inline Comments

Inline comments are placed on the line immediately above the statement that they are describing.
If the inline comment is sufficiently short, it can be placed on the same line as the
statement (separated by a single space from the end of the statement).

All inline comments should start with a `#` and a single space.

Do not use inline comments when they state the obvious:

```coffeescript
  # No
  x = x + 1 # Increment x
```

However, inline comments can be useful in certain scenarios:

```coffeescript
  # Yes
  x = x + 1 # Compensate for border
```

<a name="naming_conventions"/>
## Naming Conventions

Use `camelCase` to name all variables, methods, and object properties.

Use `PascalCase` to name all classes.

_(The **official** CoffeeScript convention is camelcase, because this simplifies interoperability with JavaScript. For more on this decision, see [here][coffeescript-issue-425].)_

For constants, use all uppercase with underscores:

```coffeescript
CONSTANT_LIKE_THIS
```

Methods and variables that are intended to be "private" should begin with a leading underscore:

```coffeescript
_privateMethod: ->
```

<a name='objects'/>
## Objects

Objects should be nested in-line unless a level with multiple key/value pairs is
included.  Colons should be aligned for values of the same level.  Nested values
should start two characters deeper than the previous key.

```coffeescript
test = sample: nested: values: 'object' # Yes
test = sample:
         nested:
           values: 'object'             # No

test = sample: nested:
                 values   : [1, 2, 3]
                 meta_info: ['o', 't', 't'] # Yes

```

<a name="functions"/>
## Functions

_(These guidelines also apply to the methods of a class.)_

When declaring a function that takes arguments, always use a single space after the closing parenthesis of the arguments list:

```coffeescript
foo = (arg1, arg2) -> # Yes
foo = (arg1, arg2)->  # No
```

Do not use parentheses when declaring functions that take no arguments:

```coffeescript
bar = ->    # Yes
bar = () -> # No
```

Only use fat arrow syntax when `@` is needed within the function body

```coffeescript
foo = (bar) => console.log bar # No
foo = => console.log @bar      # Yes
```

Don't assign default arguments in front of positional arguments:

```coffeescript
bad = (foo = 'bar', baz) -> # No
bad = (foo, bar = 'baz') -> # Yes
```

When a function declaration cannot fit on a single line align the arguments one
per line in the following fashion:

```coffeescript
foo = (sample_name,
       sample_value,
       testing_object,
       control_value        = 789,
       randomization_factor = 16.0) -> # Yes

foo = (sample_name, sample_value, testing_object, control_value = 789, randomization_factor = 16.0) -> # No

foo = (sample_name,
       sample_value,
       testing_object,
       control_value = 789,
       randomization_factor = 16.0) -> # No
```

Note that when default parameter values are used they are aligned as mentioned
above.


In cases where method calls are being chained and the code does not fit on a single line, each call should be placed on a separate line and indented by one level (i.e., two spaces), with a leading `.`.

```coffeescript
[1..3]
  .map((x) -> x * x)
  .concat([10..12])
  .filter((x) -> x < 11)
  .reduce((x, y) -> x + y)
```

When calling functions, choose to omit or include parentheses in such a way that optimizes for readability. Keeping in mind that "readability" can be subjective, the following examples demonstrate cases where parentheses have been omitted or included in a manner that the community deems to be optimal:

```coffeescript
baz 12

brush.ellipse x: 10, y: 20 # Braces can also be omitted or included for readability

foo(4).bar(8)

obj.value(10, 20) / obj.value(20, 10)

print inspect value

new Tag(new Value(a, b), new Arg(c))
```

<a name="strings"/>
## Strings

Use string interpolation instead of string concatenation:

```coffeescript
"this is an #{ adjective } string"      # Yes
"this is an " + adjective + " string"   # No
```

Prefer single quoted strings (`''`) instead of double quoted (`""`) strings, unless
features like string interpolation are being used for the given string.

Use string blocks for large strings.

```
'''
  Sample large string block.  Notice how it is
  indented one level further than the code around
  it as well.
'''
```

<a name="conditionals"/>
## Conditionals

Choice between keywords such as `is`, `isnt`, `unless`, `if`, etc. should be
made with regards to code readability.

Multi-line if/else clauses should use indentation.  Use inline form
when the conditional body only contains one statement.

<a name="looping_and_comprehensions"/>
## Looping and Comprehensions

Take advantage of comprehensions whenever possible:

```coffeescript
  # Yes
  result = (item.name for item in array)

  # No
  results = []
  for item in array
    results.push item.name
```

To filter:

```coffeescript
result = (item for item in array when item.name is "test")
```

To iterate over the keys and values of objects:

```coffeescript
object = one: 1, two: 2
for key, value of object
  alert "#{ key } = #{ value }"
```

<a name="exceptions"/>
## Exceptions

Do not suppress exceptions.

<a name="annotations"/>
## Annotations

Use annotations when necessary to describe a specific action that must be taken against the indicated block of code.

Write the annotation on the line immediately above the code that the annotation is describing.

The annotation keyword should be followed by a colon and a space, and a descriptive note.

```coffeescript
  # FIXME: The client's current state should *not* affect payload processing.
  resetClientState()
  processPayload()
```

If multiple lines are required by the description, indent subsequent lines to align text:

```coffeescript
  # TODO: Ensure that the value returned by this call falls within a certain
  #       range, or throw an exception.
  analyze()
```

Annotation types:

- `TODO`: describe missing functionality that should be added at a later date
- `FIXME`: describe broken code that must be fixed
- `OPTIMIZE`: describe code that is inefficient and may become a bottleneck
- `HACK`: describe the use of a questionable (or ingenious) coding practice
- `REVIEW`: describe code that should be reviewed to confirm implementation

If a custom annotation is required, the annotation should be documented in the project's README.

<a name="miscellaneous"/>
## Miscellaneous

`and` is preferred over `&&`.

`or` is preferred over `||`.

`is` is preferred over `==`.

`isnt` is preferred over `!=`.

`not` is preferred over `!`.

`?=` is preferred over `or=` when the same functionality is achieved.

`0.54` is preferred over `.54`.

Prefer shorthand notation (`::`) for accessing an object's prototype:

```coffeescript
Array::slice          # Yes
Array.prototype.slice # No
```

Prefer `@property` over `this.property`.

```coffeescript
return @property     # Yes
return this.property # No
```

Use the explicit `return` to increase clarity.

Use splats (`...`) when working with functions that accept variable numbers of arguments:

```coffeescript
console.log args...   # Yes

(a, b, c, rest...) -> # Yes
```

<a name="idioms"/>
## Idioms

* Beautiful is better than ugly
* Explicit is better than implicit
* Simple is better than complex
* Flat is better than nested
* Sparse is better than dense
* Readability counts
* Special cases aren't special enough to break the rules
  * Although practicality beats purity
* If the implementation is hard to explain, it's a bad idea
* If the implementation is easy to explain, it might be a good idea
* Consistency counts
* DRY counts

<a name="readability"/>
## Readability

Strive for readability.  Code is written once, but read many times.

Too much syntactic sugar causes diabetes. Don't use something just because it's
cool. Never use something in case you even _slightly_ hesitate that you may be
the only person in the company being aware of how it works:

```coffeescript
included = 'a long test string'.indexOf('test') isnt -1 # Yes
included = !!~ 'a long test string'.indexOf 'test' # No
```


[coffeescript]: http://jashkenas.github.com/coffee-script/
[coffeescript-issue-425]: https://github.com/jashkenas/coffee-script/issues/425
[spine-js]: http://spinejs.com/
[spine-js-code-review]: https://gist.github.com/1005723
[pep8]: http://www.python.org/dev/peps/pep-0008/
[ruby-style-guide]: https://github.com/bbatsov/ruby-style-guide
[google-js-styleguide]: http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml
[common-coffeescript-idioms]: http://arcturo.github.com/library/coffeescript/04_idioms.html
[coffeescript-specific-style-guide]: http://awardwinningfjords.com/2011/05/13/coffeescript-specific-style-guide.html
[coffeescript-faq]: https://github.com/jashkenas/coffee-script/wiki/FAQ
[camel-case-variations]: http://en.wikipedia.org/wiki/CamelCase#Variations_and_synonyms
[apiary-guide]: https://github.com/apiaryio/coffeescript-style-guide
