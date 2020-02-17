# LC-3 Preprocessor
A simple script to do preprocessing on LC-3 Assembly files. It was built for use in CS2110 at Georgia Tech. It works somewhat like the C Preprocessor in that it modifies the source file before passing it off to the compiler. Thus, using this preprocessor can make code harder to debug since lines matter in assembly, but it tries to compensate by keeping comments.

## Usage
The script is written in Perl, which should be installed by default on most Linux distributions. To run it, first ensure that Perl is installed and that the first line of the script is `#!/absolute/path/to/perl`. Then, run it as any other program with the following options:
* `-i input_file.asm`: Sets a file to be the input to this program. Default is standard input.
* `-o output_file.asm`: Sets a file to be the output of this program. Default is standard output.

## Directives
These can be put in the input file to tell this preprocessor to take special action. They must be put at the start of the line with no leading whitespace, just like Assembly labels. All preprocessor directives start with a `#` and are case-insensitive.
* `#include include_file.asm`: Places the content of `include_file.asm` into the output, recursively expanding preprocessor directives
* `#constant NAME VALUE`: Defines the constant `NAME` to have the value `VALUE`. It will be replaced when encountered later in the file being passed as an argument to a command or macro
* `#macro NAME PARAMETERS`: Defines the macro `NAME` to take a comma-separated list of parameters. The lines following this one and going up to `#endmacro`  are treated as part of the macro. The syntax for usage is the same as for commands, and it will be expanded if encountered later in the file.

## TODO
* **Code Review:** Get someone else to look at this code to make sure it is sane
* **If Statements:** Adding directives for checking whether or not a constant or macro is defined would make for safer code.
* **Strict Mode:** Once if statements are added, a strict mode can be added where redefining an existing program or macro causes failure.
