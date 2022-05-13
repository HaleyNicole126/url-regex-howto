# url-regex-howto

Link to Gist: 
https://gist.github.com/HaleyNicole126/6eae1f74609dc25e2edfaab30d725508.js

Regex Tutorial - Matching a URL
This tutorial indends to provide an explanation of a regular expression, or regex, that defines a search pattern that will match a URL. Regular expressions are useful if we want to check if a string matches a particular combination of characters, such as when validating data that someone has entered into a form. This explanation will include a breakdown of the individual components of a regular expression that matches a URL to help improve web development students' understanding of regular expressions both in this specific situation as well as how they function more broadly. The intention is to describe what each piece is doing in this regular expression as well as how we can use the components in other regular expressions.

Summary
This tutorial will focus on the regex below that matches a URL. This type of regex could be used in many situations, such as anytime we need to validate data input to make sure the user entered a valid URL. Regular expressions can also be used instead of strings in some methods that accept string arguments such as search() and replace(). Regular expressions can allow these methods to search more broadly for matches rather than strictly searching for a specific string, and this regular expression could be useful if we wanted to find all of the URLs in a dataset.

/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/

Table of Contents
Anchors
Quantifiers
OR Operator
Character Classes
Flags
Grouping and Capturing
Bracket Expressions
Greedy and Lazy Match
Boundaries
Back-references
Look-ahead and Look-behind
Regex Components
/ and / indicate the boundaries of the regular expression, so the expression is what is contained between the forward slashes. The following sections will break down the components of the regular expression that matches a URL.

Anchors
^ - The ^ anchor marks the beginning of the sequence of characters we want to match. $ - The $ anchor marks the end of the sequence of characters we want to match. The combination of the ^ and $ components will match the sequence between the anchors. In this regular expression the anchors designate the beginning and end of the search pattern that will match the URL, and they do not actually match any characters themselves they actually match the position before the first character (in the case of the ^) or the position after the last character (in the case of the $).

