

```python
#imports
import pandas as pd
import numpy as np
import json
```


```python
# read the json file  // THERE IS ONLY ONE DATA SET FOR THIS PROBLEM
with open('purchase_data.json') as file:
    j_data = json.load(file)
j_data
```




    [{'Age': 38,
      'Gender': 'Male',
      'Item ID': 165,
      'Item Name': 'Bone Crushing Silver Skewer',
      'Price': 3.37,
      'SN': 'Aelalis34'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 119,
      'Item Name': 'Stormbringer, Dark Blade of Ending Misery',
      'Price': 2.32,
      'SN': 'Eolo46'},
     {'Age': 34,
      'Gender': 'Male',
      'Item ID': 174,
      'Item Name': 'Primitive Blade',
      'Price': 2.46,
      'SN': 'Assastnya25'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 92,
      'Item Name': 'Final Critic',
      'Price': 1.36,
      'SN': 'Pheusrical25'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 63,
      'Item Name': 'Stormfury Mace',
      'Price': 1.27,
      'SN': 'Aela59'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 10,
      'Item Name': 'Sleepwalker',
      'Price': 1.73,
      'SN': 'Tanimnya91'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 153,
      'Item Name': 'Mercenary Sabre',
      'Price': 4.57,
      'SN': 'Undjaskla97'},
     {'Age': 29,
      'Gender': 'Female',
      'Item ID': 169,
      'Item Name': 'Interrogator, Blood Blade of the Queen',
      'Price': 3.32,
      'SN': 'Iathenudil29'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 118,
      'Item Name': 'Ghost Reaver, Longsword of Magic',
      'Price': 2.77,
      'SN': 'Sondenasta63'},
     {'Age': 31,
      'Gender': 'Male',
      'Item ID': 99,
      'Item Name': 'Expiration, Warscythe Of Lost Worlds',
      'Price': 4.53,
      'SN': 'Hilaerin92'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 57,
      'Item Name': 'Despair, Favor of Due Diligence',
      'Price': 3.81,
      'SN': 'Chamosia29'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 47,
      'Item Name': 'Alpha, Reach of Ending Hope',
      'Price': 1.55,
      'SN': 'Sally64'},
     {'Age': 30,
      'Gender': 'Male',
      'Item ID': 81,
      'Item Name': 'Dreamkiss',
      'Price': 4.06,
      'SN': 'Iskossa88'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 77,
      'Item Name': 'Piety, Guardian of Riddles',
      'Price': 3.68,
      'SN': 'Seorithstilis90'},
     {'Age': 40,
      'Gender': 'Male',
      'Item ID': 44,
      'Item Name': 'Bonecarvin Battle Axe',
      'Price': 2.46,
      'SN': 'Sundast29'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 96,
      'Item Name': 'Blood-Forged Skeletal Spine',
      'Price': 4.77,
      'SN': 'Haellysu29'},
     {'Age': 22,
      'Gender': 'Female',
      'Item ID': 123,
      'Item Name': "Twilight's Carver",
      'Price': 1.14,
      'SN': 'Sundista85'},
     {'Age': 22,
      'Gender': 'Female',
      'Item ID': 59,
      'Item Name': 'Lightning, Etcher of the King',
      'Price': 1.65,
      'SN': 'Aenarap34'},
     {'Age': 28,
      'Gender': 'Male',
      'Item ID': 91,
      'Item Name': 'Celeste',
      'Price': 3.71,
      'SN': 'Iskista88'},
     {'Age': 31,
      'Gender': 'Male',
      'Item ID': 177,
      'Item Name': 'Winterthorn, Defender of Shifting Worlds',
      'Price': 4.89,
      'SN': 'Assossa43'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 78,
      'Item Name': 'Glimmer, Ender of the Moon',
      'Price': 2.33,
      'SN': 'Irith83'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 3,
      'Item Name': 'Phantomlight',
      'Price': 1.79,
      'SN': 'Iaralrgue74'},
     {'Age': 11,
      'Gender': 'Female',
      'Item ID': 11,
      'Item Name': 'Brimstone',
      'Price': 2.52,
      'SN': 'Deural48'},
     {'Age': 19,
      'Gender': 'Male',
      'Item ID': 183,
      'Item Name': "Dragon's Greatsword",
      'Price': 2.36,
      'SN': 'Chanosia65'},
     {'Age': 11,
      'Gender': 'Male',
      'Item ID': 65,
      'Item Name': 'Conqueror Adamantite Mace',
      'Price': 1.96,
      'SN': 'Qarwen67'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 63,
      'Item Name': 'Stormfury Mace',
      'Price': 1.27,
      'SN': 'Idai61'},
     {'Age': 29,
      'Gender': 'Male',
      'Item ID': 132,
      'Item Name': 'Persuasion',
      'Price': 3.9,
      'SN': 'Aerithllora36'},
     {'Age': 34,
      'Gender': 'Male',
      'Item ID': 106,
      'Item Name': 'Crying Steel Sickle',
      'Price': 2.29,
      'SN': 'Assastnya25'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 49,
      'Item Name': 'The Oculus, Token of Lost Worlds',
      'Price': 4.23,
      'SN': 'Ilariarin45'},
     {'Age': 16,
      'Gender': 'Female',
      'Item ID': 45,
      'Item Name': 'Glinting Glass Edge',
      'Price': 2.46,
      'SN': 'Phaedai25'},
     {'Age': 21,
      'Gender': 'Female',
      'Item ID': 155,
      'Item Name': 'War-Forged Gold Deflector',
      'Price': 3.73,
      'SN': 'Eulaeria40'},
     {'Age': 18,
      'Gender': 'Male',
      'Item ID': 37,
      'Item Name': 'Shadow Strike, Glory of Ending Hope',
      'Price': 1.93,
      'SN': 'Iarilis73'},
     {'Age': 19,
      'Gender': 'Male',
      'Item ID': 48,
      'Item Name': 'Rage, Legacy of the Lone Victor',
      'Price': 4.32,
      'SN': 'Malunil62'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 90,
      'Item Name': 'Betrayer',
      'Price': 1.67,
      'SN': 'Iskimnya76'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 47,
      'Item Name': 'Alpha, Reach of Ending Hope',
      'Price': 1.55,
      'SN': 'Yararmol43'},
     {'Age': 21,
      'Gender': 'Female',
      'Item ID': 13,
      'Item Name': 'Serenity',
      'Price': 1.49,
      'SN': 'Aisur51'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 44,
      'Item Name': 'Bonecarvin Battle Axe',
      'Price': 2.46,
      'SN': 'Undare39'},
     {'Age': 31,
      'Gender': 'Male',
      'Item ID': 171,
      'Item Name': 'Scalpel',
      'Price': 3.62,
      'SN': 'Sondossa91'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 25,
      'Item Name': 'Hero Cane',
      'Price': 1.03,
      'SN': 'Chamjasknya65'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 63,
      'Item Name': 'Stormfury Mace',
      'Price': 1.27,
      'SN': 'Lassilsa63'},
     {'Age': 32,
      'Gender': 'Male',
      'Item ID': 7,
      'Item Name': 'Thorn, Satchel of Dark Souls',
      'Price': 4.51,
      'SN': 'Tyisur83'},
     {'Age': 19,
      'Gender': 'Female',
      'Item ID': 124,
      'Item Name': 'Venom Claymore',
      'Price': 2.72,
      'SN': 'Aeral43'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 25,
      'Item Name': 'Hero Cane',
      'Price': 1.03,
      'SN': 'Lassadarsda57'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 68,
      'Item Name': 'Storm-Weaver, Slayer of Inception',
      'Price': 2.49,
      'SN': 'Alaephos75'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 85,
      'Item Name': 'Malificent Bag',
      'Price': 2.17,
      'SN': 'Frichjask31'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 120,
      'Item Name': 'Agatha',
      'Price': 1.91,
      'SN': 'Eusur90'},
     {'Age': 11,
      'Gender': 'Male',
      'Item ID': 17,
      'Item Name': 'Lazarus, Terror of the Earth',
      'Price': 3.47,
      'SN': 'Palatyon26'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 141,
      'Item Name': 'Persuasion',
      'Price': 3.27,
      'SN': 'Saellyra72'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 73,
      'Item Name': 'Ritual Mace',
      'Price': 3.74,
      'SN': 'Ililsa62'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 151,
      'Item Name': 'Severance',
      'Price': 1.85,
      'SN': 'Eosur70'},
     {'Age': 32,
      'Gender': 'Female',
      'Item ID': 32,
      'Item Name': 'Orenmir',
      'Price': 4.95,
      'SN': 'Saistyphos30'},
     {'Age': 16,
      'Gender': 'Male',
      'Item ID': 169,
      'Item Name': 'Interrogator, Blood Blade of the Queen',
      'Price': 3.32,
      'SN': 'Reula64'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 165,
      'Item Name': 'Bone Crushing Silver Skewer',
      'Price': 3.37,
      'SN': 'Chanirrala39'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 51,
      'Item Name': 'Endbringer',
      'Price': 2.67,
      'SN': 'Chadanto83'},
     {'Age': 25,
      'Gender': 'Female',
      'Item ID': 101,
      'Item Name': 'Final Critic',
      'Price': 4.62,
      'SN': 'Minduli80'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 140,
      'Item Name': 'Striker',
      'Price': 3.82,
      'SN': 'Heunadil74'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 31,
      'Item Name': 'Trickster',
      'Price': 2.07,
      'SN': 'Marilsasya33'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 34,
      'Item Name': 'Retribution Axe',
      'Price': 4.14,
      'SN': 'Alallo58'},
     {'Age': 24,
      'Gender': 'Female',
      'Item ID': 65,
      'Item Name': 'Conqueror Adamantite Mace',
      'Price': 1.96,
      'SN': 'Tyaeristi78'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 2,
      'Item Name': 'Verdict',
      'Price': 3.4,
      'SN': 'Ila44'},
     {'Age': 31,
      'Gender': 'Male',
      'Item ID': 86,
      'Item Name': 'Stormfury Lantern',
      'Price': 1.28,
      'SN': 'Iskossaya95'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 39,
      'Item Name': 'Betrayal, Whisper of Grieving Widows',
      'Price': 2.35,
      'SN': 'Rinallorap73'},
     {'Age': 19,
      'Gender': 'Female',
      'Item ID': 39,
      'Item Name': 'Betrayal, Whisper of Grieving Widows',
      'Price': 2.35,
      'SN': 'Aeri84'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 28,
      'Item Name': 'Flux, Destroyer of Due Diligence',
      'Price': 3.04,
      'SN': 'Ryanara76'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 160,
      'Item Name': 'Azurewrath',
      'Price': 2.22,
      'SN': 'Syally44'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 134,
      'Item Name': 'Undead Crusader',
      'Price': 4.67,
      'SN': 'Shaidanu32'},
     {'Age': 18,
      'Gender': 'Male',
      'Item ID': 13,
      'Item Name': 'Serenity',
      'Price': 1.49,
      'SN': 'Syasriria69'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 83,
      'Item Name': 'Lifebender',
      'Price': 3.51,
      'SN': 'Lisiriya82'},
     {'Age': 11,
      'Gender': 'Male',
      'Item ID': 38,
      'Item Name': 'The Void, Vengeance of Dark Magic',
      'Price': 2.82,
      'SN': 'Qarwen67'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 7,
      'Item Name': 'Thorn, Satchel of Dark Souls',
      'Price': 4.51,
      'SN': 'Iskosia51'},
     {'Age': 7,
      'Gender': 'Female',
      'Item ID': 158,
      'Item Name': 'Darkheart, Butcher of the Champion',
      'Price': 3.56,
      'SN': 'Eosurdru76'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 85,
      'Item Name': 'Malificent Bag',
      'Price': 2.17,
      'SN': 'Lassimla92'},
     {'Age': 34,
      'Gender': 'Male',
      'Item ID': 110,
      'Item Name': 'Suspension',
      'Price': 2.11,
      'SN': 'Tauldilsa43'},
     {'Age': 16,
      'Gender': 'Male',
      'Item ID': 122,
      'Item Name': 'Unending Tyranny',
      'Price': 1.21,
      'SN': 'Erudrion71'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 54,
      'Item Name': 'Eternal Cleaver',
      'Price': 3.14,
      'SN': 'Chanjaskan37'},
     {'Age': 31,
      'Gender': 'Male',
      'Item ID': 31,
      'Item Name': 'Trickster',
      'Price': 2.07,
      'SN': 'Sondastan54'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 105,
      'Item Name': 'Hailstorm Shadowsteel Scythe',
      'Price': 3.73,
      'SN': 'Strithenu87'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 87,
      'Item Name': 'Deluge, Edge of the West',
      'Price': 2.2,
      'SN': 'Chanastsda67'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 23,
      'Item Name': 'Crucifer',
      'Price': 2.77,
      'SN': 'Baelollodeu94'},
     {'Age': 29,
      'Gender': 'Male',
      'Item ID': 144,
      'Item Name': 'Blood Infused Guardian',
      'Price': 2.86,
      'SN': 'Undirrala66'},
     {'Age': 16,
      'Gender': 'Female',
      'Item ID': 128,
      'Item Name': 'Blazeguard, Reach of Eternity',
      'Price': 4.0,
      'SN': 'Chanosseya79'},
     {'Age': 38,
      'Gender': 'Male',
      'Item ID': 175,
      'Item Name': 'Woeful Adamantite Claymore',
      'Price': 1.24,
      'SN': 'Yaristi64'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 46,
      'Item Name': 'Hopeless Ebon Dualblade',
      'Price': 4.75,
      'SN': 'Airi27'},
     {'Age': 25,
      'Gender': 'Female',
      'Item ID': 32,
      'Item Name': 'Orenmir',
      'Price': 4.95,
      'SN': 'Frichaststa61'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 7,
      'Item Name': 'Thorn, Satchel of Dark Souls',
      'Price': 4.51,
      'SN': 'Raysistast71'},
     {'Age': 20,
      'Gender': 'Female',
      'Item ID': 150,
      'Item Name': 'Deathraze',
      'Price': 4.54,
      'SN': 'Ithergue48'},
     {'Age': 27,
      'Gender': 'Male',
      'Item ID': 152,
      'Item Name': 'Darkheart',
      'Price': 3.15,
      'SN': 'Chanastst38'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 108,
      'Item Name': 'Extraction, Quickblade Of Trembling Hands',
      'Price': 3.39,
      'SN': 'Sundosiasta28'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 132,
      'Item Name': 'Persuasion',
      'Price': 3.9,
      'SN': 'Undotesta33'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 172,
      'Item Name': 'Blade of the Grave',
      'Price': 1.69,
      'SN': 'Tyiaduenuru55'},
     {'Age': 33,
      'Gender': 'Male',
      'Item ID': 91,
      'Item Name': 'Celeste',
      'Price': 3.71,
      'SN': 'Iskjaskst81'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 167,
      'Item Name': 'Malice, Legacy of the Queen',
      'Price': 2.38,
      'SN': 'Iskjaskan81'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 181,
      'Item Name': "Reaper's Toll",
      'Price': 4.56,
      'SN': 'Frichim27'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 20,
      'Item Name': 'Netherbane',
      'Price': 1.48,
      'SN': 'Hailaphos89'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 130,
      'Item Name': 'Alpha',
      'Price': 1.56,
      'SN': 'Seorithstilis90'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 111,
      'Item Name': "Misery's End",
      'Price': 2.91,
      'SN': 'Jiskjask80'},
     {'Age': 22,
      'Gender': 'Female',
      'Item ID': 54,
      'Item Name': 'Eternal Cleaver',
      'Price': 3.14,
      'SN': 'Yasurra52'},
     {'Age': 17,
      'Gender': 'Female',
      'Item ID': 49,
      'Item Name': 'The Oculus, Token of Lost Worlds',
      'Price': 4.23,
      'SN': 'Assassasta79'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 47,
      'Item Name': 'Alpha, Reach of Ending Hope',
      'Price': 1.55,
      'SN': 'Lamyon68'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 110,
      'Item Name': 'Suspension',
      'Price': 2.11,
      'SN': 'Alo67'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 103,
      'Item Name': 'Singed Scalpel',
      'Price': 4.87,
      'SN': 'Farenon57'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 30,
      'Item Name': 'Stormcaller',
      'Price': 4.15,
      'SN': 'Assistasda90'},
     {'Age': 30,
      'Gender': 'Male',
      'Item ID': 51,
      'Item Name': 'Endbringer',
      'Price': 2.67,
      'SN': 'Frichaya88'},
     {'Age': 27,
      'Gender': 'Male',
      'Item ID': 139,
      'Item Name': 'Mercy, Katana of Dismay',
      'Price': 4.37,
      'SN': 'Marassanya92'},
     {'Age': 34,
      'Gender': 'Male',
      'Item ID': 173,
      'Item Name': 'Stormfury Longsword',
      'Price': 4.83,
      'SN': 'Iskista96'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 55,
      'Item Name': 'Vindictive Glass Edge',
      'Price': 4.26,
      'SN': 'Mindirra92'},
     {'Age': 37,
      'Gender': 'Female',
      'Item ID': 174,
      'Item Name': 'Primitive Blade',
      'Price': 2.46,
      'SN': 'Chadossa56'},
     {'Age': 29,
      'Gender': 'Male',
      'Item ID': 115,
      'Item Name': 'Spectral Diamond Doomblade',
      'Price': 4.25,
      'SN': 'Undirrala66'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 35,
      'Item Name': 'Heartless Bone Dualblade',
      'Price': 2.63,
      'SN': 'Eoda93'},
     {'Age': 20,
      'Gender': 'Female',
      'Item ID': 42,
      'Item Name': 'The Decapitator',
      'Price': 4.82,
      'SN': 'Lassast89'},
     {'Age': 20,
      'Gender': 'Female',
      'Item ID': 13,
      'Item Name': 'Serenity',
      'Price': 1.49,
      'SN': 'Philodil43'},
     {'Age': 19,
      'Gender': 'Male',
      'Item ID': 160,
      'Item Name': 'Azurewrath',
      'Price': 2.22,
      'SN': 'Tyirithnu40'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 57,
      'Item Name': 'Despair, Favor of Due Diligence',
      'Price': 3.81,
      'SN': 'Haerith37'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 152,
      'Item Name': 'Darkheart',
      'Price': 3.15,
      'SN': 'Jeyciman68'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 130,
      'Item Name': 'Alpha',
      'Price': 1.56,
      'SN': 'Chamirraya83'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 9,
      'Item Name': 'Thorn, Conqueror of the Corrupted',
      'Price': 2.04,
      'SN': 'Yasur85'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 84,
      'Item Name': 'Arcane Gem',
      'Price': 2.23,
      'SN': 'Koikirra25'},
     {'Age': 11,
      'Gender': 'Male',
      'Item ID': 160,
      'Item Name': 'Azurewrath',
      'Price': 2.22,
      'SN': 'Qarwen67'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 46,
      'Item Name': 'Hopeless Ebon Dualblade',
      'Price': 4.75,
      'SN': 'Quarunarn52'},
     {'Age': 19,
      'Gender': 'Male',
      'Item ID': 180,
      'Item Name': 'Stormcaller',
      'Price': 2.78,
      'SN': 'Yasur35'},
     {'Age': 31,
      'Gender': 'Male',
      'Item ID': 102,
      'Item Name': 'Avenger',
      'Price': 4.16,
      'SN': 'Isurriarap71'},
     {'Age': 7,
      'Gender': 'Male',
      'Item ID': 175,
      'Item Name': 'Woeful Adamantite Claymore',
      'Price': 1.24,
      'SN': 'Lassjask63'},
     {'Age': 18,
      'Gender': 'Female',
      'Item ID': 53,
      'Item Name': 'Vengeance Cleaver',
      'Price': 3.7,
      'SN': 'Iliel92'},
     {'Age': 19,
      'Gender': 'Male',
      'Item ID': 73,
      'Item Name': 'Ritual Mace',
      'Price': 3.74,
      'SN': 'Arithllorin55'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 18,
      'Item Name': 'Torchlight, Bond of Storms',
      'Price': 1.77,
      'SN': 'Silideu44'},
     {'Age': 7,
      'Gender': 'Female',
      'Item ID': 10,
      'Item Name': 'Sleepwalker',
      'Price': 1.73,
      'SN': 'Heosurnuru52'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 34,
      'Item Name': 'Retribution Axe',
      'Price': 4.14,
      'SN': 'Raesty92'},
     {'Age': 23,
      'Gender': 'Female',
      'Item ID': 74,
      'Item Name': 'Yearning Crusher',
      'Price': 1.06,
      'SN': 'Eyircil84'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 140,
      'Item Name': 'Striker',
      'Price': 3.82,
      'SN': 'Isursti83'},
     {'Age': 23,
      'Gender': 'Female',
      'Item ID': 126,
      'Item Name': 'Exiled Mithril Longsword',
      'Price': 3.25,
      'SN': 'Eurinu48'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 50,
      'Item Name': 'Dawn',
      'Price': 2.55,
      'SN': 'Saedaiphos46'},
     {'Age': 29,
      'Gender': 'Male',
      'Item ID': 62,
      'Item Name': 'Piece Maker',
      'Price': 4.36,
      'SN': 'Undirrala66'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 125,
      'Item Name': 'Whistling Mithril Warblade',
      'Price': 4.32,
      'SN': 'Jiskossa51'},
     {'Age': 17,
      'Gender': 'Female',
      'Item ID': 108,
      'Item Name': 'Extraction, Quickblade Of Trembling Hands',
      'Price': 3.39,
      'SN': 'Sundossast30'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 152,
      'Item Name': 'Darkheart',
      'Price': 3.15,
      'SN': 'Ialallo29'},
     {'Age': 18,
      'Gender': 'Male',
      'Item ID': 68,
      'Item Name': 'Storm-Weaver, Slayer of Inception',
      'Price': 2.49,
      'SN': 'Syasriria69'},
     {'Age': 16,
      'Gender': 'Male',
      'Item ID': 121,
      'Item Name': 'Massacre',
      'Price': 3.42,
      'SN': 'Chanosia60'},
     {'Age': 13,
      'Gender': 'Female',
      'Item ID': 20,
      'Item Name': 'Netherbane',
      'Price': 1.48,
      'SN': 'Ilosia37'},
     {'Age': 28,
      'Gender': 'Male',
      'Item ID': 129,
      'Item Name': 'Fate, Vengeance of Eternal Justice',
      'Price': 1.55,
      'SN': 'Tyeulisu40'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 91,
      'Item Name': 'Celeste',
      'Price': 3.71,
      'SN': 'Yaliru88'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 149,
      'Item Name': 'Tranquility, Razor of Black Magic',
      'Price': 2.47,
      'SN': 'Jiskassa76'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 12,
      'Item Name': 'Dawne',
      'Price': 4.3,
      'SN': 'Idairin80'},
     {'Age': 17,
      'Gender': 'Male',
      'Item ID': 7,
      'Item Name': 'Thorn, Satchel of Dark Souls',
      'Price': 4.51,
      'SN': 'Dyally87'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 175,
      'Item Name': 'Woeful Adamantite Claymore',
      'Price': 1.24,
      'SN': 'Quarusrion32'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 44,
      'Item Name': 'Bonecarvin Battle Axe',
      'Price': 2.46,
      'SN': 'Adairialis76'},
     {'Age': 11,
      'Gender': 'Male',
      'Item ID': 71,
      'Item Name': 'Demise',
      'Price': 4.07,
      'SN': 'Lirtilsan89'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 71,
      'Item Name': 'Demise',
      'Price': 4.07,
      'SN': 'Reolacal36'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 158,
      'Item Name': 'Darkheart, Butcher of the Champion',
      'Price': 3.56,
      'SN': 'Chadanto83'},
     {'Age': 18,
      'Gender': 'Male',
      'Item ID': 14,
      'Item Name': 'Possessed Core',
      'Price': 1.59,
      'SN': 'Lisirrast82'},
     {'Age': 13,
      'Gender': 'Male',
      'Item ID': 175,
      'Item Name': 'Woeful Adamantite Claymore',
      'Price': 1.24,
      'SN': 'Ilrian97'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 58,
      'Item Name': "Freak's Bite, Favor of Holy Might",
      'Price': 3.03,
      'SN': 'Tyadaru49'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 37,
      'Item Name': 'Shadow Strike, Glory of Ending Hope',
      'Price': 1.93,
      'SN': 'Sweecossa42'},
     {'Age': 13,
      'Gender': 'Male',
      'Item ID': 17,
      'Item Name': 'Lazarus, Terror of the Earth',
      'Price': 3.47,
      'SN': 'Streural92'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 155,
      'Item Name': 'War-Forged Gold Deflector',
      'Price': 3.73,
      'SN': 'Queusurra38'},
     {'Age': 27,
      'Gender': 'Female',
      'Item ID': 39,
      'Item Name': 'Betrayal, Whisper of Grieving Widows',
      'Price': 2.35,
      'SN': 'Lassilsa41'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 105,
      'Item Name': 'Hailstorm Shadowsteel Scythe',
      'Price': 3.73,
      'SN': 'Aisurphos78'},
     {'Age': 17,
      'Gender': 'Female',
      'Item ID': 27,
      'Item Name': 'Riddle, Tribute of Ended Dreams',
      'Price': 3.96,
      'SN': 'Marim28'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 52,
      'Item Name': 'Hatred',
      'Price': 4.39,
      'SN': 'Taeduenu92'},
     {'Age': 25,
      'Gender': 'Female',
      'Item ID': 66,
      'Item Name': 'Victor Iron Spikes',
      'Price': 3.55,
      'SN': 'Eodailis27'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 100,
      'Item Name': 'Blindscythe',
      'Price': 3.66,
      'SN': 'Lassjaskan73'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 112,
      'Item Name': 'Worldbreaker',
      'Price': 3.29,
      'SN': 'Yadanun74'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 24,
      'Item Name': 'Warped Fetish',
      'Price': 2.41,
      'SN': 'Iskossasda43'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 94,
      'Item Name': 'Mourning Blade',
      'Price': 1.82,
      'SN': 'Aesty51'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 158,
      'Item Name': 'Darkheart, Butcher of the Champion',
      'Price': 3.56,
      'SN': 'Tyida79'},
     {'Age': 27,
      'Gender': 'Male',
      'Item ID': 107,
      'Item Name': 'Splitter, Foe Of Subtlety',
      'Price': 3.61,
      'SN': 'Frichossast75'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 106,
      'Item Name': 'Crying Steel Sickle',
      'Price': 2.29,
      'SN': 'Eratiel90'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 173,
      'Item Name': 'Stormfury Longsword',
      'Price': 4.83,
      'SN': 'Eoda93'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 86,
      'Item Name': 'Stormfury Lantern',
      'Price': 1.28,
      'SN': 'Chamirra53'},
     {'Age': 17,
      'Gender': 'Male',
      'Item ID': 124,
      'Item Name': 'Venom Claymore',
      'Price': 2.72,
      'SN': 'Alarap40'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 102,
      'Item Name': 'Avenger',
      'Price': 4.16,
      'SN': 'Ralaeriadeu65'},
     {'Age': 9,
      'Gender': 'Male',
      'Item ID': 71,
      'Item Name': 'Demise',
      'Price': 4.07,
      'SN': 'Reulae52'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 84,
      'Item Name': 'Arcane Gem',
      'Price': 2.23,
      'SN': 'Stryanastip77'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 106,
      'Item Name': 'Crying Steel Sickle',
      'Price': 2.29,
      'SN': 'Iskirra45'},
     {'Age': 30,
      'Gender': 'Male',
      'Item ID': 0,
      'Item Name': 'Splinter',
      'Price': 1.82,
      'SN': 'Chadadarya31'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 182,
      'Item Name': 'Toothpick',
      'Price': 3.48,
      'SN': 'Heuli25'},
     {'Age': 35,
      'Gender': 'Male',
      'Item ID': 34,
      'Item Name': 'Retribution Axe',
      'Price': 4.14,
      'SN': 'Raillydeu47'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 182,
      'Item Name': 'Toothpick',
      'Price': 3.48,
      'SN': 'Chamadar61'},
     {'Age': 34,
      'Gender': 'Other / Non-Disclosed',
      'Item ID': 155,
      'Item Name': 'War-Forged Gold Deflector',
      'Price': 3.73,
      'SN': 'Assassa38'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 97,
      'Item Name': 'Swan Song, Gouger Of Terror',
      'Price': 3.58,
      'SN': 'Shaidanu32'},
     {'Age': 40,
      'Gender': 'Male',
      'Item ID': 70,
      'Item Name': "Hope's End",
      'Price': 3.89,
      'SN': 'Chanosiaya39'},
     {'Age': 18,
      'Gender': 'Female',
      'Item ID': 89,
      'Item Name': 'Blazefury, Protector of Delusions',
      'Price': 1.5,
      'SN': 'Raeri71'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 1,
      'Item Name': 'Crucifer',
      'Price': 2.28,
      'SN': 'Hiasri33'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 130,
      'Item Name': 'Alpha',
      'Price': 1.56,
      'SN': 'Lisossa25'},
     {'Age': 23,
      'Gender': 'Female',
      'Item ID': 87,
      'Item Name': 'Deluge, Edge of the West',
      'Price': 2.2,
      'SN': 'Sundassa93'},
     {'Age': 11,
      'Gender': 'Male',
      'Item ID': 170,
      'Item Name': 'Shadowsteel',
      'Price': 1.98,
      'SN': 'Rina82'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 167,
      'Item Name': 'Malice, Legacy of the Queen',
      'Price': 2.38,
      'SN': 'Siarinum43'},
     {'Age': 40,
      'Gender': 'Male',
      'Item ID': 144,
      'Item Name': 'Blood Infused Guardian',
      'Price': 2.86,
      'SN': 'Chanosiaya39'},
     {'Age': 20,
      'Gender': 'Female',
      'Item ID': 93,
      'Item Name': 'Apocalyptic Battlescythe',
      'Price': 3.91,
      'SN': 'Eurallo89'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 78,
      'Item Name': 'Glimmer, Ender of the Moon',
      'Price': 2.33,
      'SN': 'Hirirap39'},
     {'Age': 35,
      'Gender': 'Male',
      'Item ID': 179,
      'Item Name': 'Wolf, Promise of the Moonwalker',
      'Price': 1.88,
      'SN': 'Raillydeu47'},
     {'Age': 30,
      'Gender': 'Male',
      'Item ID': 36,
      'Item Name': 'Spectral Bone Axe',
      'Price': 2.98,
      'SN': 'Frichaya88'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 75,
      'Item Name': 'Brutality Ivory Warmace',
      'Price': 1.72,
      'SN': 'Aidaira26'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 91,
      'Item Name': 'Celeste',
      'Price': 3.71,
      'SN': 'Zontibe81'},
     {'Age': 19,
      'Gender': 'Male',
      'Item ID': 101,
      'Item Name': 'Final Critic',
      'Price': 4.62,
      'SN': 'Farusrian86'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 39,
      'Item Name': 'Betrayal, Whisper of Grieving Widows',
      'Price': 2.35,
      'SN': 'Undadarla37'},
     {'Age': 14,
      'Gender': 'Male',
      'Item ID': 160,
      'Item Name': 'Azurewrath',
      'Price': 2.22,
      'SN': 'Lirtossa78'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 89,
      'Item Name': 'Blazefury, Protector of Delusions',
      'Price': 1.5,
      'SN': 'Chanirra56'},
     {'Age': 20,
      'Gender': 'Female',
      'Item ID': 65,
      'Item Name': 'Conqueror Adamantite Mace',
      'Price': 1.96,
      'SN': 'Lassast89'},
     {'Age': 18,
      'Gender': 'Male',
      'Item ID': 44,
      'Item Name': 'Bonecarvin Battle Axe',
      'Price': 2.46,
      'SN': 'Lisasi93'},
     {'Age': 30,
      'Gender': 'Female',
      'Item ID': 180,
      'Item Name': 'Stormcaller',
      'Price': 2.78,
      'SN': 'Phadai31'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 143,
      'Item Name': 'Frenzied Scimitar',
      'Price': 2.6,
      'SN': 'Tyithesura58'},
     {'Age': 12,
      'Gender': 'Male',
      'Item ID': 137,
      'Item Name': 'Aetherius, Boon of the Blessed',
      'Price': 4.75,
      'SN': 'Marilsa48'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 176,
      'Item Name': 'Relentless Iron Skewer',
      'Price': 2.97,
      'SN': 'Siarithria38'},
     {'Age': 18,
      'Gender': 'Male',
      'Item ID': 148,
      'Item Name': "Warmonger, Gift of Suffering's End",
      'Price': 3.96,
      'SN': 'Lisasi93'},
     {'Age': 19,
      'Gender': 'Male',
      'Item ID': 127,
      'Item Name': 'Heartseeker, Reaver of Souls',
      'Price': 3.21,
      'SN': 'Marirrasta50'},
     {'Age': 17,
      'Gender': 'Male',
      'Item ID': 147,
      'Item Name': 'Hellreaver, Heirloom of Inception',
      'Price': 3.59,
      'SN': 'Airidil41'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 161,
      'Item Name': 'Devine',
      'Price': 1.45,
      'SN': 'Sausosia74'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 154,
      'Item Name': 'Feral Katana',
      'Price': 2.19,
      'SN': 'Yadanun74'},
     {'Age': 22,
      'Gender': 'Female',
      'Item ID': 13,
      'Item Name': 'Serenity',
      'Price': 1.49,
      'SN': 'Sialaera37'},
     {'Age': 33,
      'Gender': 'Other / Non-Disclosed',
      'Item ID': 157,
      'Item Name': 'Spada, Etcher of Hatred',
      'Price': 2.21,
      'SN': 'Frichistasta59'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 152,
      'Item Name': 'Darkheart',
      'Price': 3.15,
      'SN': 'Phadue96'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 176,
      'Item Name': 'Relentless Iron Skewer',
      'Price': 2.97,
      'SN': 'Chanirra79'},
     {'Age': 40,
      'Gender': 'Male',
      'Item ID': 111,
      'Item Name': "Misery's End",
      'Price': 2.91,
      'SN': 'Yarmol79'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 127,
      'Item Name': 'Heartseeker, Reaver of Souls',
      'Price': 3.21,
      'SN': 'Astydil38'},
     {'Age': 27,
      'Gender': 'Female',
      'Item ID': 148,
      'Item Name': "Warmonger, Gift of Suffering's End",
      'Price': 3.96,
      'SN': 'Jiskirran77'},
     {'Age': 20,
      'Gender': 'Female',
      'Item ID': 154,
      'Item Name': 'Feral Katana',
      'Price': 2.19,
      'SN': 'Marjasksda39'},
     {'Age': 13,
      'Gender': 'Female',
      'Item ID': 116,
      'Item Name': 'Renewed Skeletal Katana',
      'Price': 2.37,
      'SN': 'Eoralphos86'},
     {'Age': 18,
      'Gender': 'Male',
      'Item ID': 106,
      'Item Name': 'Crying Steel Sickle',
      'Price': 2.29,
      'SN': 'Lisovynya38'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 31,
      'Item Name': 'Trickster',
      'Price': 2.07,
      'SN': 'Hailaphos89'},
     {'Age': 27,
      'Gender': 'Male',
      'Item ID': 148,
      'Item Name': "Warmonger, Gift of Suffering's End",
      'Price': 3.96,
      'SN': 'Frichim77'},
     {'Age': 33,
      'Gender': 'Male',
      'Item ID': 152,
      'Item Name': 'Darkheart',
      'Price': 3.15,
      'SN': 'Aellyrialis39'},
     {'Age': 24,
      'Gender': 'Female',
      'Item ID': 61,
      'Item Name': 'Ragnarok',
      'Price': 3.97,
      'SN': 'Chamilsan75'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 131,
      'Item Name': 'Fury',
      'Price': 4.82,
      'SN': 'Saida58'},
     {'Age': 30,
      'Gender': 'Male',
      'Item ID': 41,
      'Item Name': 'Orbit',
      'Price': 1.16,
      'SN': 'Eusri70'},
     {'Age': 26,
      'Gender': 'Male',
      'Item ID': 106,
      'Item Name': 'Crying Steel Sickle',
      'Price': 2.29,
      'SN': 'Aeduera68'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 152,
      'Item Name': 'Darkheart',
      'Price': 3.15,
      'SN': 'Qilatie51'},
     {'Age': 25,
      'Gender': 'Female',
      'Item ID': 92,
      'Item Name': 'Final Critic',
      'Price': 1.36,
      'SN': 'Chamistast30'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 32,
      'Item Name': 'Orenmir',
      'Price': 4.95,
      'SN': 'Qiluard68'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 145,
      'Item Name': 'Fiery Glass Crusader',
      'Price': 4.45,
      'SN': 'Tyaelo67'},
     {'Age': 26,
      'Gender': 'Female',
      'Item ID': 129,
      'Item Name': 'Fate, Vengeance of Eternal Justice',
      'Price': 1.55,
      'SN': 'Rithe77'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 140,
      'Item Name': 'Striker',
      'Price': 3.82,
      'SN': 'Tyeosristi57'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 125,
      'Item Name': 'Whistling Mithril Warblade',
      'Price': 4.32,
      'SN': 'Lassjaskan73'},
     {'Age': 16,
      'Gender': 'Female',
      'Item ID': 60,
      'Item Name': 'Wolf',
      'Price': 1.84,
      'SN': 'Eoral49'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 129,
      'Item Name': 'Fate, Vengeance of Eternal Justice',
      'Price': 1.55,
      'SN': 'Aelollo59'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 123,
      'Item Name': "Twilight's Carver",
      'Price': 1.14,
      'SN': 'Lisossa63'},
     {'Age': 35,
      'Gender': 'Male',
      'Item ID': 162,
      'Item Name': 'Abyssal Shard',
      'Price': 2.04,
      'SN': 'Wailin72'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 154,
      'Item Name': 'Feral Katana',
      'Price': 2.19,
      'SN': 'Yarithllodeu72'},
     {'Age': 7,
      'Gender': 'Male',
      'Item ID': 121,
      'Item Name': 'Massacre',
      'Price': 3.42,
      'SN': 'Lisistaya47'},
     {'Age': 40,
      'Gender': 'Female',
      'Item ID': 49,
      'Item Name': 'The Oculus, Token of Lost Worlds',
      'Price': 4.23,
      'SN': 'Chamadar27'},
     {'Age': 24,
      'Gender': 'Female',
      'Item ID': 58,
      'Item Name': "Freak's Bite, Favor of Holy Might",
      'Price': 3.03,
      'SN': 'Ethruard50'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 121,
      'Item Name': 'Massacre',
      'Price': 3.42,
      'SN': 'Lisossa63'},
     {'Age': 32,
      'Gender': 'Male',
      'Item ID': 135,
      'Item Name': 'Warped Diamond Crusader',
      'Price': 4.66,
      'SN': 'Yathecal72'},
     {'Age': 27,
      'Gender': 'Female',
      'Item ID': 182,
      'Item Name': 'Toothpick',
      'Price': 3.48,
      'SN': 'Ilimya66'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 157,
      'Item Name': 'Spada, Etcher of Hatred',
      'Price': 2.21,
      'SN': 'Ialistidru50'},
     {'Age': 21,
      'Gender': 'Other / Non-Disclosed',
      'Item ID': 183,
      'Item Name': "Dragon's Greatsword",
      'Price': 2.36,
      'SN': 'Tyaerith73'},
     {'Age': 30,
      'Gender': 'Male',
      'Item ID': 8,
      'Item Name': 'Purgatory, Gem of Regret',
      'Price': 3.91,
      'SN': 'Lisistasya93'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 12,
      'Item Name': 'Dawne',
      'Price': 4.3,
      'SN': 'Chamadar79'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 23,
      'Item Name': 'Crucifer',
      'Price': 2.77,
      'SN': 'Haerith37'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 40,
      'Item Name': 'Second Chance',
      'Price': 2.34,
      'SN': 'Iallyphos37'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 15,
      'Item Name': 'Soul Infused Crystal',
      'Price': 1.03,
      'SN': 'Tyaelo67'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 115,
      'Item Name': 'Spectral Diamond Doomblade',
      'Price': 4.25,
      'SN': 'Ilogha82'},
     {'Age': 19,
      'Gender': 'Female',
      'Item ID': 115,
      'Item Name': 'Spectral Diamond Doomblade',
      'Price': 4.25,
      'SN': 'Aeri84'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 1,
      'Item Name': 'Crucifer',
      'Price': 2.28,
      'SN': 'Ilaesudil92'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 149,
      'Item Name': 'Tranquility, Razor of Black Magic',
      'Price': 2.47,
      'SN': 'Meosridil82'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 1,
      'Item Name': 'Crucifer',
      'Price': 2.28,
      'SN': 'Undirrasta89'},
     {'Age': 27,
      'Gender': 'Male',
      'Item ID': 121,
      'Item Name': 'Massacre',
      'Price': 3.42,
      'SN': 'Lirtistanya48'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 17,
      'Item Name': 'Lazarus, Terror of the Earth',
      'Price': 3.47,
      'SN': 'Iadueria43'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 154,
      'Item Name': 'Feral Katana',
      'Price': 2.19,
      'SN': 'Chanirrala39'},
     {'Age': 25,
      'Gender': 'Female',
      'Item ID': 97,
      'Item Name': 'Swan Song, Gouger Of Terror',
      'Price': 3.58,
      'SN': 'Lisjaskan36'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 13,
      'Item Name': 'Serenity',
      'Price': 1.49,
      'SN': 'Saedue76'},
     {'Age': 9,
      'Gender': 'Male',
      'Item ID': 99,
      'Item Name': 'Expiration, Warscythe Of Lost Worlds',
      'Price': 4.53,
      'SN': 'Undjasksya56'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 46,
      'Item Name': 'Hopeless Ebon Dualblade',
      'Price': 4.75,
      'SN': 'Irithrap69'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 29,
      'Item Name': 'Chaos, Ender of the End',
      'Price': 3.79,
      'SN': 'Quanenrian83'},
     {'Age': 18,
      'Gender': 'Male',
      'Item ID': 137,
      'Item Name': 'Aetherius, Boon of the Blessed',
      'Price': 4.75,
      'SN': 'Phenastya51'},
     {'Age': 45,
      'Gender': 'Male',
      'Item ID': 124,
      'Item Name': 'Venom Claymore',
      'Price': 2.72,
      'SN': 'Marassaya49'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 8,
      'Item Name': 'Purgatory, Gem of Regret',
      'Price': 3.91,
      'SN': 'Saellyra72'},
     {'Age': 39,
      'Gender': 'Female',
      'Item ID': 143,
      'Item Name': 'Frenzied Scimitar',
      'Price': 2.6,
      'SN': 'Yasrisu92'},
     {'Age': 33,
      'Gender': 'Other / Non-Disclosed',
      'Item ID': 65,
      'Item Name': 'Conqueror Adamantite Mace',
      'Price': 1.96,
      'SN': 'Frichistasta59'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 36,
      'Item Name': 'Spectral Bone Axe',
      'Price': 2.98,
      'SN': 'Qilanrion65'},
     {'Age': 37,
      'Gender': 'Male',
      'Item ID': 72,
      'Item Name': "Winter's Bite",
      'Price': 1.39,
      'SN': 'Chanassa48'},
     {'Age': 29,
      'Gender': 'Male',
      'Item ID': 114,
      'Item Name': 'Yearning Mageblade',
      'Price': 1.79,
      'SN': 'Iskassa50'},
     {'Age': 7,
      'Gender': 'Male',
      'Item ID': 77,
      'Item Name': 'Piety, Guardian of Riddles',
      'Price': 3.68,
      'SN': 'Frichjaskan98'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 117,
      'Item Name': 'Heartstriker, Legacy of the Light',
      'Price': 4.15,
      'SN': 'Sirira97'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 13,
      'Item Name': 'Serenity',
      'Price': 1.49,
      'SN': 'Eoduenurin62'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 79,
      'Item Name': 'Alpha, Oath of Zeal',
      'Price': 2.88,
      'SN': 'Yarirarn35'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 107,
      'Item Name': 'Splitter, Foe Of Subtlety',
      'Price': 3.61,
      'SN': 'Yadanun74'},
     {'Age': 12,
      'Gender': 'Other / Non-Disclosed',
      'Item ID': 128,
      'Item Name': 'Blazeguard, Reach of Eternity',
      'Price': 4.0,
      'SN': 'Aillycal84'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 128,
      'Item Name': 'Blazeguard, Reach of Eternity',
      'Price': 4.0,
      'SN': 'Eosur70'},
     {'Age': 29,
      'Gender': 'Male',
      'Item ID': 107,
      'Item Name': 'Splitter, Foe Of Subtlety',
      'Price': 3.61,
      'SN': 'Chanadar44'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 171,
      'Item Name': 'Scalpel',
      'Price': 3.62,
      'SN': 'Lisimsda29'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 85,
      'Item Name': 'Malificent Bag',
      'Price': 2.17,
      'SN': 'Tyidue95'},
     {'Age': 40,
      'Gender': 'Male',
      'Item ID': 47,
      'Item Name': 'Alpha, Reach of Ending Hope',
      'Price': 1.55,
      'SN': 'Yaralnura48'},
     {'Age': 29,
      'Gender': 'Male',
      'Item ID': 48,
      'Item Name': 'Rage, Legacy of the Lone Victor',
      'Price': 4.32,
      'SN': 'Irillo49'},
     {'Age': 35,
      'Gender': 'Male',
      'Item ID': 73,
      'Item Name': 'Ritual Mace',
      'Price': 3.74,
      'SN': 'Isri59'},
     {'Age': 25,
      'Gender': 'Female',
      'Item ID': 88,
      'Item Name': 'Emberling, Defender of Delusions',
      'Price': 4.1,
      'SN': 'Lisjaskan36'},
     {'Age': 29,
      'Gender': 'Male',
      'Item ID': 78,
      'Item Name': 'Glimmer, Ender of the Moon',
      'Price': 2.33,
      'SN': 'Aiduecal76'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 54,
      'Item Name': 'Eternal Cleaver',
      'Price': 3.14,
      'SN': 'Frichosiala98'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 170,
      'Item Name': 'Shadowsteel',
      'Price': 1.98,
      'SN': 'Deelilsasya30'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 99,
      'Item Name': 'Expiration, Warscythe Of Lost Worlds',
      'Price': 4.53,
      'SN': 'Mindilsa60'},
     {'Age': 8,
      'Gender': 'Male',
      'Item ID': 79,
      'Item Name': 'Alpha, Oath of Zeal',
      'Price': 2.88,
      'SN': 'Iladarla40'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 104,
      'Item Name': "Gladiator's Glaive",
      'Price': 1.36,
      'SN': 'Chrathybust28'},
     {'Age': 7,
      'Gender': 'Male',
      'Item ID': 53,
      'Item Name': 'Vengeance Cleaver',
      'Price': 3.7,
      'SN': 'Yarithsurgue62'},
     {'Age': 7,
      'Gender': 'Male',
      'Item ID': 121,
      'Item Name': 'Massacre',
      'Price': 3.42,
      'SN': 'Lisistaya47'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 95,
      'Item Name': 'Singed Onyx Warscythe',
      'Price': 1.03,
      'SN': 'Mindossa76'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 64,
      'Item Name': 'Fusion Pummel',
      'Price': 3.58,
      'SN': 'Assilsan72'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 135,
      'Item Name': 'Warped Diamond Crusader',
      'Price': 4.66,
      'SN': 'Frichosiala98'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 70,
      'Item Name': "Hope's End",
      'Price': 3.89,
      'SN': 'Assassa43'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 84,
      'Item Name': 'Arcane Gem',
      'Price': 2.23,
      'SN': 'Yarolwen77'},
     {'Age': 26,
      'Gender': 'Other / Non-Disclosed',
      'Item ID': 141,
      'Item Name': 'Persuasion',
      'Price': 3.27,
      'SN': 'Faralcil63'},
     {'Age': 18,
      'Gender': 'Male',
      'Item ID': 119,
      'Item Name': 'Stormbringer, Dark Blade of Ending Misery',
      'Price': 2.32,
      'SN': 'Sondilsa40'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 99,
      'Item Name': 'Expiration, Warscythe Of Lost Worlds',
      'Price': 4.53,
      'SN': 'Lisossan98'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 44,
      'Item Name': 'Bonecarvin Battle Axe',
      'Price': 2.46,
      'SN': 'Chadossa89'},
     {'Age': 34,
      'Gender': 'Male',
      'Item ID': 183,
      'Item Name': "Dragon's Greatsword",
      'Price': 2.36,
      'SN': 'Eosrirgue62'},
     {'Age': 27,
      'Gender': 'Female',
      'Item ID': 31,
      'Item Name': 'Trickster',
      'Price': 2.07,
      'SN': 'Lassilsa41'},
     {'Age': 31,
      'Gender': 'Male',
      'Item ID': 173,
      'Item Name': 'Stormfury Longsword',
      'Price': 4.83,
      'SN': 'Sondastan54'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 98,
      'Item Name': 'Deadline, Voice Of Subtlety',
      'Price': 3.62,
      'SN': 'Filrion44'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 102,
      'Item Name': 'Avenger',
      'Price': 4.16,
      'SN': 'Lassassasda30'},
     {'Age': 26,
      'Gender': 'Male',
      'Item ID': 180,
      'Item Name': 'Stormcaller',
      'Price': 2.78,
      'SN': 'Aidain51'},
     {'Age': 37,
      'Gender': 'Male',
      'Item ID': 79,
      'Item Name': 'Alpha, Oath of Zeal',
      'Price': 2.88,
      'SN': 'Aduephos78'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 108,
      'Item Name': 'Extraction, Quickblade Of Trembling Hands',
      'Price': 3.39,
      'SN': 'Hainaria90'},
     {'Age': 30,
      'Gender': 'Male',
      'Item ID': 131,
      'Item Name': 'Fury',
      'Price': 4.82,
      'SN': 'Eusri70'},
     {'Age': 18,
      'Gender': 'Male',
      'Item ID': 115,
      'Item Name': 'Spectral Diamond Doomblade',
      'Price': 4.25,
      'SN': 'Raerithsti62'},
     {'Age': 29,
      'Gender': 'Male',
      'Item ID': 68,
      'Item Name': 'Storm-Weaver, Slayer of Inception',
      'Price': 2.49,
      'SN': 'Aerithllora36'},
     {'Age': 20,
      'Gender': 'Female',
      'Item ID': 33,
      'Item Name': 'Curved Axe',
      'Price': 1.35,
      'SN': 'Reuthelis39'},
     {'Age': 22,
      'Gender': 'Female',
      'Item ID': 145,
      'Item Name': 'Fiery Glass Crusader',
      'Price': 4.45,
      'SN': 'Sundaststa26'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 54,
      'Item Name': 'Eternal Cleaver',
      'Price': 3.14,
      'SN': 'Aelin32'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 12,
      'Item Name': 'Dawne',
      'Price': 4.3,
      'SN': 'Sundadarla27'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 173,
      'Item Name': 'Stormfury Longsword',
      'Price': 4.83,
      'SN': 'Aeliru63'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 60,
      'Item Name': 'Wolf',
      'Price': 1.84,
      'SN': 'Mindilsa60'},
     {'Age': 42,
      'Gender': 'Male',
      'Item ID': 110,
      'Item Name': 'Suspension',
      'Price': 2.11,
      'SN': 'Lisista27'},
     {'Age': 23,
      'Gender': 'Female',
      'Item ID': 76,
      'Item Name': 'Haunted Bronzed Bludgeon',
      'Price': 4.12,
      'SN': 'Narirra38'},
     {'Age': 18,
      'Gender': 'Male',
      'Item ID': 137,
      'Item Name': 'Aetherius, Boon of the Blessed',
      'Price': 4.75,
      'SN': 'Eustyria89'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 29,
      'Item Name': 'Chaos, Ender of the End',
      'Price': 3.79,
      'SN': 'Phistym51'},
     {'Age': 23,
      'Gender': 'Female',
      'Item ID': 130,
      'Item Name': 'Alpha',
      'Price': 1.56,
      'SN': 'Salilis27'},
     {'Age': 27,
      'Gender': 'Male',
      'Item ID': 102,
      'Item Name': 'Avenger',
      'Price': 4.16,
      'SN': 'Layjask75'},
     {'Age': 24,
      'Gender': 'Female',
      'Item ID': 47,
      'Item Name': 'Alpha, Reach of Ending Hope',
      'Price': 1.55,
      'SN': 'Tyaeristi78'},
     {'Age': 19,
      'Gender': 'Male',
      'Item ID': 60,
      'Item Name': 'Wolf',
      'Price': 1.84,
      'SN': 'Lirtyrdesta65'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 7,
      'Item Name': 'Thorn, Satchel of Dark Souls',
      'Price': 4.51,
      'SN': 'Syalollorap93'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 125,
      'Item Name': 'Whistling Mithril Warblade',
      'Price': 4.32,
      'SN': 'Assylla81'},
     {'Age': 27,
      'Gender': 'Other / Non-Disclosed',
      'Item ID': 61,
      'Item Name': 'Ragnarok',
      'Price': 3.97,
      'SN': 'Eurisuru25'},
     {'Age': 23,
      'Gender': 'Female',
      'Item ID': 12,
      'Item Name': 'Dawne',
      'Price': 4.3,
      'SN': 'Narirra38'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 70,
      'Item Name': "Hope's End",
      'Price': 3.89,
      'SN': 'Mindjasksya61'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 50,
      'Item Name': 'Dawn',
      'Price': 2.55,
      'SN': 'Eusri44'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 30,
      'Item Name': 'Stormcaller',
      'Price': 4.15,
      'SN': 'Aeliru63'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 15,
      'Item Name': 'Soul Infused Crystal',
      'Price': 1.03,
      'SN': 'Rarith48'},
     {'Age': 16,
      'Gender': 'Male',
      'Item ID': 179,
      'Item Name': 'Wolf, Promise of the Moonwalker',
      'Price': 1.88,
      'SN': 'Yalaeria91'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 173,
      'Item Name': 'Stormfury Longsword',
      'Price': 4.83,
      'SN': 'Iskadarya95'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 140,
      'Item Name': 'Striker',
      'Price': 3.82,
      'SN': 'Saedue76'},
     {'Age': 17,
      'Gender': 'Male',
      'Item ID': 84,
      'Item Name': 'Arcane Gem',
      'Price': 2.23,
      'SN': 'Lisossanya98'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 57,
      'Item Name': 'Despair, Favor of Due Diligence',
      'Price': 3.81,
      'SN': 'Iarithdil76'},
     {'Age': 16,
      'Gender': 'Male',
      'Item ID': 169,
      'Item Name': 'Interrogator, Blood Blade of the Queen',
      'Price': 3.32,
      'SN': 'Chanosia60'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 9,
      'Item Name': 'Thorn, Conqueror of the Corrupted',
      'Price': 2.04,
      'SN': 'Aeliriarin93'},
     {'Age': 15,
      'Gender': 'Female',
      'Item ID': 50,
      'Item Name': 'Dawn',
      'Price': 2.55,
      'SN': 'Raedalis34'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 33,
      'Item Name': 'Curved Axe',
      'Price': 1.35,
      'SN': 'Meosridil82'},
     {'Age': 12,
      'Gender': 'Male',
      'Item ID': 66,
      'Item Name': 'Victor Iron Spikes',
      'Price': 3.55,
      'SN': 'Sondossa55'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 15,
      'Item Name': 'Soul Infused Crystal',
      'Price': 1.03,
      'SN': 'Iadueria43'},
     {'Age': 17,
      'Gender': 'Male',
      'Item ID': 14,
      'Item Name': 'Possessed Core',
      'Price': 1.59,
      'SN': 'Lisico81'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 146,
      'Item Name': 'Warped Iron Scimitar',
      'Price': 4.08,
      'SN': 'Ialo60'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 177,
      'Item Name': 'Winterthorn, Defender of Shifting Worlds',
      'Price': 4.89,
      'SN': 'Syathe73'},
     {'Age': 33,
      'Gender': 'Male',
      'Item ID': 166,
      'Item Name': 'Thirsty Iron Reaver',
      'Price': 4.25,
      'SN': 'Lisassa26'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 93,
      'Item Name': 'Apocalyptic Battlescythe',
      'Price': 3.91,
      'SN': 'Rasrirgue43'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 179,
      'Item Name': 'Wolf, Promise of the Moonwalker',
      'Price': 1.88,
      'SN': 'Aerillorin70'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 56,
      'Item Name': 'Foul Titanium Battle Axe',
      'Price': 4.33,
      'SN': 'Quelatarn54'},
     {'Age': 31,
      'Gender': 'Female',
      'Item ID': 22,
      'Item Name': 'Amnesia',
      'Price': 3.57,
      'SN': 'Airithrin43'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 84,
      'Item Name': 'Arcane Gem',
      'Price': 2.23,
      'SN': 'Mindirra92'},
     {'Age': 26,
      'Gender': 'Female',
      'Item ID': 85,
      'Item Name': 'Malificent Bag',
      'Price': 2.17,
      'SN': 'Lisjasksda68'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 172,
      'Item Name': 'Blade of the Grave',
      'Price': 1.69,
      'SN': 'Aerithnuphos61'},
     {'Age': 40,
      'Gender': 'Male',
      'Item ID': 65,
      'Item Name': 'Conqueror Adamantite Mace',
      'Price': 1.96,
      'SN': 'Sundast29'},
     {'Age': 14,
      'Gender': 'Male',
      'Item ID': 87,
      'Item Name': 'Deluge, Edge of the West',
      'Price': 2.2,
      'SN': 'Lirtosia72'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 32,
      'Item Name': 'Orenmir',
      'Price': 4.95,
      'SN': 'Aeliriam77'},
     {'Age': 7,
      'Gender': 'Female',
      'Item ID': 21,
      'Item Name': 'Souleater',
      'Price': 3.27,
      'SN': 'Lisirra55'},
     {'Age': 14,
      'Gender': 'Male',
      'Item ID': 39,
      'Item Name': 'Betrayal, Whisper of Grieving Widows',
      'Price': 2.35,
      'SN': 'Aeral97'},
     {'Age': 36,
      'Gender': 'Male',
      'Item ID': 39,
      'Item Name': 'Betrayal, Whisper of Grieving Widows',
      'Price': 2.35,
      'SN': 'Lisosiast26'},
     {'Age': 32,
      'Gender': 'Male',
      'Item ID': 16,
      'Item Name': 'Restored Bauble',
      'Price': 3.11,
      'SN': 'Yathecal72'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 31,
      'Item Name': 'Trickster',
      'Price': 2.07,
      'SN': 'Lirtistasta79'},
     {'Age': 31,
      'Gender': 'Male',
      'Item ID': 67,
      'Item Name': 'Celeste, Incarnation of the Corrupted',
      'Price': 2.31,
      'SN': 'Lisadar44'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 133,
      'Item Name': "Faith's Scimitar",
      'Price': 3.82,
      'SN': 'Jiskossa51'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 100,
      'Item Name': 'Blindscythe',
      'Price': 3.66,
      'SN': 'Qilatie51'},
     {'Age': 30,
      'Gender': 'Male',
      'Item ID': 153,
      'Item Name': 'Mercenary Sabre',
      'Price': 4.57,
      'SN': 'Eusri70'},
     {'Age': 18,
      'Gender': 'Female',
      'Item ID': 118,
      'Item Name': 'Ghost Reaver, Longsword of Magic',
      'Price': 2.77,
      'SN': 'Isurria36'},
     {'Age': 7,
      'Gender': 'Male',
      'Item ID': 151,
      'Item Name': 'Severance',
      'Price': 1.85,
      'SN': 'Sundastnya66'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 81,
      'Item Name': 'Dreamkiss',
      'Price': 4.06,
      'SN': 'Raesursurap33'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 94,
      'Item Name': 'Mourning Blade',
      'Price': 1.82,
      'SN': 'Sondassasya91'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 114,
      'Item Name': 'Yearning Mageblade',
      'Price': 1.79,
      'SN': 'Ermol76'},
     {'Age': 7,
      'Gender': 'Female',
      'Item ID': 77,
      'Item Name': 'Piety, Guardian of Riddles',
      'Price': 3.68,
      'SN': 'Eosurdru76'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 42,
      'Item Name': 'The Decapitator',
      'Price': 4.82,
      'SN': 'Yadaisuir65'},
     {'Age': 17,
      'Gender': 'Male',
      'Item ID': 33,
      'Item Name': 'Curved Axe',
      'Price': 1.35,
      'SN': 'Zhisrisu83'},
     {'Age': 37,
      'Gender': 'Male',
      'Item ID': 174,
      'Item Name': 'Primitive Blade',
      'Price': 2.46,
      'SN': 'Aduephos78'},
     {'Age': 30,
      'Gender': 'Male',
      'Item ID': 69,
      'Item Name': 'Frenzy, Defender of the Harvest',
      'Price': 1.06,
      'SN': 'Sondassa68'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 141,
      'Item Name': 'Persuasion',
      'Price': 3.27,
      'SN': 'Chamirraya83'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 34,
      'Item Name': 'Retribution Axe',
      'Price': 4.14,
      'SN': 'Alaephos75'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 166,
      'Item Name': 'Thirsty Iron Reaver',
      'Price': 4.25,
      'SN': 'Haellysu29'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 39,
      'Item Name': 'Betrayal, Whisper of Grieving Widows',
      'Price': 2.35,
      'SN': 'Yarithphos28'},
     {'Age': 7,
      'Gender': 'Male',
      'Item ID': 66,
      'Item Name': 'Victor Iron Spikes',
      'Price': 3.55,
      'SN': 'Ingatcil75'},
     {'Age': 30,
      'Gender': 'Male',
      'Item ID': 143,
      'Item Name': 'Frenzied Scimitar',
      'Price': 2.6,
      'SN': 'Eothe56'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 158,
      'Item Name': 'Darkheart, Butcher of the Champion',
      'Price': 3.56,
      'SN': 'Haerith37'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 107,
      'Item Name': 'Splitter, Foe Of Subtlety',
      'Price': 3.61,
      'SN': 'Assithasta65'},
     {'Age': 24,
      'Gender': 'Female',
      'Item ID': 51,
      'Item Name': 'Endbringer',
      'Price': 2.67,
      'SN': 'Ethruard50'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 32,
      'Item Name': 'Orenmir',
      'Price': 4.95,
      'SN': 'Palurrian69'},
     {'Age': 37,
      'Gender': 'Male',
      'Item ID': 34,
      'Item Name': 'Retribution Axe',
      'Price': 4.14,
      'SN': 'Iskistasda86'},
     {'Age': 17,
      'Gender': 'Female',
      'Item ID': 86,
      'Item Name': 'Stormfury Lantern',
      'Price': 1.28,
      'SN': 'Tyaili86'},
     {'Age': 32,
      'Gender': 'Male',
      'Item ID': 141,
      'Item Name': 'Persuasion',
      'Price': 3.27,
      'SN': 'Liawista80'},
     {'Age': 35,
      'Gender': 'Male',
      'Item ID': 159,
      'Item Name': 'Oathbreaker, Spellblade of Trials',
      'Price': 3.01,
      'SN': 'Seosri62'},
     {'Age': 9,
      'Gender': 'Male',
      'Item ID': 16,
      'Item Name': 'Restored Bauble',
      'Price': 3.11,
      'SN': 'Silinu63'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 44,
      'Item Name': 'Bonecarvin Battle Axe',
      'Price': 2.46,
      'SN': 'Aela49'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 38,
      'Item Name': 'The Void, Vengeance of Dark Magic',
      'Price': 2.82,
      'SN': 'Assosiasta83'},
     {'Age': 40,
      'Gender': 'Female',
      'Item ID': 77,
      'Item Name': 'Piety, Guardian of Riddles',
      'Price': 3.68,
      'SN': 'Saelollop56'},
     {'Age': 35,
      'Gender': 'Female',
      'Item ID': 108,
      'Item Name': 'Extraction, Quickblade Of Trembling Hands',
      'Price': 3.39,
      'SN': 'Saena74'},
     {'Age': 25,
      'Gender': 'Female',
      'Item ID': 96,
      'Item Name': 'Blood-Forged Skeletal Spine',
      'Price': 4.77,
      'SN': 'Tyaelistidru84'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 82,
      'Item Name': 'Nirvana',
      'Price': 1.11,
      'SN': 'Chamirrasya33'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 27,
      'Item Name': 'Riddle, Tribute of Ended Dreams',
      'Price': 3.96,
      'SN': 'Smecherdi88'},
     {'Age': 17,
      'Gender': 'Male',
      'Item ID': 121,
      'Item Name': 'Massacre',
      'Price': 3.42,
      'SN': 'Leulaesti78'},
     {'Age': 8,
      'Gender': 'Male',
      'Item ID': 65,
      'Item Name': 'Conqueror Adamantite Mace',
      'Price': 1.96,
      'SN': 'Tyaenasti87'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 113,
      'Item Name': "Solitude's Reaver",
      'Price': 2.67,
      'SN': 'Sondassa48'},
     {'Age': 11,
      'Gender': 'Female',
      'Item ID': 46,
      'Item Name': 'Hopeless Ebon Dualblade',
      'Price': 4.75,
      'SN': 'Deural48'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 76,
      'Item Name': 'Haunted Bronzed Bludgeon',
      'Price': 4.12,
      'SN': 'Saistydru69'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 39,
      'Item Name': 'Betrayal, Whisper of Grieving Widows',
      'Price': 2.35,
      'SN': 'Chamosia29'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 108,
      'Item Name': 'Extraction, Quickblade Of Trembling Hands',
      'Price': 3.39,
      'SN': 'Saisrilis27'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 106,
      'Item Name': 'Crying Steel Sickle',
      'Price': 2.29,
      'SN': 'Indonmol95'},
     {'Age': 20,
      'Gender': 'Female',
      'Item ID': 45,
      'Item Name': 'Glinting Glass Edge',
      'Price': 2.46,
      'SN': 'Fironon91'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 27,
      'Item Name': 'Riddle, Tribute of Ended Dreams',
      'Price': 3.96,
      'SN': 'Ryanara76'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 7,
      'Item Name': 'Thorn, Satchel of Dark Souls',
      'Price': 4.51,
      'SN': 'Saedue76'},
     {'Age': 24,
      'Gender': 'Female',
      'Item ID': 114,
      'Item Name': 'Yearning Mageblade',
      'Price': 1.79,
      'SN': 'Lirtossanya27'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 34,
      'Item Name': 'Retribution Axe',
      'Price': 4.14,
      'SN': 'Sondadar26'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 10,
      'Item Name': 'Sleepwalker',
      'Price': 1.73,
      'SN': 'Phalinun47'},
     {'Age': 25,
      'Gender': 'Female',
      'Item ID': 92,
      'Item Name': 'Final Critic',
      'Price': 1.36,
      'SN': 'Chamistast30'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 84,
      'Item Name': 'Arcane Gem',
      'Price': 2.23,
      'SN': 'Hiarideu73'},
     {'Age': 16,
      'Gender': 'Male',
      'Item ID': 119,
      'Item Name': 'Stormbringer, Dark Blade of Ending Misery',
      'Price': 2.32,
      'SN': 'Qilunan34'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 66,
      'Item Name': 'Victor Iron Spikes',
      'Price': 3.55,
      'SN': 'Pharithdil38'},
     {'Age': 25,
      'Gender': 'Female',
      'Item ID': 42,
      'Item Name': 'The Decapitator',
      'Price': 4.82,
      'SN': 'Tyeuladeu30'},
     {'Age': 31,
      'Gender': 'Male',
      'Item ID': 170,
      'Item Name': 'Shadowsteel',
      'Price': 1.98,
      'SN': 'Sondastan54'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 150,
      'Item Name': 'Deathraze',
      'Price': 4.54,
      'SN': 'Ina92'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 164,
      'Item Name': 'Exiled Doomblade',
      'Price': 1.92,
      'SN': 'Saida58'},
     {'Age': 32,
      'Gender': 'Other / Non-Disclosed',
      'Item ID': 29,
      'Item Name': 'Chaos, Ender of the End',
      'Price': 3.79,
      'SN': 'Aithelis62'},
     {'Age': 40,
      'Gender': 'Male',
      'Item ID': 139,
      'Item Name': 'Mercy, Katana of Dismay',
      'Price': 4.37,
      'SN': 'Indcil77'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 14,
      'Item Name': 'Possessed Core',
      'Price': 1.59,
      'SN': 'Hallysucal81'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 152,
      'Item Name': 'Darkheart',
      'Price': 3.15,
      'SN': 'Tyeuduephos81'},
     {'Age': 19,
      'Gender': 'Male',
      'Item ID': 131,
      'Item Name': 'Fury',
      'Price': 4.82,
      'SN': 'Heosrisuir72'},
     {'Age': 37,
      'Gender': 'Female',
      'Item ID': 175,
      'Item Name': 'Woeful Adamantite Claymore',
      'Price': 1.24,
      'SN': 'Chadossa56'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 82,
      'Item Name': 'Nirvana',
      'Price': 1.11,
      'SN': 'Hailaphos89'},
     {'Age': 27,
      'Gender': 'Male',
      'Item ID': 74,
      'Item Name': 'Yearning Crusher',
      'Price': 1.06,
      'SN': 'Lirtassa47'},
     {'Age': 37,
      'Gender': 'Male',
      'Item ID': 92,
      'Item Name': 'Final Critic',
      'Price': 1.36,
      'SN': 'Aduephos78'},
     {'Age': 18,
      'Gender': 'Male',
      'Item ID': 20,
      'Item Name': 'Netherbane',
      'Price': 1.48,
      'SN': 'Sondilsa40'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 180,
      'Item Name': 'Stormcaller',
      'Price': 2.78,
      'SN': 'Ithesuphos68'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 98,
      'Item Name': 'Deadline, Voice Of Subtlety',
      'Price': 3.62,
      'SN': 'Eula35'},
     {'Age': 27,
      'Gender': 'Female',
      'Item ID': 159,
      'Item Name': 'Oathbreaker, Spellblade of Trials',
      'Price': 3.01,
      'SN': 'Aina42'},
     {'Age': 10,
      'Gender': 'Male',
      'Item ID': 131,
      'Item Name': 'Fury',
      'Price': 4.82,
      'SN': 'Ethrusuard41'},
     {'Age': 17,
      'Gender': 'Male',
      'Item ID': 82,
      'Item Name': 'Nirvana',
      'Price': 1.11,
      'SN': 'Zhisrisu83'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 111,
      'Item Name': "Misery's End",
      'Price': 2.91,
      'SN': 'Isursti83'},
     {'Age': 19,
      'Gender': 'Male',
      'Item ID': 41,
      'Item Name': 'Orbit',
      'Price': 1.16,
      'SN': 'Chanirrasta87'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 84,
      'Item Name': 'Arcane Gem',
      'Price': 2.23,
      'SN': 'Stryanastip77'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 107,
      'Item Name': 'Splitter, Foe Of Subtlety',
      'Price': 3.61,
      'SN': 'Ilirrasda54'},
     {'Age': 7,
      'Gender': 'Male',
      'Item ID': 34,
      'Item Name': 'Retribution Axe',
      'Price': 4.14,
      'SN': 'Liri91'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 8,
      'Item Name': 'Purgatory, Gem of Regret',
      'Price': 3.91,
      'SN': 'Undadar97'},
     {'Age': 20,
      'Gender': 'Female',
      'Item ID': 179,
      'Item Name': 'Wolf, Promise of the Moonwalker',
      'Price': 1.88,
      'SN': 'Ithergue48'},
     {'Age': 32,
      'Gender': 'Female',
      'Item ID': 95,
      'Item Name': 'Singed Onyx Warscythe',
      'Price': 1.03,
      'SN': 'Saistyphos30'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 47,
      'Item Name': 'Alpha, Reach of Ending Hope',
      'Price': 1.55,
      'SN': 'Lisosianya62'},
     {'Age': 25,
      'Gender': 'Female',
      'Item ID': 6,
      'Item Name': 'Rusty Skull',
      'Price': 1.2,
      'SN': 'Tyaelistidru84'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 34,
      'Item Name': 'Retribution Axe',
      'Price': 4.14,
      'SN': 'Sausosia74'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 123,
      'Item Name': "Twilight's Carver",
      'Price': 1.14,
      'SN': 'Frichosiala98'},
     {'Age': 39,
      'Gender': 'Female',
      'Item ID': 140,
      'Item Name': 'Striker',
      'Price': 3.82,
      'SN': 'Mindimnya67'},
     {'Age': 12,
      'Gender': 'Male',
      'Item ID': 163,
      'Item Name': 'Thunderfury Scimitar',
      'Price': 3.02,
      'SN': 'Undistasta86'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 172,
      'Item Name': 'Blade of the Grave',
      'Price': 1.69,
      'SN': 'Lirtistasta79'},
     {'Age': 18,
      'Gender': 'Female',
      'Item ID': 95,
      'Item Name': 'Singed Onyx Warscythe',
      'Price': 1.03,
      'SN': 'Alaesu91'},
     {'Age': 9,
      'Gender': 'Female',
      'Item ID': 100,
      'Item Name': 'Blindscythe',
      'Price': 3.66,
      'SN': 'Jiskosiala43'},
     {'Age': 30,
      'Gender': 'Male',
      'Item ID': 137,
      'Item Name': 'Aetherius, Boon of the Blessed',
      'Price': 4.75,
      'SN': 'Heuralsti66'},
     {'Age': 23,
      'Gender': 'Female',
      'Item ID': 66,
      'Item Name': 'Victor Iron Spikes',
      'Price': 3.55,
      'SN': 'Umuard36'},
     {'Age': 29,
      'Gender': 'Male',
      'Item ID': 68,
      'Item Name': 'Storm-Weaver, Slayer of Inception',
      'Price': 2.49,
      'SN': 'Asur53'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 92,
      'Item Name': 'Final Critic',
      'Price': 1.36,
      'SN': 'Jiskassa76'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 124,
      'Item Name': 'Venom Claymore',
      'Price': 2.72,
      'SN': 'Thryallym62'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 5,
      'Item Name': 'Putrid Fan',
      'Price': 1.32,
      'SN': 'Raesty92'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 69,
      'Item Name': 'Frenzy, Defender of the Harvest',
      'Price': 1.06,
      'SN': 'Frichassala85'},
     {'Age': 24,
      'Gender': 'Female',
      'Item ID': 90,
      'Item Name': 'Betrayer',
      'Price': 1.67,
      'SN': 'Chamilsan75'},
     {'Age': 33,
      'Gender': 'Male',
      'Item ID': 38,
      'Item Name': 'The Void, Vengeance of Dark Magic',
      'Price': 2.82,
      'SN': 'Ilosu82'},
     {'Age': 39,
      'Gender': 'Female',
      'Item ID': 163,
      'Item Name': 'Thunderfury Scimitar',
      'Price': 3.02,
      'SN': 'Mindimnya67'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 20,
      'Item Name': 'Netherbane',
      'Price': 1.48,
      'SN': 'Pheodai94'},
     {'Age': 18,
      'Gender': 'Male',
      'Item ID': 11,
      'Item Name': 'Brimstone',
      'Price': 2.52,
      'SN': 'Raerithsti62'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 41,
      'Item Name': 'Orbit',
      'Price': 1.16,
      'SN': 'Undirrasta74'},
     {'Age': 25,
      'Gender': 'Female',
      'Item ID': 103,
      'Item Name': 'Singed Scalpel',
      'Price': 4.87,
      'SN': 'Hiasur92'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 19,
      'Item Name': 'Pursuit, Cudgel of Necromancy',
      'Price': 3.98,
      'SN': 'Tillyrin30'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 134,
      'Item Name': 'Undead Crusader',
      'Price': 4.67,
      'SN': 'Riralsti91'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 103,
      'Item Name': 'Singed Scalpel',
      'Price': 4.87,
      'SN': 'Iasur80'},
     {'Age': 15,
      'Gender': 'Female',
      'Item ID': 110,
      'Item Name': 'Suspension',
      'Price': 2.11,
      'SN': 'Eryon48'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 146,
      'Item Name': 'Warped Iron Scimitar',
      'Price': 4.08,
      'SN': 'Whaestysu86'},
     {'Age': 29,
      'Gender': 'Female',
      'Item ID': 35,
      'Item Name': 'Heartless Bone Dualblade',
      'Price': 2.63,
      'SN': 'Aiduesu83'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 105,
      'Item Name': 'Hailstorm Shadowsteel Scythe',
      'Price': 3.73,
      'SN': 'Iaralsuir44'},
     {'Age': 36,
      'Gender': 'Male',
      'Item ID': 31,
      'Item Name': 'Trickster',
      'Price': 2.07,
      'SN': 'Chanjask65'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 158,
      'Item Name': 'Darkheart, Butcher of the Champion',
      'Price': 3.56,
      'SN': 'Frichistast39'},
     {'Age': 40,
      'Gender': 'Male',
      'Item ID': 168,
      'Item Name': 'Sun Strike, Jaws of Twisted Visions',
      'Price': 2.64,
      'SN': 'Yaralnura48'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 48,
      'Item Name': 'Rage, Legacy of the Lone Victor',
      'Price': 4.32,
      'SN': 'Isursti83'},
     {'Age': 17,
      'Gender': 'Male',
      'Item ID': 128,
      'Item Name': 'Blazeguard, Reach of Eternity',
      'Price': 4.0,
      'SN': 'Phairinum94'},
     {'Age': 27,
      'Gender': 'Male',
      'Item ID': 151,
      'Item Name': 'Severance',
      'Price': 1.85,
      'SN': 'Ethralan59'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 165,
      'Item Name': 'Bone Crushing Silver Skewer',
      'Price': 3.37,
      'SN': 'Raelly43'},
     {'Age': 33,
      'Gender': 'Female',
      'Item ID': 22,
      'Item Name': 'Amnesia',
      'Price': 3.57,
      'SN': 'Lisassasta50'},
     {'Age': 25,
      'Gender': 'Female',
      'Item ID': 104,
      'Item Name': "Gladiator's Glaive",
      'Price': 1.36,
      'SN': 'Chanastnya43'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 85,
      'Item Name': 'Malificent Bag',
      'Price': 2.17,
      'SN': 'Sondimla25'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 136,
      'Item Name': 'Ghastly Adamantite Protector',
      'Price': 3.3,
      'SN': 'Chamilsala65'},
     {'Age': 30,
      'Gender': 'Male',
      'Item ID': 103,
      'Item Name': 'Singed Scalpel',
      'Price': 4.87,
      'SN': 'Idaria87'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 76,
      'Item Name': 'Haunted Bronzed Bludgeon',
      'Price': 4.12,
      'SN': 'Eoda93'},
     {'Age': 27,
      'Gender': 'Male',
      'Item ID': 21,
      'Item Name': 'Souleater',
      'Price': 3.27,
      'SN': 'Chanastst38'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 40,
      'Item Name': 'Second Chance',
      'Price': 2.34,
      'SN': 'Lamil79'},
     {'Age': 7,
      'Gender': 'Male',
      'Item ID': 161,
      'Item Name': 'Devine',
      'Price': 1.45,
      'SN': 'Liri91'},
     {'Age': 17,
      'Gender': 'Male',
      'Item ID': 22,
      'Item Name': 'Amnesia',
      'Price': 3.57,
      'SN': 'Qaronon57'},
     {'Age': 36,
      'Gender': 'Male',
      'Item ID': 57,
      'Item Name': 'Despair, Favor of Due Diligence',
      'Price': 3.81,
      'SN': 'Chadjask77'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 52,
      'Item Name': 'Hatred',
      'Price': 4.39,
      'SN': 'Ethralista69'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 49,
      'Item Name': 'The Oculus, Token of Lost Worlds',
      'Price': 4.23,
      'SN': 'Phaeduesurgue38'},
     {'Age': 25,
      'Gender': 'Female',
      'Item ID': 95,
      'Item Name': 'Singed Onyx Warscythe',
      'Price': 1.03,
      'SN': 'Rathellorin54'},
     {'Age': 38,
      'Gender': 'Male',
      'Item ID': 40,
      'Item Name': 'Second Chance',
      'Price': 2.34,
      'SN': 'Filon68'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 160,
      'Item Name': 'Azurewrath',
      'Price': 2.22,
      'SN': 'Chamilsala65'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 1,
      'Item Name': 'Crucifer',
      'Price': 2.28,
      'SN': 'Assylla81'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 79,
      'Item Name': 'Alpha, Oath of Zeal',
      'Price': 2.88,
      'SN': 'Ingonon91'},
     {'Age': 18,
      'Gender': 'Male',
      'Item ID': 144,
      'Item Name': 'Blood Infused Guardian',
      'Price': 2.86,
      'SN': 'Lisovynya38'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 10,
      'Item Name': 'Sleepwalker',
      'Price': 1.73,
      'SN': 'Assesi91'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 125,
      'Item Name': 'Whistling Mithril Warblade',
      'Price': 4.32,
      'SN': 'Aellyria80'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 176,
      'Item Name': 'Relentless Iron Skewer',
      'Price': 2.97,
      'SN': 'Aethedru70'},
     {'Age': 8,
      'Gender': 'Male',
      'Item ID': 15,
      'Item Name': 'Soul Infused Crystal',
      'Price': 1.03,
      'SN': 'Iladarla40'},
     {'Age': 29,
      'Gender': 'Male',
      'Item ID': 180,
      'Item Name': 'Stormcaller',
      'Price': 2.78,
      'SN': 'Tyalaesu89'},
     {'Age': 16,
      'Gender': 'Male',
      'Item ID': 161,
      'Item Name': 'Devine',
      'Price': 1.45,
      'SN': 'Erudrion71'},
     {'Age': 38,
      'Gender': 'Male',
      'Item ID': 181,
      'Item Name': "Reaper's Toll",
      'Price': 4.56,
      'SN': 'Tyisriphos58'},
     {'Age': 28,
      'Gender': 'Male',
      'Item ID': 92,
      'Item Name': 'Final Critic',
      'Price': 1.36,
      'SN': 'Iskista88'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 133,
      'Item Name': "Faith's Scimitar",
      'Price': 3.82,
      'SN': 'Seudaillorap38'},
     {'Age': 12,
      'Gender': 'Male',
      'Item ID': 70,
      'Item Name': "Hope's End",
      'Price': 3.89,
      'SN': 'Sondossa55'},
     {'Age': 19,
      'Gender': 'Male',
      'Item ID': 108,
      'Item Name': 'Extraction, Quickblade Of Trembling Hands',
      'Price': 3.39,
      'SN': 'Tyirithnu40'},
     {'Age': 13,
      'Gender': 'Male',
      'Item ID': 159,
      'Item Name': 'Oathbreaker, Spellblade of Trials',
      'Price': 3.01,
      'SN': 'Malista67'},
     {'Age': 33,
      'Gender': 'Male',
      'Item ID': 120,
      'Item Name': 'Agatha',
      'Price': 1.91,
      'SN': 'Ristydru66'},
     {'Age': 40,
      'Gender': 'Male',
      'Item ID': 11,
      'Item Name': 'Brimstone',
      'Price': 2.52,
      'SN': 'Yasriphos60'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 111,
      'Item Name': "Misery's End",
      'Price': 2.91,
      'SN': 'Phainasu47'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 81,
      'Item Name': 'Dreamkiss',
      'Price': 4.06,
      'SN': 'Eural50'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 31,
      'Item Name': 'Trickster',
      'Price': 2.07,
      'SN': 'Mindassast27'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 62,
      'Item Name': 'Piece Maker',
      'Price': 4.36,
      'SN': 'Iskossan49'},
     {'Age': 30,
      'Gender': 'Male',
      'Item ID': 145,
      'Item Name': 'Fiery Glass Crusader',
      'Price': 4.45,
      'SN': 'Qarrian82'},
     {'Age': 16,
      'Gender': 'Female',
      'Item ID': 170,
      'Item Name': 'Shadowsteel',
      'Price': 1.98,
      'SN': 'Eulidru49'},
     {'Age': 38,
      'Gender': 'Male',
      'Item ID': 148,
      'Item Name': "Warmonger, Gift of Suffering's End",
      'Price': 3.96,
      'SN': 'Inguard95'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 161,
      'Item Name': 'Devine',
      'Price': 1.45,
      'SN': 'Hiral75'},
     {'Age': 16,
      'Gender': 'Male',
      'Item ID': 162,
      'Item Name': 'Abyssal Shard',
      'Price': 2.04,
      'SN': 'Undast38'},
     {'Age': 36,
      'Gender': 'Male',
      'Item ID': 182,
      'Item Name': 'Toothpick',
      'Price': 3.48,
      'SN': 'Chadjask77'},
     {'Age': 17,
      'Gender': 'Female',
      'Item ID': 143,
      'Item Name': 'Frenzied Scimitar',
      'Price': 2.6,
      'SN': 'Marim28'},
     {'Age': 40,
      'Gender': 'Male',
      'Item ID': 55,
      'Item Name': 'Vindictive Glass Edge',
      'Price': 4.26,
      'SN': 'Yasriphos60'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 22,
      'Item Name': 'Amnesia',
      'Price': 3.57,
      'SN': 'Ialistidru50'},
     {'Age': 38,
      'Gender': 'Male',
      'Item ID': 172,
      'Item Name': 'Blade of the Grave',
      'Price': 1.69,
      'SN': 'Aelalis34'},
     {'Age': 35,
      'Gender': 'Male',
      'Item ID': 113,
      'Item Name': "Solitude's Reaver",
      'Price': 2.67,
      'SN': 'Airal46'},
     {'Age': 14,
      'Gender': 'Male',
      'Item ID': 80,
      'Item Name': 'Dreamsong',
      'Price': 3.81,
      'SN': 'Lirtosia72'},
     {'Age': 17,
      'Gender': 'Female',
      'Item ID': 177,
      'Item Name': 'Winterthorn, Defender of Shifting Worlds',
      'Price': 4.89,
      'SN': 'Assassasta79'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 183,
      'Item Name': "Dragon's Greatsword",
      'Price': 2.36,
      'SN': 'Saerallora71'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 98,
      'Item Name': 'Deadline, Voice Of Subtlety',
      'Price': 3.62,
      'SN': 'Frichossast86'},
     {'Age': 23,
      'Gender': 'Female',
      'Item ID': 30,
      'Item Name': 'Stormcaller',
      'Price': 4.15,
      'SN': 'Undirra73'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 145,
      'Item Name': 'Fiery Glass Crusader',
      'Price': 4.45,
      'SN': 'Chanastsda67'},
     {'Age': 29,
      'Gender': 'Male',
      'Item ID': 18,
      'Item Name': 'Torchlight, Bond of Storms',
      'Price': 1.77,
      'SN': 'Undirrala66'},
     {'Age': 14,
      'Gender': 'Male',
      'Item ID': 183,
      'Item Name': "Dragon's Greatsword",
      'Price': 2.36,
      'SN': 'Lirtosia72'},
     {'Age': 31,
      'Gender': 'Male',
      'Item ID': 171,
      'Item Name': 'Scalpel',
      'Price': 3.62,
      'SN': 'Phaestycal84'},
     {'Age': 19,
      'Gender': 'Male',
      'Item ID': 153,
      'Item Name': 'Mercenary Sabre',
      'Price': 4.57,
      'SN': 'Malunil62'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 84,
      'Item Name': 'Arcane Gem',
      'Price': 2.23,
      'SN': 'Eosursurap97'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 153,
      'Item Name': 'Mercenary Sabre',
      'Price': 4.57,
      'SN': 'Iaralrgue74'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 8,
      'Item Name': 'Purgatory, Gem of Regret',
      'Price': 3.91,
      'SN': 'Seolollo93'},
     {'Age': 18,
      'Gender': 'Male',
      'Item ID': 15,
      'Item Name': 'Soul Infused Crystal',
      'Price': 1.03,
      'SN': 'Ililsan66'},
     {'Age': 40,
      'Gender': 'Male',
      'Item ID': 171,
      'Item Name': 'Scalpel',
      'Price': 3.62,
      'SN': 'Yasriphos60'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 154,
      'Item Name': 'Feral Katana',
      'Price': 2.19,
      'SN': 'Iskosia51'},
     {'Age': 18,
      'Gender': 'Female',
      'Item ID': 171,
      'Item Name': 'Scalpel',
      'Price': 3.62,
      'SN': 'Isurria36'},
     {'Age': 29,
      'Gender': 'Male',
      'Item ID': 129,
      'Item Name': 'Fate, Vengeance of Eternal Justice',
      'Price': 1.55,
      'SN': 'Asur53'},
     {'Age': 34,
      'Gender': 'Male',
      'Item ID': 135,
      'Item Name': 'Warped Diamond Crusader',
      'Price': 4.66,
      'SN': 'Aesur96'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 108,
      'Item Name': 'Extraction, Quickblade Of Trembling Hands',
      'Price': 3.39,
      'SN': 'Iskosian40'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 100,
      'Item Name': 'Blindscythe',
      'Price': 3.66,
      'SN': 'Ililsa62'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 60,
      'Item Name': 'Wolf',
      'Price': 1.84,
      'SN': 'Aillyriadru65'},
     {'Age': 24,
      'Gender': 'Female',
      'Item ID': 110,
      'Item Name': 'Suspension',
      'Price': 2.11,
      'SN': 'Lisassa49'},
     {'Age': 7,
      'Gender': 'Male',
      'Item ID': 39,
      'Item Name': 'Betrayal, Whisper of Grieving Widows',
      'Price': 2.35,
      'SN': 'Lisistaya47'},
     {'Age': 19,
      'Gender': 'Male',
      'Item ID': 175,
      'Item Name': 'Woeful Adamantite Claymore',
      'Price': 1.24,
      'SN': 'Ialidru40'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 35,
      'Item Name': 'Heartless Bone Dualblade',
      'Price': 2.63,
      'SN': 'Sondim43'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 30,
      'Item Name': 'Stormcaller',
      'Price': 4.15,
      'SN': 'Iskimnya76'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 119,
      'Item Name': 'Stormbringer, Dark Blade of Ending Misery',
      'Price': 2.32,
      'SN': 'Aethe80'},
     {'Age': 25,
      'Gender': 'Female',
      'Item ID': 65,
      'Item Name': 'Conqueror Adamantite Mace',
      'Price': 1.96,
      'SN': 'Rathellorin54'},
     {'Age': 29,
      'Gender': 'Male',
      'Item ID': 64,
      'Item Name': 'Fusion Pummel',
      'Price': 3.58,
      'SN': 'Chanadar44'},
     {'Age': 33,
      'Gender': 'Male',
      'Item ID': 83,
      'Item Name': 'Lifebender',
      'Price': 3.51,
      'SN': 'Eudasu82'},
     {'Age': 19,
      'Gender': 'Male',
      'Item ID': 88,
      'Item Name': 'Emberling, Defender of Delusions',
      'Price': 4.1,
      'SN': 'Lisirraya76'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 26,
      'Item Name': 'Unholy Wand',
      'Price': 1.88,
      'SN': 'Lisossa25'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 133,
      'Item Name': "Faith's Scimitar",
      'Price': 3.82,
      'SN': 'Haedasu65'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 97,
      'Item Name': 'Swan Song, Gouger Of Terror',
      'Price': 3.58,
      'SN': 'Iral74'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 16,
      'Item Name': 'Restored Bauble',
      'Price': 3.11,
      'SN': 'Lisjaskya84'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 181,
      'Item Name': "Reaper's Toll",
      'Price': 4.56,
      'SN': 'Saelaephos52'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 76,
      'Item Name': 'Haunted Bronzed Bludgeon',
      'Price': 4.12,
      'SN': 'Chamim85'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 154,
      'Item Name': 'Feral Katana',
      'Price': 2.19,
      'SN': 'Chamadar61'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 142,
      'Item Name': 'Righteous Might',
      'Price': 4.36,
      'SN': 'Lirtista72'},
     {'Age': 17,
      'Gender': 'Male',
      'Item ID': 113,
      'Item Name': "Solitude's Reaver",
      'Price': 2.67,
      'SN': 'Seudanu38'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 92,
      'Item Name': 'Final Critic',
      'Price': 1.36,
      'SN': 'Lisossa63'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 36,
      'Item Name': 'Spectral Bone Axe',
      'Price': 2.98,
      'SN': 'Siathecal92'},
     {'Age': 7,
      'Gender': 'Male',
      'Item ID': 39,
      'Item Name': 'Betrayal, Whisper of Grieving Widows',
      'Price': 2.35,
      'SN': 'Eullydru35'},
     {'Age': 25,
      'Gender': 'Female',
      'Item ID': 18,
      'Item Name': 'Torchlight, Bond of Storms',
      'Price': 1.77,
      'SN': 'Chamistast30'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 142,
      'Item Name': 'Righteous Might',
      'Price': 4.36,
      'SN': 'Isrirgue68'},
     {'Age': 20,
      'Gender': 'Female',
      'Item ID': 172,
      'Item Name': 'Blade of the Grave',
      'Price': 1.69,
      'SN': 'Eurallo89'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 107,
      'Item Name': 'Splitter, Foe Of Subtlety',
      'Price': 3.61,
      'SN': 'Raithe71'},
     {'Age': 31,
      'Gender': 'Male',
      'Item ID': 151,
      'Item Name': 'Severance',
      'Price': 1.85,
      'SN': 'Iskossaya95'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 178,
      'Item Name': 'Oathbreaker, Last Hope of the Breaking Storm',
      'Price': 2.41,
      'SN': 'Yathecal82'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 68,
      'Item Name': 'Storm-Weaver, Slayer of Inception',
      'Price': 2.49,
      'SN': 'Filrion44'},
     {'Age': 9,
      'Gender': 'Male',
      'Item ID': 26,
      'Item Name': 'Unholy Wand',
      'Price': 1.88,
      'SN': 'Saralp86'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 13,
      'Item Name': 'Serenity',
      'Price': 1.49,
      'SN': 'Tyeuduen32'},
     {'Age': 21,
      'Gender': 'Female',
      'Item ID': 174,
      'Item Name': 'Primitive Blade',
      'Price': 2.46,
      'SN': 'Aina43'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 23,
      'Item Name': 'Crucifer',
      'Price': 2.77,
      'SN': 'Undiwinya88'},
     {'Age': 29,
      'Gender': 'Male',
      'Item ID': 75,
      'Item Name': 'Brutality Ivory Warmace',
      'Price': 1.72,
      'SN': 'Silaera56'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 27,
      'Item Name': 'Riddle, Tribute of Ended Dreams',
      'Price': 3.96,
      'SN': 'Iskadarya95'},
     {'Age': 13,
      'Gender': 'Female',
      'Item ID': 26,
      'Item Name': 'Unholy Wand',
      'Price': 1.88,
      'SN': 'Eoralphos86'},
     {'Age': 27,
      'Gender': 'Male',
      'Item ID': 144,
      'Item Name': 'Blood Infused Guardian',
      'Price': 2.86,
      'SN': 'Billysu76'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 152,
      'Item Name': 'Darkheart',
      'Price': 3.15,
      'SN': 'Seorithstilis90'},
     {'Age': 30,
      'Gender': 'Male',
      'Item ID': 10,
      'Item Name': 'Sleepwalker',
      'Price': 1.73,
      'SN': 'Aidaira48'},
     {'Age': 39,
      'Gender': 'Female',
      'Item ID': 145,
      'Item Name': 'Fiery Glass Crusader',
      'Price': 4.45,
      'SN': 'Mindimnya67'},
     {'Age': 22,
      'Gender': 'Other / Non-Disclosed',
      'Item ID': 115,
      'Item Name': 'Spectral Diamond Doomblade',
      'Price': 4.25,
      'SN': 'Euna48'},
     {'Age': 33,
      'Gender': 'Female',
      'Item ID': 163,
      'Item Name': 'Thunderfury Scimitar',
      'Price': 3.02,
      'SN': 'Lisassasta50'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 30,
      'Item Name': 'Stormcaller',
      'Price': 4.15,
      'SN': 'Eusur90'},
     {'Age': 29,
      'Gender': 'Male',
      'Item ID': 133,
      'Item Name': "Faith's Scimitar",
      'Price': 3.82,
      'SN': 'Undirrala66'},
     {'Age': 16,
      'Gender': 'Male',
      'Item ID': 13,
      'Item Name': 'Serenity',
      'Price': 1.49,
      'SN': 'Lamil70'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 12,
      'Item Name': 'Dawne',
      'Price': 4.3,
      'SN': 'Chamadarnya73'},
     {'Age': 20,
      'Gender': 'Female',
      'Item ID': 6,
      'Item Name': 'Rusty Skull',
      'Price': 1.2,
      'SN': 'Ilast79'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 97,
      'Item Name': 'Swan Song, Gouger Of Terror',
      'Price': 3.58,
      'SN': 'Sondilsa35'},
     {'Age': 26,
      'Gender': 'Male',
      'Item ID': 148,
      'Item Name': "Warmonger, Gift of Suffering's End",
      'Price': 3.96,
      'SN': 'Ralonurin90'},
     {'Age': 24,
      'Gender': 'Female',
      'Item ID': 71,
      'Item Name': 'Demise',
      'Price': 4.07,
      'SN': 'Marundi65'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 60,
      'Item Name': 'Wolf',
      'Price': 1.84,
      'SN': 'Phaedan76'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 18,
      'Item Name': 'Torchlight, Bond of Storms',
      'Price': 1.77,
      'SN': 'Farenon57'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 157,
      'Item Name': 'Spada, Etcher of Hatred',
      'Price': 2.21,
      'SN': 'Ilassa51'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 101,
      'Item Name': 'Final Critic',
      'Price': 4.62,
      'SN': 'Lirtossa84'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 38,
      'Item Name': 'The Void, Vengeance of Dark Magic',
      'Price': 2.82,
      'SN': 'Airi27'},
     {'Age': 40,
      'Gender': 'Male',
      'Item ID': 102,
      'Item Name': 'Avenger',
      'Price': 4.16,
      'SN': 'Indcil77'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 53,
      'Item Name': 'Vengeance Cleaver',
      'Price': 3.7,
      'SN': 'Chamastya76'},
     {'Age': 7,
      'Gender': 'Male',
      'Item ID': 158,
      'Item Name': 'Darkheart, Butcher of the Champion',
      'Price': 3.56,
      'SN': 'Lassjask63'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 175,
      'Item Name': 'Woeful Adamantite Claymore',
      'Price': 1.24,
      'SN': 'Heolo60'},
     {'Age': 18,
      'Gender': 'Female',
      'Item ID': 101,
      'Item Name': 'Final Critic',
      'Price': 4.62,
      'SN': 'Isurria36'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 153,
      'Item Name': 'Mercenary Sabre',
      'Price': 4.57,
      'SN': 'Lisossan98'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 19,
      'Item Name': 'Pursuit, Cudgel of Necromancy',
      'Price': 3.98,
      'SN': 'Sondim43'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 11,
      'Item Name': 'Brimstone',
      'Price': 2.52,
      'SN': 'Mindirra92'},
     {'Age': 20,
      'Gender': 'Female',
      'Item ID': 11,
      'Item Name': 'Brimstone',
      'Price': 2.52,
      'SN': 'Reuthelis39'},
     {'Age': 18,
      'Gender': 'Male',
      'Item ID': 166,
      'Item Name': 'Thirsty Iron Reaver',
      'Price': 4.25,
      'SN': 'Thourdirra92'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 49,
      'Item Name': 'The Oculus, Token of Lost Worlds',
      'Price': 4.23,
      'SN': 'Frichadar89'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 123,
      'Item Name': "Twilight's Carver",
      'Price': 1.14,
      'SN': 'Raesursurap33'},
     {'Age': 20,
      'Gender': 'Female',
      'Item ID': 80,
      'Item Name': 'Dreamsong',
      'Price': 3.81,
      'SN': 'Jiskilsa35'},
     {'Age': 33,
      'Gender': 'Male',
      'Item ID': 172,
      'Item Name': 'Blade of the Grave',
      'Price': 1.69,
      'SN': 'Philistirap41'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 144,
      'Item Name': 'Blood Infused Guardian',
      'Price': 2.86,
      'SN': 'Tyidainu31'},
     {'Age': 39,
      'Gender': 'Female',
      'Item ID': 161,
      'Item Name': 'Devine',
      'Price': 1.45,
      'SN': 'Mindimnya67'},
     {'Age': 37,
      'Gender': 'Female',
      'Item ID': 95,
      'Item Name': 'Singed Onyx Warscythe',
      'Price': 1.03,
      'SN': 'Tridaira71'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 90,
      'Item Name': 'Betrayer',
      'Price': 1.67,
      'SN': 'Queusurra38'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 124,
      'Item Name': 'Venom Claymore',
      'Price': 2.72,
      'SN': 'Mindadaran26'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 130,
      'Item Name': 'Alpha',
      'Price': 1.56,
      'SN': 'Lisassa39'},
     {'Age': 32,
      'Gender': 'Male',
      'Item ID': 78,
      'Item Name': 'Glimmer, Ender of the Moon',
      'Price': 2.33,
      'SN': 'Alaesu77'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 142,
      'Item Name': 'Righteous Might',
      'Price': 4.36,
      'SN': 'Ilogha82'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 178,
      'Item Name': 'Oathbreaker, Last Hope of the Breaking Storm',
      'Price': 2.41,
      'SN': 'Pharithdil38'},
     {'Age': 26,
      'Gender': 'Male',
      'Item ID': 85,
      'Item Name': 'Malificent Bag',
      'Price': 2.17,
      'SN': 'Mindossasya74'},
     {'Age': 16,
      'Gender': 'Male',
      'Item ID': 22,
      'Item Name': 'Amnesia',
      'Price': 3.57,
      'SN': 'Syadaillo88'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 127,
      'Item Name': 'Heartseeker, Reaver of Souls',
      'Price': 3.21,
      'SN': 'Lassilsala30'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 111,
      'Item Name': "Misery's End",
      'Price': 2.91,
      'SN': 'Eusri26'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 67,
      'Item Name': 'Celeste, Incarnation of the Corrupted',
      'Price': 2.31,
      'SN': 'Chanastsda67'},
     {'Age': 31,
      'Gender': 'Male',
      'Item ID': 40,
      'Item Name': 'Second Chance',
      'Price': 2.34,
      'SN': 'Hilaerin92'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 18,
      'Item Name': 'Torchlight, Bond of Storms',
      'Price': 1.77,
      'SN': 'Aeliriam77'},
     {'Age': 35,
      'Gender': 'Male',
      'Item ID': 83,
      'Item Name': 'Lifebender',
      'Price': 3.51,
      'SN': 'Lirtossan50'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 94,
      'Item Name': 'Mourning Blade',
      'Price': 1.82,
      'SN': 'Iskossan49'},
     {'Age': 16,
      'Gender': 'Male',
      'Item ID': 22,
      'Item Name': 'Amnesia',
      'Price': 3.57,
      'SN': 'Sondim73'},
     {'Age': 16,
      'Gender': 'Male',
      'Item ID': 37,
      'Item Name': 'Shadow Strike, Glory of Ending Hope',
      'Price': 1.93,
      'SN': 'Assosia38'},
     {'Age': 16,
      'Gender': 'Male',
      'Item ID': 115,
      'Item Name': 'Spectral Diamond Doomblade',
      'Price': 4.25,
      'SN': 'Reula64'},
     {'Age': 31,
      'Gender': 'Male',
      'Item ID': 182,
      'Item Name': 'Toothpick',
      'Price': 3.48,
      'SN': 'Tyeosri53'},
     {'Age': 43,
      'Gender': 'Male',
      'Item ID': 57,
      'Item Name': 'Despair, Favor of Due Diligence',
      'Price': 3.81,
      'SN': 'Raesurdil91'},
     {'Age': 20,
      'Gender': 'Female',
      'Item ID': 103,
      'Item Name': 'Singed Scalpel',
      'Price': 4.87,
      'SN': 'Anallorgue57'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 78,
      'Item Name': 'Glimmer, Ender of the Moon',
      'Price': 2.33,
      'SN': 'Idai61'},
     {'Age': 26,
      'Gender': 'Male',
      'Item ID': 156,
      'Item Name': 'Soul-Forged Steel Shortsword',
      'Price': 1.16,
      'SN': 'Aeduera68'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 92,
      'Item Name': 'Final Critic',
      'Price': 1.36,
      'SN': 'Rithe53'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 44,
      'Item Name': 'Bonecarvin Battle Axe',
      'Price': 2.46,
      'SN': 'Quinarap53'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 109,
      'Item Name': 'Downfall, Scalpel Of The Emperor',
      'Price': 3.2,
      'SN': 'Haerithp41'},
     {'Age': 30,
      'Gender': 'Female',
      'Item ID': 79,
      'Item Name': 'Alpha, Oath of Zeal',
      'Price': 2.88,
      'SN': 'Seuthelis34'},
     {'Age': 21,
      'Gender': 'Female',
      'Item ID': 8,
      'Item Name': 'Purgatory, Gem of Regret',
      'Price': 3.91,
      'SN': 'Styaduen40'},
     {'Age': 32,
      'Gender': 'Male',
      'Item ID': 120,
      'Item Name': 'Agatha',
      'Price': 1.91,
      'SN': 'Ennoncil86'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 120,
      'Item Name': 'Agatha',
      'Price': 1.91,
      'SN': 'Lassassasda30'},
     {'Age': 31,
      'Gender': 'Male',
      'Item ID': 10,
      'Item Name': 'Sleepwalker',
      'Price': 1.73,
      'SN': 'Tyeosri53'},
     {'Age': 10,
      'Gender': 'Female',
      'Item ID': 63,
      'Item Name': 'Stormfury Mace',
      'Price': 1.27,
      'SN': 'Ilaststa70'},
     {'Age': 28,
      'Gender': 'Male',
      'Item ID': 32,
      'Item Name': 'Orenmir',
      'Price': 4.95,
      'SN': 'Tyarithn67'},
     {'Age': 13,
      'Gender': 'Male',
      'Item ID': 14,
      'Item Name': 'Possessed Core',
      'Price': 1.59,
      'SN': 'Streural92'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 91,
      'Item Name': 'Celeste',
      'Price': 3.71,
      'SN': 'Haellysu29'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 73,
      'Item Name': 'Ritual Mace',
      'Price': 3.74,
      'SN': 'Yadaisuir65'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 172,
      'Item Name': 'Blade of the Grave',
      'Price': 1.69,
      'SN': 'Aerithnucal56'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 77,
      'Item Name': 'Piety, Guardian of Riddles',
      'Price': 3.68,
      'SN': 'Sundjask71'},
     {'Age': 38,
      'Gender': 'Male',
      'Item ID': 101,
      'Item Name': 'Final Critic',
      'Price': 4.62,
      'SN': 'Tyisriphos58'},
     {'Age': 22,
      'Gender': 'Female',
      'Item ID': 33,
      'Item Name': 'Curved Axe',
      'Price': 1.35,
      'SN': 'Sundaststa26'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 24,
      'Item Name': 'Warped Fetish',
      'Price': 2.41,
      'SN': 'Yalo71'},
     {'Age': 16,
      'Gender': 'Male',
      'Item ID': 67,
      'Item Name': 'Celeste, Incarnation of the Corrupted',
      'Price': 2.31,
      'SN': 'Mindetosya30'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 15,
      'Item Name': 'Soul Infused Crystal',
      'Price': 1.03,
      'SN': 'Chanjaskan89'},
     {'Age': 36,
      'Gender': 'Male',
      'Item ID': 124,
      'Item Name': 'Venom Claymore',
      'Price': 2.72,
      'SN': 'Chadjask77'},
     {'Age': 32,
      'Gender': 'Male',
      'Item ID': 66,
      'Item Name': 'Victor Iron Spikes',
      'Price': 3.55,
      'SN': 'Lirtast83'},
     {'Age': 7,
      'Gender': 'Male',
      'Item ID': 177,
      'Item Name': 'Winterthorn, Defender of Shifting Worlds',
      'Price': 4.89,
      'SN': 'Ingatcil75'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 61,
      'Item Name': 'Ragnarok',
      'Price': 3.97,
      'SN': 'Lassassast73'},
     {'Age': 18,
      'Gender': 'Male',
      'Item ID': 157,
      'Item Name': 'Spada, Etcher of Hatred',
      'Price': 2.21,
      'SN': 'Strairisti57'},
     {'Age': 11,
      'Gender': 'Male',
      'Item ID': 176,
      'Item Name': 'Relentless Iron Skewer',
      'Price': 2.97,
      'SN': 'Qarwen67'},
     {'Age': 35,
      'Gender': 'Male',
      'Item ID': 31,
      'Item Name': 'Trickster',
      'Price': 2.07,
      'SN': 'Filrion59'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 118,
      'Item Name': 'Ghost Reaver, Longsword of Magic',
      'Price': 2.77,
      'SN': 'Sondim43'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 107,
      'Item Name': 'Splitter, Foe Of Subtlety',
      'Price': 3.61,
      'SN': 'Aellysup38'},
     {'Age': 38,
      'Gender': 'Male',
      'Item ID': 75,
      'Item Name': 'Brutality Ivory Warmace',
      'Price': 1.72,
      'SN': 'Hala31'},
     {'Age': 26,
      'Gender': 'Female',
      'Item ID': 65,
      'Item Name': 'Conqueror Adamantite Mace',
      'Price': 1.96,
      'SN': 'Rithe77'},
     {'Age': 19,
      'Gender': 'Male',
      'Item ID': 159,
      'Item Name': 'Oathbreaker, Spellblade of Trials',
      'Price': 3.01,
      'SN': 'Marirrasta50'},
     {'Age': 13,
      'Gender': 'Female',
      'Item ID': 18,
      'Item Name': 'Torchlight, Bond of Storms',
      'Price': 1.77,
      'SN': 'Chanosiast43'},
     {'Age': 20,
      'Gender': 'Female',
      'Item ID': 100,
      'Item Name': 'Blindscythe',
      'Price': 3.66,
      'SN': 'Sundim98'},
     {'Age': 30,
      'Gender': 'Male',
      'Item ID': 83,
      'Item Name': 'Lifebender',
      'Price': 3.51,
      'SN': 'Frichaya88'},
     {'Age': 27,
      'Gender': 'Male',
      'Item ID': 25,
      'Item Name': 'Hero Cane',
      'Price': 1.03,
      'SN': 'Lirtassa47'},
     {'Age': 29,
      'Gender': 'Female',
      'Item ID': 130,
      'Item Name': 'Alpha',
      'Price': 1.56,
      'SN': 'Iathenudil29'},
     {'Age': 7,
      'Gender': 'Female',
      'Item ID': 11,
      'Item Name': 'Brimstone',
      'Price': 2.52,
      'SN': 'Lisirra55'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 46,
      'Item Name': 'Hopeless Ebon Dualblade',
      'Price': 4.75,
      'SN': 'Yarolwen77'},
     {'Age': 15,
      'Gender': 'Female',
      'Item ID': 112,
      'Item Name': 'Worldbreaker',
      'Price': 3.29,
      'SN': 'Crausirra42'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 87,
      'Item Name': 'Deluge, Edge of the West',
      'Price': 2.2,
      'SN': 'Frichast72'},
     {'Age': 16,
      'Gender': 'Female',
      'Item ID': 33,
      'Item Name': 'Curved Axe',
      'Price': 1.35,
      'SN': 'Eulidru49'},
     {'Age': 26,
      'Gender': 'Male',
      'Item ID': 81,
      'Item Name': 'Dreamkiss',
      'Price': 4.06,
      'SN': 'Aidain51'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 40,
      'Item Name': 'Second Chance',
      'Price': 2.34,
      'SN': 'Sida61'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 23,
      'Item Name': 'Crucifer',
      'Price': 2.77,
      'SN': 'Chamjasknya65'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 128,
      'Item Name': 'Blazeguard, Reach of Eternity',
      'Price': 4.0,
      'SN': 'Iri67'},
     {'Age': 20,
      'Gender': 'Female',
      'Item ID': 91,
      'Item Name': 'Celeste',
      'Price': 3.71,
      'SN': 'Ririp86'},
     {'Age': 37,
      'Gender': 'Female',
      'Item ID': 117,
      'Item Name': 'Heartstriker, Legacy of the Light',
      'Price': 4.15,
      'SN': 'Chadossa56'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 26,
      'Item Name': 'Unholy Wand',
      'Price': 1.88,
      'SN': 'Chanjaskan89'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 93,
      'Item Name': 'Apocalyptic Battlescythe',
      'Price': 3.91,
      'SN': 'Jiskimsda56'},
     {'Age': 19,
      'Gender': 'Male',
      'Item ID': 66,
      'Item Name': 'Victor Iron Spikes',
      'Price': 3.55,
      'SN': 'Assistast50'},
     {'Age': 16,
      'Gender': 'Male',
      'Item ID': 162,
      'Item Name': 'Abyssal Shard',
      'Price': 2.04,
      'SN': 'Euliria52'},
     {'Age': 16,
      'Gender': 'Male',
      'Item ID': 43,
      'Item Name': 'Foul Edge',
      'Price': 2.38,
      'SN': 'Aerithriaphos45'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 170,
      'Item Name': 'Shadowsteel',
      'Price': 1.98,
      'SN': 'Ila44'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 128,
      'Item Name': 'Blazeguard, Reach of Eternity',
      'Price': 4.0,
      'SN': 'Sida61'},
     {'Age': 38,
      'Gender': 'Male',
      'Item ID': 106,
      'Item Name': 'Crying Steel Sickle',
      'Price': 2.29,
      'SN': 'Phyali88'},
     {'Age': 30,
      'Gender': 'Male',
      'Item ID': 72,
      'Item Name': "Winter's Bite",
      'Price': 1.39,
      'SN': 'Iskossa88'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 115,
      'Item Name': 'Spectral Diamond Doomblade',
      'Price': 4.25,
      'SN': 'Aeral85'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 61,
      'Item Name': 'Ragnarok',
      'Price': 3.97,
      'SN': 'Rinallorap73'},
     {'Age': 36,
      'Gender': 'Male',
      'Item ID': 5,
      'Item Name': 'Putrid Fan',
      'Price': 1.32,
      'SN': 'Chanjask65'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 73,
      'Item Name': 'Ritual Mace',
      'Price': 3.74,
      'SN': 'Saedue76'},
     {'Age': 34,
      'Gender': 'Other / Non-Disclosed',
      'Item ID': 179,
      'Item Name': 'Wolf, Promise of the Moonwalker',
      'Price': 1.88,
      'SN': 'Assassa38'},
     {'Age': 27,
      'Gender': 'Female',
      'Item ID': 67,
      'Item Name': 'Celeste, Incarnation of the Corrupted',
      'Price': 2.31,
      'SN': 'Tyaelorgue39'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 84,
      'Item Name': 'Arcane Gem',
      'Price': 2.23,
      'SN': 'Tyananurgue44'},
     {'Age': 13,
      'Gender': 'Male',
      'Item ID': 5,
      'Item Name': 'Putrid Fan',
      'Price': 1.32,
      'SN': 'Isketo41'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 159,
      'Item Name': 'Oathbreaker, Spellblade of Trials',
      'Price': 3.01,
      'SN': 'Sundast87'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 37,
      'Item Name': 'Shadow Strike, Glory of Ending Hope',
      'Price': 1.93,
      'SN': 'Yadacal26'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 174,
      'Item Name': 'Primitive Blade',
      'Price': 2.46,
      'SN': 'Ila44'},
     {'Age': 9,
      'Gender': 'Male',
      'Item ID': 103,
      'Item Name': 'Singed Scalpel',
      'Price': 4.87,
      'SN': 'Ilophos58'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 102,
      'Item Name': 'Avenger',
      'Price': 4.16,
      'SN': 'Marilsanya48'},
     {'Age': 22,
      'Gender': 'Female',
      'Item ID': 79,
      'Item Name': 'Alpha, Oath of Zeal',
      'Price': 2.88,
      'SN': 'Phially37'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 169,
      'Item Name': 'Interrogator, Blood Blade of the Queen',
      'Price': 3.32,
      'SN': 'Iduedru67'},
     {'Age': 7,
      'Gender': 'Male',
      'Item ID': 82,
      'Item Name': 'Nirvana',
      'Price': 1.11,
      'SN': 'Yarithsurgue62'},
     {'Age': 26,
      'Gender': 'Male',
      'Item ID': 39,
      'Item Name': 'Betrayal, Whisper of Grieving Widows',
      'Price': 2.35,
      'SN': 'Aeduera68'},
     {'Age': 29,
      'Gender': 'Male',
      'Item ID': 18,
      'Item Name': 'Torchlight, Bond of Storms',
      'Price': 1.77,
      'SN': 'Saidairiaphos61'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 69,
      'Item Name': 'Frenzy, Defender of the Harvest',
      'Price': 1.06,
      'SN': 'Tillyrin30'},
     {'Age': 13,
      'Gender': 'Female',
      'Item ID': 117,
      'Item Name': 'Heartstriker, Legacy of the Light',
      'Price': 4.15,
      'SN': 'Chanosiast43'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 14,
      'Item Name': 'Possessed Core',
      'Price': 1.59,
      'SN': 'Quarusrion32'},
     {'Age': 18,
      'Gender': 'Male',
      'Item ID': 21,
      'Item Name': 'Souleater',
      'Price': 3.27,
      'SN': 'Chamimla73'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 139,
      'Item Name': 'Mercy, Katana of Dismay',
      'Price': 4.37,
      'SN': 'Eurith26'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 48,
      'Item Name': 'Rage, Legacy of the Lone Victor',
      'Price': 4.32,
      'SN': 'Tyananurgue44'},
     {'Age': 16,
      'Gender': 'Male',
      'Item ID': 134,
      'Item Name': 'Undead Crusader',
      'Price': 4.67,
      'SN': 'Iskichinya81'},
     {'Age': 10,
      'Gender': 'Female',
      'Item ID': 148,
      'Item Name': "Warmonger, Gift of Suffering's End",
      'Price': 3.96,
      'SN': 'Hiadanurin36'},
     {'Age': 20,
      'Gender': 'Female',
      'Item ID': 106,
      'Item Name': 'Crying Steel Sickle',
      'Price': 2.29,
      'SN': 'Tyaelly53'},
     {'Age': 23,
      'Gender': 'Female',
      'Item ID': 37,
      'Item Name': 'Shadow Strike, Glory of Ending Hope',
      'Price': 1.93,
      'SN': 'Shidai42'},
     {'Age': 16,
      'Gender': 'Male',
      'Item ID': 8,
      'Item Name': 'Purgatory, Gem of Regret',
      'Price': 3.91,
      'SN': 'Bartassaya73'},
     {'Age': 13,
      'Gender': 'Male',
      'Item ID': 175,
      'Item Name': 'Woeful Adamantite Claymore',
      'Price': 1.24,
      'SN': 'Mindosiasya28'},
     {'Age': 10,
      'Gender': 'Male',
      'Item ID': 16,
      'Item Name': 'Restored Bauble',
      'Price': 3.11,
      'SN': 'Ethrusuard41'},
     {'Age': 19,
      'Gender': 'Male',
      'Item ID': 45,
      'Item Name': 'Glinting Glass Edge',
      'Price': 2.46,
      'SN': 'Indirrian56'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 101,
      'Item Name': 'Final Critic',
      'Price': 4.62,
      'SN': 'Sondim68'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 56,
      'Item Name': 'Foul Titanium Battle Axe',
      'Price': 4.33,
      'SN': 'Tyadaru49'},
     {'Age': 35,
      'Gender': 'Female',
      'Item ID': 93,
      'Item Name': 'Apocalyptic Battlescythe',
      'Price': 3.91,
      'SN': 'Cosadar58'},
     {'Age': 19,
      'Gender': 'Male',
      'Item ID': 154,
      'Item Name': 'Feral Katana',
      'Price': 2.19,
      'SN': 'Farusrian86'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 145,
      'Item Name': 'Fiery Glass Crusader',
      'Price': 4.45,
      'SN': 'Leyirra83'},
     {'Age': 26,
      'Gender': 'Male',
      'Item ID': 84,
      'Item Name': 'Arcane Gem',
      'Price': 2.23,
      'SN': 'Inguron55'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 134,
      'Item Name': 'Undead Crusader',
      'Price': 4.67,
      'SN': 'Haedasu65'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 130,
      'Item Name': 'Alpha',
      'Price': 1.56,
      'SN': 'Ialistidru50'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 79,
      'Item Name': 'Alpha, Oath of Zeal',
      'Price': 2.88,
      'SN': 'Sweecossa42'},
     {'Age': 35,
      'Gender': 'Male',
      'Item ID': 34,
      'Item Name': 'Retribution Axe',
      'Price': 4.14,
      'SN': 'Ralasti48'},
     {'Age': 32,
      'Gender': 'Male',
      'Item ID': 52,
      'Item Name': 'Hatred',
      'Price': 4.39,
      'SN': 'Lamon28'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 120,
      'Item Name': 'Agatha',
      'Price': 1.91,
      'SN': 'Isri49'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 114,
      'Item Name': 'Yearning Mageblade',
      'Price': 1.79,
      'SN': 'Frichassala85'},
     {'Age': 23,
      'Gender': 'Male',
      'Item ID': 86,
      'Item Name': 'Stormfury Lantern',
      'Price': 1.28,
      'SN': 'Eollym91'},
     {'Age': 26,
      'Gender': 'Female',
      'Item ID': 179,
      'Item Name': 'Wolf, Promise of the Moonwalker',
      'Price': 1.88,
      'SN': 'Lisjasksda68'},
     {'Age': 15,
      'Gender': 'Female',
      'Item ID': 116,
      'Item Name': 'Renewed Skeletal Katana',
      'Price': 2.37,
      'SN': 'Yalostiphos68'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 4,
      'Item Name': "Bloodlord's Fetish",
      'Price': 2.28,
      'SN': 'Thryallym62'},
     {'Age': 31,
      'Gender': 'Male',
      'Item ID': 104,
      'Item Name': "Gladiator's Glaive",
      'Price': 1.36,
      'SN': 'Sondastan54'},
     {'Age': 22,
      'Gender': 'Female',
      'Item ID': 179,
      'Item Name': 'Wolf, Promise of the Moonwalker',
      'Price': 1.88,
      'SN': 'Ailaesuir66'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 6,
      'Item Name': 'Rusty Skull',
      'Price': 1.2,
      'SN': 'Siasri67'},
     {'Age': 35,
      'Gender': 'Male',
      'Item ID': 11,
      'Item Name': 'Brimstone',
      'Price': 2.52,
      'SN': 'Seosri62'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 122,
      'Item Name': 'Unending Tyranny',
      'Price': 1.21,
      'SN': 'Ryastycal90'},
     {'Age': 19,
      'Gender': 'Male',
      'Item ID': 87,
      'Item Name': 'Deluge, Edge of the West',
      'Price': 2.2,
      'SN': 'Chanirrasta87'},
     {'Age': 29,
      'Gender': 'Male',
      'Item ID': 81,
      'Item Name': 'Dreamkiss',
      'Price': 4.06,
      'SN': 'Aerithllora36'},
     {'Age': 28,
      'Gender': 'Male',
      'Item ID': 175,
      'Item Name': 'Woeful Adamantite Claymore',
      'Price': 1.24,
      'SN': 'Raeduerin33'},
     {'Age': 36,
      'Gender': 'Male',
      'Item ID': 52,
      'Item Name': 'Hatred',
      'Price': 4.39,
      'SN': 'Lisosiast26'},
     {'Age': 27,
      'Gender': 'Other / Non-Disclosed',
      'Item ID': 48,
      'Item Name': 'Rage, Legacy of the Lone Victor',
      'Price': 4.32,
      'SN': 'Eurisuru25'},
     {'Age': 25,
      'Gender': 'Male',
      'Item ID': 70,
      'Item Name': "Hope's End",
      'Price': 3.89,
      'SN': 'Assassasda84'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 13,
      'Item Name': 'Serenity',
      'Price': 1.49,
      'SN': 'Aerithnucal56'},
     {'Age': 22,
      'Gender': 'Female',
      'Item ID': 84,
      'Item Name': 'Arcane Gem',
      'Price': 2.23,
      'SN': 'Nitherian58'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 122,
      'Item Name': 'Unending Tyranny',
      'Price': 1.21,
      'SN': 'Hailaphos89'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 158,
      'Item Name': 'Darkheart, Butcher of the Champion',
      'Price': 3.56,
      'SN': 'Chamucosda93'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 73,
      'Item Name': 'Ritual Mace',
      'Price': 3.74,
      'SN': 'Frichilsasya78'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 141,
      'Item Name': 'Persuasion',
      'Price': 3.27,
      'SN': 'Aenasu69'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 25,
      'Item Name': 'Hero Cane',
      'Price': 1.03,
      'SN': 'Lassista97'},
     {'Age': 15,
      'Gender': 'Male',
      'Item ID': 31,
      'Item Name': 'Trickster',
      'Price': 2.07,
      'SN': 'Sidap51'},
     {'Age': 21,
      'Gender': 'Male',
      'Item ID': 44,
      'Item Name': 'Bonecarvin Battle Axe',
      'Price': 2.46,
      'SN': 'Chamadarsda63'},
     {'Age': 24,
      'Gender': 'Male',
      'Item ID': 123,
      'Item Name': "Twilight's Carver",
      'Price': 1.14,
      'SN': 'Lassassast73'},
     {'Age': 22,
      'Gender': 'Male',
      'Item ID': 98,
      'Item Name': 'Deadline, Voice Of Subtlety',
      'Price': 3.62,
      'SN': 'Eural50'},
     {'Age': 14,
      'Gender': 'Male',
      'Item ID': 104,
      'Item Name': "Gladiator's Glaive",
      'Price': 1.36,
      'SN': 'Lirtossa78'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 117,
      'Item Name': 'Heartstriker, Legacy of the Light',
      'Price': 4.15,
      'SN': 'Tillyrin30'},
     {'Age': 20,
      'Gender': 'Male',
      'Item ID': 75,
      'Item Name': 'Brutality Ivory Warmace',
      'Price': 1.72,
      'SN': 'Quelaton80'},
     {'Age': 23,
      'Gender': 'Female',
      'Item ID': 107,
      'Item Name': 'Splitter, Foe Of Subtlety',
      'Price': 3.61,
      'SN': 'Alim85'}]




