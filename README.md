## Description
This is an attempt to build a CPU from scratch; first in Logisim and then with ICs.
CPU.circ is the version before implementing the memory device bus, CPU_2.circ is the newer version which also implements pointer manipulation as well as conditional skip for branching.

![Screenshot of the main logisim module](https://raw.githubusercontent.com/erdlof/cpu/master/main.png)

## Instructions
Instructions consist of an 8 bit argument followed by the 8 bit command. The usage of the argument depends on the context.

### List of instructions (HEX)
| Instruction | Assembler command | Description                                                                                                                                                                                                   |
|-------------|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0x01        | accl              | Accumulator load (from memory device). The argument is the address.                                                                                                                                           |
| 0x81        | iaccl             | Accumulator load (immediate). The argument is the value to load.                                                                                                                                              |
| 0x03        | accw              | Accumulator write on bus (to address stored in memory). The argument is the address of the address.                                                                                                           |
| 0x83        | iaccw             | Accumulator write on bus (to address specified in the argument).                                                                                                                                              |
| 0x04        | add               | Arithmetic ADD (from memory device). Adds a value to the accumulator. The argument is the address of the value.                                                                                               |
| 0x84        | iadd              | Arithmetic ADD (immediate). Adds the argument to the accumulator.                                                                                                                                             |
| 0x05        | sub               | Arithmetic SUB (from memory device). Subtracts a value from the accumulator. The argument is the address of the value.                                                                                        |
| 0x85        | isub              | Arithmetic SUB (immediate). Subtracts the argument from the accumulator.                                                                                                                                      |
| 0x06        | mul               | Arithmetic MUL (from memory device). Multiplies the accumulator with a value. The argument is the address of the value.                                                                                       |
| 0x86        | imul              | Arithmetic MUL (immediate). Multiplies the accumulator with the argument.                                                                                                                                     |
| 0x07        | div               | Arithmetic DIV (from memory device). Divides the accumulator by a value. The argument is the address of the value.                                                                                            |
| 0x87        | idiv              | Arithmetic DIV (immediate). Divides the accumulator by the argument.                                                                                                                                          |
| 0x08        | ipset             | Set instruction pointer (from memory device). Sets the instruction pointer to a value. The argument is the address of the value.                                                                              |
| 0x88        | iipset            | Set instruction pointer (immediate). Sets the instruction pointer to the argument.                                                                                                                            |
| 0x09        | aipset            | Set instruction pointer (from accumulator). Sets the instruction pointer to the value stored in the accumulator. The argument is ignored.                                                                     |
| 0x0a        | and               | Logical AND (from memory device). Executes a bitwise AND operation on the accumulator. The argument is the address.                                                                                           |
| 0x8a        | iand              | Logical AND (immediate). Executes a bitwise AND operation on the accumulator. The argument is the value.                                                                                                      |
| 0x0b        | or                | Logical OR (from memory device). Executes a bitwise OR operation on the accumulator. The argument is the address.                                                                                             |
| 0x8b        | ior               | Logical OR (immediate). Executes a bitwise OR operation on the accumulator. The argument is the value.                                                                                                        |
| 0x0c        | xor               | Logical XOR (from memory device). Executes a bitwise XOR operation on the accumulator. The argument is the address.                                                                                           |
| 0x8c        | ixor              | Logical XOR (immediate). Executes a bitwise XOR operation on the accumulator. The argument is the value.                                                                                                      |
| 0x0d        | ainv              | Invert accumulator. Executes a bitwise invert operation on the accumulator. The argument is ignored.                                                                                                          |
| 0x0e        | less              | Conditional skip if ACC < VALUE (from memory device). Skips the next instruction if the value stored in the accumulator is less than the value provided by the memory device. The argument is the address.    |
| 0x8e        | iless             | Conditional skip if ACC < VALUE (immediate). Skips the next instruction if the value stored in the accumulator is less than the value provided in the argument.                                               |
| 0x0f        | eq                | Conditional skip if ACC == VALUE (from memory device). Skips the next instruction if the value stored in the accumulator is equal to the value provided by the memory device. The argument is the address.    |
| 0x8f        | ieq               | Conditional skip if ACC == VALUE (immediate). Skips the next instruction if the value stored in the accumulator is equal to the value provided in the argument.                                               |
| 0x10        | great             | Conditional skip if ACC > VALUE (from memory device). Skips the next instruction if the value stored in the accumulator is greater than the value provided by the memory device. The argument is the address. |
| 0x90        | igreat            | Conditional skip if ACC > VALUE (immediate). Skips the next instruction if the value stored in the accumulator is greater than the value provided in the argument.                                            |
