# Title

Learning regular expressions (regex) through date validation.

## Summary

The following regular expression is used for validating dates in the format dd/mm/yyyy, dd-mm-yyyy, or dd.mm.yyyy, considering leap years.

```
/^(?:(?:31(\/|-|\.)(?:0?[13578]|1[02]))\1|(?:(?:29|30)(\/|-|\.)(?:0?[1,3-9]|1[0-2])\2))(?:(?:1[6-9]|[2-9]\d)?\d{2})$|^(?:29(\/|-|\.)0?2\3(?:(?:(?:1[6-9]|[2-9]\d)?(?:0[48]|[2468][048]|[13579][26])|(?:(?:16|[2468][048]|[3579][26])00))))$|^(?:0?[1-9]|1\d|2[0-8])(\/|-|\.)(?:(?:0?[1-9])|(?:1[0-2]))\4(?:(?:1[6-9]|[2-9]\d)?\d{2})$/
```

## Table of Contents

- [Anchors](#anchors)

Anchors indicate start `^` or end `$` of a string of code. For example, 
This section of of the regular expression is checking whether a given string represents a valid date for February 29th and accounting for leap years. The beginning of the string asserted with the `^` and the end of the string is declared with the `$`
```

"^(?:29(\/|-|\.)0?2\3(?:(?:(?:1[6-9]|[2-9]\d)?(?:0[48]|[2468][048]|[13579][26])|(?:(?:16|[2468][048]|[3579][26])00))))$|
```
Can you find the 3 starts and ends of strings in the full example code?

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

## Regex Components

### Anchors
Anchors indicate start `^` or end `$` of a string of code. For example, 
This section of of the regular expression is checking whether a given string represents a valid date for February 29th and accounting for leap years. The beginning of the string asserted with the `^` and the end of the string is declared with the `$`
```

"^(?:29(\/|-|\.)0?2\3(?:(?:(?:1[6-9]|[2-9]\d)?(?:0[48]|[2468][048]|[13579][26])|(?:(?:16|[2468][048]|[3579][26])00))))$|
```
Can you find the 3 starts and ends of strings in the full example code?

### Quantifiers

Quantifiers specify the number of occurrences of a character or a group of characters. THere are several. `*` means that there are 0 or more occurances preceding a character or group. `?` matches 0 or 1 time, `+` 1 or more times. There are also {n}, {n,} and {n,m}, which match exactly n, at least n times or n to m times respectively. 

For example, (?:(?:1[6-9]|[2-9]\d)?\d{2})$ matches the component of the date between the years 1600 and 9999. We'll see more below, the `?` quantifier at the end of the string means it can match 0 or 1 times. This allows for the entry of no year (0 times) or a two digit year. The {2} quantifier means it must match twice. 

### OR Operator

The OR operator, or `|` allows for more than one possibility. In the example about the OR operator allows for the year to start with 1 or with any integer from 2 to 9. 

### Character Classes

Character classes allow for designating a set of from which a character should match. They are signified by square brackets []. If you look at the example for quantifiers, there are two [6-9] and [2-9]. This indicates that the input should be 6, 7, 8 or 9 (thus 1600-1900) or 2 through 9, allowing for 2000s, 2100s, etc to 9999. 

Can you pinpoint where the first [] character class is in the full example above? What characters is it limiting to. Why do you think that is in this case?

### Flags

Flags are coding language specific and alter how 
the engine intreprets the expression. There are no flags in our example, but flags are usually specified after the closing `\`. Common flags might be  `i` and `g` flags allow for the regex engine to ignore case `i` or find all matches `g`
### Grouping and Capturing

### Bracket Expressions

### Greedy and Lazy Match

### Boundaries

### Back-references

### Look-ahead and Look-behind

## Author

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)
