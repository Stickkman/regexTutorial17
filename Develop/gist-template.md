# Regex Tutorial: Validating an Email Explained

Regex, short for Regular Expressions, are a unique sequence of characters that form a search pattern.  They can be used for finding a specific pattern of text, manipulating a single/sequence of characters within a string, validating input, and depending on your imagination much more!  The best part is that Regex functions are universal, meaning that they are not tailored for use for just a single programming language like javascript, or php, but can be used in all programming languages.  This makes them something any developer should love and use as I hope you will.

## Summary

Briefly summarize the regex you will be describing and what you will explain. Include a code snippet of the regex. Replace this text with your summary.
I will be breaking down the structure of a regex for validating an Email in this tutorial.  Explaining what each part does and providing examples. 
The particular regex for this is `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/` and we will be referencing it multiple times throughout.


## Table of Contents
- [Common Use Cases](#Common-Use-Cases)
- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Summary](#summary)

## Common Use Cases
1. Search and replace: With Regex, you can search for a specific pattern within a string and replace it with another string. For example, you can search for all occurrences of a certain word in a text document and replace it with another word.

2. Validating data: Regex can be used to validate data input such as email addresses, phone numbers, and credit card numbers. By defining the expected pattern for each type of data, regex can quickly determine whether the input data is valid or not.

3. Parsing text: Regex can be used to extract specific pieces of information from text documents. For example, you can extract all the URLs from an HTML page, or extract all the email addresses from a list of contacts.

4. Data cleaning: Regex can be used to clean up messy data by removing unwanted characters or formatting. For example, you can remove all non-numeric characters from a phone number or remove all punctuation marks from a text document.

## Regex Components
Regex Components can vary in complexity depending on which one you choose to use/create.  The `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/` regex we are using in this tutorial is used to match/validate email addresses that have a specific pattern of:
- one or more characters that are lowercase letters, digits, undersocres, dots, or hyphens
- that must be followed by an `@` symbol
- which in turn must be followed by one or more characters that are digits, lowercase letters, dots, or hyphens, followed by a period
- which also in turn must be followed by 2 to 6 lowercase letters or periods.

Don't worry is this seems a little complex, I will be breaking down each component below.

### Anchors
In the sample regex of `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`, the `^` and the `$` are both considered `anchors`
1. `^`
    - The `^` signifies a string that begins with the characters that follow it.  So with this example the `^` means that the email address must `START` with the pattern specified immediately after it, with this case being:
    - any any alphanumeric character defined by: `a-z0-9` section of the code
    - including underscores, dots or hyphens defined by : `_\.-` section of the code, Note the brackets`[]` indicate a range
    - So all together `^([a-z0-9_\.-]` would include both the above 

2. `$`
    - The `$` matches the end of the string.  In this example it ensures that the email address must `END` with the pattern specified.
    - So the `([a-z\.]{2,6})$` section of the above code means that the pattern must `END` with a pattern of:
        - lowercase character and/or period,
        - the `\` before the period is used to `escape` the period so it is not confused as something else because it usually has a special meaning/use   in regexs.  Again notice how the `[]` brackets are used to contain the range. 

### Quantifiers
Quantifiers set the limits/constraints of the string that the regex matches.  They usually include both a min and max number of characters that your looking for. Common uses of quatifiers are as follows:
    - `*` Matches the pattern zero or more times
    - `+` Matches the pattern one or more times
    - `?` Matches the pattern zero or one time
    - `{}` Curly brackets can provide three different ways to set limits for a match:
        - `{ n }`    Matches the pattern exactly n number of times
        - `{ n,}`    Matches the pattern at least n number of times
        - `{ n, x }` Matches the pattern from a minimum of n number of times to a maximum of x number of times
So in our example of `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/` the quantifier section would be `{2,6}`
    - This equates to saying that the previous character set should be between `2` and `6` characters.

### OR Operator
This is not used in the example expression but for fluidity the `|` is known as the `OR Operator` is simply means or.
An example of this would be:
    - `[C|r|a|i|g|]` this means that any `C` or `r` or `a` or `i` or `g` would consitute a successful match.
    - `(Craig)` would equal the same as above, keep in mind that this is case sensitive in both cases.  Meaning that `c` would not be a match, only 
                `C`in upper case form would.
          
### Character Classes
A character class in regex deifines a set of characters to be included in the pattern.  They can be both `positive` and `negative`
Common character classes include:
    - `.` matches any character execpt `\n` newline character.
    - `\d` matches any digit, the same as `[0-9]
    - `\w` matches any alphanumeric character *including underscore* `_`, same as `[A-Za-z0-9_]`
    - `\s` matches a single whitespace
    - *sidenote:* character classes can be used to preform the inverse of their original intention by captializing them
        - example `\D` would match NON digit characters, instead of `\d` which matches only digit characters

 In our specific example of `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/` the character classes would be:
 - `[a-z0-9_\.-]` A character set that matches any lowercase letter, digit, underscore, period `.`, or hyphen `-`
 - `[\d]`         A character set that matches any digit `(0-9)` 
 - `[a-z\.]`      A character set that matches any lowercase letter or a period `.`. The backslash before the period is used to `escape` the
                    period, which has a special meaning in regular expressions (it matches any character). So, we're using a literal period here.
  
### Flags
Flags are placed at the end of a regex after the second `/`.  They define additional limits for the regex.  There are a total of six flags which are optional, here are 3 common ones:
    - `g` Global Search, means they should be tested against all possible matches, pretty much a `find all`
    - `i` Case Insensitive, means case is ignored while matching
    - `m` Multi Line Search, a multi line search should be treated like multiple lines

Our example of `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/` does NOT include any flags but if we needed to for example ignore the case of the characters we could write it as follows: 
- `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/i` which would ignore the case when matching characters in the input string.
- With this flag the regex would match email address like `craigC@gmail.com` or `Craig_C@GMAIL.com` and not just lowercase.

### Grouping and Capturing
Grouping and capturing are 2 related concepts that are used to extract specific parts of a matched string
    - Grouping is the process of enclosing part of a regex in parentheses `()` to create a subexpression.  This consists of a range of characters including quantifiers and sets of characters.  Grouping is usefull for specifiying the scope of the regex.
    - Capturing is the process of assigning a captured substring to a numbered group/named group.  Bascially when a regular experssion matches a string that contains a grouped subexpression, the matched substring is captured and stored in memory for later use.  Capturing is useful for extracting specific parts of a matched string for manipulation.

In our example of `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`:
    - `([a-z0-9_\.-]+)` - This is a capturing group that matches one or more characters that are either lowercase letters, digits, underscores, dots, 
                          or hyphens.

### Bracket Expressions
Bracket Expressions are anything inside a set of square brackets `[]` which represent a range of characters we want to match.
They can be either:
    - `Postitive Character Group` meaning characters we want to `INCLUDE`
    - `Negative Character Group` meaning characters we want to `EXCLUDE`
In our example of `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`:
    - The first set of brackets `[a-z0-9_\.-]` matches any lowercase letter from a to z, any digit from 0 to 9, underscore (_), dot (.) and hyphen (-).
      The + quantifier after the brackets means that this character class can occur one or more times, which allows the regex to match email addresses with multiple characters before the @ symbol.
    - The second set of brackets `[\da-z\.-]` matches any digit (\d is a shorthand for any digit), any lowercase letter from a to z, dot (.) and hyphen
      (-). Again, the + quantifier means that this character class can occur one or more times.
    - The third set of brackets [a-z\.]{2,6} matches any lowercase letter from a to z or dot (.) and must occur between 2 to 6 times. This is to match 
      the top-level domain name, which can have a maximum length of 6 characters.  

### Greedy and Lazy Match
In regular expressions, quantifiers such as + and * are greedy by default, which means they try to match as much as possible. However, if we want to match as little as possible, we can use the `lazy match` or `non-greedy` quantifier `+?` or `*?`

In the example regex `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`, the `+` after each character class `([a-z0-9_\.-]+)` and `([\da-z\.-]+)` indicates that the characters inside the brackets can occur one or more times, and the `+` is `greedy` by *default*, which means it will match as many characters as possible. Similarly, the `{2,6}` after the last character class of `([a-z\.]{2,6})` specifies that the last group should contain between 2 and 6 lowercase letters or dots.

To make these quantifiers `lazy`, we can add a `?` after the `+` and `{2,6}`. This will match the minimum number of characters required to satisfy the pattern, instead of matching as many as possible.

### Boundaries
In regex, boundaries are used to specify the limits or positions where a pattern should match. There are two types of boundaries:
1. Start of line boundary: It specifies that the pattern should match only at the beginning of a line or string. It is represented by the`(^)`
2. End of line boundary: It specifies that the pattern should match only at the end of a line or string. It is represented by the `($)`

Using both start and end of line boundaries can be helpful in ensuring that a pattern matches only when it is found at the beginning and/or end of a line or string.

In our example of `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`, 
the `(^)` and `($)` are our boundaries.
    - The `^` Matches the start of the input string. 
    - The `$` Matches the end of the input string.
This has been explain in more detail above [Anchors](#anchors)

## Summary
In summary the regex is a highly useful tool for any developer, especially considering it is not bound or limited by a single programming language because it works in all of them.  You can also use regex inside of various other programs such as `VSCODE`.  The `CTRL + F` shorcut is basically a regex that is equivalent to a literal character search.  You will notice that inside VSCODe when you `CTRL + F` there is a button that will enable the use of regex searches as shown below.
    ![regex search inside of vscode example](https://github.com/Stickkman/portfolioStickkman02/blob/main/assets/images/screenshot.jpg?raw=true)

## Author

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)
