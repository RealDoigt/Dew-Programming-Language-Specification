# Dew Programming Language Specification
NOTE: This document often refers to imaginary variables like "value". In any case, those values can come from any expression which generates a value. Where indicated otherwise, the use of the expression operators `()` is mandatory for using an expression.
* [Introduction](spec.md#introduction)
* [Comments](spec.md#comments)
* [Identifiers](spec.md#identifiers)
* [Operators](spec.md#binary-logical-boolean-arithmetic-and-array-operators)
  * [Array Operators](spec.md#array-operators)
  * [Unary Operators](spec.md#unary-operators)
* [Literals](spec.md#literals)
  * [Boolean](spec.md#boolean)
  * [String](spec.md#string)
  * [Character](spec.md#character)
  * [Numeric](spec.md#numeric)
  * [Escape Sequences](spec.md#escape-sequences)
* [Code Blocks](spec.md#code-blocks)
  * [Do](spec.md#do)
    * [Then](spec.md#then)
  * [As](spec.md#as)
    * [Such](spec.md#such) 
* [Variables and Types](spec.md#variables-and-types)
  * [Types](spec.md#types)
    * [Type Table](spec.md#type-table)
  * [Type Families](spec.md#type-families)
  * [Arrays](spec.md#arrays)
    * [Flexible Arrays](spec.md#flexible-arrays)
    * [Strings](spec.md#strings)
    * [Bits](spec.md#bits)
    * [Maps](spec.md#maps)
    * [Multidimensional Arrays](spec.md#multidimensional-arrays)
  * [References](spec.md#references)
  * [Initialising a Variable](spec.md#initialising-a-variable)
    * [By Doing Nothing](spec.md#by-doing-nothing)
    * [Using the Assign Operator](spec.md#using-the-assign-operator)
    * [Using the Initialize Operator](spec.md#using-the-initialize-operator)
    * [Using the Extract Operator](spec.md#using-the-extract-operator)
    * [Using Specialized Variants of the Assign and Initialize Operators](spec.md#using-specialized-variants-of-the-assign-and-initialize-operators)
  * [Tuple](spec.md#tuple)
* [Type Aliases](spec.md#type-aliases)
  * [Mode](spec.md#mode)
  * [Enum](spec.md#enum)
* [Control Flow](spec.md#control-flow)
  * [Conditionals](spec.md#conditionals)
    * [If](spec.md#if)
    * [Un](spec.md#un)
    * [Elif](spec.md#elif)
    * [Elun](spec.md#elun)
    * [Else](spec.md#else)
    * [Once](spec.md#once)
    * [When](spec.md#when)
    * [Vech](spec.md#vech)
    * [Otch](spec.md#otch)
    * [Other](spec.md#other)
  * [Loops](spec.md#loops)
    * [While](spec.md#while)
    * [Until](spec.md#until)
    * [Forever](spec.md#forever)
    * [Foreach](spec.md#foreach)
    * [For](spec.md#for)
    * [Repeat](spec.md#repeat)
    * [Where](spec.md#where)
  * [Break](spec.md#break)
  * [Next](spec.md#next)
* [Callables](spec.md#callables)
  * [Sub](spec.md#return)
  * [Return](spec.md#return)
* [Complex Types](spec.md#complex-types)
  * [Using a Complex Type](spec.md#using-a-complex-type) 
  * [Struct](spec.md#struct)
  * [Record](spec.md#record)
  * [Union](spec.md#union)
  * [Comp](spec.md#comp)
    * [Include](spec.md#include)
    * [Simultaneous Callables](spec.md#simultaneous-callables)
    * [Key Structure](spec.md#key-structure)  
* [Type Casting](spec.md#type-casting)
    * [Semi-Implicit Type Casting](spec.md#semi-implicit-type-casting)
* [Templates](spec.md#templates)
    * [Type Templates](spec.md#type-templates)
    * [Value Templates](spec.md#value-templates)
    * [Callable Templates](spec.md#callable-templates)
    * [Composite Templates](spec.md#composite-templates)
* [Modules](spec.md#modules)
* [Precedence](spec.md#precedence)

## Introduction
Dew is a high level programming language intended for experimenting with niche concepts. It is called Dew because it is Doigt's first serious language project and dew usually appears during the morning, which is the first part of the day. Dew's syntax is highly inspired by Algol 68, Bash and B as well as more modern languages such as D. As far as the author is aware, there is only one active project working on a Dew compiler and it is his own project, which is far from complete. This language specification doesn't describe what current compiler(s) can do but what they should do.

This language specification also doubles as user guide, hence the less formal and more helpful document structure. But make no mistake, this is a language specification first.

## Comments
Single line comments start with a hash symbol `#`.
Multiline comments start with the 2 cent digraph and ends with its inverted digraph `¢2` `2¢`.

## Identifiers
Dew identifiers are user-defined names for functions, procedures, variables, modules and custom types. A valid identifier starts with an underscore `_` or any letter of the latin alphabet. Then the rest of the identifier can be any alphanumeric character or underscore. No matter where the character is in the identifier, the character can be lower case or upper case.

## Binary, Logical, Boolean, Arithmetic and Array Operators
Dew comes with a wide variety of useful operators. This is not an exhaustive list as there are other types of operators which are mentionned with their purpose explained further down this document. The operators listed here are infix operators which need two parameters and return a result.
|operator|name|type|definition|
|-|-|-|-|
|\+|add|arithmetic|returns the sum of two numbers|
|-|sub|arithmetic|returns the difference of two numbers|
|/|div|arithmetic|returns the quotient of two numbers|
|*|mul|arithmetic|returns the product of two numbers|
|%|mod|arithmetic|returns the remainder a division of two integers|
|^|power|arithmetic|returns the result of raising the left operand to the power of the right operand|
|and|land|logical|returns true if both boolean expressions return true|
|or|lor|logical|returns true if either boolean expressions return true|
|eor|leor|logical|returns true if only one boolean expression returns true|
|nand|lnand|logical|returns true if either boolean expressions return false|
|nor|lnor|logical|returns true if neither boolean expressions return true|
|eand|leand|logical|returns true if both boolean expressions return the same result|
|<|lower|boolean|returns true if the left operand is smaller than the right operand|
|>|greater|boolean|returns true if the left operand is greater than the right operand|
|=|equal|boolean|returns true if both operands are equal|
|<>|different|boolean|returns true if neither operands are equal|
|<=|loe|boolean|returns true if the operands are equal or the left operand is smaller than the right operand|
|>=|goe|boolean|returns true if the operands are equal or the left operand is greater than the right operand|
|is|is|boolean|returns true if the left operand's type is the same or is a child of the type in the right|
|isnt|isnot|boolean|returns true if the left operand's type is not the same or is not a child of the type in the right|
|in|in|boolean|returns the index of the position where the first instance of the left operand can be found in the array, returns -1 if it was not found|
|has|isin|boolean|returns true if the right operand can be found in the array| 
|&|band|binary|returns the result of anding the bits of the left operand with those of the right operand|
|\||bor|binary|returns the result of oring the bits of the left operand with those of the right operand|
|\|\||beor|binary|returns the result of xoring the bits of the left operand with those of the right operand|
|!&|bnand|binary|returns the result of nanding the bits of the left operand with those of the right operand|
|!\||bnor|binary|returns the result of noring the bits of the left operand with those of the right operand|
|&&|beand|binary|returns the result of xnoring the bits of the left operand with those of the right operand|
|<<|lshift|binary|returns the result of shifting the bits of the left operand to the left by the right operand|
|>>|rshift|binary|returns the result of shifting the bits of the left operand to the right by the right operand|
|<@|lrot|binary|returns the result of rotating the bits of the left operand to the left by the right operand|
|@>|rrot|binary|returns the result of rotating the bits of the left operand to the right by the right operand|

### Array Operators
Array operators are usually infix operators which will create a new array. They also work with the string type to a certain extent.
|operator|name|definition|effect on string|
|-|-|-|-|
|+|addarr|if the left operand is an array and the right operand is either an array or a number, return the matrix sum of both operands|NA|
|-|subarr|if the left operand is an array and the right operand is either an array or a number, return the matrix difference of both operands|NA|
|*|subarr|if the left operand is an array and the right operand is either an array or a number, return the matrix product of both operands|NA|
|/|divarr|if the left operand is an array and the right operand is either an array or a number, return the matrix quotient of both operands|NA|
|~|concatenate|create a new array from both operands and order them from left to right|if one of the operands is a string, create a new string from both operands and order them from left to right|
|~~|repeat|if the left operand is an array, create an array which has its elements repeated times the right operand|if the left operand is a string, create a new string which has its characters repeated times the right operand|
|!~|remove|return a new array where all instances of right operand in left operand have been removed|return a new string where all instances of right operand in left operand have been removed|

### Unary Operators
Unary operators are prefix operators with only one parameter.
|operator|name|type|definition|
|-|-|-|-|
|-|minus|arithmetic|returns the operand, which must be numeric, with the opposite sign|
|+|plus|arithmetic|returns the absolute value of the operand|
|--|decrement|arithmetic|decrements the operand, which must be a variable|
|++|increment|arithmetic|increments the operand, which must be a variable|
|**|power2|arithmetic|multiplies the operand, which must be a variable, by itself|
| \ |sqrt|arithmetic|returns the square root of the operand, which must be a positive number|
|!|not|binary|returns the result of inverting the bits of the operand|
|-|minusarr|array|returns a new array with all the numbers of the array now of the opposite sign|
|+|plusarr|array|returns a new array with all the absolute values of the numbers in the array| 
|--|decarr|array|decrements all the elements of the array|
|++|incarr|array|increments all the elements of the array|
|**|p2arr|array|multiplies all the elements of the array by themselves|
| \ |sqrtarr|array|returns a new array with the square roots of all the elements of the array|
|!|invarr|array|returns a new array with bits of all the elements the array inverted|
|!!|pop|array|returns and removes the last element of the array|
|@|length|array|returns the length of the array or string|
|~|join|array|if the array is multidimensional, it returns a new array with all the arrays merged into one. If it's an array of strings, it returns all the strings concatenated into one string. If it's a single dimension array of chars, it creates a string.|

## Literals
Dew has 4 types of literals: boolean literals, string literals, character literals and numeric literals.

### Boolean
A boolean literal is defined as being one of two valid keywords; `true` or `false`.

### String
A string literal is defined as a sequence of characters enclosed between a pair of double quotes `"`.

### Character
A character literal is defined as a sequence of characters enclosed between a pair of single quotes `'`.

### Numeric
A numeric literal is defined as a sequence of case sensitive characters which represents binary, octal, decimal and hexadecimal numbers (0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F). Numbers can be separated by underscores `_` for added legibility. Each non-decimal sequence must start with an at sign `@` then a lower case letter representing that base: 
* Binary: @b1010_1011
* Octal: @o253
* Decimal: 171
* Hexadecimal: @xAB

Negative numbers start with a minus sign `-` and the minus sign can only be applied to decimal numbers.

### Escape Sequences
Escape sequences are special character sequences which begin with an asterisk `*`. They are used in character and string literals for characters that are not practical to type on a keyboard or characters which have a special functionality:
| name | sequence|
|-|-|
| tabulation |\*t|
| carriage return| \*r|
| new line |\*n|
| null character| \*0|
| single-quote |\*'|
| double-quote |\*"|
| asterisk |\*\*|
| backspace |\*b|
| vertical tabulation| \*v|
| bell |\*a|
| form feed| \*f|

## Code Blocks
Code blocks are areas in the code, indicated by a `do`/`od` pair, `as`/`sa` pair or their one-line shortcut variants, with which instructions or list of properties can be written.

### Do
A `do` code block is for instructions. It is terminated by the inverted form of `do`; `od`. A `do` block will span multiple lines. It can be written using Allman style only, but whether to enforce that standard or not is up to the compiler. Do blocks can be left empty.

Example of a hello world program using a `do` code block:
```dew
proc main
do
  echo("Hello, World!")
od
```

#### Then
`then` is an alternative keyword which can be used when a code block would only be made of one single line. Then blocks cannot be left empty. 
```dew
proc main then echo("Hello, World!")
```

Then blocks can be chained. In the below example, a program prints out all the arguments of main. The if is not necessary since the foreach would not execute anyways if there are no arguments, but it was just demonstrate that the `then` keyword can be chained indefinitely.
```dew
proc main(string args) then if @args > 0 then foreach string arg of args then echo(arg)
```

Note that both `do` and `then` code blocks introduce scope. By default, there's only one scope; the global scope, which is accessible from everywhere. However, created scopes are only accessible from within itself and scopes within that scope. This means for example, that two variables `a` can exist in different scopes that are not within one or the other because they will not enter into conflict with each other, but that also means that neither scope has access to the value in that other scope. When the execution leaves the scope, the values of the variables declared in that scope are forgotten and will be reset once the scope is reenterred. 

### As
An `as` code block is for listing properties of some declared type. More specifically, it is used in enums for defining enum members and in components for defining required, expected and included members. It can also be used to list overrides for keys. Just like a `do` block, the `as` block spans multiple lines and is terminated by an inverted `as`; `sa`. Elements are separated by new lines.

#### Such
`such` is an alternative keyword which can be used to make an `as` block on one line. Elements are separated by white space. To keep the code legible, it is recommend to use it only when there are few elements to list. Also, one can no longer use the keyword `is` to give a value to an enum member. `such` cannot be used with `key`.

Note that neither `as` nor `such` code blocks introduce scope.

## Variables and Types
Declaring a variable in Dew is done by typing the type information with the modifier(s) before the type name then the name of the variable. Optionally, it may also be initialised with the assign operator, the initilize operator or the extract operator as well as a few other specialised assign operators.

### Types
Dew has 9 types (`int`, `real`, `string`, `char`, `byte`, `bool`, `bits`, `void` and `inf`) and 4 type modifiers (`short`, `long`, `flex` and `ref`). One can define type aliases with the `mode` and `enum` keywords. It is also possible to define complex types with `struct`, `union`, `comp`, `model` and composition keywords `require`,  `include`, `expect`.

#### Type Table
* ID = Implementation Defined
* NA = Not Applicable
  
|type|definition|size|short|long|long long|
|-|-|-|-|-|-|
|int|signed integer|32-bits|16-bits|64-bits|NA|
|real|binary floating point number|32-bits (single)|16-bits (half)|64-bits (double)|128-bits (quadruple)|
|string|immutable character array|variable (utf-8)|variable (ascii)|variable|variable|
|char|character|1~4 bytes (utf-8)|1 byte (ascii)|ID|ID|
|byte|unsigned integer|8-bits|NA|ID|ID|
|bool|boolean|8-bits|NA|NA|NA|
|bits|bit mask|8-bits|NA|ID|ID|
|void|no return value; not a real type|NA|NA|NA|NA|
|inf|infers the type based on the value assigned to the variable; not a real type|NA|NA|NA|NA|

### Type Families
Type families are used for comparing types, which is useful for type constraints and component expectations.
A type family belonging to the atomic category is a type family which doesn't contain other type families. The opposite case is called the composite category.

|family|children|category|
|-|-|-|
|integer|byte, long byte, long long byte, short int, int, long int|atomic|
|decimal|short real, real, long real, long long real|atomic|
|boolean|bool|atomic|
|bitmask|bits, long bits, long long bits|atomic|
|stringf|short string, string, long string, long long string|atomic|
|numeric|integer, decimal|composite|
|text|stringf, char|composite|
|binary|numeric, boolean, bitmask, char|composite|
|primitive|binary, text|composite|
|plural|stringf, arrays of any type|composite|
|array|plural, bitmask|composite|

### Arrays
An array is declared by adding the index operators `[]` after the type. If the size of the array is known in advance, but the elements aren't, one can type the size within the index operators. In all other cases, the index operators can be empty. Following Algol tradition, `ints`, `reals`, `strings`, `bytes` and `bools` are aliases for arrays of their corresponding type.

#### Flexible Arrays
The `flex` keyword is used in the variable declaration to indicate that an array is flexible, meaning it can both increase and decrease in capacity and number of elements. In other languages, flexible arrays are also called dynamic arrays or lists.

#### Strings
A string is in almost every way an array of char. There are only a few differences:
* Instead of writing `['H' 'e' 'l' 'l' 'o' ',' ' ' 'w' 'o' 'r' 'l' 'd' '!']`, which is long and tedious, strings in Dew are typed using double quotes: `"Hello, world!"`.
* While you can use the index operators to access the individual char values contained in a specific string, you cannot modify that value since Dew strings are immutable.
* Dew strings, just like properly formatted C strings, use the null terminator to indicate the end of a string.

#### Bits
On the surface, bits look like an array of bools. However in truth, the bits type is not a real array. It's just syntax sugar. One can use bits variables as if one were using an array. The bits type is not compatible with array operations except the index operators. The bits type cannot be made into a flexible array either. Because the bits type is really just a byte, it is compatible with all operators and functions that work on bytes.

#### Maps
Maps are declared the same way a normal array would be declared, however the type of the index must be declared within the index operators like in this example: `int[string] mymap`. Maps are always flexible. To initialize the value of map, one separate the pairs with commas `,` with the key first and the value second like in this example: `int[string] villain rankings := ["Darth Vader" 10, "The Goblin" 2, "Blackbear" 7, "Pain" 5]`

#### Multidimensional Arrays
A multidimensional array can either be declared in the form of `type[z y x] arr_name` or `type[z][y][x] arr_name`. 
1. The first case is called a rectangular array. It has the following properties:
   * Cannot be flexible.
   * Guarrantees that each sub array will have the exact dimensions that were declared. This means arrays of the same level have the same length.
2. The second case is called a jagged array. It has the following properties:
   * Can be flexible.
   * Each sub array can vary in length. This means arrays from the same dimension are not guarrenteed to have the same length.

### Tuple
A tuple is an anonymous `record`, useful for returning multiple values from a callable. The syntax for declaring one is by listing the types inside the tuple operators `{}` then the variable's name.

Example:
```dew
{int string char} my_tuple
```

To assign values to a tuple, you assign all values at once by using the tuple operators again and by following the order of the types declared.
Example:
```dew
{int string char} my_tuple := {24 "Hello" 'C'}
```

To get the value of an individual tuple field, one has to type the variable's name follow by a dot `.` then the field's identifier. The field's identifier is composed of an underscore followed by a number representing a position in the order of declaration (starts at 0).

Example:
```dew
echo(my_tuple._2) # prints C
echo(my_tuple._0) # prints 24
echo(my_tuple._1) # prints Hello
```

A tuple's fields may be readonly, but it shouldn't prevent reusing the same tuple to assign a new value to it. This will be considered a new tuple. When only one field has a different value compared to the previous tuple, a shortcut can be used by typing the variable's name, the tuple operators with the position of the field that is changing then assigning the changed value.

Example:
```dew
¢2
  The line below this comment is the exact same thing as typing:
  my_tuple := {34 my_tuple._1 my_tuple._2}
2¢
my_tuple{0} := 34
```

### References
The `ref` keyword is used in function signatures and function calls on parameters which hold a copy of the address of the variable rather than a copy of the variable's value. Dereferencing is done automatically.

Example:
```dew
proc void increment(ref int a) then ++a

proc void main
do
  int i := 1
  increment(ref i)
  echo(i) # prints 2
od
```

### Initialising a Variable
A variable can be initialised in many ways.

#### By Doing Nothing
Just by declaring a variable, it will automatically be assigned a default value. Here's a list of default values by type:
|type|default|
|-|-|
|int|0|
|real|0|
|string|"" (empty string)|
|char|'*0'|
|byte|0|
|bool|false|
|bits|\[false false false false false false false false\]|
|type[] (array)|[] (empty array)|
|type\[\<number\>\]|\[\<default value of the type times the number\>\]

#### Using the Assign Operator
The assign operator `:=` can be used in order to assign a value to a variable or set all the values of an array to one value if the index operators are omitted.
If an expression is needed inside the index operators, one must use the expression operators `()`.

Example:
```dew
proc void main
do
  # variable a is set to 1
  int a := 1

  # variable b's three elements are set to 10, 20 and 30 respectively
  ints b := [10 20 (25 + 5)]

  # all six values of the array are set to 5
  int[6] c := 5
od
```

#### Using the Initialize Operator
The initialize operator `:` can be used to assign values to a group of variables. If there are less values than variables, then the last variables that don't have a matching value get the last value. The compiler should throw an error and refuse to compile if there is only one variable being initialized or if there are fewer variables than there are values. Whether the initialize operator works with `inf` or not is up to the individual compiler. The initialize operator is intended for use with simple use cases such as function calls, literals or other variables. If you need to assign the result of an expression, such as `2 * userCount / 3`, it will not compile due to how the syntax works, but you can use the expression operators `()` to bypass this issue.

Example:
```dew
proc void main
do
  # set a to 1, b to 2 and c to 3
  int a b c : 1 2 (3 + 0)

  # set d to [10 128 52] and e to [23 55]
  bytes d e : [10 128 52] [23 55]

  # all elements of f are set to 400,000 and g is set to [7 8 2]
  long int[3] f g : 400_000 [7 8 2]

  # h, i and j are all set to -45
  int h i j : -45

  # k is set to "Hello" while l and m are set to "World!"
  string k l m : "Hello" "World!"
od
```
#### Using the Extract Operator
The extract operator `::` can be used to assign values from an array, bits, string or struct. If there are not enough variables to hold all the values, those values are simply ignored. Whether the extract operator works with `inf` or not is up to the individual compiler.

Example:
```dew
proc void main
do
  ints a := [4 10 29 678]
  int b c d e :: a
  int f g :: a # the first two values are assigned to f and g, but the rest of the values in a are ignored

  echo(b) # prints 4
  echo(c) # prints 10
  echo(d) # prints 29
  echo(e) # prints 678
  echo(f) # prints 4
  echo(g) # prints 10
od
```
#### Using Specialized Variants of the Assign and Initialize Operators
The assign and initialize operators can also be used on variables which have already been assigned a value. However, there are many specialised variants of these two operators for common usecases.

|assign variant|initialize variant|assign name|initialize name|definition|examples|equivalent example|
|-|-|-|-|-|-|-|
|+=|+:|addassign|addinit|adds the value(s) of the right expression to the value held by the variable(s) and assigns the result to the variable(s), matrix math applies if used on arrays|`a += 16` and `a b +: 16 8`|`a := a + 16` and `a b : (a + 16) (b + 8)`|
|-=|-:|subassign|subinit|substracts the value(s) of the right expression to the value held by the variable(s) and assigns the result to the variable(s), matrix math applies if used on arrays|`a -= 16` and `a b -: 16 8`|`a := a - 16` and `a b : (a - 16) (b - 8)`|
|/=|/:|divassign|divinit|divides the value(s) of the right expression to the value held by the variable(s) and assigns the result to the variable(s), matrix math applies if used on arrays|`a /= 16` and `a b /: 16 8`|`a := a / 16` and `a b : (a / 16) (b / 8)`|
|*=|*:|mulassign|mulinit|multiplies the value(s) of the right expression to the value held by the variable(s) and assigns the result to the variable(s), matrix math applies if used on arrays|`a *= 16` and `a b *: 16 8`|`a := a * 16` and `a b : (a * 16) (b * 8)`|
|^=|^:|powerassign|powerinit|gets the result(s) of the variable(s) raised to the power of the expression and assigns it to the variable(s)|`a ^= 16` and `a b ^: 16 8`|`a := a ^ 16` and `a b : (a ^ 16) (b ^ 8)`|
|%=|%:|modassign|modinit|divides the value(s) of the right expression to the value held by the variable(s) and assigns the remainder to the variable(s)|`a %= 16` and `a b %: 16 8`|`a := a % 16` and `a b : (a % 16) (b % 8)`|
|&=|&:|andassign|andinit|ands the bits of value(s) of the right expression to the bits of the value held by the variable(s) and assigns the result to the variable(s)|`a &= 16` and `a b &: 16 8`|`a := a & 16` and `a b : (a & 16) (b & 8)`|
|\|=|\|:|orassign|orinit|ors the bits of value(s) of the right expression to the bits of the value held by the variable(s) and assigns the result to the variable(s)|`a \|= 16` and `a b \|: 16 8`|`a := a \| 16` and `a b : (a \| 16) (b \| 8)`|
|~=|~:|catassign|catinit|concats the array(s) or string(s) with the result of the left expression and assigns the new array to the arrays on the left-side of the operator. If the array is flexible, no new array is created, the extant array is simply expanded.|`a ~= 16` and `a b ~: 16 8`|`a := a ~ 16` and `a b : (a ~ 16) (b ~ 8)`|

#### By Other Means
There are other specialised ways by using the cast `?` operator and there exists some shortcuts for callables, but those methods are discussed in their respective sections.

## Type Aliases
Custom types can be defined as aliases using the `enum` and `mode` keywords. These types are should ideally be handled at compile time or by a preprocessor.

### Mode
The `mode` keyword is used for simple type aliases. Whether it is used as a way to save some typing time or as a way to more clearly and visually establish API equivalences between languages and frameworks. The basic syntax is `mode custom_type_name is <type>`. A more advanced syntax can be used for array types: `mode custom_array_type(n m etc) is \<array type>\[n]`

Example 1:
```dew
use std.math

¢2
 this example makes "quad"
 an alias for long long real
2¢
mode quad is long long real

proc main
do
  quad tau := PI * 2
  echo(tau) # prints 6.28318530718..........................
od
```

Example 2:
```dew
¢2
 this example establishes equivalent
 types for use with SQL
2¢

mode CHAR(size) is char[size]
mode VARCHAR(size) is flex char[size]
mode INT is int
mode TINYINT is byte

proc main
do
  CHAR(5) c5 := ['H' 'e' 'l' 'l' 'o']
  VARCHAR(7) vc := [' ' 'w' 'o' 'r' 'l' 'd']
  vc := c5 ~ vc
  echo(~vc) # prints Hello world
od
```

### Enum
The `enum` keyword is used for compile-time/pre-processor constants. Enums have three different syntaxes:
1. `enum type_name is expression`
2. `enum type_name(n m etc) is expression`
3. `enum type_name as enum_member1 enum_member2 enum_member3 sa`

Example 1:
```dew
enum WHITE is @xFFFFFF

proc void main
do
  draw_pixel(0 0 WHITE)
od
```

Example 2:
```dew
struct color then byte r g b a
enum BLUE(alpha) is set color such 0 0 255 alpha

proc void main
do
  draw_pixel(15 20 BLUE(255))
od
```

By default, enum members are aliases for integer values starting from zero. However one can change the value of an enum member at any point and the incrementation will start from there. The `is` keyword is used to set a non default value to an enum number.
Example 3:
```dew
enum WEEKDAYS
as
  SUNDAY is 1
  MONDAY # 2
  TUESDAY # 3
  WEDNESDAY is 5
  THURSDAY # 6
  FRIDAY # 7
  SATURDAY # 8
sa
```
## Control Flow
Control flow is almost every classic branching intruction where there's a choice involved, so conditionals and loops.

### Conditionals
A conditional is a statement which indicates that the code which follows is only to be executed once and if a condition(s) is satisfied. The way satisfaction is obtained is by using a boolean expression which returns true.

#### If
`if` is the keyword used in Dew for making an if conditional statement. A code block must follow an if statement.
```dew
if ¢2insert condition here2¢
do
  # your code here
od
```

Concrete example where a method prints out "you're old" to the console if the variable age is higher than 49.
```dew
enum OLDAGE is 50

meth say_old_if_old(int age)
do
  if age >= OLDAGE
  do
    echo("you're old")
  od
od
```

#### Un
`un`, short for "unless", works like an inverted if. The result of the condition is inverted before being evaluated. So if the condition returns true, it will return false and if it returns false, it will return true instead. Using the example above, we'd have to change it to make it work with un:
```dew
meth say_old_if_old(int age)
do
  un age < OLDAGE then echo("you're old")
od
```

#### Elif
`elif`, short for "else if", is an alternative branching condition for a preceding `if`, `un`, `elif` or `elun`. If the preceding conditional evaluated to false, it the code of the `elif` will be evaluated and if true, the code block of the `elif` will be executed. If false, it will be skipped like an ordinary `if`. You can chain multiple elifs and eluns together.

#### Elun
`elun`, short for "else unless", is the equivalent else if construct for `un`.

#### Else
If none of the conditionals in a chain are executed, the `else`, which should be last in the chain, will have its code block executed. It doesn't come with a condition. The `else` is always optional.

Example else usage with if, elun and elif:
```dew
if age <= 12 then echo('*nYou are a child.')
elun age >= 18 then echo('*nYou are a teen.')
elif age >= 65 then echo('*nYou are an elder.')
else then echo('*nYou are an adult of working age.')
```

#### Once
`once` is a shortcut for writing an if/un/elif/elun/else chain. It starts with `once`, the variable to evaluate then, optionally, an operator or a booleam callable which takes exactly two parameters. The callable's name should be typed without parentheses. The default operator is `=`. The first match in the `once` will be executed. If there is no match, the `else` will be executed. The `once` uses an alternative code block syntax where each case starts with the a list of values separated by spaces followed by an arrow `=>`. If the code is only one line, then it can also be typed out on the same line, otherwise it follows on separate lines.

```dew
# selects and execute the first case where age is under the value being tested
once age <
do
  12   => echo("You*'re very young.")
  16   => echo('You*'re young.')
  20   => echo('You*'re still young.')
  26   =>
          echo('You*'re getting older.
          echo('but don*'t worry because the night is still young.')
  30   => echo('You*'re getting older.')
  50   => echo('You*'re officially old')
  else => echo('You are either considering or enjoying retirement!')
od
```

#### When
`when` is a shortcut for writing a group of consecutive if/un. It works exactly like `once`, but instead all the matches will be executed. An `else` will still only be executed if no other match was found.

Example using an enum
```dew
# icecream_flavours is an array of custom enum type ICECREAM_FLAVOURS 
when icecream_flavours has
do
  # note: the first case will trigger on two seperate values
  STRAWBERRY VANILLA => echo("You have some boring flavors.*n")
  CHOCOLATE => echo("A true classic.*n")
  BANANA => echo("You like it weird and I respect that.*n")
  else => echo("There was no notable flavour.")
od
```

#### Vech
`vech`\*, short for "version check", is for code that is only going to be executed under certain compiler version or target system. Ideally, this should be evaluated in the preprocessor or at compile time. The codes or names used are implementation defined. `and` and `or` can be used if there is more than one platform for which the code should run on.

Abstract example:
```dew
vech LINUX and ARM64
do
  # code here
od
```
\*Whatever you prefer between /vɛt͡ʃ/ or /vɛk/ is good pronunciation.

#### Otch
`otch`\*, short for "other version check", is the else if construct of the version check.

```dew
vech GAMEBOY then # code here
otch GAMEBOY_COLOR then # code here
```
\*Whatever you prefer between /ɒtʃ/, /ɑt͡ʃ/, /ɒk/ or /ɑk/ is good pronunciation.

#### Other
`other`, short for "otherwise", is the else construct of the version check.

```dew
vech DEWC_11
do
  # code here
od

other then # code here
```

### Loops
A loop is a section of code which is executed repeatedly. Dew has many different kinds of loops to choose from.

#### While
A `while` loop is a loop which repeats the code block which follows while the condition is true. The basic syntax of this loop is `while condition do/then`.

A `while` loop example which is used to validate user input:
```dew
short int age
    
while age <= 0 then age := read_sint()
```

#### Until
An `until` loop is a `while` loop which has the result of condition inverted before being evaluated. So if the condition is true, it will evaluate to false and vice versa.

The same example as above, modified to work with `until`:
```dew
short int age
    
until age > 0 then age := read_sint()
```

#### Forever
A `forever` loop will, as its name implies, run forever. The only way for the forever loop to stop is to force it to stop.

Example of using a forever loop with a break statement:
```dew
use raylib

proc void main
do
  init_window(1080 720 "A raylib game")
  set_target_fps(60)

  forever
  do
    begin_drawing()
    clear_background()
    if window_should_close() then break this
  od

  end_drawing()
od
```

#### Foreach
A `foreach` loop is a loop which iterates over each element of an array, string or bits variable. The syntax of a `foreach` loop is `foreach [ref] type var_name of array_name do/then`. A multidimensional array's elements are considered to be arrays themselves, so at least another foreach loop would be necessary to iterate over every single array in the multidimensional array depending on the number of dimensions. `ref` is an optional keyword which indicates that the temporary variable holds a reference rather than a copy of the element. That means using `ref` will change the value of the variable if that value is changed in the `foreach` loop. Otherwise, no changes should apply. `ref` doesn't work with bits, because it is impossible to hold a reference to a bit in a byte.

#### For
`for` is a loop which repeats until the loop variable is equal to the set limit. For loops either increment (`upto`) or decrement (`downto`) by 1 the loop variable.
The basic syntax of a `for` loop is `for var_name := value upto/downto limit do/then`. If the value change should be different than 1, then it takes this form: `for var_name := value to limit by change do/then`. 

#### Repeat
`repeat` is a very simple loop where it repeats the code block for a set number of times. The syntax is as follows: `repeat value do/then`.

#### Where
A `where` loop is a loop which iterates over each element of an array, string or bits variable that matches a specific condition. If the condition is not met, that element is skipped. The syntax of a `where` loop is `where [ref] type variable_name of array_name condition do/then`.

### Break
The `break` statement can be used to forcibly break from loops. `break all` breaks from all the nested loops. `break this` breaks from the currently executing loop. `break to n` will jump the program back up in the nested loops until it reaches the nth parent loop.

### Next
The `next` statement, also known as `continue` in other languages, forces the loop to jump to the next iteration.

## Callables
In Dew, a callable is what is called a function in other languages. There are four types of callables:
* Functions (keyword: `func`) are pure callables, meaning that for the same input, they always produce the same output and no side effect is allowed. No random numbers, no modifying modifying variables outside the callable's scope nor any references and no IO. If a function is not pure, then the compiler should refuse to compile.
* Methods (keyword: `meth`) are callables that always produce the same output for the same input, but side effects are allowed.
* Actions (keyword: `actn`) are callables that are not allowed to have side effects. However, they are not guaranteed to always produce the same output for the same input.
* Procedures (keyword: `proc`) are completely impure callables with absolutely no guarantees.

To declare a callable in Dew, the type of the callable goes first, followed by the return type then the name and the (optional) parameter list enclosed within parentheses. If there are no parameters, the parentheses can be omitted or left empty.

### Sub
`sub` is a callable modifier which can only be used on methods and procedures in a component. It is used to indicate that the side effects of a procedure or method are exclusively limited to the fields of the component it is in. The syntax is `sub proc` and `sub meth`.

### Return
There are three ways to exit a callable:
* The exit `><` statement is used to exit from a callable. If there was no set return value, it will return the default type value of the function.
* The return `->` statement simultaneously sets the return value then exits the callable. The proper syntax is `-> value`
* The program reaches the end of the callable's code block, in which case the behaviour is identical to using an `><`.
Only `><` can be used to exit a void callable without reaching the end of the callable's code block.

The return set `<-` statement sets the return value without exiting the callable. The proper syntax is `<- value` The value in the return value can be accessed with the dollar sign `$`. `$` only returns the value, it cannot be used as a variable to modify the state of the return value.

### Callable Examples

Example 1:
```dew
proc int post_inc(ref int x)
do
  <- x
  ++x
od
```

Example 2:
```dew
func int get_cash_reward(int player_level)
do
  when player_level >=
  do
    => 1 <- 10
    => 5 <- $ * 2
    => 10 <- $ * 10
  od
od
```

Example 3:
```dew
meth void say_moo(ANIMALS a)
do
  if a <> COW then ><
  echo("Moo!*n")
od
```

Example 4:
```dew
func int fib(int n)
do
  if n < 2 then -> n
  -> fib((n - 1)) + fib((n - 2))
od
```

Example 5:
```dew
func int factorial(int n)
do
  if n = 0 then -> 1
  -> n * factorial((n - 1))
od
```

### Call-Assign Syntax
There is a way to "make" a specialised assign operator with a callable. To do this, one must type the callable's name then the equal sign `=`. By default, it will use the variable being assigned to as the first parameter, so the first parameter must be omitted from the call. If the variable being assigned to is intended as another parameter, then it must be indicated with an at sign `@`. Whether to allow Shortened Call Syntax or not within the usage of Call-Assign Syntax is up to the individual implementation. Parentheses `()` are only used as expression operators.

Examples calling a function add_three(int a int b int c):
```dew
int total := 10;

# This is the same as typing total := add_three(total 20 34)
total add_three= 20 34 # result is 64

# This is the same as typing total := add_three(5 total 5)
total add_three= 5 @ 5 # result is 74
```

### Shortened Call Syntax
One can omit the last parameter(s) from a callable call and those parameters will be assigned their type's default value. If more than one parameter is omitted from the callable call, those parameters must follow each other in the callable's signature.

Valid SCS of a string array callable called find_match(string str string find int max_matches). If max_matches is set to 0, it will find all matches:
```dew
find_match("Hello" "l") # same as find_match("Hello" "l" 0)
```

Invalid SCS of a callable called some_callable(string s int i char c):
```dew
some_callable('c')
some_callable(1 'a')
some_callable("something something" 'n')
```

Valid calls of the above callable would be:
```dew
some_callable()
some_callable("Hello")
some_callable("Hello" 5)
```
## Complex Types
Complex types are user-defined types which can be made of several variables of different types, which are called fields. Most types can only contain fields, but components can also have callables. 

### Using a Complex Type
To use a complex type, one must write the type's name, then the variable's name and choose "where" the type will live. Using the `new` keyword will allocate it on the heap, while using `set` will allocate it on the stack. Optionally, the fields of the complex type can be initialised. The fields can be accessed with a dot `.`.

First example without initialising the fields on declaration\*.
```dew
struct color then byte r g b

proc void main
do
  # allocates on the stack
  color my_color := set color
  my_color.r my_color.b : 255
  draw_pixel(0 0 my_color) # draws a magenta pixel to the screen
od
```
\*Keep in mind that the variables in the complex type will be automatically assigned a default value if declared without initialising on declaration.

Second example with initialising the fields on declaration
```dew
struct color then byte r g b

proc void main
do
  # allocates on the heap
  color my_color := new color
  as
    r := 10
    g b : 50
  sa

  draw_pixel(0 0 my_color)
od
```

Alternatively, one can omit the field names on initialisation. The values will be attributed to the fields in the order they were declared in the type.
```dew
struct color then byte r g b

proc void main
do
  color my_color := new color such 255 255 255
  draw_pixel(0 0 my_color) # draws white to the screen
od
```

### Struct
A `struct`, short for data structure, is an arbitrarily user-defined type which is a grouping of one or more variables of various types.

### Record
A `record` is a read-only struct. Once the values of a record are initialised, they cannot be changed. A new instance of a record should not be declared without initialising it because otherwise the default values will be assigned to the variables.

### Union
A `union` is a struct where only one field of the struct can be used at a time. The total size of the `union` will always be of the larger type. When the other field of the struct that was not in use gets assigned a value, it becomes the active field and the other field becomes the useless field. Reading from the inactive field is implementation defined so it could yield garbage data. 

### Comp
A `comp`, short for component, is an arbitrarily user-defined type which is a grouping of one or more variables and callables of various types.

#### Include
Components can be combined together or with structs and records to form new types by using the `include` keyword. Include may only appear once inside a `comp`. There is no limit to the quantity of types that can be included. The syntax is `include as/such types`.

Example with only one included type:
```dew
struct color then byte r g b

comp alpha_color
do
  include such color
  real a
od
```

Example with many includes:
```dew
comp car
do
  include
  as
    motor
    pilot
    tank
  sa

 wheel[4] wheels
 real drag

 key
 as
   wheels is wheels
   drag is drag
   capacity from tank is fuel_capacity
   quantity from tank is fuel_reserves
 sa
od
```
The example above has the key keyword, which will be explained in [Key Structure](spec.md#key-structure).

#### Simultaneous Callables
Callables of the same name but from different components are executed in a sequence with the first being the host component then following the order in which the callables' respective components were included.

This behaviour can be altered with `last` and `first` which are callable modifiers that modify the order of calling. However, if callables with the same modifier clash, then the original order is used to sort out the calling order among them.

The `override` keyword will prevent the other callables from being called. If there is more than one `override` for the same simultaneous callable, then the host callable will be the one to be called. If there is no host, then the callable from the last component included will be called. Again, this order can be changed with the `last` and `first` keywords and are subject to the same rules as explained above.

Note: The host component's callable must be compatible with the other callables. This means that if the host component's callable is a function, then all other callables with that name from other components must also be functions.

Here is a compatibility table:
|callable type|function|method|action|procedure|sub method|sub procedure|
|-|-|-|-|-|-|-|
|function|yes|no|no|no|no|no|
|method|yes|yes|no|no|yes|no|
|action|yes|no|yes|no|no|no|
|procedure|yes|yes|yes|yes|yes|yes|
|sub method|yes|no|no|no|yes|no|
|sub procedure|yes|no|yes|no|yes|yes|

#### Key Structure
The key structure is defined as the elements of a component which are used to establish a bridge between two or more components. When a component has expectations or requirements, they will expect key elements to be there so that it may properly function. These key elements can be callables, specific fields or they can be ambiguous in-betweens of sorts. These are defined with the keywords `key`, `expect`, `require`, `from`, `is`, `let` and `get`.

* The `key` keyword is used to indicate where to find the keys and what they are. The `is` keyword is used to establish that a specific field is the expected/required field. `from` is used for when a key is from another component. When callables are used to simulate a variable that is expected, the `let` and `get` keyword are used in front of the individual key callables to indicate which has the writing role and which has the reading one, in that order.

* The `expect` keyword is used from the included component to establish an expectation. An expectation is defined as something that the component needs to properly function. This doesn't need to be strictly fulfilled by a host component, meaning an alternative can be given (as was mentionned above where two callables which simulate a field are given instead of exactly what is expected). It also means that the expectation can be ambiguous. For example, instead of expecting a field of type `int`, the expectation could be any field of the `integer` type family. The syntax for declaring an expectation is `expect type(s)/field(s) as/such`.

* The `require` keyword is used from the included component to establish a requirement. A requirement is also defined as something that the component needs to properly function. However, in contrast to an expectation, a requirement needs to be strictly fulfilled. As such, it doesn't allow alternatives nor does it allow a requirement to have any ambiguity in its definition. The syntax for declaring a requirement is `require type(s)/field(s) as/such`.

Do note that is up to the individual programmer whether to use the plural forms of keywords `type` and `field` or not. The plural forms are aliases of the singular forms. Likewise, there's a plural alias for `key`; `keys`.

Another thing to note is that even though a field is strictly a variable within the component's root scope, callable members of a component are also defined alongside fields under the `field` keyword. 

Example of meeting an expectation with an alternative that can also work same roles because its definition is compatible with the expectation:
```dew
struct color then byte r g b
struct alpha_color then byte r g b a

comp a
do
  expect type such color
od

comp b
do
  include
  as
    alpha_color
    a
  sa

  # because color has all the same members in its definition, even though they are disctinct, it is acceptable as an alternative
  key such alpha_color is color
od
```

Another one which is more advanced. Do note that if the included component has a callable that needs to modify the blue field, it shouldn't be accepted. But because it doesn't, this is valid:
```dew
comp crazy_color
do
  byte r g

  actn byte random_blue()
  do
    # code here
  od
od

comp c
do
  include
  as
    crazy_color
    a
  sa

  # because data structures are fused together, the type can be individually separated into single keys for identification purposes.
  keys
  as
    r from crazy_color is r from color
    g from crazy_color is g from color
    get random_blue from crazy_color is b from color
  sa
od
```

## Type Casting
An expression of one type can be casted into another type with the casting operator `?`. The syntax for casting is `expression ? type`. Implicit type casting is impossible in Dew, but semi-implicit type casting is; details in section [Semi-Implicit Type Casting](spec.md#semi-implicit-type-casting). 

Expressions can only be cast into compatible types. For values of primitive types, this means that types from the `binary` type family can be cast into each other and members of the `array` family can be cast into each other. 

For values from complex types, this means the target type's fields must exist as is or as equivalents in the value's complex type structure. 
For example, the following complex types:
```dew
struct color then byte r g b

struct alpha_color then byte r g b a

struct alpha_color_r
do
  byte r g b
  real a
od

record quaternion_i then int x y z w

struct student
do
  string name id
  int age
od
```
* A value of type `student` cannot be casted into any of the other types because its fields do not match the structure of the other types. It is also not possible to convert any the other types into `student` for the same reason.
* A value of type `quaternion_i` cannot be cast into `alpha_color_r`, because values may only be cast into members of an atomic type family at this level (a manual cast of each member would be needed by creating manually a new `alpha_color_r` and casting each field seperately). However, `quaternion_i` values can be cast into an `alpha_color` and a `color`.
* A value of type `alpha_color` can be cast into `color` and `quaternion_i`, but not `alpha_color_r`.
* A value of type `color` cannot be cast into any other the other types.

It is not possible to cast into unions. For components, the complex type rules only apply when casting _from_ a component. Components can be cast into structs and records, but the opposite is not allowed.

### Semi-Implicit Type Casting
Semi-Implicit Type Casting combines the best of two worlds; the convenience of implicit type casting and the rigorous clarity that explicit type casting brings. It says "here I'm type casting, it should be obvious what I'm doing if you take a short moment to think about it". It avoids making the code ugly and cluttered where a lot of type conversions would be necessary.

To cast semi-implicitely, one must use one of the Semi-Implicit Casting Operators:

|operator|name|definition|examples|
|-|-|-|-|
|?=|castassign|Converts the value from the right expression to the type of variable to the left, then assigns that value to the variable.|myIntVar ?= 1.5 + 2.5|
|?:|castinit|Converts the values from the right expresions to the types of the variables to the left, then assigns the values to those variables|myIntVar myStringVar ?: 1.1 2|
|?+|castplus|Converts the right operand to the type of the left operand, then returns the sum of the two operands|1.3 ?+ 2|
|?-|castminus|Converts the right operand to the type of the left operand, then returns the difference of the two operands|1.3 ?- 2|
|?*|casttimes|Converts the right operand to the type of the left operand, then returns the product of the two operands|1.3 ?* 2|
|?/|castdiv|Converts the right operand to the type of the left operand, then returns the quotient of the two operands|1.3 ?/ 2|
|?%|castmod|Converts the right operand to the type of the left operand, then returns the remainder of the two operands|1 ?% 2.3|
|?^|castpow|Converts the right operand to the type of the left operand, then returns the result of raising the left operand to the power of the right operand|1.3 ?^ 2|
|?&|castand|Converts the right operand to the type of the left operand, then returns the result of anding the two operands|1 ?& 2.3|
|?\||castor|Converts the right operand to the type of the left operand, then returns the result of oring the two operands|1 ?\| 2.3|
|?&&|casteand|Converts the right operand to the type of the left operand, then returns the result of xnoring the two operands|1 ?&& 2.3|
|?\|\||casteor|Converts the right operand to the type of the left operand, then returns the result of xoring the two operands|1 ?\|\| 2.3|
|?!&|castnand|Converts the right operand to the type of the left operand, then returns the result of nanding the two operands|1 ?!& 2.3|
|?!\||castnor|Converts the right operand to the type of the left operand, then returns the result of noring the two operands|1 ?!\| 2.3|
|?<<|castlshift|Converts the right operand to the type of the left operand, then returns the result of shifting the bits of the left operand to the left by the right operand|1 ?<< 2.3|
|?>>|castrshift|Converts the right operand to the type of the left operand, then returns the result of shifting the bits of the left operand to the right by the right operand|1 ?>> 2.3|
|?<@|castlrot|Converts the right operand to the type of the left operand, then returns the result of rotating the bits of the left operand to the left by the right operand|1 ?<@ 2.3|
|?@>|castrrot|Converts the right operand to the type of the left operand, then returns the result of rotating the bits of the left operand to the right by the right operand|1 ?@> 2.3|
|?->|castreturn|Converts the value to the return type of the callable, sets the return value to that value then return.|func int myfunction(real a real b) then ?-> a + b|
|?<-|castretset|Converts the value to the return type of the callable and sets the return value to that value|func int myfunction(real a real b) then ?<- a + b|
|?~|castcat|Converts the right operand to the type of the left operand, then returns the concatenation of the two operands|\[1 2 3\] ?~ \[4.4 5.5 6.6\]|

## Templates
Templates are made using the casting operator `?`. There are 3 types of templates:
* Type Template: a template made using one or more types. Applicable to callables and complex types.
* Value Template: a template made using a value. Applicable to callables.
* Callable Template: a template made using a callable. Results in a non-complex user-defined type.
* Composite Template: a template made using other templates. Results in a template.

### Type Templates
The type template is the simplest kind of template. It allows for simply making a callable or complex type available for more than one type. For example, if you have an addition callable, you may want it to work for all integer types, but it would take a lot of time to essentially copy and paste the same callable. So what one should do is to use a template like so:
```dew
?T func T add(T right T left) then -> right + left
```
In order to be sure that the type is corect, you may use a type family instead of a completely generic template:
```dew
# note: integer already exists, so no need to write ?integer before the func keyword
func integer add(integer right integer left) then -> right + left
```
Multiple types may be templated at once:
```dew
??T R G? proc void some_proc(T a R b G c)
do
  # your code here
od
```
You may also use the latter notation for only one if you prefer.

From the calling side, this is what it looks like:
```
inf result := add?int(10 (5 * 2))
```
### Value Templates
The value template is a semantic template for indicating the nature of what is being used. It's not a real template. For example, `base?8(mynumber)` or `measure?"centimeter"(table)` are really just a semantically alternative way of writing `base(8 mynumber)` and `measure("centimeter" table)` respectively. Here is how that works for declaring the signature of a value template now:

For base:
```dew
?B:int func int base(B number_base int number)
do
  # your code here
od
```

For measure:
```dew
?S:string func double measure(S unit Object3D obj)
do
  # your code here
od
```
### Callable Templates
A callable template is a way to bind a value to an arbitrary and reduced range of values which are not necessarily consecutive. For example, one might could define a callable template that describes a type which can only be odd; `?:odd_int(int i) such i % 2 = 0`. Or perhaps always lower-case character: `?:lower_char(char c) such c >= 'a' and c <= 'z'`. The syntax is always ?: followed by identifier then a single parameter followed by an as/such block in which one or more boolean conditions are defined, separated by newlines or a logical operator. New lines in this block default to `and` but can become any operator by starting the next line with the intended operator.

```dew
# example from earlier but on multiple lines 
?:lower_char(char c)
as
 c >= 'a'
 c <= 'z'
sa

# only "saturday" or "friday"
?:weekend_day(string s)
as
 s = "saturday"
 or s = "friday"
sa

# one liner version of above
?:weekend_day(string s) such s = "saturday" or s = "friday"
```
