# Opcodes

[[toc]]

CHIP-8 has 35 opcodes, which are all two bytes long and stored big-endian. The opcodes are listed below, in hexadecimal and with the following symbols:

- NNN: Address.
- NN: 8-bit constant.
- N: 4-bit constant.
- X & Y: 4-bit register identifier.
- PC: Program counter.
- I: 12-bit register.
- VN: One of the 16 available variables. N may be 0 - F.

 Opcode | Type    | C Pseudocode           | Explanation 
 ------ | ------- | ---------------------- | ----------- 
  0NNN  | Call    |                        | Calls machine code routine at address NNN.
  00E0  | Display | `disp\_clear()`        | Clears the screen.
  00EE  | Flow    | `return;`              | Returns from a subroutine.
  1NNN  | Flow    | `goto NNN;`            | Jumps to address NNN.
  2NNN  | Flow    | `*(0xNNN)()`           | Calls subroutine at NNN.
  3XNN  | Flow    | `if (Vx == NN)`        | Skips the next instruction if VX equals NN (Usually the next instruction is a jump to skip a code block).
  4XNN  | Cond.   | `if (Vx != NN)`        | Skips the next instruction if VX does not equal NN (usually the next instruction is a jump to skip a code block).
  5XY0  | Cond.   | `if (Vx == Vy)`        | Skips the next instruction if VX equals VY (usually the next instruction is a jump to skip a code block).
  6XNN  | Const   | `VX = NN`              | Sets VX to NN.
  7XNN  | Const   | `VX += NN`             | Adds NN to VX (carry flag is not changed).
  8XY0  | Assign  | `VX = VY`              | Sets VX to the value of VY.
  8XY1  | Bit Op. | `VX \|= VY`            | Sets VX to (VX OR VY) (bitwise OR operation).
  8XY2  | Bit Op. | `VX &= VY`             | Sets VX to (VX AND VY) (bitwise AND operation).
  8XY3  | Bit Op. | `VX ^= VY`             | Sets VX to (VX XOR VY) (bitwise XOR operation).
  8XY4  | Math    | `VX += VY`             | Adds VY to VX. VF is set to 1 when there's an overflow, 0 when there is not.
  8XY5  | Math    | `VX -= VY`             | Subtracts VY from VX. VF is set to 0 when there's an underflow, 1 when there is not.
  8XY6  | Bit Op. | `VX >>= 1`             | Shifts VX to the right by 1, then stores the least significat bit of VX prior to the shift into VF.
  8XY7  | Math    | `VX = VY - VX`         | Sets VX to VY minus VX. VF is set to 0 when there's an underflow, 1 when there is not.
  8XYE  | Bit Op. | `VX <<= 1`             | Shifts VX to the left by 1, then sets VF to 1 to the most significant bit of VX prior to the shift into VF.
  9XY0  | Cond.   | `if (VX != VY)`        | Skips the next instruction if VX does not equal VY. (Usually the next instruction is a jump to skip a code block).
  ANNN  | Memory  | `I = NNN`              | Sets I to the address NNN.
  BNNN  | Flow    | `PC = V0 + NNN`        | Jumps to the address NNN plus V0.
  CXNN  | Random  | `VX = rand() & NN`     | Sets VX to the result of a bitwise and operation of a random number (Typically: 0 to 255) and NN.
  DXYN  | Display | `draw(VX, VY, N)`      | Draws a sprite at coordinate (VX, VY) that has a width of 8 pixels and a height of N pixels. Each row of 8 pixels is read as bit-coded starting from memory location I; I value does not change after the execution of this instruction. As described above, VF is set to 1 if any screen pixels are flipped from set to unset when the sprite is drawn, and to 0 if that does not happen.
  EX9E  | Key Op. | `if (key() == VX)`     | Skips the next instruction if the key stored in VX(only consider the lowest nibble) is pressed (usually the next instruction is a jump to skip a code block).
  EXA1  | Key Op. | `if (key() != VX)`     | Skips the next instruction if the key stored in VX(only consider the lowest nibble) is not pressed (usually the next instruction is a jump to skip a code block).
  FX07  | Timer   | `VX = get\_delay()`    | Sets VX to the value of the delay timer.
  FX0A  | Key Op. | `VX = get\_key()`      | A key press is awaited, and then stored in VX (blocking operation, all instruction halted until next key event, delay and sound timers should continue processing).
  FX15  | Timer   | `delay\_timer(VX)`     | Sets the delay timer to VX.
  FX18  | Sound   | `sound\_timer(VX)`     | Sets the sound timer to VX.
  FX1E  | Memory  | `I += VX`              | Adds VX to I. VF is not affected.
  FX29  | Memory  | `I = sprite\_addr[VX]` | Sets I to the location of the sprite for the character in VX(only consider the lowest nibble). Characters 0-F (in hexadecimal) are represented by a 4x5 font.
  FX33  | BCD     | `set_BCD(VX); *(I+0) = BCD(3); *(I+1) = BCD(2); *(I+2) = BCD(1);` | Stores the binary-coded decimal representation of VX, with the hundreds digit in memory at location in I, the tens digit at location I+1, and the ones digit at location I+2.
  FX55  | Memory  | `reg\_dump(VX, &I)`    | Stores from V0 to VX (including VX) in memory, starting at address I. The offset from I is increased by 1 for each value written, but I itself is left unmodified.
  FX65  | Memory  | `reg\_load(VX, &I)`    | Fills from V0 to VX (including VX) with values from memory, starting at address I. The offset from I is increased by 1 for each value read, but I itself is left unmodified.
