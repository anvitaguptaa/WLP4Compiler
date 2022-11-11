# WLP4Compiler

## Introduction to WLP4

WLP4 (pronounced "Wool P Four") is a subset of C++ which stands for “Waterloo, Language, Plus, Pointers, Plus, Procedures”. This language includes functions, integers, pointers, arrays, conditional statements, and while loops, and is taught within the ["Foundations of Sequential Programs"](https://www.student.cs.uwaterloo.ca/~cs241) course at the University of Waterloo.

For more information on WLP4, check out:
- [WLP4 Programming Language Tutorial](https://www.student.cs.uwaterloo.ca/~cs241/wlp4/WLP4tutorial.html)
- [WLP4 Programming Language Specification](https://www.student.cs.uwaterloo.ca/~cs241/wlp4/WLP4.html)

## WLP4 Compiler

This WLP4 Compiler implements scanning, parsing, context sensitive analysis, and code generation of WLP4 Code. The overall project consists of building a compiler which is able to translate WLP4 code into MIPS assembly language. The source code for this project is not public, feel free to email me at anvita.gupta@uwaterloo.ca to see it.

### Compiler Processes:

#### 1) Scanning
The compiler first tokenizes/scans given WLP4 code. Scanning is implemented through a <a href="https://en.wikipedia.org/wiki/Maximal_munch">Simplified Maximal Munch Algorithm</a>, which attempts to consume input until it gets "stuck", at which point it is determined whether or not the input is in an accepting state. If in an accepting state, a token will be produced. Otherwise, the input will be rejected. The algorithm scanned through the code uses an <a href="https://en.wikipedia.org/wiki/Nondeterministic_finite_automaton">NFA</a>, for which the lexical syntax used can be found <a href="https://student.cs.uwaterloo.ca/~cs241/wlp4/WLP4.html">here</a> 
<!-- A3 -->

#### 2) Parsing

Parsing is implemented using <a href="https://en.wikipedia.org/wiki/Pushdown_automaton">Pushdown Automata</a> to determine if the code can be recognized using a <a href="https://en.wikipedia.org/wiki/Context-free_grammar">Context Free Grammar (CFG)</a>. The context-free syntax of WLP4 can be found <a href="https://student.cs.uwaterloo.ca/~cs241/wlp4/WLP4.html">here</a>. The final product upon parsing a CFG generates a derivation of the input string, which uniquely defines a parse tree used to represent the structure of the program. For the purposes of this compiler, a <a href="https://en.wikipedia.org/wiki/Bottom-up_parsing">Bottom-Up Parsing</a> algorithm is used, specifically the <a href="https://en.wikipedia.org/wiki/Simple_LR_parser">SLR(1)</a> parser. 
<!-- A5 -->

#### 3) Context-Sensitive Analysis
The next step of the compiler is to determie if the code follows the context-sensitive rules of WLP4. Examples of common rules used by popular languages are:
- Not declaring multiple variables with the same name
- Not using a variable prior to its declaration

The full set of semantic/type-inference rules can be found <a href="https://student.cs.uwaterloo.ca/~cs241/wlp4/typerules.pdf">here</a>, and the full set of context-sensitive rules can be found <a href="https://student.cs.uwaterloo.ca/~cs241/wlp4/WLP4.html">here</a>. To accomplish this, the compiler parses through the parse tree generated from the last step to ensure each rule is followed.
<!-- A6 -->

#### 4) Code Generation
The final part of the compilation process is code generation, and completing the process of translating WLP4 source code to MIPS assembly language. Basic features are supported including code generation for the main procedure, integer variables and constants, declarations, assignment, arithmetic, control flow, and printing, and additional support for pointers, other procedures, and dynamic memory allocation is also implemented. 
<!-- A7/A8 -->