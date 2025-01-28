# Graphics & Sound

[[toc]]

Original CHIP-8 display resolution is 64×32 pixels, and color is monochrome. Graphics are drawn to the screen solely by drawing sprites, which are 8 pixels wide and may be from 1 to 15 pixels in height. Sprite pixels are XOR'd with corresponding screen pixels. In other words, sprite pixels that are set flip the color of the corresponding screen pixel, while unset sprite pixels do nothing. The carry flag (VF) is set to 1 if any screen pixels are flipped from set to unset when a sprite is drawn and set to 0 otherwise. This is used for collision detection.

As previously described, a beeping sound is played when the value of the sound timer is nonzero.

## Design

### Requirements
- [ ] 64x32 pixel "screen".
- [ ] Monochrome.
- [ ] Implement sprites.
- [ ] Work out how to do the sound.
