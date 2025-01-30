
# msx-to-sc-3000-migration
VDP main routines:

|  | MSX 1 | SC-3000 / SG-1000
|:---:|:---:|:---:|
|Fast Writes <br> (vblank + unrolled)|outi<br>outi<br>outi<br>...|outi<br>outi<br>outi<br>...|
|Slow Writes <br> (29 T-States minimum <br>+ unrolled)|.label:<br>outi ; (18 T)<br>jr nz, .label ; (12 T)<br>; Total: 31 T-States|.label:<br>nop ;(4 T)<br>outi ; (16 T)<br>jp nz, .label ; (10 T)<br>; Total: 30 T-States
