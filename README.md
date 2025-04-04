# The thyme keyboard

![blueprint](https://raw.githubusercontent.com/taciturnaxolotl/thyme/main/.github/images/blueprint.svg)

<img src="https://raw.githubusercontent.com/taciturnaxolotl/thyme/main/.github/images/tanabata.svg" width="150" align="right">

> ### More deets coming soon 👀  
> A split, low-profile, wireless mechanical keyboard inspired by the Corne design. Made possible through the [`hackpad`](https://hackpad.hackclub.com) grant from Hack Club.

## BOM

| Part | Quantity | Price | Link | Description | Notes |
| --- | --- | --- | --- | --- | --- |
| PCB | 1 | `$25.15` | [JLCPCB](https://jlcpcb.com) | 2-layer, 1.6mm, black, leaded Hasl | I wanted to get ENIG but that bumped the price by `$20` |
| | | | | | |
| Choc v1 switches | 50 | `$27.50` | [Chosfox](https://chosfox.com/products/kailh-chocs?variant=42514648006850) | pink variant: `20+-5 gf` linear | `$0.55` per switch |
| | | | | | |
| 1u keycaps | 40 | `$14.00` | [Chosfox](https://chosfox.com/collections/low-profile-keycaps/products/chocfox-cfx-choc-keycaps) | White PBT low profile | `$0.35` per keycap |
| 1u homing keycaps | 2 | `$0.80` | [Chosfox](https://chosfox.com/collections/low-profile-keycaps/products/chocfox-cfx-choc-keycaps) | White PBT low profile | `$0.40` per keycap |
| 1.75u keycaps | 2 | `$1.65` | [Chosfox](https://chosfox.com/collections/low-profile-keycaps/products/chocfox-cfx-choc-keycaps) | White PBT low profile | `$0.83` per keycap |
| Total cost: `$16.45` | | | | average of `$0.41` per keycap | |
| | | | | | |
| SuperMini NRF52840 (Nice!Nano footprint) | 2 | `$8.30` | [AliExpress](https://www.aliexpress.us/item/3256805848952479.html) | Wireless Microcontroller | `$4.15` per MCU |
| | | | | | |
| Machine Sockets 2.54mm | 1 | `$1.75` | [AliExpress](https://www.aliexpress.us/item/2251832794091942.html) | 26x2 needed to socket the two MCUs | comes in a 10 pack of 40x1 rows |
| Machine Pins | 1 | `$3.99` | [AliExpress](https://www.aliexpress.us/item/2251832672116019.html) | 26x2 needed to socket the two MCUs | comes in a 100 pack of 4 per header |
| Power Switch | 4 | `$0.39` | [DigiKey](https://www.digikey.com/en/products/detail/same-sky-formerly-cui-devices/SLW-1277744-3A-N-D/24399208) | added an extra switch for each side as backup | `$0.10` per switch |
| JST PH 2.0mm 2-pin Connector | 4 | `$0.40` | [DigiKey](https://www.digikey.com/en/products/detail/jst-sales-america-inc/S2B-PH-K-S/926626) | | `$0.10` per connector |
| Diodes | 42 | `$1.43` | [DigiKey](https://www.digikey.com/en/products/detail/diotec-semiconductor/1N4148/13164514) | 1N4148 | `$0.03` per diode |
| Total cost: `$7.66` | | | | | |
| | | | | | |
| 301230 3.7V 110mAh LiPo Battery | 2 | `$6.30` | [AliExpress](https://www.aliexpress.us/item/3256805162053912.html) | the non jst ones are cheaper but the crimper is 60 bucks and there is no way im buying that | `$3.15` per battery |

Total cost: `$85.11`  

### Shipping / Tax / Tariffs / Per store shopping list

| Store | Shipping | Subtotal | Total | Items |
| --- | --- | --- | --- | --- |
| AliExpress | `$9.43` | `$26.64` | `$36.07` | 2x SuperMini NRF52840, Machine Sockets, Machine Pins, 2x LiPo Battery |
| DigiKey | `$6.99` | `$4.49` (tarrifs and tax) | `$11.48` | 4x Power Switch, 4x JST Connector, 42x Diodes |
| Chosfox | `$5.00` | `$43.95` | `$48.95` | 50x Choc v1 switches, 40x 1u keycaps, 2x 1u homing keycaps, 2x 1.75u keycaps |
| JLCPCB | `$10.55` | `$14.60` | `$25.15` | 1x PCB |

Total shipping: `$31.97`  
Total cost: `$122.67` (including shipping, tax, and tarrifs)  

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

Firmware is `zmk` and is maintained in the submodule [/zmk](https://github.com/taciturnaxolotl/thyme-module). The latest firmware build can be grabbed from [nightly.link/taciturnaxolotl/thyme-module/workflows/build](https://nightly.link/taciturnaxolotl/thyme-module/workflows/build/main) as a zip containing the left and right half `uf2` files.

The case was made in onshape and is available in [this document](https://cad.onshape.com/documents/eb30178d0af4291efc746ab6/w/0d165c7d0bf8d717a9598c9f/e/3dd4b0baac9c9ef14c8041ba?renderMode=0&uiState=67efb22294ee2703b96c81ea). The case is made of PLA and printed on an A1 mini. It is likely to change quite a bit once I get my pcb assembled and can fit test stuff. Evenentually I would like to add a top plate that attaches to the bottom with magnets and mill the whole case out of aluminum.

A major tool that helped with the research and organization of my thoughts was my [figjam board](https://www.figma.com/board/wyCQS9SeIG2Sutu5v6OT2m/thyme---split-mech-keyboard?node-id=0-1&t=SG0VuRAT0FkSCQlS-1)! I used it to keep track of all the resources I found and what parts I wanted to use. Once I got to actually picking specific parts I moved that to the bom table above.

![figjam board](https://raw.githubusercontent.com/taciturnaxolotl/thyme/main/.github/images/figjam.png)

<p align="center">
	<img src="https://raw.githubusercontent.com/taciturnaxolotl/carriage/master/.github/images/line-break.svg" />
</p>

<p align="center">
	<i><code>&copy 2025-present <a href="https://github.com/taciturnaxolotl">Kieran Klukas</a></code></i>
</p>

<p align="center">
	<a href="https://github.com/taciturnaxolotl/thyme/blob/master/LICENSE.md"><img src="https://img.shields.io/static/v1.svg?style=for-the-badge&label=License&message=MIT&logoColor=d9e0ee&colorA=363a4f&colorB=b7bdf8"/></a>
</p>
