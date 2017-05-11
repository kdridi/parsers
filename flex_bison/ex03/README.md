# EX03: A more complicated example for a C like syntax
Let's say we want to parse a file that looks like this:
```
logging {
  category lame-servers { null; };
  category cname { null; };
};

zone "." {
  type hint;
  file "/etc/bind/db.root";
};
```

We clearly see a number of categories (tokens) in this file:
* WORDs, like 'zone' and 'type'
* FILENAMEs, like '_etc_bind/db.root'
* QUOTEs, like those surrounding the filename
* OBRACEs, {
* EBRACEs, }
* SEMICOLONs, ;

The corresponding Lex file is Example 3:
```
%{
#include <stdio.h>
%}

%%
[a-zA-Z][a-zA-Z0-9]*    printf("WORD ");
[a-zA-Z0-9\/.-]+        printf("FILENAME ");
\"                      printf("QUOTE ");
\{                      printf("OBRACE ");
\}                      printf("EBRACE ");
;                       printf("SEMICOLON ");
\n                      printf("\n");
[ \t]+                  /* ignore whitespace */;
%%
```

When we feed our file to the program this Lex file generates (using example3.compile), we get:

```
WORD OBRACE
WORD FILENAME OBRACE WORD SEMICOLON EBRACE SEMICOLON
WORD WORD OBRACE WORD SEMICOLON EBRACE SEMICOLON
EBRACE SEMICOLON

WORD QUOTE FILENAME QUOTE OBRACE
WORD WORD SEMICOLON
WORD QUOTE FILENAME QUOTE SEMICOLON
EBRACE SEMICOLON
```

When compared with the configuration file mentioned above, it is clear that we have neatly 'Tokenized' it. Each part of the configuration file has been matched, and converted into a token.

And this is exactly what we need to put YACC to good use.

# RESOURCES
[http://www.tldp.org/HOWTO/Lex-YACC-HOWTO-3.html](http://www.tldp.org/HOWTO/Lex-YACC-HOWTO-3.html)