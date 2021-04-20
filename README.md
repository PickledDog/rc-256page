# rc-256page
 128K+128K fully pageable RAM/ROM card for RC2014
![Assembled PD110](/img/assembled.jpg)

## Overview
This RC2014-compatible board provides RAM and flash ROM, software-pageable in 32k pages. 4 ROM and 4 RAM pages may be paged into both the lower and upper 32k of Z80 memory.

## Memory details
For ROM, a SST39SF010 128k x 8 flash chip is used. It can be programmed in-place using Will Sowerbutts' FLASH4 utility (included with RomWBW). For RAM, an AS6C1008 128k x 8 SRAM is used, providing 128K of addressable memory. Both are divided into 32k pages, and are presented to the system via 2 32k address blocks (so 2 pages selectable from 8 total).

## Paging
Upon reset, ROM page 0 is mapped to both the lower **and** upper 32k (initialization code in page 0 *must* select a RAM page for normal operation). A single config register is used to set **both** currently mapped pages, presented as an I/O device at 0x78 (the address used by most "large" Z80 memory systems). The low nibble of this configures the lower page, and the high nibble the higher page. For each nibble, the high bit selects the chip (0 for ROM, 1 for RAM).

## Firmware
This board can be used as an affordable way to add [RomWBW](https://github.com/wwarthen/RomWBW) support to an RC2014 (see below). It is also presented as a programming challenge for adventurous RC2014 builders, who want an inexpensive way to add fully software-pageable memory to their computers. Beyond RomWBW, *there are currently no standard ROM images for this board* (that is, no BASIC ROM etc). None of the standard RC2014 ROM images can be used as-is. Building a ROM image (or modifying an existing one) is left up to the user.

### RomWBW
For RomWBW, a new memory mapper needs to be added. A patch file to do this can be found in the [firmware](/firmware) directory (along with an example image).

## Part selection
Bill Of Materials and part references are below. I recommend using gold-plated header for the bus connection - I use these ones from [Pololu](https://www.pololu.com/product/967) or [Sparkfun](https://www.sparkfun.com/products/553). A nice detail of these, is that they sit at the same height as double-row header in a backplane.

The specified parts are just the ones I used, and can be substituted as needed - Mouser links provided for convenience and reference.

| Reference | Value | Qty | Mouser link |
| --------- | ----- | --- | ----------- |
| C1-C5 | 100nF ceramic | 5 | [KEMET C315C104M5U5TA](https://www.mouser.com/ProductDetail/C315C104M5U5TA7303) |
| J1 | 1x40 right-angle header | 1 | [Wurth 61304011021](https://www.mouser.com/ProductDetail/61304011021) |
| U1 | SST39SF010 NOR flash | 1 | [Microchip SST39SF010A-70-4C-PHE](https://www.mouser.com/ProductDetail/SST39SF010A-70-4C-PHE) |
| U2 | AS6C1008 SRAM | 1 | [Alliance AS6C1008-55PCN](https://www.mouser.com/ProductDetail/AS6C1008-55PCN) |
| | sockets | 2 | [Amphenol DILB32P-223TLF](https://www.mouser.com/ProductDetail/DILB32P-223TLF) |
| U3 | 74HCT138 | 1 | [TI SN74HCT138N](https://www.mouser.com/ProductDetail/SN74HCT138N) |
| U4 | 74HCT174 | 1 | [TI CD74HCT174E](https://www.mouser.com/ProductDetail/CD74HCT174E) |
| U5 | 74HCT257 | 1 | [TI SN74HCT257N](https://www.mouser.com/ProductDetail/SN74HCT257N) |