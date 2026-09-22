Alps RKJXT1F42001 7-Way Switch and Encoder I2C Breakout
-------------------------------------------------------

I2C breakout for Alps RKJXT1F42001 using Adafruit Seesaw library on the SAMD09.
Schematic is a copy of the I2C "Stemma QT" Rotary Encoder breakout board
(product 4991), though the NeoPixel and 2x STEMMA QT (JST SH 4-pin) connectors
had to be dropped due to layout constraints. The RKJXT1F is a significantly
larger through-hole device than the rotary encoder and the Stemma QT connectors
simply would not fit in their original locations. However, identical board
shape (1in x 1in) and mounting holes were retained. Due to an oversight, the
pin ordering in the through-hole connection was flipped from the reference
design.

Pins were kept the same as the reference design, so the firmware built on main
branch of adafruit/seesaw works laregly correctly. There is a difference in how
the RKJXT1F handles the rotary encoding compared to typical encoders, so a fork
of the seesaw library is pushed and pending merge back to main. With the
updated firmware, the I2C protocol works as intended. The GPIO Seesaw registers
can be used for the new A/B/C/D pins.

| Direction | GPIO Number |
|-----------|-------------|
| A         | 16          |
| B         | 17          |
| C         | 7           |
| D         | 2           |
| PUSH      | 24          |

The logic to handle the directions is simple enough to not require integration
into the seesaw library. Per the RKJXT1F datasheet, when PUSH goes active
(low), check if any of A/B/C/D are also active (low). If so, it's a directional
press. Else, it was a PUSH.

