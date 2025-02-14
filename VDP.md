


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
|out (vdp_data_port), a| 12 T-States | 11 T-States 
|ld c, vdp_data_port<br>out ( c ), a | 14 T-States | 12 T-States 
|Fast Writes <br>(2 us minimum<br> vblank + unrolled)|outi ; (18 T / 5.028 us)<br>outi ; (18 T / 5.028 us)<br>outi ; (18 T / 5.028 us)<br>...|outi ; (16 T / 4.470 us)<br>outi ; (16 T / 4.470 us)<br>outi ; (16 T / 4.470 us)<br>...|
|Slow Writes <br> (29 T-States minimum)|Copy256:<br><br>ld b, 0<br><br>.loop_256:<br>outi ; (18 T)<br>jp nz, .loop_256 ; (11 T)|Copy256:<br>ld b, 0<br><br>.loop_128_1:<br>outi ; (16 T)<br>djnz .loop_128_1 ; (13 T)<br><br>.loop_128_2:<br>outi ; (16 T)<br>djnz .loop_128_2 ; (13 T)
||Total: 29 T-States / byte|Total: 29 T-States / byte
<br>
<br>
VDP bytes transfer:

|  | MSX 1 | SC-3000 / SG-1000
|:---:|:---:|:---:|
|RENDER AREA (PAL/NTSC)<br> (192 lines)| 1509 bytes | 1509 bytes
|NTSC VBLANK (70 lines)| 886 bytes | 997 bytes
|PAL VBLANK (121 lines)| 1532 bytes | 1724 bytes
