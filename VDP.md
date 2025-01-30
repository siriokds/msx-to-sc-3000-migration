
# msx-to-sc-3000-migration
VDP main routines:

|  | MSX 1 | SC-3000 / SG-1000
|:---:|:---:|:---:|
|Fast Writes <br> (vblank + unrolled)|outi ; (18 T)<br>outi ; (18 T)<br>outi ; (18 T)<br>...|outi ; (16 T)<br>outi ; (16 T)<br>outi ; (16 T)<br>...|
|Slow Writes <br> (29 T-States minimum <br>+ unrolled)|.label:<br>outi ; (18 T)<br>jp nz, .label ; (11 T)|.label:<br>nop ;(4 T)<br>outi ; (16 T)<br>jp nz, .label ; (10 T)
||Total: 29 T-States|Total: 30 T-States
