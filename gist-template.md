# Title

Learning regular expressions (regex) through date validation.

## Summary

The following regular expression (regex) is used for validating dates in the format dd/mm/yyyy, dd-mm-yyyy, or dd.mm.yyyy, considering leap years. The sections below dissect some of the regex and describe much of the functionality of this (and other) regex. 

```
/^(?:(?:31(\/|-|\.)(?:0?[13578]|1[02]))\1|(?:(?:29|30)(\/|-|\.)(?:0?[1,3-9]|1[0-2])\2))(?:(?:1[6-9]|[2-9]\d)?\d{2})$|^(?:29(\/|-|\.)0?2\3(?:(?:(?:1[6-9]|[2-9]\d)?(?:0[48]|[2468][048]|[13579][26])|(?:(?:16|[2468][048]|[3579][26])00))))$|^(?:0?[1-9]|1\d|2[0-8])(\/|-|\.)(?:(?:0?[1-9])|(?:1[0-2]))\4(?:(?:1[6-9]|[2-9]\d)?\d{2})$/
```

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)
- [Resources](#resources)



## Regex Components

### Anchors

Anchors indicate start `^` or end `$` of a string of code. For example, 
This section of of the regular expression is checking whether a given string represents a valid date for February 29th and accounting for leap years. The beginning of the string asserted with the `^` and the end of the string is declared with the `$`
```

"^(?:29(\/|-|\.)0?2\3(?:(?:(?:1[6-9]|[2-9]\d)?(?:0[48]|[2468][048]|[13579][26])|(?:(?:16|[2468][048]|[3579][26])00))))$|
```
Can you find the 3 starts and ends of strings in the full example code?

### Quantifiers

Quantifiers specify the number of occurrences of a character or a group of characters. THere are several. `*` means that there are 0 or more occurances preceding a character or group. `?` matches 0 or 1 time, `+` 1 or more times. There are also `{n}, {n,} and {n,m}`, which match exactly n, at least n times or n to m times respectively. 

For example, `(?:(?:1[6-9]|[2-9]\d)?\d{2})$` matches the component of the date between the years 1600 and 9999. We'll see more below, the `?` quantifier at the end of the string means it can match 0 or 1 times. This allows for the entry of no year (0 times) or a two digit year. The `{2}` quantifier means it must match twice. 

### OR Operator

The OR operator, or `|` allows for more than one possibility. In the example about the OR operator allows for the year to start with 1 or with any integer from 2 to 9. 
We can also see the OR operator in the section that and matches days of the month and the months 1, 3, 5,  `|` in the above expression in this string:
`^(?:(?:31(\/|-|\.)(?:0?[13578]|1[02]))\1:`
`|` in this section `(\/|-|\.)` matching delimeters `\` OR
`^`: Asserts the start of the string.
`(?:31(\/|-|\.)`: Non-capturing group matching the days from 01 to 31, followed by a delimiter slash `(/)`, hyphen `(-)`, or period `(.)`.
`(?:0?[13578]|1[02])`: Non-capturing group matching the months 01, 03, 05, 07, 08, 10, or 12.
`\1`: Backreference to the delimiter used after days.

### Character Classes

Character classes allow for designating a set of from which a character should match. They are signified by square brackets `[]`. If you look at the example for quantifiers, there are two `[6-9]` and `[2-9]`. This indicates that the input should be 6, 7, 8 or 9 (thus 1600-1900) or 2 through 9, allowing for 2000s, 2100s, etc to 9999. 

Can you pinpoint where the first `[]` character class is in the full example above? What characters is it limiting to. Why do you think that is in this case?

### Flags

Flags are coding language specific and alter how 
the engine intreprets the expression. There are no flags in our example, but flags are usually specified after the closing `\`. Common flags might be  `i` and `g` flags allow for the regex engine to ignore case `i` or find all matches `g` instead of stopping at the first match. 

What other flags are there? 

### Grouping and Capturing

Grouping is indicated by paranthesis `()` and and is used to group parts of the regex. Non-capturing groupings are needed for matching but are not needed for a referencing later in the regex. Usually, if the opening `(` is follwed immediately by a `?`, it is not a capturing group.  `(\d{2})` This on the otherhand is and can be referenced later in the regex by the order in which it appears in the regex. For example, if `(\d{2})` is the first occurance of a capturing group, can later be references by `\1`, and so on. 

### Bracket Expressions

The term bracket expression `[]` is used interchangeby with character class as described above. 

### Greedy and Lazy Match

Greedy matches match as many characters as they are able. In other words, a quantifier tells the engine to match as many instances of its quantified pattern as possible. By default quantifiers such as `*, ?, + and others` are greedy. 
A lazy match tells the regex engine to find as few matches as needed, or none. Lazy matches are usually signified by a `?` after the quantifier such as `*?, ??, +?`. This is not necessarily the shortest match in the search of a section.


### Boundaries

Boundaries are used to show positions where word characters transition to non-word characters or vice versa within the input text. THey are signified by 
`\b`, word boundary and `\B`, non-word boundary. There are no examples of this in the provided text. 

### Back-references

Back references allow the user to refer back to previously captured groups within the same expression. As suggested in the grouping and capturing section, there are back references in the full example above. 

For example, in this part of the regex `(\d{2})[./-]\1[./-]\d{4}`  `\1` refers back to the first capturing group `[./-]` to which ensures the delimiter in the date is the same in both instances. 

### Look-ahead and Look-behind

Look-ahead and look-behind are advanced features in regular expressions that allow you to assert whether a particular pattern does or does not follow or precede the current match position, without including that pattern in the match itself.

They are not used in the regex above for date validation. Instead, more basic components such as grouping, quantifiers, character classes, and anchors are used to validate the date formats.

The syntax of a look-ahead feature is Syntax: `(?= ... )` This requires a certain pattern (the lookahead) must be present after the current position. For example, if we want to match all instances of "feefi" that are followed by "fofum", but we only want to match "feefi" itself. We can use a positive lookahead assertion for this: `feefi(?=fofum)`.
`(?<= ... )` is a look-behind assertion. 
Using the same example above, `(?<=feefi)fofum` would search for fofum, but only if preced by feefi.


## Breakdown

Now, using what we learned above, let's break down the regular expression we started with:

A. `^(?:(?:31(\/|-|\.)(?:0?[13578]|1[02]))\1`
^: Asserts the start of the string.
`(?:31(\/|-|\.)`: This non capturing group matches the days from 01 to 31, followed by either a slash (/), hyphen (-), or period (.).
 `(?:0?[13578]|1[02])`: This matches the months 01, 03, 05, 07, 08, 10, or 12.
`\1:` This references back to the delimiters for day, requring the same. 
B.`|(?:(?:29|30)(\/|-|\.)(?:0?[1,3-9]|1[0-2])\2)):`
`|` the OR operator.
`(?:29|30)(\/|-|\.)`: Group (non-capturing) for days 29 or 30 followed by a delimiter.
`(?:0?[1,3-9]|1[0-2])`: Group (also NC) matching months 01 to 09 and 10 to 12.
`\2`: This references back to the previous delimeter.

C. `(?:(?:1[6-9]|[2-9]\d)?\d{2})$:`
`(?:1[6-9]|[2-9]\d)?\d{2}`: Non-capturing group for years from 1600 to 9999 as described above
`$`: Asserts the end of the string.

D. `|^(?:29(\/|-|\.)0?2\3:`
`|`: OR operator.
`(?:29(\/|-|\.)`: Non-capturing group for the 29th day, followed by a delimiter.
`0?2`: Matches the month of February (02) with an optional leading zero.
`\3`: Backreference to the delimiter used after days.

E. `(?:(?:(?:1[6-9]|[2-9]\d)?(?:0[48]|[2468][048]|[13579][26])|(?:(?:16|[2468][048]|[3579][26])00))))$`:
`(?:1[6-9]|[2-9]\d)?`: Group (NC) for years from 1600 to 9999.
`(?:0[48]|[2468][048]|[13579][26])`: Group (NC) for leap years divisible by 4 but not by 100, or divisible by 400.
`(?:16|[2468][048]|[3579][26])00`: Group for leap years divisible by 400 or divisible by 4 but not by 100.
`$`: The end of the string.

F. `|^(?:0?[1-9]|1\d|2[0-8])(\/|-|\.)`:
`|`: OR operator.
`(?:0?[1-9]|1\d|2[0-8])`: Group for days 01 to 28.
`(\/|-|\.)`: Matches the delimiter after days.

G. `(?:(?:0?[1-9])|(?:1[0-2]))\4`:
`(?:0?[1-9])|(?:1[0-2])`: Group (NC) for months 01 to 12 with a allowed leading zero.
`\4`: Backreference to the delimiter used after days.

H. `(?:(?:1[6-9]|[2-9]\d)?\d{2})$`:
`(?:1[6-9]|[2-9]\d)?\d{2}`: Group for years from 1600 to 9999.
`$`: Asserts the end of the string.


## Author

The author of this short tutorial is Trey Lathe, a soon-to-be graduate of the UC Berkely Extentsion Fullstack Coding BootCamp. His profile can be found at https://github.com/TreyLathe 

## Resources

For a deeper understanding of regular expresssions, the two following sites are helpful:

[Regex101.com](https://www.Regex101.com)
[Regexr.com](https://www.regexr.com)
