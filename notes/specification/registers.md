# Registers

[[toc]]

CHIP-8 has 16 8-bit data registers named V0 to VF. The VF register doubles as a flag for some instructions; thus, it should be avoided. In an addition operation, VF is the carry flag, while in subtraction, it is the "no borrow" flag. In the draw instruction VF is set upon pixel collision.

The address register, which is named I, is 12 bits wide and is used with several opcodes that involve memory operations.

## Design

### Requirements

- [ ] Register struct w/ all 16 data registers & the address register.
