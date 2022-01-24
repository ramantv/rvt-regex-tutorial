# rvt-regex-tutorial - For Matching a URL

This is a tutorial for a regular expressions using the example of a regular expression for matching a URL.

## Summary

This tutorial will explain the following regular expression for matching a URL: 

```
  /^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/
```

We will break down the expression and provide detailed explanations of each piece. 

## Table of Contents

- [rvt-regex-tutorial - For Matching a URL](#rvt-regex-tutorial---for-matching-a-url)
  - [Summary](#summary)
  - [Table of Contents](#table-of-contents)
  - [Regex Components](#regex-components)
    - [Anchors](#anchors)
    - [Quantifiers](#quantifiers)
    - [Character Classes](#character-classes)
    - [Flags](#flags)
    - [Literals](#literals)
    - [Grouping and Capturing](#grouping-and-capturing)
    - [Bracket Expressions](#bracket-expressions)
  - [Author](#author)

## Regex Components

### Anchors
The anchors are identified by two characters seen throughout regular expressions. Primarily, they are the ^ and the $ -- signifying what we will be looking for at the beginning and end of the string. The anchors identify when the start and end of the string we are looking for will occur. 

Beginning anchor: 

^

Closing anchor:

$


### Quantifiers

The common quantifiers that are seen in this regular expression are the ? and * symbols. 

The question mark is used to identify optional characters and is seen a few times in this regular expression: 

```
  (https?:\/\/)? and *\/?$/
```

The first question mark labels the "s" in "https" as optional. This is because some URLs start with http:// and others start with https://. We would want the regular expression to find both. In other words, it is saying the literal string "http" followed by zero or one "s". The ? after the first grouping marks the entire first grouping as optional. Just like with the character "s" in the string, some URLs will just begin with "www." thus making the http:// or https:// obsolete in some cases. We would still want to flag any URLs without the beginning http. The question mark before the ending anchor marks the final "/" in a URL. It is optional as www.github.com/ramantv/ and www.github.com/ramantv would both be valid URLs. 

The * is seen twice near the end of the regular expression:

```
  ([\/\w \.-]*)*\/?$/
```

We previously discussed the \w grouping which allows for any alphanumerical character. In this grouping, there are also some symbols allowed in the filepath portion. The * is marking that the final grouping can happen any number of times and be followed by the same thing multiple times. For example, www.github.com/ramantv/repositories/new/data-man. The question mark only allows for zero or one of the preceding character or grouping. 

The final quantifier is the {2,6}. This says that we can only have 2 to 6 characters in this portion of the URL. This is limited between 2-6 because it is most commonly .com, .au, etc.-- which refers to the top-level domain (TLD) in the Domain Name System of the Internet, in many cases it denotes the country of the top-level domain. 

### Character Classes

The character classes that are used in this expression are the \d in the second group and the \w in the last group: 

```
  [\da-z\.-]
```

The \d matches any single character that is a digit. This entire expression is looking for the domain name. For example, www.google or www.W3School would all be found as this expression is looking for any digit, any letter a-z, and any '.' or '-'. 

The last group is identifying the last portion of the URL which leads to a specific filepath. These can be any amount of '/' or words that are necessary. The \w identifies any alphanumeric character. The grouping is seen here:

```
  [\/\w \.-]
```

This would identify any words or directories that are written post the domain. For example, http://www.github.com/Ramantv would be found because this section of the regular expression would capture the "Ramantv" portion as they are all alphanumeric characters.

### Flags

Commonly, regular expressions are delimited by the '/'. We see this at the beginning and end of the expression, even after the anchors that we previously discussed. It is possible to identify search criteria outside of the flags to help mark the expression as global (g), multi-line (m), or insensitive (i). 

### Literals

Many symbols have special powers in regular expressions. The abundance of "\\" in this expression identify literals in a series of characters. In a URL we will commonly see the "//" or ".com". We can tell the expression when to look for these specific symbols. For example, in between grouping one and two we see a "\." : 

```
  ([\da-z\.-]+)\.([a-z\.]{2,6})
```

This is saying to look for the character ".". The "." can also be used to identify any character. The ".\*" is known as the wild card -- any character, any number of times. Without the \ before these symbols, they would have a special power instead of be a literal character. 

### Grouping and Capturing

The expression is four significant groups:

```
  /^(https?:\/\/)? and ([\da-z\.-]+)\. and ([a-z\.]{2,6}) and ([\/\w \.-]*)*\/?$/
```

The first group is the optional http portion. The second group is looking for any characters that would represent a domain name, followed by a ".". The third group is most commonly seen as a ".com" and is limited to 2-6 characters. The final group is the filepath or directory specification. This can be repeated any number of times and be any word. 

### Bracket Expressions

The bracket expressions in this regular expression:

```
  [\da-z\.-] and ([a-z\.]{2,6} and [\/\w \.-]
```

The bracket expressions identify which portions of the expressions can be any or all of the characters within each bracket. In the initial bracket expression, we can say that we are looking for any digit, or any character a-z, or any "." or "-". Similarly with the last two brackets, we are looking for any or all of those characters. 

## Author
This Regex tutorial was written by [Raman TV](https://github.com/ramantv)