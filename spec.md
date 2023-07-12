 # Dew Programming Language Specification
## Introduction
Dew is a high level programming language intended for experimenting with niche concepts. It is called Dew because it is Doigt's first serious language project and dew usually appears during the morning, which is the first part of the day. Dew's syntax is highly inspired by Algol 68, Bash and B as well as more modern languages such as D. As far as the author is aware, there is only one active project working on a Dew compiler and it is his own project, which is far from complete. This language specification doesn't describe what current compiler(s) can do but what they should do.

## Comments
Single line comments start with a hash tag `#`.
Multiline comments start and end with a cent symbol `¢`.

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
|eand|leand|logical|returns true if both boolean expressions returns the same result|
|<|lower|boolean|returns true if the left operand is smaller than the right operand|
|>|greater|boolean|returns true if the left operand is greater than the right operand|
|=|equal|boolean|returns true if both operands are equal|
|<>|different|boolean|returns true neither operands are equal|
|<=|loe|boolean|returns true if the operands are equal or the left operand is smaller than the right operand|
|>=|goe|boolean|returns true if the operands are equal or the left operand is greater than the right operand|
|is|is|boolean|returns true if the left operand's type is the same or is a child of the type in the right|
|isnt|isnot|boolean|returns true if the left operand's type is not the same or is not a child of the type in the right|
|in|in|boolean|returns the index of the position where the first instance of the left operand can be found in the array, returns -1 if it was not found|
|has|isin|boolean|returns true if the left operand can be found in the array| 
|&|band|binary|returns the result of anding the bits of the left operand with those of the right operand|
|\||bor|binary|returns the result of oring the bits of the left operand with those of the right operand|
|\|\||beor|binary|returns the result of xoring the bits of the left operand with those of the right operand|
|!&|bnand|binary|returns the result of nanding the bits of the left operand with those of the right operand|
|!\||bnor|binary|returns the result of noring the bits of the left operand with those of the right operand|
|&&|beand|binary|returns the result of xnoring the bits of the left operand with those of the right operand|
|<<|lshift|binary|returns the result of shifting the bits of the left operand to the left by right operand|
|>>|rshift|binary|returns the result of shifting the bits of the left operand to the right by right operand|
|<@|lrot|binary|returns the result of rotating the bits of the left operand to the left by right operand|
|@>|rrot|binary|returns the result of rotating the bits of the left operand to the right by right operand|

### Array Operators
Array operators are usually infix operators which will create a new array. They also work with the string type to a certain extent.
|operator|name|definition|effect on string|
|-|-|-|-|
|+|add-arr|if the left operand is an array and the right operand is either an array or a number, return the matrix sum of both operands|NA|
|-|sub-arr|if the left operand is an array and the right operand is either an array or a number, return the matrix difference of both operands|NA|
|*|sub-arr|if the left operand is an array and the right operand is either an array or a number, return the matrix product of both operands|NA|
|/|div-arr|if the left operand is an array and the right operand is either an array or a number, return the matrix quotient of both operands|NA|
|~|concatenate|create a new array from both operands and order them from left to right|if one of the operands is a string, create a new string from both operands and order them from left to right|
|~~|repeat|if the left operand is an array, create an array which has its elements repeated times the right operand|if the left operand is a string, create a new string which has its characters repeated times the right operand|
|!~|remove|return a new array where all instances of right operand in left operand have been removed|return a new string where all instances of right operand in left operand have been removed|

