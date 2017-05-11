# EX01: Lex
The program Lex generates a so called _Lexer_. This is a function that takes a stream of characters as its input, and whenever it sees a group of characters that match a key, takes a certain action. A very simple example:
```
%{
#include <stdio.h>
%}

%%
stop    printf("Stop command received\n");
start   printf("Start command received\n");
%%
```
The first section, in between the **%{** and **%}** pair is included directly in the output program. We need this, because we use **printf** later on, which is defined in **stdio.h**.

Sections are separated using **%%**, so the first line of the second section starts with the _stop_ key. Whenever the _stop_ key is encountered in the input, the rest of the line (a printf() call) is executed.

Besides _stop_, we've also defined _start_, which otherwise does mostly the same.

We terminate the code section with **%%** again.

To compile Example 1, do this:
```
lex ex01.l
cc lex.yy.c -o ex01 -ll
```

# NOTE
If you are using flex, instead of lex, you may have to change **-ll** to **-lfl** in the compilation scripts. RedHat 6.x and SuSE need this, even when you invoke _flex_ as _lex_!

This will generate the file _ex01_. If you run it, it waits for you to type some input. Whenever you type something that is not matched by any of the defined keys (ie, _stop_ and _start_) it's output again. If you enter _stop_ it will output _'Stop command received'_;

Terminate with a **EOF** (^D).

You may wonder how the program runs, as we didn't define a main() function. This function is defined for you in libl (liblex) which we compiled in with the -ll command.

# RESOURCES
[http://www.tldp.org/HOWTO/Lex-YACC-HOWTO-3.html](http://www.tldp.org/HOWTO/Lex-YACC-HOWTO-3.html)