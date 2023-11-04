#JS/TS 
Regular Expression in Javascript are a powerful tool to validate strings such as passwords, filenames etc. and/or perform find and replace operations with ease.

### Format:
```Javascript
const regex = /[a-zA-Z0-9]*/
console.log(regex.test("HelloWorld"))
```

### Syntax:
- _/   /_ = Regex open and Close (Search pattern)
- _/abc/_ = Only finds string "abc"
- _/abc|xyz/_ = | is logical or. Finds abc or 
- _/(a|b)c/_ = () Creates group/expression to be chained. Matches ac | bc
- _/a?b/_ = ? occurs 0 or 1 times. Matches ab | b
- _/a*b/_ = * is kleene closure. {b, ab, aab, aaab ....}
- _/a+b/_ = + is positive closure. {ab, aab, aaab ....}
- _/a{1,3}/_ = {MIN, MAX} number of occurences. Matches {a, aa, aaa}
- _/\w/_ = / matches character classes such as digit or word etc
- _/[A-Z]/_ = [] creates custom character set
- _/[\^ A-D]/_ = ^ negates character sets

### Functions:
- exec() : Executes search for a match
- test() : Returns boolena value of true/false for match/no-match
- match() : Returns an array of all the matches
- matchAll() : Returns iterator containing all matches
- search() : Returns index of match
- replace() : Replaces matched string
- replaceAll() : Replaces all matched strings
- split() : Uses regex as delimiter