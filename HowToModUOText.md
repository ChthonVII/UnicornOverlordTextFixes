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

Use [fmsxml](https://github.com/ChthonVII/fmsxml) to convert to easily editable xml and back again.

**Markup:**
Unicorn Overlord uses a simple markup language for formatting and special symbols.
Here are a few examples that have been observed so far:
- %s = will be replaced with a numerical value at runtime (color coding is also done automatically at runtime)
- %% = escape sequence to get a percent sign
- #(56) = AP symbol
- #(57) = PP symbol
- #itext#/i = italic text
- (bold text was not observed, but it's probably #btext#/b)
- #c(10)text#/c = green text (this is probably "color 10," and there are other colors too)


## Repacking the CPK File
Use PyCriCodecs with CpkMode=1. See above.

## Install the Mod
- On real Switch hardware, you must be jailbroken/modchipped with [Atmosphere](https://github.com/Atmosphere-NX/Atmosphere/releases) installed. Place Unicorn_US.CPK in the appropriate directory for RomFS replacement.
- On a Switch emulator, Place Unicorn_US.CPK in [the appropriate directory](https://github.com/Ryujinx/Ryujinx/wiki/Ryujinx-Setup-&-Configuration-Guide#managing-mods) for RomFS replacement.
- What about PS4/5? I don't own a PS4/5, and I have no idea if modding games on them is even possible. Probably takes a jailbreak of some kind? In theory you'd figure out where Unicorn_US.CPK lives and replace it.
