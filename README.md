# LC-3 Preprocessor
A simple script to do preprocessing on LC-3 Assembly files. It was built for use in CS2110 at Georgia Tech. It works somewhat like the C Preprocessor in that it modifies the source file before passing it off to the compiler. Thus, using this preprocessor can make code harder to debug since lines matter in assembly, but it tries to compensate by keeping comments.

## File Notes
Not all valid LC-3 Assembly files will work with this preprocessor. Perhaps most noteworthy is that directives and instructions must have some whitespace before them. Otherwise, the parser will simply treat them as labels.

## Usage
The script is written in Perl, which should be installed by default on most Linux distributions. To run it, first ensure that Perl is installed and that the first line of the script is `#!/absolute/path/to/perl`. Then, run it as any other program with the following options:
* `-i input_file.asm`: Sets a file to be the input to this program. Default is standard input.
* `-o output_file.asm`: Sets a file to be the output of this program. Default is standard output.
* `-l`: Switches to lazy mode from the default strict mode. Will not fail when constants and macros are redefined.

## Directives
These can be put in the input file to tell this preprocessor to take special action. They must be put at the start of the line with no leading whitespace, just like Assembly labels. All preprocessor directives start with a `#` and are case-insensitive.
* `#include include_file.asm`: Places the content of `include_file.asm` into the output, recursively expanding preprocessor directives
* `#constant NAME VALUE`: Defines the constant `NAME` to have the value `VALUE`. It will be replaced when encountered later in the file being passed as an argument to a command or macro
* `#macro NAME PARAMETERS`: Defines the macro `NAME` to take a comma-separated list of parameters. The lines following this one and going up to `#endmacro`  are treated as part of the macro. The syntax for usage is the same as for commands, and it will be expanded if encountered later in the file.
* `#if(n?)(c|m) NAME`: Checks if the symbol `NAME` is defined -- as a constant if `c` is asserted, or as a macro if `m` is. The result is inverted if the `n` is present. If the result comes out to true, preprocess the lines up to the `#endif`, otherwise ignore them.

## TODO
* **Code Review:** Get someone else to look at this code to make sure it is sane
