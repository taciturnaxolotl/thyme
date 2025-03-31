# The thyme keyboard

<img src="https://raw.githubusercontent.com/taciturnaxolotl/thyme/main/.github/images/tanabata.svg" width="150" align="right">

> ### More deets coming soon 👀  
> A split, low-profile, wireless mechanical keyboard inspired by the Corne design. Made possible through the [`hackpad`](https://hackpad.hackclub.com) grant from Hack Club.

## Schematics

![schematic](https://raw.githubusercontent.com/taciturnaxolotl/thyme/main/.github/images/schematic.svg)

![pcb](https://raw.githubusercontent.com/taciturnaxolotl/thyme/main/.github/images/pcb.svg)

## Build Notes

Panelization is the most annoying bit of this whole process. I was able to finally get it work work by using `kikit` to generate rails and tabs. 

```bash
kikit panelize \
    --layout 'grid; rows: 1; cols: 1; space: 3mm;' \
    --tabs 'fixed; width: 3mm; vcount: 8;' \
    --cuts 'mousebites; drill: 0.5mm; spacing: 1mm; offset: 0.2mm; prolong: 0.5mm;' \
    --framing 'railstb; width: 5mm; space: 3mm; chamfer: 1mm;' \
    --tooling '3hole; hoffset: 2.5mm; voffset: 2.5mm; size: 1.5mm;' \
    --fiducials '3fid; hoffset: 5mm; voffset: 2.5mm; coppersize: 2mm; opening: 1mm;' \
    --post 'millradius: 1mm;' \
    --text 'simple; text: "THYME v1.14"; anchor: mt; voffset: 2mm;' \
    --text2 'simple; text: Created on {date} JLC Order: JLCJLCJLC; anchor: mb; voffset: -2.5mm; hjustify: center; vjustify: center;' \
    thyme.kicad_pcb panelization/panelized.kicad_pcb
```

![panelized](https://raw.githubusercontent.com/taciturnaxolotl/thyme/main/.github/images/panelized.svg)

<p align="center">
	<img src="https://raw.githubusercontent.com/taciturnaxolotl/carriage/master/.github/images/line-break.svg" />
</p>

<p align="center">
	<i><code>&copy 2025-present <a href="https://github.com/taciturnaxolotl">Kieran Klukas</a></code></i>
</p>

<p align="center">
	<a href="https://github.com/taciturnaxolotl/thyme/blob/master/LICENSE.md"><img src="https://img.shields.io/static/v1.svg?style=for-the-badge&label=License&message=MIT&logoColor=d9e0ee&colorA=363a4f&colorB=b7bdf8"/></a>
</p>
