# How to Modify Text in Unicorn Overlord

This is a brief guide about how to mod text in Unicorn Overlord on Switch and Switch emulators.

## Overview

There are five general steps:
1. Dump RomFS.
2. Unpack the CPK file.
3. Edit the fms file.
4. Repack the CPK file.
5. Install the mod.

## Dump RomFS

If you are already set up to do this on a jailbroken/modchipped Switch console, I'll assume you know what you're doing. Otherwise, it is *much* simpler to obtain a pirate copy and use a Switch emulator. (For example, in Ryujinx, just right-click the game and select "Extract Data">"RomFS".)

Inside the RomFS, there should be 7 files. Unicorn.CPK and UnicornPatch.CPK are the (patched) core game files with Japanese language. The other 5 files are localizations for other languages. Unicorn_US.CPK is the English language file.

## Unpacking and Repacking the CPK File

You need a tool that can unpack and repack CPK files, *and that produces repacked files that Unicorn Overload can read*. One tool that can do this is [PyCriCodecs](https://github.com/Youjose/PyCriCodecs). Make sure to use CpkMode=1 when repacking. This isn't a perfect solution since PyCriCodecs doesn't support packing with CIRLAYLA compression, which would make the files smaller. If anyone finds a tool that produces repacked files that Unicorn Overload can read *and* supports CIRLAYLA compression, please drop me a line. (To test a packer, just repack the unpacked files without modifying them, place the resulting CPK in your mod folder, and see if Unicorn Overlord still works.)

(I had poor luck with other tools. The first tool I tried (CriPakGUI) could unpack just fine, but Unicorn Overlord couldn't read its output (resulting in no text in game). The second and third tools I tried (YAKcpkTool and SkythTools) wouldn't run at all because they try to load vcrun2010 dlls in some weird non-standard way that I couldn't satisfy on my system.)

The CPK files contains a number of files with fairly descriptive file names. The skill descriptions are in MsgSheet/UcSkillList.fms.

## Editing the fms file.

For this you'll need a hex editor and basic knowledge about how to use one. Here is the file structure:

| Offset  | Length | Type | Const | What |
| ------------- | ------------- | ------------- | ------------- | ------------- | 
| 0x0 | 4 bytes | magic | 0x464D5342 | magic word = FMSB |
| 0x4 | 4 bytes | int | | length of data section in bytes (*little endian*) (equals file size minus 48) |
| 0x8 | 4 bytes | int | 0x20 | header size in bytes, seems to always be 0x20 (=32) (*little endian*) |
| 0xc | 4 bytes | ? | 0x0 | unknown, seems to always be zero |
| 0x10 | 4 bytes | ? | 0x0 | unknown, seems to always be zero |
| 0x14 | 4 bytes | int | | number of strings (*little endian*) (should be 2886 for UcSkillList.fms) |
| 0x18 | 4 bytes | int | 0x3 | unknown, seems to always be 0x3 (=3) (*little endian*) |
| 0x1c | 4 bytes | ? | 0x0 | unknown, seems to always be zero |
| 0x20 | varies | ? | 0x0 | unknown, 8 bytes per string, seems to always be zero |
| varies | varies | strings | | the strings themselves, stored end-to-end. see format below |
| varies | varies | bytes | 0x0 | zero padding to make the file length at this point an even multiple of 16 bytes |
| end - 0x10 | 4 bytes | magic | 0x46454F43 | magic word = FEOC |
| end - 0xc | 4 bytes | ? | 0x0 | unknown, seems to always be zero |
| end - 0x8 | 4 bytes | int | 0x10 | footer size in bytes, seems to always be 0x10 (=16) (*little endian*) |
| end - 0x4 | 4 bytes | ? | 0x0 | unknown, seems to always be zero |

**String Format:**
- UTF8 character encoding.
- Strings are terminated with a single zero byte.
- Strings are just placed end-to-end within the file, separated by their terminating zero bytes.
- The following special characters and sequences have been observed:
  - 0x0a = linebreak (no silly Windows CRLF stuff).
  - %s = will be replaced with a numerical value at runtime (color coding is also done automatically at runtime)
  - %% = escape sequence to get a percent sign
  - #(56) = AP symbol
  - #(57) = PP symbol
  - #itext#/i = italic text
  - (bold text was not observed, but it's probably #btext#/b)
  - #c(10)text#/c = green text (this is probably "color 10," and there are other colors too)

**Process:**  
From the above, we can derive a fairly straightforward editing process.
1. Edit the strings as desired, overwriting, inserting, or deleting bytes freely. (Just make sure to preserve the terminating zero bytes.)
2. Adjust the padding before the footer to make the file length is an even multiple of 16 bytes.
3. Check the file size in bytes, subtract 48, and overwrite the value at offset 0x04. (Remember *little endian*!)

## Repacking the CPK File
Use PyCriCodecs with CpkMode=1. See above.

## Install the Mod
- On real Switch hardware, you must be jailbroken/modchipped with [Atmosphere](https://github.com/Atmosphere-NX/Atmosphere/releases) installed. Place Unicorn_US.CPK in the appropriate directory for RomFS replacement.
- On a Switch emulator, Place Unicorn_US.CPK in [the appropriate directory](https://github.com/Ryujinx/Ryujinx/wiki/Ryujinx-Setup-&-Configuration-Guide#managing-mods) for RomFS replacement.
- What about PS4/5? I don't own a PS4/5, and I have no idea if modding games on them is even possible. Probably takes a jailbreak of some kind? In theory you'd figure out where Unicorn_US.CPK lives and replace it.
