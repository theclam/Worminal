Worminal v0.1 alpha
===================

Worminal is an ANSI / CP437 capable terminal emulator for RiscOS, developed on
the A3020. It is mostly written in assembler to allow it to reach speeds of 
"up to" 19200 baud using the on-board serial controller.

I mainly wrote Worminal because the only other terminal I could get working on
the Acorn:
1) didn't handle CP437 characters, which made most BBSes look gross
2) didn't use the "standard" VGA colours, which made most BBSes look gross
3) didn't understand colour intensity, which meant I couldn't play Bubble Boggle

So those are the founding principles of the software :)

Please note - the .txt files are listings that can be directly entered, the non-txt files are BASIC 

Please see the following sections if you want to make it actually work.

IMPORTANT - YOU NEED A FONT FILE
================================

Worminal requires an 8x16 bitmap font in an optimised (proprietary) format for
efficiency. To get true VGA fonts, you may want to download the full font pack
at https://int10h.org/oldschool-pc-fonts/download/

Inside this you will find a "fon - Bm (windows bitmap)" directory which contains
various font files including the "Bm437_IGS_VGA_8x16.FON" which I use.

Run that font through the converter program:

```
*blobify
Blobify - takes an 8x16 fixed bitmap Windows font file
and outputs a blob containing the 4bpp version suitable
for Worminal to dispplay.
Enter source font file?8x16
Enter destination font file (enter for 'fontblob')?
Completed.
*
```

IMPORTANT - YOU NEED TO SET YOUR FONT FILE LOCATION
===================================================

I'm OK at making hardware do stuff but I only started using RiscOS in 2022 so I
don't honestly know what I'm doing with it. For example, I don't know how to
tell it to look for the font file in the same directory where the BASIC program
is located so that has to be hard coded into the BASIC file. I moved it to the
top for "convenience":

```
ffile$ = "ADFS::CF.$.Worminal.fontblob"
```

Edit it to point at the file you just created.
 
Bugs
====

Yes.

Working Features
================
- Control codes for:
  - Colours
  - Intensity
  - Clear line / screen
  - Locate / up / down / left / right movement
  - Cursor location reporting (used to find terminal size)
- Basic Telnet negotiation (terminal size / speed / ANSI capability)
- Ding on ^G
- Clear screen on form feed

Baud rates up to 19200 supported - for now you have to edit the code, though.

Wishlist
========

- X / Y / Zmodem
- Screenshot capability
- Baud rate adjustment (without editing the code)
- Scrollback
