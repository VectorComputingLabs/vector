---
title: Vector Programming Language Specification
version: 0.1
date:
editor: Higenyi Tobias Thomas
---

## Introduction
This document describes the Vector Programming Language.
It focuses on Syntax and Semantics rather than implementation.
The current version described in this document is version 0.1.
The various sections in this document describe various aspects of
the language and how it is represented.
This document uses a simplified Backus-Naur Form (BNF) to express
language details.

### Description of Notation
The simplified Backus-Naur Form of expression used in this document is
described below. The notation is composed of productions.
Productions describe elements and entities in Vector.
They are made up of a name and a description separated by the `:=` symbol.
```
name := description
```
A description is composed of a combination of tokens,
symbols and productions themselves. Tokens are atomic building blocks 
of the language. They include keywords, literals, operators, separators
and white space. Descriptions are written as regular expressions.
If T is a term in a description D, then:
- T+ = T appears 1 or more times
- T* = T appears 0 or more times
- T1|T2 = either T1 or T2
- (T1,T2) = a group of T1 and T2
- [T] = T is optional

## Literals
Literals are a representation of supported builtin types in vector.
There are 4 literal types namely: integers, floats, strings and boolean
### Integers
Integers are numeric data represented by digits. Integers can be written
in binary, decimal and hexadecimal form. Binary numbers start with a `0(b|B)`
prefix followed by a sequence of 1 or 0 integers.
Decimal numbers are not prefixed. They contain a sequence of `0 - 9` integers.
Hexadecimal numbers start with a `0(x|X)` prefix followed by a sequence of
`0 - 9` digits and `a|A ... f|F` characters. The sequence of digits of a
number can optionally contain an underscore ('_') character as a separator.
Decimal numbers are signed. Prefixing them with a minus sign ('-') converts
them into negative numbers. Decimal numbers can also have an exponential
postfix represented by character ('e') followed by a sequence of digits.
The sequence of digits can also be a negative number
```
binary-digit       := (0|1)
digit              := (binary-digit|2|3|4|5|6|7|8|9)
alpha-digit        := digit|'a'|'b'|'c'|'d'|'e'|'f'|'A'|'B'|'C'|'D'|'E'|'F'
binary-number      := 0('b'|'B') binary-digit (['_'] binary-digit)*
decimal-number     := [-]digit (['_']digit)* ['e'['-']digit+]
hexadecimal-number := 0('x'|'X') alpha-digit (['_'] alpha-digit)*
```
### Floating-point numbers
Floating-point numbers are numeric data represented by a sequence of digits
separated by a single period character ('.'). The sequence of digits on the
left-hand part is called the `whole number` 
while the sequence on the right is called `mantissa`.
Floating point numbers are only represented with decimal integers.
The mantissa can be postfixed with an exponent number.
Binary and Hexadecimal numbers cannot be used as floating-point numbers
```
floating-point-number := [-]digit+ '.' digit+['e' digit+]
```


## Scope
Scope is an execution context in which variables are defined.
They include:
    - Module Scope
    - Instance Scope
    - Function Scope

## Identifiers
Identifiers are valid names for entities in a vector program.
They are sequences of alpha-numeric characters of variable length.
Identifiers SHOULD NOT start with numeric characters.
Identifiers CAN contain underscore characters (_).
Identifiers that start with an underscore character are considered
private to the current scope they are defined in.
```
identifier        := [_]alpha-numeric-seq
alpha-numeric-seq := char[char|int|"_"]*
``` 

## Keywords
Keywords are words that carry special meaning in vector and cannont
be used as identifiers. They include
```
def      if        else       switch
case     for       while      endif
endfor   endwhile  endswitch  end
return   yield     new        is
in
```

## Modifiers
Modifiers are special words that alter or enhance how an entity is
created or used. They include:
### const
The const modifier is used to define constant variables who's value is
unchanged throughout the life-time of the running program
### dataonly

## Comments

## Variables
Variables are memory locations that store addresses to values.
They are written with a type annotation first, followed by the variable name
and then assigned to a value of the same type as the variable.
```
variable-definition := [modifier] type-annotation name "=" value
type-annotation     := type-definition
```