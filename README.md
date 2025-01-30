

# msx-to-sc-3000-migration
A bunch of docs about cross programming between MSX and SC-3000/SG-1000


|  | MSX 1 | SC-3000 | SG-1000
|:---:|:---:|:---:|:---:|
|CPU|Z80 @3.58Mhz|Z80 @3.58Mhz|Z80 @3.579545Mhz|
|CPU M1 wait states|1 T-States|0 T-States|0 T-States|
|RAM|8 to 64KB|2KB expandable with cartridge|1KB expandable with cartridge|
|[VDP](VDP.md) |TMS9918 (NTSC)<br> / TMS9929 (PAL)|TMS9918 (NTSC)<br> / TMS9929 (PAL)|TMS9918 (NTSC)|
|PSG|AY-3-8910|SN76489 <br>(same as Colecovision)|SN76489 <br>(same as Colecovision)|
|Keyboard|Yes|Yes|Optional|
|BIOS|Yes 16KB|None|None|
|Internal Mapper|Yes (Page, opt. SubPage) + External on cartridge|External on cartridge|External on cartridge|
