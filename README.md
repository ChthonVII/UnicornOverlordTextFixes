# UnicornOverlordTextFixes
A mod for Unicorn Overlord on Switch (& emulators) that fixes translation errors in skill descriptions.

This mod does ***not*** modify gameplay; it merely corrects the mistranslated skill descriptions to match their actual behavior.

The current release is for Unicorn Overlord 1.03.

### List of Fixes


- Defensive Curse (Class: Shaman/Druid)
  - Original Text: Inflicts Phys. Attack %s, Mag. Attack %s,{linebreak}and Guard Seal on a row of enemies.
  - Corrected Text: Inflicts Phys. Defense %s, Mag. Defense %s,{linebreak}and Guard Seal on a row of enemies.
- Aerial Shift (Item: General's Longbow)
  - Original Text: Buff a row of allies.{linebreak}Grants %s Attack and %s Critical Rate to flying allies.
  - Corrected Text: Buff a row of allies.{linebreak}Grants %s Attack and %s Critical Rate against{linebreak}flying enemies.
- Phalanx Shift (Item: General's Pike)
  - Original Text: Buff a row of allies.{linebreak}Grants %s Attack and %s Critical Rate to cavalry allies.
  - Corrected Text: Buff a row of allies.{linebreak}Grants %s Attack and %s Critical Rate against{linebreak}cavalry enemies.
- Photon Arrow (Class: Featherbow)
  - Original Text: Attack two enemies.{linebreak}Inflicts Phys. Defense %s.{linebreak}Inflicts Passive Seal during the day.
  - Corrected Text: Attack two enemies.{linebreak}Inflicts Phys. Defense %s.{linebreak}Inflicts Guard Seal during the day.
- Aerial Smite (Class: Gryphon Knight/Master)
  - Original Text: Attack a row of enemies.{linebreak}Cavalry targets cannot guard against this attack.{linebreak}Grants the user %s #(56)AP if a target is at 100%% HP.
  - Corrected Text: Attack a row of enemies.{linebreak}Cavalry targets cannot guard against this attack.{linebreak}Inflicts %s #(56)AP on targets at 100%% HP.
- Active Steal (Class: Thief/Rogue)
  - Original Text: Attack a single enemy.{linebreak}Steal all of the enemy's #(56)AP.{linebreak}(Does not apply if they guard the first hit.)
  - Corrected Text: Attack a single enemy.{linebreak}Steal #c(10)1#/c #(56)AP from the enemy.{linebreak}(Does not apply if they guard the first hit.)
- Hastened Cast (Item: Magia Heart)
  - Original Text: Grants an ally max Initiative for their next action.
  - Corrected Text: Grants the user max Initiative for their next action.
- Guardian (Class: Hoplite/Legionnaire)
  - Original Text: Grants the user %s Phys. Attack and %s Guard Rate.{linebreak}(Effect stacks.)
  - Corrected Text: Grants the user %s Phys. Defense and{linebreak}%s Guard Rate. (Effect stacks.)
- "3 or Fewer Enemies" Skill Condition
  - Original Text: 2 or Fewer Enemies
  - Corrected Text: 3 or Fewer Enemies

### Installation
- On real Switch hardware, you must be jailbroken/modchipped with [Atmosphere](https://github.com/Atmosphere-NX/Atmosphere/releases) installed. Place Unicorn_US.CPK in the appropriate directory for RomFS replacement.
- On a Switch emulator, Place Unicorn_US.CPK in [the appropriate directory](https://github.com/Ryujinx/Ryujinx/wiki/Ryujinx-Setup-&-Configuration-Guide#managing-mods) for RomFS replacement.
- What about PS4/5? I don't own a PS4/5, and I have no idea if modding games on them is even possible. Probably takes a jailbreak of some kind? In theory you'd figure out where Unicorn_US.CPK lives and replace it.
- It's not very fair that pirates and people with hacked Switch hardware get this mod, while everyone else is stuck with the bad skill translations. I'm not super happy about this. I really wish that (a) Vanillaware had put more care into getting the skill translations correct in the first place, (b) that they'd promptly patched the mistranslations, and/or (c) that they'd do a PC release so I could mod that instead.

### Help Wanted

- Found another mistranslated skill description? Please report it in [this reddit thread](https://www.reddit.com/r/UnicornOverlord/comments/1bvcvqp/collecting_and_fixing_translation_errors_in_skill/). (People there are better equipped to rapidly confirm/clarify the actual skill behavior than just me alone.)
- Do you speak fluent German, Spanish, French, or Italian? Do you know your way around a hex editor? Then please contribute fixes for those languages. See [HowToModUOText.md](HowToModUOText.md) in this repo for information on how to do that.
- Are you able to unpack the PS4/5 edition of the game? Please drop me a line. I'd really like to make a 4K mod for Switch (and its emulators).

