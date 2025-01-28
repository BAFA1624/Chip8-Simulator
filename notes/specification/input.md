# Input

[[toc]]

Input is done with a hex keyboard that has 16 keys ranging 0 to F. The '8', '4', '6', and '2' keys are typically used for directional input. Three opcodes are used to detect input. One skips an instruction if a specific key is pressed, while another does the same if a specific key is not pressed. The third waits for a key press, and then stores it in one of the data registers.

## Design

### Requirements
- [ ] 16 key input keyboard.
    - [ ] Key capture.
    - [ ] Handling for invalid keystrokes.