^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$ searches for the sequence of characters between the ^ and the $, so it is actually searching for (https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/? with ^ defining the beginning and $ defining the end.

Quantifiers
The quantifiers included in this expression are ?, +, {}, and *:

? - The ? quantifier matches a sequence of characters that has zero or one of the character or sequence before the ?. In this expression, there are three ? quantifiers. The ? that follows the s in https? searches for zero or one s, which allows this expression to match URLs that start with http or https. The ? that follows (https?:\/\/)? searches for zero or one or more of the sequence of characters contained in the parenthese immediately before the ? (which includes another ? that only affects the s), so this expression will match URLs that start with https:// or http:// as well as URLs that do not start with either. The final ? is at the end of the expression right before the $ anchor. This quantifier applies to the escaped / directly before it \/?. (Note the / needs to be escaped with a backslash() so that the expression matches the literal / rather than identifying it as the boundary of the expression.) This ? will match zero or one / at the end of the URL, so it will match URLs that end with a forward slash as well as those that do not.

+ - The + quantifier matches with one or more of whatever character or sequence precedes it. In this expression, the + quantifier [\da-z\.-]+ matches one or more of the characters contained in the brackets direclty before it. This means we need at least one character that can be any of the following: a digit between 0 and 9 (\d), a letter from a to z (a-z), a period (\.), or a hyphen (-). The brackets allow us to match any character contained in the brackets, and the + quantifier means we are looking for at least one of those characters. It will match any string containing a combination of those characters of any length as long as there is at least one character.

{2,6} - The curly braces {} provide an exact amount or a range of how many of the character or sequence that precedes it. In this expression [a-z\.]{2,6} indicates that we want at least two but not more than six of the set of characters contained in the brackets. This expression will match a string that contains at least two letters and/or periods but not more than six.

* - The asterisk * is the most flexible quantifier matching zero or more of wahtever character or sequence precedes it. In this expression ([\/\w \.-]*)* we have two asterisks. Starting with the asterisk after the brackets but inside of the parentheses, this will match a string containing any number (including zero) of forward slashes \/, alphanumeric characters\w, periods \., or hyphens -. The parentheses create a group containing any number of these characters and the asterisk outisde of the parentheses will match any number of groups containing these characters.

OR Operator
| - The | symbol is how the OR operator is specified in regex. It will either match what is directly before the symbol or directly after the |. Brackets can be used in a way similar to | and those are what are used in the regular expression used to match a URL in this tutorial.

Character Classes
The character classes included in this expression include /d and /w. \d - This represents the digit character class, which will match any digit and is essentially the same as [0-9]. In the expression to match a URL, \d is used alongside other characters inside of brackets: [\da-z\.-]. This bracket expression will match any digit with \d, letter with a-z, period with \., or hyphen-.

\w - This represents the word character class and will match any alphanumeric character as well as underscores. It is essentially a shorter version of [a-zA-Z0-9_]. In the expression to match a URL, \w is used inside of a bracket expression [\/\w \.-] which also includes and escaped forward slash \/, an escaped period \., and a hyphen -, so it will match any of these characters or any alphanumeric character or an underscore.

Flags
Flags can be used outside of the forward slashes / that mark the boundaries of the regular expression. This expression doesn't have flags, but we could specify a flag after the final forward slash. Flags include g for global, m for multi-line, or i for insensitive. The global flag g will generate a global search for matches and won't return after the first match. The multi-line flag m allows the anchors to be used to mark the end of the row instead of the beginning and end of the entire string. The insensitive flag i makes the expression case-insentive meaning it doesn't matter if the letters are uppercase or lowercase when normally case does matter in regular expressions.

Grouping and Capturing
() Parenthese allow us to group expressions, which is helpful as the search patterns become more complex. Using () as grouping constructs allow us to specify a portion of the string we want to match as well as to use quantifiers like those described previously. In the example matching the URL, there are several sections of the expression that are bound by parentheses. For instance (https?:\/\/)? is an expression that is grouped by parentheses and followed by a quantifier to indicate that it is looking to match zero or one instances of the expression inside of the parentheses as described in the section on quantifiers.

Bracket Expressions
[] - Bracket expressions allow us to specify character sets and work similar to the OR operator. A bracket expression will match any of the characters contained inside of the brackets. In the URL example, the bracket expressions include [\da-z\.-], [a-z\.], [\/\w \.-], and are all followed by quantifiers that indicate how many matches the expression is looking for. The expressions containing the character classes \d and \w are described in the section on character classes. The second bracket expression [a-z\.] will match any lowercase letter or period, and since it is followed by a quantifier in curly braces {2,6}, the expression is looking to match at least two but not more than six of the characters specified inside of the bracket expression.

Greedy and Lazy Match
Greedy and lazy match are related to quantifiers. A lazy quantifier will try to match an element the minimum number of times whereas a greedy quantifier will try to match an element as many times as possible. The lazy mode is specified by putting a ? after the quantifier, so + is greedy whereas +? is lazy and ? is greedy while ?? is lazy. Greedy matches will match the longest possible string whereas lazy matches will match the shortest possible string. In our example, all of the quantifiers are greedy not lazy, but we could add a ? after any of the quantifers to make them lazy.

Boundaries
Bondaries like \b work similar to the anchors ^ and $ but it allows us to match whole words. The URL expression example does not contain boundaries, but if we wanted to target a specific string of characters, we could use word boundaries.

Back-references
Back-references are used to match the same capturing group again. This example expression does not contain back-refrences, but if we wanted to match one of the expressions contained inside of parentheses again, we could use a back-refrence. For instance, if we wanted to match a group of characters we already defined in a capturing group again, we could reference the capturing group using \1, \2, \3, and \4 for the first, second, third, and fourth capturing groups respectively.

Look-ahead and Look-behind
Look-ahead ?= and look-behind ?<= will look to find patterns and assert whether the pattern is present next to the lookaround, as they are collectivley called. This example expression does not contain any lookarounds, but if we wanted to see whether a pattern satisfies certain conditions, we could use a look-ahead or look-behind. This would be useful if wanted to match something but only if it was valid, which we could check with a lookaround.

Author
Haley Schwenk is taking a full-stack development bootcamp through the University of Utah.

https://github.com/HaleyNicole126
