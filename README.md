# HAL2+HTK2 = HAUL2
HAUL2, like HAUL1, consists of the language *HAL2* (HotKey's Average Language 2) and *HTKs* (HAL2 Translation Kernels). Except this time it actually uses some concept of "tokens" for the translation. The language *HAL2* now looks less like assembly and is actually quite clean and readable.

HAUL2 can translate itself into other languages and package everything up into one stand-alone file. So you can have a .py file that turns into a .js file when running it. This chain can go on and on and on...

Though this is already really entertaining, the choices of destination languages is still pretty limited by the fact that there is no real AST. That means, that it can only translate into other scripting languages that are somewhat similar in style.

But, all in all, this is a funny little toy!

Have fun and don't break things!

//HotKey

## Versions
This second version was in development between early 2012 and 2013. It is based on the ugly PHP based first version [HAUL1](https://github.com/hotkeymuc/haul1) which was more like a proof-of-concept.

It has been superseded by [HAUL3](https://github.com/hotkeymuc/haul3) which comes with a more powerful lexer and parser that knows namespaces and has a real AST.


## Features and Limitations
* Lexer+Tokenizer+Translator in one piece
* Idea: Let the language itself be a perfect AST representation, even if it makes the source look strange
* Still, first word of every line is the command, which makes it very easy to parse
* Parsing on-the-fly in one pass (Read byte -> Tokenizer -> Translator). The implementation simply instructs the translator to output something, which leads to a request-bubble to the tokenizer to get another token, which calls the lexer (stream reader) to grab a byte
* + Needs just very little memory (ideally). It skips back and forth in the input stream if needed
* + Funny looking language (looks like php), allows variable types, expressions, comments, arbitrary formatting and all that goodness. Robust, since the language structure has almost no exceptions
* + It needs no explicit AST data structure, since it parses AND outputs in (ideally) one pass
* = 400 lines (13kb) per output kernel
* - Needs boot strapper
* - The output modules need to be able to parse data on-the-fly -- or else they end up implementing their own local AST-like implementations...
* - Depending on the source code structure, some sort of AST might still emerge somewhere in memory/stack in order to re-order code fragments

## Usage
* Write your code in *HAL2*
* Use `bootstrap.py` to translate and bundle it up into one self-contained file