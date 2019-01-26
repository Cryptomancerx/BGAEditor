# BGAEditor

Readme for BGAEditor v1.9 by Cryptomancer

INTRODUCTION:  
This is a saved game editor for Battlefleet Gothic: Armada. It supports editing solo skirmish profiles and campaign saved games.  

FEATURES SUPPORTED:  
Edit admiral level, ship slots, escort ship upgrade slots, renown, and elite level.  
Edit deployments and resolve all non-priority missions available in campaign mode.  
Edit ship level, captain picture, crew points, crew upgrade levels, upgrade slots, and battles waged.  

INTERFACE:  
The interface is purely CLI. Input is done through a series of text prompts in the form of: Number:Value or Command:Explanation.  

To select a given option enter everything to the left of the colon verbatim. This includes capitalization and punctuation. If you see a property enclosed in parenthesis then it is displayed purely FYI and is not editable. For example:  

(Faction): IMPERIUM -- This is NOT editable  
Renown: 100 -- This is editable  

NOTE THAT INPUTS ARE NOT VALIDATED. THIS EDITOR WILL BLINDLY EDIT YOUR PROFILE WITH WHATEVER VALUES YOU PROVIDE AND INVALID VALUES WILL BREAK YOUR GAMES!!!  
NOTE THAT THIS EDITOR DOES NOT CREATE BACKUPS OF YOUR SAVED GAMES SO TAKE MANUAL BACKUPS  
Saved games location: C:\Users\%USERNAME%\AppData\Local\BattleFleetGothic\Saved\SaveGames  
If you don't see the AppData folder then enable Show Hidden Folders in Folder Options. This program only modifies files in the form of <admiral name>.sav. Files in the form of <admiral name>_Meta.sav are untouched and do not need to be backed up.  

DETAILED EXPLANATION AND VALID INPUT VALUES:  
Here I will cover non-self explanatory input prompts and provide proper values where appropriate.  

Admiral Properties:  
Level -- For skirmish profiles the max level is 8. Note that setting the level does not give you additional ship slots. For that you need to use the Ship prompt.  
Renown -- This is a 32-bit integer so the max value is 4294967295. I suggest setting it to 25000 to allow you to max all your ships.  
Deployments -- This is the total number of deployments for a given turn. Available deployments will be this value minus any deployments already used in the current turn. (CAMPAIGN ONLY)  
Missions -- This will resolve all non-priority missions and restore control of all worlds to the Imperium. It will also reset the threat counters for all enemy factions to 0. (CAMPAIGN ONLY)  
Ship -- This will add a ship slot to your admiral's fleet of the given class for your faction. Valid values are LIGHT_CRUISER, CRUISER, BATTLECRUISER, BATTLESHIP. These are the values as taken from the saved game data and must be entered verbatim. BATTLECRUISER is not valid for Space Marines. BATTLECRUISER for Tau will be Auxiliary Ships.  
EscortUpgrades -- Sets number of upgrade slots for all ESCORT class ships (includes Transports) to 3.  
NextLevel -- Sets XP equal to that required for next level - 100 so one victory will level up the admiral.  
MAXADMIRAL! -- Sets level to 8 and gives 100K renown. This will also add ship slots your admiral's fleet as if he was level 8. You will have 4 light cruisers, 3 cruisers, 2 battle cruisers, and 1 battleship. Space Marine faction will instead have 0 battle cruisers, 4 cruisers, and 2 battleships.  

Ship Properties:  
Level -- The max level is 10. Note that this does not actually do anything.  
CaptainPicture -- Valid values are 0-5 (0-30 for Space Marines). If you find a picture you like, view that ship's properties and then use that value for your other ships.  
CrewPoints -- This is the number of available crew upgrade points. A level 10 ship with no spent crew upgrades will have 9 crew points. 18 crew points will max every crew skill.  
UpgradeSlots -- This is the maximum number of upgrades your ship can have. Valid values are 0-9.  
BattlesWaged -- This is the number of battles the ship has fought in. Note that this does not actually do anything.  
MAXSHIP! -- This will set UpgradeSlots to 5, CrewPoints to 9, and Level to 10.  

CHANGELOG:  
v1.1 - Fixed a bug on Solo Skirmish Admirals with difficulty set to EASY. Added MAXADMIRAL! and EscortUpgrades commands.  
v1.2 - Added campaign support.  
v1.3 - Fixed a bug with Admiral XP values being incorrectly displayed. Fixed a bug that would display blank lines in the ship list if you did MAXFLEET! from a level 2+ Admiral. Added ability to edit deployments in the campaign.  
v1.4 - Added Missions command which will resolve all non-priority missions in the campaign.  
v1.5 - Added support for Space Marines faction. Fixed ship data parsing to accomodate new format introduced in Space Marine patch (1.5.8468). Removed MAXFLEET! command. MAXADMIRAL! now includes EscortUpgrades. Removed ability to display and edit individual crew skill values for ships (see note below for explanation).  
v1.6 - Fixed crash when a ship is named the same as the ship class (Example: Imperial Navy Dauntless class Light Cruiser named Dauntless). Added ability to edit elite level. Added chapter display to Space Marine admirals.  
v1.7 - Added support for Tau faction. Fixed MAXADMIRAL! command for Space Marines to give 4 Cruisers. Added sanity check to ship name length value to fix crash with Tau transport ship.  
v1.8 - Added NextLevel command.  
v1.9 - Updated editor to support changes to ship data format introduced in game patch 1.8.10317.

Note about Crew Skill values:  
As of the Space Marine patch (1.5.8468), the data structure for ships was changed. Before this patch all crew skills used the names of the Imperial Navy fleet so the same parsing code would work for any faction. With the Space Marine patch, the crew skill names are faction specific. This means I would have to write unique parsing code for each faction and quite frankly that's a pain in the ass that I don't feel is worth it. Users can still set crew points and distribute them as they wish.  

To compile BGAEditor into a Windows binary you will need pyinstaller which can be installed via pip. Use the following command:  
pyinstaller -F -i BGA.ico BGAEditor.py.
