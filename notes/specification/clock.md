# Clocks

[[toc]]

CHIP-8 has two timers. They both count down at 60 hertz, until they reach 0:

    - Delay timer: This timer is intended to be used for timing the events of games. Its value can be set and read.
    - Sound timer: This timer is used for sound effects. When its value is nonzero, a beeping sound is made. Its value can only be set.

## Design

### Requirements
- [ ] Generic timer class
    - [ ] Delay timer
    - [ ] Sound timer
