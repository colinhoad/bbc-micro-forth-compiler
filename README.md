# FROTH - a BBC BASIC FORTH compiler

This is a manual rekeying of **Jeremy Ruston's** [FORTH](https://en.wikipedia.org/wiki/Forth_(programming_language)) compiler in his book [The BBC Micro Compendium](https://archive.org/details/BBCMicroCompendium/mode/2up) published in 1983.

The original copyright to the book and original code is Copyright (c) Jeremy Ruston, December 1983.

I have made several corrections to the original listing, which can be referenced in the [correction](https://github.com/colinhoad/bbc-micro-forth-compiler/blob/main/listing-correction.png) file.

## Instructions

The **.BAS** file contains a plain text version of the type-in listing for FROTH, inclusive of corrections to ensure it runs. 

The **.BBC** file contains a tokenised version of the listing, but note that due to the use of inline assembler it will not run under BBC BASIC For Windows or SDL.

The **.SSD** file is a disk image that can be run under emulation by issuing the command 
`CHAIN "FROTH"`

On loading the compiler, you will be taken directly to a FORTH-style command prompt (represented as an arrow in MODE 7). 

You can test FROTH is working by running the following: `2 2 + PRINT CR` which should give a result of 4.

Entering the command `VOCAB` will list all of the known commands available to FROTH (similar to VLIST in FORTH itself).

## The FROTH threaded language

*Below is the introduction to FROTH provided by Jeremy Ruston, starting on page 88 of the book.*

The language I have chosen to compile in this section is a little like FORTH. FORTH is not quite as useful for general programming as BBC BASIC, but it is extraordinarily easy to compile. The version here is not quite similar enough to FORTH to be called FORTH, so I've taken the liberty of calling it FROTH.

The first thing to bear in mind about any language is that it is based upon a number of standard routines for carrying out tasks such as addition, multiplication, subtraction, division and so on. Before you write a language, it is a good idea to have decided upon the arithmetic routines you are going to use and to have coded these routines. Doing this helps to separate the tasks of writing the compiler, and allows you to spend time ensuring that the routines are as fast as possible.

The routines I would recommend are addition, subtraction, multiplication, division, the modulus operation, the indirection operators, greater than, less than, equal to, not equal to, greater than or equal to, less than or equal to and possibly the Boolean operators AND, OR, NOT and EOR.

Any serious language should have variables that are at least 16 bits wide, which allows it to have a numeric range of either 0 to 65535, or -32768 to 32767 (if two's complement notation is used) which is sometimes more useful for general programming.

Once all the routines have been written, you can start work on the language.

FROTH is based around a stack of 16 bit numbers, like most FORTH implementations. You interact with FROTH by typing one or more words on the keyboard, terminated by pressing carriage return, and separated by spaces. A word can then be made up of any characters except spaces and carriage returns. For convenience, control characters cannot be used either.

The words you type in fall into two categories. If a word is made up of just digits (including a leading plus or minus sign), then the word is converted to a binary number and pushed onto the stack. If it is not a number, the computer searches through a list of known words, and executes any word which matches that typed in. If no match is found, the computer reports an error.

Some examples of these words are '+', '\*' and 'PRINT'. '+' pulls two numbers off the stack, adds them together and pushes the answers on the stack, '\*' does the same for multiplication and 'PRINT' simply pulls and prints the number on top of the stack.

This simple language description allows the creation of RPN expressions using the other arithmetic words, combined with other words which allow you to define more words, carry out loops and so on.

Here is the listing of FROTH. There are some examples of it in operation following the listing, which will give an idea of how the language works.
