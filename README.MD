# Rubik's Programming Language

> Programming language based on Rubik's cubes that operates on a 2D plane with 3D storage. Currently based on a 2x2

# RPL Opcodes
> These are 3 character control codes that let you do things

## Stack Functions

 | OPCODE | Definition                     | Usage           | Implemented |
 | ------ | ------------------------------ | --------------- | ----------- |
 | PUS    | Push defined value to stack    | `PUS 000000000` | Cube.PUS()  |
 | POP    | Pop top value from stack       | `POP`           | Cube.POP()  |
 | POF    | Pop top value, move forward    | `POF`           | No          |
 | POB    | Pop top value, move backward   | `POB`           | No          |
 | POL    | Pop top value, move left       | `POL`           | No          |
 | POR    | Pop top value, move right      | `POR`           | No          |

## Print Functions

 | OPCODE | Definition                           | Usage | Implemented |
 | ------ | ------------------------------------ | ----- | ----------- |
 | PRN    | Print top value of stack as ASCII    | `PRN` | No          |
 | PRB    | Print top value of stack as Binary   | `PRB` | No          |
 | PRD    | Print top value of stack as Decimal  | `PRD` | No          |

## General Functions

 | OPCODE | Definition                                      | Usage         | Implemented |
 | ------ | ----------------------------------------------- | ------------- | ----------- |
 | EXT    | Immediately exit the program                    | `EXT`         | No          |
 | CID    | Check if there's a value on top of the stack    | `CID`         | No          |
 | JUT    | Jump to defined line if false, continue if true | `JUT 000 CID` | No          |
 | RET    | Return to last JUT                              | `RET`         | No          |

## Math

 | OPCODE | Definition                             | Usage                                      | Implemented             |
 | ------ | -------------------------------------- | ------------------------------------------ | ----------------------- |
 | ADD    | Add first number by second number, push result to top of stack      | `ADD 000 101` | Interpreter.parseLine() |
 | SUB    | Subtract first number by second number, push result to top of stack | `SUB 000 101` | Interpreter.parseLine() |
 | MUL    | Multiply first number by second number, push result to top of stack | `MUL 000 101` | Interpreter.parseLine() |
 | DIV    | Divide first number by second number, push result to top of stack   | `DIV 000 101` | Interpreter.parseLine() |
 | NEG    | Perform a binary negate on top value, push result to top of stack   | `NEG 010`     | No                      |

## Pointer

  | OPCODE | Definition                | Usage | Implemented |
  | ------ | ------------------------- | ----- | ----------- |
  | OPF    | Move the pointer forward  | `OPF` | No          |
  | OPB    | Move the pointer backward | `OPB` | No          |
  | OPL    | Move the pointer left     | `OPL` | No          |
  | OPR    | Move the pointer right    | `OPR` | No          |

## Rubik's Notation

  | OPCODE | Definition                      | Usage    | Implemented |
  | ------ | ------------------------------- | -------- | ----------- |
  | MOV L  | Move left face clockwise        | `MOV L`  | No          |
  | MOV R  | Move right face clockwise       | `MOV R`  | No          |
  | MOV F  | Move front face clockwise       | `MOV F`  | No          |
  | MOV B  | Move back face clockwise        | `MOV B`  | No          |
  | MOV T  | Move top face clockwise         | `MOV T`  | Cube.MOV()  |
  | MOV D  | Move bottom face clockwise      | `MOV D`  | No          |
  |        |                                 |          |             |
  | MOV LN | Move left face counterclockwise | `MOV LN` | No          |
  | MOV RN | Move left face counterclockwise | `MOV RN` | No          |
  | MOV FN | Move left face counterclockwise | `MOV FN` | No          |
  | MOV BN | Move left face counterclockwise | `MOV BN` | No          |
  | MOV TN | Move left face counterclockwise | `MOV TN` | Cube.MOV()  |
  | MOV DN | Move left face counterclockwise | `MOV DN` | No          |

# Interpreter / Language Rules

[line number] [operator] [operator arguments]

 - Each line to be executed needs a line number
 - Any line without a line number is interpreted as a comment
 - All data values are represented as 9 character long binary strings with the first number reserved as negate
 - All line redirects are 3 digit long integers
 - Each cell contains a stack, each stack can contain 64 values
 - The working face is composed of 4 cells labeled 000, 001, 010, 011 in left > right, top > down order. Make the first digit a 1 to call the negate of the stored value
 - The cube has to be in a solved state for the code to execute

# Examples

## Math
The four cells are represented by binary numbers 0-3 in a three digit binary number. The first digit is reserved as a negate, 0 for the value as is or 1 to negate the value.

 - ADD 010 100 (this will add cell 1 to the negative of cell 0)
 - SUB 010 100 (this will subtract the negative of cell 0 by cell 1)
 - MUL 010 100 (this will multiply cell 1 by the negative of cell 0)
 - DIV 010 100 (this will divide the negative of cell 0 by cell 1)

# Code Examples

## Hello World
```
VER 1.0
001 PUS 001000100 // D
002 PUS 001001100 // L
003 PUS 001010010 // R
004 PUS 001001111 // O
005 PUS 001010111 // W
006 PUS 000100000 // Space
007 PUS 001001111 // O
008 PUS 001001100 // L
009 PUS 001001100 // L
010 PUS 001000110 // E
011 PUS 001010000 // H

This function checks if theres data on the current stack,
prints the top value as ascii if there is any and skips
the loop if the stack is empty. Easy way to print prestored
words

012 JUT 015 CID
013 PRN
014 RET
EXT
```
