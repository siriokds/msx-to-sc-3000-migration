

# msx-to-sc-3000-migration

VDP CPU I/O timings:

| Condition | Mode | Sprites<br>enabled |VDP Delay | Time waiting <br> for an access window | Total time | Total T-States<br>@ 3.58 Mhz
| :---: | :---: | :---: | :---: | :---: | :---: | :---:
| Active display area | Text | No |2 us | 0 - 1.1 us | 2 - 3.1 us | 12
| Active display area | Graphics I/II | Yes |2 us | 0 - 5.95 us | 2 - 8 us | 29
| Active display area | Multicolor | Yes |2 us | 0 - 1.5 us | 2 - 3.5 us | 13
| 4300 us after (16 T-States) <br>Vertical Interrupt Signal | All | | 2 us | 0 us | 2 us | 8
| Register 1 Blank Bit 0 | All | | 2 us | 0 us | 2 us | 8
<br>
<br>
VDP main routines:

|  | MSX 1 | SC-3000 / SG-1000
|:---:|:---:|:---:|
|Fast Writes <br>(2 us minimum<br> vblank + unrolled)|outi ; (18 T / 5.028 us)<br>outi ; (18 T / 5.028 us)<br>outi ; (18 T / 5.028 us)<br>...|outi ; (16 T / 4.470 us)<br>outi ; (16 T / 4.470 us)<br>outi ; (16 T / 4.470 us)<br>...|
|Slow Writes <br> (29 T-States minimum)|.label:<br>outi ; (18 T)<br>jp nz, .label ; (11 T)|.label:<br>nop ;(4 T)<br>outi ; (16 T)<br>jp nz, .label ; (10 T)
||Total: 29 T-States|Total: 30 T-States
