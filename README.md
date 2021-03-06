# CBT Heat for BT 1.9

CBT Heat brings Classic Battletech Tabletop heat rules feeling into HBS's BATTLETECH game.  In the Classic Battletech Tabletop game, heat management had a more press-your-luck style component to it.  This mod is an attempt to fit that style of mechanic into the heat system of this game.  Note that this is more of an attempt to blend the 2 systems together than a total reimplementation.

Firstly, a mech will no longer suffer damage from overheating.  This seemed a little unfair considering the rest of the changes and really didn't happen in CBT. To counter not being damaged, your mech will have a chance to shutdown and have its ammo explode every turn you are overheated.  The chances of that happening depend on the number of rounds you have been overheated.  I've tried to convert the original CBT heat chart in to percentages and apply them here.  The original CBT heat scale had 4 Shutdown roll chances and 4 Ammo Explosion chances as well as Heat modifiers to Hit.  So I've converted those chances (which were originally 2d6 rolls) and applied them to the overheat mechanic of the game. The game will roll randomly for each percentage.  Ammo Explosion results are applied first.

__NEW in v0.2.0__: Movement Modifiers

Movement modifiers work the same way ToHit Modifiers.  The movement modifier will increase the longer your mech is overheated.  That means the longer you overheat, the less movement you will have available.  This only affects walk and sprint movement.  Jump is unaffected.

The way the game applies movement modifiers is that it adds up all the the modifiers, subtracts them from 1 to get what is essentially a percentage, and then multiplies that by your total movement. So that means, for example, on the first overheat turn, you will have 90% of your total movement available to use (assuming you don't have any other movement modifiers, like a missing leg).


| Rounds Overheated | Shutdown Chance | Ammo Explosion Chance | ToHit Modifier | Move Modifier |
|:-----------------:|:---------------:|:---------------------:|:--------------:|:-------------:|
| 1                 | 8.3%            | 0                     | +1             | 0.1           |
| 2                 | 27.8%           | 8.3%                  | +2             | 0.2           |
| 3                 | 58.3%           | 27.8%                 | +3             | 0.3           |
| 4+                | 83.3%           | 58.3%                 | +4             | 0.4           |

These chances are also displayed in the Overheat notification badge above the heat bar.  Bringing your heat bar all the way to shutdown still shuts the mech down.

All chances and modifiers are configurable in the mod.json file.

__NEW in v0.6.0__: Heat level based shutdown chance

In mod.json if you have "UseCurrentHeat" to true the shutdown chance will be calculated as following:
ShutdownChance = (CurrentHealtLevel - OverheatThreshold)/(MaxHeat - OverHeatThreshold)
Then you roll against ShutdownChance.

In this mode you will not shutdown based on how long you've been overheating, meaning that if you succeed to maintain your overheat rather low you'll have a better chance to avoid shutdown as turns passed. On the other end, if you overheat by a large margin you're more likely to shutdown earlier.
This doesn't change anything on the other modifiers and they are still based on turns. So ammo cooking is still bad and dangerous.

You will not see "Ammo Explosion Avoided!" anymore if ammo explosion chance is 0 (so on the first turn on default settings).

## Installation

[ModTek](https://github.com/BattletechModders/ModTek/releases). Extract files to `BATTLETECH\Mods\CBTHeat\`.

## Changelog

### v0.7
Quick fix for 1.7.

### v0.6.0
Quick fix for BT 1.6.1. 
Added Heat level based shutdown chance

### v0.2.0
Added an overheat movement modifier in a way that's similar to ToHit modifier.  This version sets the base OverheatedMovePenalty to 0 in CombatGameConstants.json and adds the mods modifier table set in mod.json.

### v0.1.1
Added the ability to add a Guts Modifier to the Ammo Explosion and Shutdown chance rolls.  This is disabled by default.  To enable it, change the "UseGuts" setting to true in mod.json. The Guts modifier is currently calculated by essentially taking Guts / GutsDivisor.  The base GutsDivisor of 20 was too low, so I changed it to 40.  So a Guts of 5 would add 12.5% to the 2 rolls.
