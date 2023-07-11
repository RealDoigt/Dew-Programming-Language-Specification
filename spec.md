# Dew Programming Language Specification
## Introduction
Dew is a high level programming language intended for experimenting with niche concepts. It is called Dew because it is Doigt's first serious language project and dew usually appears during the morning, which is the first part of the day. Dew's syntax is highly inspired by Algol 68, Bash and B as well as more modern languages such as D. As far as the author is aware, there is only one active project working on a Dew compiler and it is his own project, which is far from complete. This language specification doesn't describe what current compiler(s) can do but what they should do.

## Literals
Dew has 4 types of literals: boolean literals, string literals, character literals and numeric literals.

### Boolean
A boolean literal is defined as being one of two valid keywords; `true` or `false`.

### String
A string literal is defined as a sequence of characters enclosed between a pair of double quotes `"`.

### Character
A character literal is defined as a sequence of characters enclosed between a pair of single quotes `'`.

### Numeric
A numeric literal is defined as a sequence of case sensitive characters which represents binary, octal, decimal and hexadecimal numbers (0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F). Numbers can be separated by underscores `_` for added legibility. Each non-decimal sequence must start with a dollar sign `$` then a lower case letter representing that base: 
* Binary: $b1010_1011
* Octal: $o253
* Decimal: 171
* Hexadecimal: $xAB

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
On the surface, bits look like an array of bools. However in truth, the bits type is not a real array. It's just syntax sugar. One can use bits variables as if one were using an array. The bits type is compatible with all array operations exception concatenation. The bits type cannot be made into a flexible array either. Because the bits type is really just a byte, it is compatible with all operators and functions that work on bytes.

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

Example:
```dew
proc void main
do
  # variable a is set to 1
  int a := 1

  # variable b's three elements are set to 10, 20 and 30 respectively
  ints b := [10 20 30]

  # all six values of the array are set to 5
  int[6] c := 5
od
```

#### Using the Initialize Operator
The initialize operator `:` can be used to assign values to a group of variables. If there are less values than variables, then the last variables that don't have a matching value get the last value. The compiler should throw an error and refuse to compile if there is only one variable being initialized or if there are fewer variables than there are values. Whether the initialize operator works with `inf` or not is up to the individual compiler. The initialize operator is intended for use with simple use cases such as function calls, literals or other variables. If you need something that needs more operators such as `2 * userCount / 3`, it will not compile due to how the syntax works.

Example:
```dew
proc void main
do
  # set a to 1, b to 2 and c to 3
  int a b c : 1 2 3

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
### Assiging Values Using Speciliazed Variants of the Assign and Initialize Operators
The assign and initialize operators can also be used on variables which have already been assigned a value. However, there are many specialised variants of these two operators for common usecases.

|assign variant|initialize variant|assign name|initialize name|definition|examples|equivalent example\*|
|-|-|-|-|-|-|-|
|+=|+:|add-assign|add-init|adds the value(s) of the right expression to the value held by the variable(s) and assigns the result to the variable(s)|`a += 16` and `a b +: 16 8`|`a := a + 16`|
|-=|-:|sub-assign|sub-init|substracts the value(s) of the right expression to the value held by the variable(s) and assigns the result to the variable(s)|`a -= 16` and `a b -: 16 8`|`a := a - 16`|
|/=|/:|div-assign|div-init|divides the value(s) of the right expression to the value held by the variable(s) and assigns the result to the variable(s)|`a /= 16` and `a b /: 16 8`|`a := a / 16`|
|*=|*:|mul-assign|mul-init|multiplies the value(s) of the right expression to the value held by the variable(s) and assigns the result to the variable(s)|`a *= 16` and `a b *: 16 8`|`a := a * 16`|
|^=|^:|power-assign|power-init|gets the result(s) of the variable(s) raised to the power of the expression and assigns it to the variable(s)|`a ^= 16` and `a b ^: 16 8`|`a := a ^ 16`|
|%=|%:|mod-assign|mod-init|divides the value(s) of the left expression to the value held by the variable(s) and assigns the remainder to the variable(s)|`a %= 16` and `a b %: 16 8`|`a := a % 16`|

\*Please refer to the section on the initialize operator for the reason why the equivalent example column doesn't present any example with the initialize operator.