```python
# to see the dataframe keys
head = j_data[0].keys()
print(head)    
df = pd.DataFrame(j_data)
```

    dict_keys(['SN', 'Age', 'Gender', 'Item ID', 'Item Name', 'Price'])
    


```python
# FINAL REPORT
print("_____________ F I N A L    R E P O R T ________________")
```

    _____________ F I N A L    R E P O R T ________________
    


```python
#Player Count: number of unique players
print("Total Number of Players: ", df["SN"].nunique())
```

    Total Number of Players:  573
    


```python
#Purchasing Analysis (Total)
    
print("Number of Unique Items: ", df["Item Name"].nunique())
print("Average Purchase Price:", round(df["Price"].mean(), 2))
print("Total Number of Purchases: ", df["Item Name"].count())
print("Total Revenue", round(df["Price"].sum(), 2))
```

    Number of Unique Items:  179
    Average Purchase Price: 2.93
    Total Number of Purchases:  780
    Total Revenue 2286.33
    


```python
# Gender Demographics

# Count and Percentage of Male Players
# Count and Percentage of Female Players
# Count and Percentage of Other / Non-Disclosed

df_SN = df[["SN", "Gender"]].drop_duplicates()
genders = df_SN.groupby(['Gender']).count().reset_index().rename(columns={"SN":"Total Count"})
genders["Percentage"] = round(genders["Total Count"] / genders["Total Count"].sum() * 100, 2) 
genders
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Gender</th>
      <th>Total Count</th>
      <th>Percentage</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Female</td>
      <td>100</td>
      <td>17.45</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Male</td>
      <td>465</td>
      <td>81.15</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Other / Non-Disclosed</td>
      <td>8</td>
      <td>1.40</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Purchasing Analysis (Gender):
df_price_gender = df[["Gender", "Price"]]
```


