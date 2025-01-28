# Memory

[[toc]]

CHIP-8 was most commonly implemented on 4K systems, such as the Cosmac VIP and the Telmac 1800. These machines had 4096 (0x1000) memory locations, all of which are 8 bits (a byte) which is where the term CHIP-8 originated. However, the CHIP-8 interpreter itself occupies the first 512 bytes of the memory space on these machines. For this reason, most programs written for the original system begin at memory location 512 (0x200) and do not access any of the memory below the location 512 (0x200). The uppermost 256 bytes (0xF00-0xFFF) are reserved for display refresh, and the 96 bytes below that (0xEA0-0xEFF) were reserved for the call stack, internal use, and other variables.

In modern CHIP-8 implementations, where the interpreter is running natively outside the 4K memory space, there is no need to avoid the lower 512 bytes of memory (0x000-0x1FF), and it is common to store font data there.

## Design

### Requirements
- [ ] Access memory by address.
- [ ] Access memory by address range.
