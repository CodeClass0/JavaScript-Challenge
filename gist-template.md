# Regex Tutorial on Hex Code Matching

This is a tutorial to help bootcamp students get a clearer picture of Regex (AKA, Regular Expressions). Regex is a powerful tool that allows us to find patterns of characters in a string. Whether we need to find a literal word on the page, or verify that a user has entered an email, phone number, or password in a format that we require, Regex can handle it..

## Summary

In this tutorial, we will go over how you can verify that a hex code is correctly entered. 

Our expression for this tutorial is as follows:
```
/^#?([a-f0-9]{6}|[a-f0-9]{3})$/
```

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)

## Regex Components

### Anchors
Anchors are used at the beginning and end of the string. There are two anchors. The first one is ```^```, which applies the expression to the start of the string. If we said we wanted to return the literal ```/^SAMPLE/```, then we would get a match on "SAMPLE", but we would also get a hit on "SAMPLE1". 

To close the expression, we use the ```$``` anchor. Now we might use the expression ```/^SAMPLE$/```. This would stop us from getting hits on anything that doesn't end with the characters we specified. So "!SAMPLE" would not be a hit, and neither would "SAMPLE!" Only "SAMPLE" would be a match.

So in our hex code search, we open with ```/^``` and close with ```$/```, ensuring we get back matches that are most likely to be hex codes. 

### Quantifiers
Quantifiers tell us how many times a character or group can be present for a match. 

The greedy quantifiers are as follows:

```*```, which hits on 0 or more instances.

```+```, which hits on 1 or more instance.

```?```, which hits on 0 or 1 instance.

```{n}```, which matches exactly n times.

```{n,}```, which matchest at least n times.

```{n,m}```, which matches from n to m times.

Quantifiers can be greedy or lazy. Greedy quantifiers look for the longest string we can match, lazy ones look for the shortest. To denote that a qualifer is lazy, ```?``` is used on the right side of the a greedy quantifier. So ```*?```, ```+/```, ```??```, ```{n}?```, ```{n,}?```, and ```{n,m}?``` are the lazy quantifiers.

In our hex code example, we think a user might use a ```#``` at the start of the hex code, but we aren't sure. To write an expression that takes that into account, we add ```#?``` in between our starting ```/^``` and ending ```$/``` anchors. 

We also know that a hex code can be three or six characters. We don't quite know how to express that yet, but a ```{3}``` and a ```{6}``` are used to denote that.

The result so far is:

```/^#?``` to start the expression, ```{3}``` and ```{6}``` somewhere in the middle, and ```$/``` to end it.

### OR Operator
The OR statement, also known as "Alternation", is denoted by a simple ```|``` character. The OR statement will return a hit when at least one of its conditions is met. 

Because we know that a hex code can be three or six characters, we want to use an OR statement, where one part looks for a three-character match while the other looks for a six-character match.

The OR operator is how we will get a match on three or six-letter codes. 

```/^#? {3}``` goes on one side of the ``` | ``` and ```{6} $/``` goes on the back side.

Now our expression is ```/^#? {3} | {6} $/```. We still need to specify what characters can occur three or six times, but we're almost there.

### Grouping and Capturing
Grouping constructs apply differing criteria to the same string. Groups are created using ```()```. An example would be if we need a string that contains three consecutive digits and three consecutive letters, we might want to use two parts. ```(\d\d\d)``` to find the digits, and ```(\w\w\w)``` to find the letters.

To join these into what's called a subexpression, we use ```:```. So our expression would be ```(\d\d\d):(\w\w\w)```.

Grouping constructs can be capturing or non-capturing. Capturing groups capture a hit, where non-capturing groups simply check for the presence of the required criteria. To turn a standard group into a non-capturing group, a ```?``` is inserted inside the first ```(```. So our above example would be made non-capturing in the following manner: ```(?\d\d\d):(\w\w\w)```


### Bracket Expressions
Bracket expressions are used to encapsulate a range of characters. We might want a simple ```1```, ```2```, or ```3```, so we would use ```[123]``` to denote that range. If we want ```a```, ```b```, or ```c```, we would use ```[abc]```. 

For our purposes in a hex code regex, we want to find a range of letters or numbers. To do so, we would employ a hyphen, as with ```[a-f]``` and ```[0-9]```. 

Other useful ranges are:

```[a-zA-Z]```, which hits with both lower case and upper case letters.

```[_-]```, which allows for hyphens and underscores.

Finally, we can specify what characters to search for in our regex. We want all characters and all digits, three or six times, possibly with a ```#```. 

So our completed hex code regex is:
```/^#?([a-f0-9]{6}|[a-f0-9]{3})$/```


## Author

I am currently a student in a fullstack bootcamp. Contact me or view my profile at [https://github.com/CodeClass0](https://github.com/CodeClass0)