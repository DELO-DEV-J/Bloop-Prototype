# Godel's Bloop Language Compiler

## Overview
This repository contains an implementation of a compiler for a pseudo-language inspired by Gödel's "Bloop" (a simplified programming language). The main purpose of this project is to parse a custom input format, generate corresponding tokens, and compile the tokens into a basic C-like language that can be saved into a `.c` file and run using a C compiler.

## Features
- **Custom language parsing** with support for procedures, conditionals, loops, and statements.
- **Token-based compilation** that translates high-level pseudo-code into C-style code.
- **Basic error handling** for unmatched blocks and unsupported tokens.
- **Outputs a runnable C file.**

## Project Structure
```
.
├── Compile.java      # Contains the logic for converting tokens into C-style code.
├── Main.java         # The entry point for the program, handles file input and triggers parsing and compilation.
├── Parser.java       # Handles the parsing of input source code into tokens.
├── Token.java        # Represents individual tokens within the parsed code.
├── README.TXT        # Contains basic project documentation (this file can be extended).
└── package.bluej     # Metadata for the BlueJ Java IDE.
```

### Class Descriptions
- **Compile.java:** Defines the `Compile` class, responsible for translating a sequence of tokens into C-like code. It iterates over tokens, identifies their type, and appends the corresponding code while managing block depth and closures.
- **Main.java:** Contains the entry point for the program. It reads input from a file, converts it to tokens using the `Parser` class, and compiles it into C-like code.
- **Parser.java:** Converts raw text input into tokens. It recognizes constructs like procedures, conditionals, loops, and statements and converts them into instances of the `Token` class.
- **Token.java:** Represents a single token, encapsulating its type, name, and parameters. Provides constructors and methods for efficient token manipulation.

## Getting Started
1. **Setup:** Clone the repository and open it in your preferred Java IDE (e.g., BlueJ or IntelliJ).
2. **Build and Run:** Execute the `Main` class to start the compiler. It will prompt for an input file containing pseudo-code in the custom language.
3. **Input Example:** You can provide code in a format similar to:
   ```
   DEFINE PROCEDURE "MINUS" [M, N]:
   BLOCK 0: BEGIN
       IF M < N THEN:
           QUIT BLOCK 0;
       CELL(0) ⇐ 0;
       LOOP AT MOST M + 1 TIMES:
           IF N + CELL(0) = M THEN:
               ABORT LOOP;
           CELL(0) ⇐ CELL(0) + 1;
   OUTPUT ⇐ CELL(0);
   BLOCK 0: END
   ```

4. **Compile Output:** After running the program, it will generate a C-like code output, saved into a `.c` file.

## Example Compilation Output
The generated C-like code will look similar to:
```c
void MINUS(int M, int N) {
    if (M < N) {
        return;
    }
    CELL(0) = 0;
    for (int i = 0; i < M + 1; i++) {
        if (N + CELL(0) == M) {
            break;
        }
        CELL(0) += 1;
    }
    printf("%d\n", CELL(0));
}
```

## Compiling and Running the C Code
1. **Save the generated code:** Save the output into a file named, for example, `output.c`.
2. **Compile using a C compiler:** Run the command below to compile the C code:
   ```
   gcc -o output output.c
   ```
3. **Run the compiled code:** Execute the generated output file:
   ```
   ./output
   ```

## Known Issues
- Nested blocks with unmatched `BEGIN` and `END` may not be handled gracefully.
- Limited support for complex expressions or conditions.
- Error messages are logged to the console and may need improvement.

## Future Improvements
- Enhanced error handling and logging.
- Support for additional language features and syntax.
- Optimization of generated code.
