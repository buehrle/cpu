## Description
This is an attempt to build a CPU from scratch; first in Logisim and then with ICs.
CPU.circ is the version before implementing the memory device bus, CPU_2.circ is the newer version which also implements pointer manipulation as well as conditional skip for branching.

![Screenshot of the main logisim module](https://raw.githubusercontent.com/erdlof/cpu/master/main.png)

## Instructions
Instructions consist of an 8 bit argument followed by the 8 bit command. The usage of the argument depends on the context.
For example, the instruction to load the value 0x34 into the accumulator is 0x3481.

### List of instructions (HEX)
| Base | HEX  | Assembly | Short name                   | Additional information            | Usage example | Ticks |
|------|------|----------|------------------------------|-----------------------------------|---------------|-------|
| 0x08 | 0x08 | cload0   | Cache 0 load                 | From memory address               | cload0 r0     | 4     |
|      | 0x09 | cload1   | Cache 1 load                 |                                   | cload1 r0     | 4     |
|      | 0x88 | icload0  | Cache 0 load                 | Immediate                         | icload0 d0    | 3     |
|      | 0x89 | icload1  | Cache 1 load                 |                                   | icload1 d0    | 3     |
| 0x10 | 0x10 | add      | Add to memory                | Cache 0 + Cache 1                 | add r0        | 4     |
|      | 0x11 | sub      | Sub to memory                |                                   | sub r0        | 4     |
|      | 0x12 | mul      | Mul to memory                |                                   | mul r0        | 4     |
|      | 0x13 | div      | Div to memory                |                                   | div r0        | 4     |
|      | 0x14 | and      | Bitwise And to memory        | Cache 0 AND Cache 1               | and r0        | 4     |
|      | 0x15 | or       | Bitwise Or to memory         |                                   | or r0         | 4     |
|      | 0x16 | xor      | Bitwise Xor to memory        |                                   | xor r0        | 4     |
|      | 0x17 | inv      | Invert cache 0 to memory     | NOT cache 0                       | inv r0        | 4     |
|      | 0x90 | addc     | Add to cache 0               | Replaces existing data in cache 0 | addc          | 3     |
|      | 0x91 | subc     | Sub to cache 0               |                                   | subc          | 3     |
|      | 0x92 | mulc     | Mul to cache 0               |                                   | mulc          | 3     |
|      | 0x93 | divc     | Div to cache 0               |                                   | divc          | 3     |
|      | 0x94 | andc     | Bitwise And to cache 0       |                                   | andc          | 3     |
|      | 0x95 | orc      | Bitwise Or to cache 0        |                                   | orc           | 3     |
|      | 0x96 | xorc     | Bitwise Xor to cache 0       |                                   | xorc          | 3     |
|      | 0x97 | invc     | Invert cache 0 to cache 0    |                                   | invc          | 3     |
| 0x18 | 0x18 | mov      | Copy data                    | Register to register              | mov r0, r1    | 7     |
|      | 0x98 | imov     | Copy data                    | Immediate                         | imov d0, r0   | 6     |
| 0x20 | 0x20 | false    | Skip if (false)              | Never skips                       |               | 2     |
|      | 0x21 | gr       | Skip if (cache 0 > cache 1)  | Signed. Skips two instructions    | gr            | 3/2   |
|      | 0x22 | eq       | Skip if (cache 0 == cache 1) |                                   | eq            | 3/2   |
|      | 0x23 | ge       | Skip if (cache 0 >= cache 1) |                                   | ge            | 3/2   |
|      | 0x24 | le       | Skip if (cache 0 < cache 1)  |                                   | le            | 3/2   |
|      | 0x25 | ne       | Skip if (cache 0 != cache 1) |                                   | ne            | 3/2   |
|      | 0x26 | leq      | Skip if (cache 0 <= cache 1) |                                   | leq           | 3/2   |
|      | 0x27 | true     | Skip if (true)               | Always skips                      |               | 3     |
|      | 0xa0 | false    |                              |                                   |               | 2     |
|      | 0xa1 | ugr      |                              | Unsigned                          | ugr           | 3/2   |
|      | 0xa2 | ueq      |                              |                                   | ueq           | 3/2   |
|      | 0xa3 | uge      |                              |                                   | uge           | 3/2   |
|      | 0xa4 | ule      |                              |                                   | ule           | 3/2   |
|      | 0xa5 | une      |                              |                                   | une           | 3/2   |
|      | 0xa6 | uleq     |                              |                                   | uleq          | 3/2   |
|      | 0xa7 | true     |                              |                                   |               | 3     |
| 0x28 | 0x28 | jmp      | Jump                         | Address saved in register         | jmp r0        | 4     |
|      | 0xa8 | ijmp     |                              | Immediate                         | ijmp d0        | 4     |
| 0x00 | 0x00 | drp      | Do nothing                   | Does nothing                      |               | 2     |