```python
#Purchase Count by gender
genders_pa1 = df_price_gender.groupby(['Gender']).count().reset_index().rename(columns={"Price":"Purchase Count"})
genders_pa1
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Gender</th>
      <th>Purchase Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Female</td>
      <td>136</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Male</td>
      <td>633</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Other / Non-Disclosed</td>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Average Purchase Price
genders_pa2 = round(df_price_gender.groupby(['Gender']).mean().reset_index().rename(columns={"Price":"Average Purchase Price"}), 2)
genders_pa2
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Gender</th>
      <th>Average Purchase Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Female</td>
      <td>2.82</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Male</td>
      <td>2.95</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Other / Non-Disclosed</td>
      <td>3.25</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Total Purchase Value
genders_pa3 = round(df_price_gender.groupby(['Gender']).sum().reset_index().rename(columns={"Price":"Total Purchase Value"}), 2)
genders_pa3
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Gender</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Female</td>
      <td>382.91</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Male</td>
      <td>1867.68</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Other / Non-Disclosed</td>
      <td>35.74</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Merging df's together
genders_all1 = pd.merge(genders_pa1, genders_pa2, on="Gender")
genders_all2 = pd.merge(genders_all1, genders_pa3, on="Gender")
genders_all = pd.merge(genders_all2, genders, on="Gender")
genders_all
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Gender</th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Total Count</th>
      <th>Percentage</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Female</td>
      <td>136</td>
      <td>2.82</td>
      <td>382.91</td>
      <td>100</td>
      <td>17.45</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Male</td>
      <td>633</td>
      <td>2.95</td>
      <td>1867.68</td>
      <td>465</td>
      <td>81.15</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Other / Non-Disclosed</td>
      <td>11</td>
      <td>3.25</td>
      <td>35.74</td>
      <td>8</td>
      <td>1.40</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Purchasing Analysis (Gender): FINAL RESULTS
genders_all["Normalized Total"] = round(genders_all["Total Purchase Value"] / genders_all["Total Count"], 2)
genders_all
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Gender</th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Total Count</th>
      <th>Percentage</th>
      <th>Normalized Total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Female</td>
      <td>136</td>
      <td>2.82</td>
      <td>382.91</td>
      <td>100</td>
      <td>17.45</td>
      <td>3.83</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Male</td>
      <td>633</td>
      <td>2.95</td>
      <td>1867.68</td>
      <td>465</td>
      <td>81.15</td>
      <td>4.02</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Other / Non-Disclosed</td>
      <td>11</td>
      <td>3.25</td>
      <td>35.74</td>
      <td>8</td>
      <td>1.40</td>
      <td>4.47</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Age Demographics

# The below each broken into bins of 4 years (i.e. <10, 10-14, 15-19, etc.)
# Create the bins in which Data will be held
my_bins = [0,10,14,19,24,29,34,39,44,49]
```