### Unary Operators
Unary operators are polish style operators with only one parameter.
|operator|name|type|definition|
|-|-|-|-|
|-|minus|arithmetic|returns the operand, which must be numeric, with the opposite sign|
|+|plus|arithmetic|returns the absolute value of the operand|
|--|decrement|arithmetic|decrements the operand, which must be a variable|
|++|increment|arithmetic|increments the operand, which must be a variable|
|**|power2|arithmetic|multiplies the operand, which must be a variable, by itself|
| \ |sqrt|arithmetic|returns the square root of the operand, which must be a positive number|
|!|not|binary|returns the result of inverting the bits of the operand|
|-|minus-arr|array|returns a new array with all the numbers of the array now of the opposite sign|
|+|plus-arr|array|returns a new array with all the absolute values of the numbers in the array| 
|--|dec-arr|array|decrements all the elements of the array|
|++|inc-arr|array|increments all the elements of the array|
|**|p2-arr|array|multiplies all the elements of the array by themselves|
| \ |sqrt-arr|array|returns a new array with the square roots of all the elements of the array|
|!|inv-arr|array|returns a new array with bits of all the elements the array inverted|
|!!|pop|array|returns and removes the last element of the array|
|$|length|array|returns the length of the array|
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
A numeric literal is defined as a sequence of case sensitive characters which represents binary, octal, decimal and hexadecimal numbers (0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F). Numbers can be separated by underscores `_` for added legibility. Each non-decimal sequence must start with a dollar sign `$` then a lower case letter representing that base: 
* Binary: $b1010_1011
* Octal: $o253
* Decimal: 171
* Hexadecimal: $xAB
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
Type families are used for comparing types, which is only useful for template constraints.
|family|children|
|-|-|
|integer|bits, long bits, long long bits, byte, long byte, long long byte, short int, int, long int|
|decimal|short real, real, long real, long long real|
|boolean|bits, long bits, long long bits, bool|
|strings|short string, string, long string, long long string|
|numeric|integer, decimal|
|text|strings, char|
|binary|numeric, boolean, char|
|primitive|binary, text|

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
### Assiging Values Using Speciliazed Variants of the Assign and Initialize Operators
The assign and initialize operators can also be used on variables which have already been assigned a value. However, there are many specialised variants of these two operators for common usecases.

|assign variant|initialize variant|assign name|initialize name|definition|examples|equivalent example|
|-|-|-|-|-|-|-|
|+=|+:|add-assign|add-init|adds the value(s) of the right expression to the value held by the variable(s) and assigns the result to the variable(s), matrix math applies if used on arrays|`a += 16` and `a b +: 16 8`|`a := a + 16` and `a b : (a + 16) (b + 8)`|
|-=|-:|sub-assign|sub-init|substracts the value(s) of the right expression to the value held by the variable(s) and assigns the result to the variable(s), matrix math applies if used on arrays|`a -= 16` and `a b -: 16 8`|`a := a - 16` and `a b : (a - 16) (b - 8)`|
|/=|/:|div-assign|div-init|divides the value(s) of the right expression to the value held by the variable(s) and assigns the result to the variable(s), matrix math applies if used on arrays|`a /= 16` and `a b /: 16 8`|`a := a / 16` and `a b : (a / 16) (b / 8)`|
|*=|*:|mul-assign|mul-init|multiplies the value(s) of the right expression to the value held by the variable(s) and assigns the result to the variable(s), matrix math applies if used on arrays|`a *= 16` and `a b *: 16 8`|`a := a * 16` and `a b : (a * 16) (b * 8)`|
|^=|^:|power-assign|power-init|gets the result(s) of the variable(s) raised to the power of the expression and assigns it to the variable(s)|`a ^= 16` and `a b ^: 16 8`|`a := a ^ 16` and `a b : (a ^ 16) (b ^ 8)`|
|%=|%:|mod-assign|mod-init|divides the value(s) of the right expression to the value held by the variable(s) and assigns the remainder to the variable(s)|`a %= 16` and `a b %: 16 8`|`a := a % 16` and `a b : (a % 16) (b % 8)`|
|&=|&:|and-assign|and-init|ands the bits of value(s) of the right expression to the bits of the value held by the variable(s) and assigns the result to the variable(s)|`a &= 16` and `a b &: 16 8`|`a := a & 16` and `a b : (a & 16) (b & 8)`|
|\|=|\|:|or-assign|or-init|ors the bits of value(s) of the right expression to the bits of the value held by the variable(s) and assigns the result to the variable(s)|`a \|= 16` and `a b \|: 16 8`|`a := a \| 16` and `a b : (a \| 16) (b \| 8)`|
|~=|~:|cat-assign|cat-init|concats the array(s) or string(s) with the result of the left expression and assigns the new array to the arrays on the left-side of the operator. If the array is flexible, no new array is created, the extant array is simply expanded.|`a ~= 16` and `a b ~: 16 8`|`a := a ~ 16` and `a b : (a ~ 16) (b ~ 8)`|

