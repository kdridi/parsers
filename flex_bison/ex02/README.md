# EX02: Regular expressions in matches
This example wasn't very useful in itself, and our next one won't be either. It will however show how to use regular expressions in Lex, which are massively useful later on.

Example 2:
```
%{
#include <stdio.h>
%}

%%
[0123456789]+           printf("NUMBER\n");
[a-zA-Z][a-zA-Z0-9]*    printf("WORD\n");
%%
```

This Lex file describes two kinds of matches (tokens): WORDs and NUMBERs. Regular expressions can be pretty daunting but with only a little work it is easy to understand them. 

Let's examine the NUMBER match: **[0123456789]+**

This says: a sequence of one or more characters from the group 0123456789. We could also have written it shorter as: **[0-9]+**

Now, the WORD match is somewhat more involved: **[a-zA-Z][a-zA-Z0-9]***

The first part matches 1 and only 1 character that is between 'a' and 'z', or between 'A' and 'Z'. In other words, a letter. This initial letter then needs to be followed by zero or more characters which are either a letter or a digit. Why use an asterisk here? The '+' signifies 1 or more matches, but a WORD might very well consist of only one character, which we've already matched. So the second part may have zero matches, so we write a '*'.

This way, we've mimicked the behavior of many programming languages which demand that a variable name **must** start with a letter, but can contain digits afterwards. In other words, 'temperature1' is a valid name, but '1temperature' is not.

Try compiling Example 2, lust like Example 1, and feed it some text. Here is a sample session:

 $ ./example2
foo
WORD

bar
WORD

123
NUMBER

bar123
WORD

123bar
NUMBER
WORD

You may also be wondering where all this whitespace is coming from in the output. The reason is simple: it was in the input, and we don't match on it anywhere, so it gets output again.

The Flex manpage documents its regular expressions in detail. Many people feel that the perl regular expression manpage (perlre) is also very useful, although Flex does not implement everything perl does.

Make sure that you do not create zero length matches like '[0-9]*' - your lexer might get confused and start matching empty strings repeatedly.

# RESOURCES
[http://www.tldp.org/HOWTO/Lex-YACC-HOWTO-3.html](http://www.tldp.org/HOWTO/Lex-YACC-HOWTO-3.html)