```python
# Create the names for the four bins
my_labels=["0-9","10-14","15-19","20-24","25-29","30-34","35-39","40-44","45-49"]
```


```python
#  place the Ages into bins
#df_price_age = df[["Age", "Price"]]
#df_price_age
df["Age Groups"]=pd.cut(df["Age"], bins=my_bins, labels=my_labels)
df.head(10)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
      <th>Age Groups</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
      <td>35-39</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
      <td>30-34</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>5</th>
      <td>20</td>
      <td>Male</td>
      <td>10</td>
      <td>Sleepwalker</td>
      <td>1.73</td>
      <td>Tanimnya91</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>6</th>
      <td>20</td>
      <td>Male</td>
      <td>153</td>
      <td>Mercenary Sabre</td>
      <td>4.57</td>
      <td>Undjaskla97</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>7</th>
      <td>29</td>
      <td>Female</td>
      <td>169</td>
      <td>Interrogator, Blood Blade of the Queen</td>
      <td>3.32</td>
      <td>Iathenudil29</td>
      <td>25-29</td>
    </tr>
    <tr>
      <th>8</th>
      <td>25</td>
      <td>Male</td>
      <td>118</td>
      <td>Ghost Reaver, Longsword of Magic</td>
      <td>2.77</td>
      <td>Sondenasta63</td>
      <td>25-29</td>
    </tr>
    <tr>
      <th>9</th>
      <td>31</td>
      <td>Male</td>
      <td>99</td>
      <td>Expiration, Warscythe Of Lost Worlds</td>
      <td>4.53</td>
      <td>Hilaerin92</td>
      <td>30-34</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_age = df[["Age Groups", "Price"]]
df_age.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age Groups</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>35-39</td>
      <td>3.37</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20-24</td>
      <td>2.32</td>
    </tr>
    <tr>
      <th>2</th>
      <td>30-34</td>
      <td>2.46</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>1.36</td>
    </tr>
    <tr>
      <th>4</th>
      <td>20-24</td>
      <td>1.27</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Purchase Count
age_pa1 = df_age.groupby(['Age Groups']).count().reset_index().rename(columns={"Price":"Purchase Count"})
age_pa1
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age Groups</th>
      <th>Purchase Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0-9</td>
      <td>32</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>31</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>133</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>336</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>125</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>64</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>42</td>
    </tr>
    <tr>
      <th>7</th>
      <td>40-44</td>
      <td>16</td>
    </tr>
    <tr>
      <th>8</th>
      <td>45-49</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Average Purchase Price
age_pa2 = round(df_age.groupby(['Age Groups']).mean().reset_index().rename(columns={"Price":"Average Purchase Price"}), 2)
age_pa2
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age Groups</th>
      <th>Average Purchase Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0-9</td>
      <td>3.02</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>2.70</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>2.91</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>2.91</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>2.96</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>3.08</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>2.84</td>
    </tr>
    <tr>
      <th>7</th>
      <td>40-44</td>
      <td>3.19</td>
    </tr>
    <tr>
      <th>8</th>
      <td>45-49</td>
      <td>2.72</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Total Purchase Value
age_pa3 = round(df_age.groupby(['Age Groups']).sum().reset_index().rename(columns={"Price":"Total Purchase Value"}), 2)
age_pa3
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age Groups</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0-9</td>
      <td>96.62</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>83.79</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>386.42</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>978.77</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>370.33</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>197.25</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>119.40</td>
    </tr>
    <tr>
      <th>7</th>
      <td>40-44</td>
      <td>51.03</td>
    </tr>
    <tr>
      <th>8</th>
      <td>45-49</td>
      <td>2.72</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_SN_age = df[["SN", "Age Groups"]].drop_duplicates()
ages_by_SN = df_SN_age.groupby(['Age Groups']).count().reset_index().rename(columns={"SN":"Total Count"})
ages_by_SN
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age Groups</th>
      <th>Total Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0-9</td>
      <td>22</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>20</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>100</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>259</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>87</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>47</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>27</td>
    </tr>
    <tr>
      <th>7</th>
      <td>40-44</td>
      <td>10</td>
    </tr>
    <tr>
      <th>8</th>
      <td>45-49</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Merging dfs
age_all1 = pd.merge(age_pa1, age_pa2, on="Age Groups")
age_all2 = pd.merge(age_all1, age_pa3, on="Age Groups")
age_all = pd.merge(age_all2, ages_by_SN, on="Age Groups")
age_all
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age Groups</th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Total Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0-9</td>
      <td>32</td>
      <td>3.02</td>
      <td>96.62</td>
      <td>22</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>31</td>
      <td>2.70</td>
      <td>83.79</td>
      <td>20</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>133</td>
      <td>2.91</td>
      <td>386.42</td>
      <td>100</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>336</td>
      <td>2.91</td>
      <td>978.77</td>
      <td>259</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>125</td>
      <td>2.96</td>
      <td>370.33</td>
      <td>87</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>64</td>
      <td>3.08</td>
      <td>197.25</td>
      <td>47</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>42</td>
      <td>2.84</td>
      <td>119.40</td>
      <td>27</td>
    </tr>
    <tr>
      <th>7</th>
      <td>40-44</td>
      <td>16</td>
      <td>3.19</td>
      <td>51.03</td>
      <td>10</td>
    </tr>
    <tr>
      <th>8</th>
      <td>45-49</td>
      <td>1</td>
      <td>2.72</td>
      <td>2.72</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Age Demographics - FINAL RESULTS
# +Normalized Totals
age_all["Normalized Total"] = round(age_all["Total Purchase Value"] / age_all["Total Count"], 2)
age_all
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age Groups</th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Total Count</th>
      <th>Normalized Total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0-9</td>
      <td>32</td>
      <td>3.02</td>
      <td>96.62</td>
      <td>22</td>
      <td>4.39</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>31</td>
      <td>2.70</td>
      <td>83.79</td>
      <td>20</td>
      <td>4.19</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>133</td>
      <td>2.91</td>
      <td>386.42</td>
      <td>100</td>
      <td>3.86</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>336</td>
      <td>2.91</td>
      <td>978.77</td>
      <td>259</td>
      <td>3.78</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>125</td>
      <td>2.96</td>
      <td>370.33</td>
      <td>87</td>
      <td>4.26</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>64</td>
      <td>3.08</td>
      <td>197.25</td>
      <td>47</td>
      <td>4.20</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>42</td>
      <td>2.84</td>
      <td>119.40</td>
      <td>27</td>
      <td>4.42</td>
    </tr>
    <tr>
      <th>7</th>
      <td>40-44</td>
      <td>16</td>
      <td>3.19</td>
      <td>51.03</td>
      <td>10</td>
      <td>5.10</td>
    </tr>
    <tr>
      <th>8</th>
      <td>45-49</td>
      <td>1</td>
      <td>2.72</td>
      <td>2.72</td>
      <td>1</td>
      <td>2.72</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Top Spenders:

#Identify the the top 5 spenders in the game by total purchase value, then list (in a table):
#"SN", "Purchase Count", "Average Purchase Price", "Total Purchase Value"

df_spenders = pd.DataFrame()

df_by_sn = df.groupby("SN")
for name, group in df_by_sn:
    #print (group)
    cnt = group["Price"].count()
    ave = group["Price"].mean()
    tot = group["Price"].sum()
    df_spenders = df_spenders.append([{"SN":name, "Purchase Count":cnt, "Average Purchase Price": ave, "Total Purchase Value":tot}])
    
my_spenders = df_spenders[["SN", "Purchase Count", "Average Purchase Price", "Total Purchase Value"]]
my_spenders = my_spenders.rename(columns={"SN":"Top Spenders"})
my_spenders.sort_values("Total Purchase Value", ascending=False).head(5) 
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Top Spenders</th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Undirrala66</td>
      <td>5</td>
      <td>3.412000</td>
      <td>17.06</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Saedue76</td>
      <td>4</td>
      <td>3.390000</td>
      <td>13.56</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Mindimnya67</td>
      <td>4</td>
      <td>3.185000</td>
      <td>12.74</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Haellysu29</td>
      <td>3</td>
      <td>4.243333</td>
      <td>12.73</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Eoda93</td>
      <td>3</td>
      <td>3.860000</td>
      <td>11.58</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Identify the 5 most popular items by purchase count, then list (in a table):
#"Item ID", "Item Name", "Purchase Count", "Item Price", "Total Purchase Value"
df_pop_items = pd.DataFrame()

df_by_item = df.groupby("Item Name")
for name, group in df_by_item:
    #print (group)
    cnt = group["Price"].count()
    ave = group["Price"].mean()
    tot = group["Price"].sum()
    id = group["Item ID"].min()
    df_pop_items = df_pop_items.append([{"Item ID":id, "Item Name":name, "Purchase Count":cnt, "Item Price": ave, "Total Purchase Value":tot}])

my_pop_items = df_pop_items[["Item Name", "Item ID", "Purchase Count", "Item Price", "Total Purchase Value"]]
my_pop_items = my_pop_items.rename(columns={"Item Name":"Most Popular Items"})    
my_pop_items.sort_values("Purchase Count", ascending=False).head(5)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Most Popular Items</th>
      <th>Item ID</th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Final Critic</td>
      <td>92</td>
      <td>14</td>
      <td>2.757143</td>
      <td>38.60</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Arcane Gem</td>
      <td>84</td>
      <td>11</td>
      <td>2.230000</td>
      <td>24.53</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Betrayal, Whisper of Grieving Widows</td>
      <td>39</td>
      <td>11</td>
      <td>2.350000</td>
      <td>25.85</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Stormcaller</td>
      <td>30</td>
      <td>10</td>
      <td>3.465000</td>
      <td>34.65</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Woeful Adamantite Claymore</td>
      <td>175</td>
      <td>9</td>
      <td>1.240000</td>
      <td>11.16</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Most Profitable Items:

#Identify the 5 most profitable items by total purchase value, then list (in a table):
#"Item ID", "Item Name", "Purchase Count", "Item Price", "Total Purchase Value"

df_prof_items = pd.DataFrame()

df_by_item_prof = df.groupby("Item Name")
for name, group in df_by_item_prof:
    #print (group)
    cnt = group["Price"].count()
    ave = group["Price"].mean()
    tot = group["Price"].sum()
    id = group["Item ID"].min()
    df_prof_items = df_prof_items.append([{"Item ID":id, "Item Name":name, "Purchase Count":cnt, "Item Price": ave, "Total Purchase Value":tot}])

my_prof_items = df_prof_items[["Item Name", "Item ID", "Purchase Count", "Item Price", "Total Purchase Value"]]
my_prof_items = my_prof_items.rename(columns={"Item Name":"Most Profitable Items"})    
my_prof_items.sort_values("Total Purchase Value", ascending=False).head(5)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Most Profitable Items</th>
      <th>Item ID</th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Final Critic</td>
      <td>92</td>
      <td>14</td>
      <td>2.757143</td>
      <td>38.60</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Retribution Axe</td>
      <td>34</td>
      <td>9</td>
      <td>4.140000</td>
      <td>37.26</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Stormcaller</td>
      <td>30</td>
      <td>10</td>
      <td>3.465000</td>
      <td>34.65</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Spectral Diamond Doomblade</td>
      <td>115</td>
      <td>7</td>
      <td>4.250000</td>
      <td>29.75</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Orenmir</td>
      <td>32</td>
      <td>6</td>
      <td>4.950000</td>
      <td>29.70</td>
    </tr>
  </tbody>
</table>
</div>




```python
# I DIDN'T SEE THE SECOND DATA-SET FOR THE 'HEROES OF PYMOLI
```


```python
#http://ucb.bootcampcontent.com/UCB-Coding-Bootcamp/UCBER201802DATA3-Class-Repository-DATA/tree/master/02-Homework/04-Numpy-Pandas/Instructions/HeroesOfPymoli
```