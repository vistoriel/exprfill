# exprfill

A command-line utility that solves mathematical equations with wildcard placeholders (`?`). It generates all valid combinations of digits and operations that satisfy the given equation.

`exprfill` takes a mathematical expression with unknown values and systematically finds all solutions. Each `?` represents a single digit (0-9) or operation sign that needs to be filled in, making this tool useful for solving number puzzles and verifying arithmetic relationships.

## Features

### Single Unknown Placeholder
Find what digit completes the equation:
```bash
$ ./ucd "2" "+" "?" "4"
2 + 2 = 4
```

### Multiple Unknowns in Operands
Discover multi-digit numbers with wildcards:
```bash
$ ./ucd "2" "+" "2?" "??"
2 + 20 = 22
2 + 21 = 23
2 + 22 = 24
2 + 23 = 25
2 + 24 = 26
2 + 25 = 27
2 + 26 = 28
2 + 27 = 29
2 + 28 = 30
2 + 29 = 31
```

### Unknown Operations
Let the program figure out which operation works:
```bash
$ ./ucd "101" "?" "?" "??"
101 - 2 = 99
101 - 3 = 98
101 - 4 = 97
101 - 5 = 96
101 - 6 = 95
101 - 7 = 94
101 - 8 = 93
101 - 9 = 92
101 * 0 = 0
101 / 2 = 50
101 / 3 = 33
101 / 4 = 25
101 / 5 = 20
101 / 6 = 16
101 / 7 = 14
101 / 8 = 12
101 / 9 = 11
```

## Usage

```bash
./ucd [operand1] [operation] [operand2] [result]
```

### Parameters

| Parameter | Description |
|-----------|-------------|
| `operand1` | First number (may contain `?` for unknown digits) |
| `operation` | Operator: `+`, `-`, `*`, `/`, or `?` for any operation |
| `operand2` | Second number (may contain `?` for unknown digits) |
| `result` | Expected result (may contain `?` for unknown digits) |

### Supported Operations

- **Addition** (`+`)
- **Subtraction** (`-`)
- **Multiplication** (`*`)
- **Division** (`/`) – integer division, excludes division by zero

### Examples

Find missing digits in the second operand:
```bash
$ ./ucd "10" "-" "?" "5"
10 - 5 = 5
```

Discover valid operations for given operands and result:
```bash
$ ./ucd "5" "?" "3" "8"
5 + 3 = 8
```

## Building

Compile the project with:
```bash
make
```

This generates the `ucd` executable.

## Technical Details

### Supported Number Format
- Positive and negative integers
- Wildcards can appear at any position in operands and result
- Each `?` expands to all possible digits (0-9)

### Calculation Strategy
The program generates all valid combinations by:
1. Creating arrays of all possible values for each component with wildcards
2. Testing all combinations against the mathematical relationship
3. Printing only the combinations that satisfy the equation
