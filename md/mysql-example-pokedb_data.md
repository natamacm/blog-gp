---
title: mysql example pokedb data (snippet)
date: 2020-03-03
tags: ["python"]
---
Python mysql example 'pokedb data'

Functions in program: 
* `def insert_pokemon():`

## python pokedb data

Python mysql example: pokedb data

```python
from  pokedb import *

def insert_pokemon():
    Pokemon( id=1,    name='Bulbasaur',         internal_name='BULBASAUR',    rarity=2).save()
    Pokemon( id=2,    name='Ivysaur',           internal_name='IVYSAUR',      rarity=3).save()
    Pokemon( id=3,    name='Venusaur',          internal_name='VENUSAUR',     rarity=4).save()
    Pokemon( id=4,    name='Charmander',        internal_name='CHARMANDER',   rarity=3).save()
    Pokemon( id=5,    name='Charmeleon',        internal_name='CHARMELEON',   rarity=4).save()
    Pokemon( id=6,    name='Charizard',         internal_name='CHARIZARD',    rarity=4).save()
    Pokemon( id=7,    name='Squirtle',          internal_name='SQUIRTLE',     rarity=2).save()
    Pokemon( id=8,    name='Wartortle',         internal_name='WARTORTLE',    rarity=3).save()
    Pokemon( id=9,    name='Blastoise',         internal_name='BLASTOISE',    rarity=4).save()
    Pokemon( id=10,   name='Caterpie',          internal_name='CATERPIE',     rarity=1).save()
    Pokemon( id=11,   name='Metapod',           internal_name='METAPOD',      rarity=3).save()
    Pokemon( id=12,   name='Butterfree',        internal_name='BUTTERFREE',   rarity=4).save()
    Pokemon( id=13,   name='Weedle',            internal_name='WEEDLE',       rarity=1).save()
    Pokemon( id=14,   name='Kakuna',            internal_name='KAKUNA',       rarity=3).save()
    Pokemon( id=15,   name='Beedrill',          internal_name='BEEDRILL',     rarity=3).save()
    Pokemon( id=16,   name='Pidgey',            internal_name='PIDGEY',       rarity=1).save()
    Pokemon( id=17,   name='Pidgeotto',         internal_name='PIDGEOTTO',    rarity=2).save()
    Pokemon( id=18,   name='Pidgeot',           internal_name='PIDGEOT',      rarity=3).save()
    Pokemon( id=19,   name='Rattata',           internal_name='RATTATA',      rarity=1).save()
    Pokemon( id=20,   name='Raticate',          internal_name='RATICATE',     rarity=3).save()
    Pokemon( id=21,   name='Spearow',           internal_name='SPEAROW',      rarity=1).save()
    Pokemon( id=22,   name='Fearow',            internal_name='FEAROW',       rarity=3).save()
    Pokemon( id=23,   name='Ekans',             internal_name='EKANS',        rarity=2).save()
    Pokemon( id=24,   name='Arbok',             internal_name='ARBOK',        rarity=4).save()
    Pokemon( id=25,   name='Pikachu',           internal_name='PIKACHU',      rarity=3).save()
    Pokemon( id=26,   name='Raichu',            internal_name='RAICHU',       rarity=5).save()
    Pokemon( id=27,   name='Sandshrew',         internal_name='SANDSHREW',    rarity=3).save()
    Pokemon( id=28,   name='Sandslash',         internal_name='SANDSLASH',    rarity=5).save()
    Pokemon( id=29,   name='NidoranFem',        internal_name='NIDORAN_FEMALE', rarity=2).save()
    Pokemon( id=30,   name='Nidorina',          internal_name='NIDORINA',     rarity=4).save()
    Pokemon( id=31,   name='Nidoqueen',         internal_name='NIDOQUEEN',    rarity=4).save()
    Pokemon( id=32,   name='NidoranMale',       internal_name='NIDORAN_MALE', rarity=2).save()
    Pokemon( id=33,   name='Nidorino',          internal_name='NIDORINO',     rarity=4).save()
    Pokemon( id=34,   name='Nidoking',          internal_name='NIDOKING',     rarity=4).save()
    Pokemon( id=35,   name='Clefairy',          internal_name='CLEFAIRY',     rarity=2).save()
    Pokemon( id=36,   name='Clefable',          internal_name='CLEFABLE',     rarity=4).save()
    Pokemon( id=37,   name='Vulpix',            internal_name='VULPIX',       rarity=3).save()
    Pokemon( id=38,   name='Ninetales',         internal_name='NINETALES',    rarity=5).save()
    Pokemon( id=39,   name='Jigglypuff',        internal_name='JIGGLYPUFF',   rarity=3).save()
    Pokemon( id=40,   name='Wigglytuff',        internal_name='WIGGLYTUFF',   rarity=5).save()
    Pokemon( id=41,   name='Zubat',             internal_name='ZUBAT',        rarity=1).save()
    Pokemon( id=42,   name='Golbat',            internal_name='GOLBAT',       rarity=3).save()
    Pokemon( id=43,   name='Oddish',            internal_name='ODDISH',       rarity=2).save()
    Pokemon( id=44,   name='Gloom',             internal_name='GLOOM',        rarity=4).save()
    Pokemon( id=45,   name='Vileplume',         internal_name='VILEPLUME',    rarity=5).save()
    Pokemon( id=46,   name='Paras',             internal_name='PARAS',        rarity=2).save()
    Pokemon( id=47,   name='Parasect',          internal_name='PARASECT',     rarity=3).save()
    Pokemon( id=48,   name='Venonat',           internal_name='VENONAT',      rarity=2).save()
    Pokemon( id=49,   name='Venomoth',          internal_name='VENOMOTH',     rarity=3).save()
    Pokemon( id=50,   name='Diglett',           internal_name='DIGLETT',      rarity=3).save()
    Pokemon( id=51,   name='Dugtrio',           internal_name='DUGTRIO',      rarity=5).save()
    Pokemon( id=52,   name='Meowth',            internal_name='MEOWTH',       rarity=3).save()
    Pokemon( id=53,   name='Persian',           internal_name='PERSIAN',      rarity=4).save()
    Pokemon( id=54,   name='Psyduck',           internal_name='PSYDUCK',      rarity=3).save()
    Pokemon( id=55,   name='Golduck',           internal_name='GOLDUCK',      rarity=4).save()
    Pokemon( id=56,   name='Mankey',            internal_name='MANKEY',       rarity=3).save()
    Pokemon( id=57,   name='Primeape',          internal_name='PRIMEAPE',     rarity=4).save()
    Pokemon( id=58,   name='Growlithe',         internal_name='GROWLITHE',    rarity=3).save()
    Pokemon( id=59,   name='Arcanine',          internal_name='ARCANINE',     rarity=4).save()
    Pokemon( id=60,   name='Poliwag',           internal_name='POLIWAG',      rarity=2).save()
    Pokemon( id=61,   name='Poliwhirl',         internal_name='POLIWHIRL',    rarity=3).save()
    Pokemon( id=62,   name='Poliwrath',         internal_name='POLIWRATH',    rarity=5).save()
    Pokemon( id=63,   name='Abra',              internal_name='ABRA',         rarity=3).save()
    Pokemon( id=64,   name='Kadabra',           internal_name='KADABRA',      rarity=4).save()
    Pokemon( id=65,   name='Alakazam',          internal_name='ALAKAZAM',     rarity=5).save()
    Pokemon( id=66,   name='Machop',            internal_name='MACHOP',       rarity=3).save()
    Pokemon( id=67,   name='Machoke',           internal_name='MACHOKE',      rarity=4).save()
    Pokemon( id=68,   name='Machamp',           internal_name='MACHAMP',      rarity=5).save()
    Pokemon( id=69,   name='Bellsprout',        internal_name='BELLSPROUT',   rarity=2).save()
    Pokemon( id=70,   name='Weepinbell',        internal_name='WEEPINBELL',   rarity=3).save()
    Pokemon( id=71,   name='Victreebel',        internal_name='VICTREEBEL',   rarity=5).save()
    Pokemon( id=72,   name='Tentacool',         internal_name='TENTACOOL',    rarity=3).save()
    Pokemon( id=73,   name='Tentacruel',        internal_name='TENTACRUEL',   rarity=4).save()
    Pokemon( id=74,   name='Geodude',           internal_name='GEODUDE',      rarity=3).save()
    Pokemon( id=75,   name='Graveler',          internal_name='GRAVELER',     rarity=4).save()
    Pokemon( id=76,   name='Golem',             internal_name='GOLEM',        rarity=5).save()
    Pokemon( id=77,   name='Ponyta',            internal_name='PONYTA',       rarity=3).save()
    Pokemon( id=78,   name='Rapidash',          internal_name='RAPIDASH',     rarity=4).save()
    Pokemon( id=79,   name='Slowpoke',          internal_name='SLOWPOKE',     rarity=3).save()
    Pokemon( id=80,   name='Slowbro',           internal_name='SLOWBRO',      rarity=4).save()
    Pokemon( id=81,   name='Magnemite',         internal_name='MAGNEMITE',    rarity=3).save()
    Pokemon( id=82,   name='Magneton',          internal_name='MAGNETON',     rarity=5).save()
    Pokemon( id=83,   name='Farfetch\'d',       internal_name='FARFETCHD',    rarity=5).save()
    Pokemon( id=84,   name='Doduo',             internal_name='DODUO',        rarity=2).save()
    Pokemon( id=85,   name='Dodrio',            internal_name='DODRIO',       rarity=4).save()
    Pokemon( id=86,   name='Seel',              internal_name='SEEL',         rarity=3).save()
    Pokemon( id=87,   name='Dewgong',           internal_name='DEWGONG',      rarity=5).save()
    Pokemon( id=88,   name='Grimer',            internal_name='GRIMER',       rarity=4).save()
    Pokemon( id=89,   name='Muk',               internal_name='MUK',          rarity=5).save()
    Pokemon( id=90,   name='Shellder',          internal_name='SHELLDER',     rarity=3).save()
    Pokemon( id=91,   name='Cloyster',          internal_name='CLOYSTER',     rarity=5).save()
    Pokemon( id=92,   name='Gastly',            internal_name='GASTLY',       rarity=2).save()
    Pokemon( id=93,   name='Haunter',           internal_name='HAUNTER',      rarity=3).save()
    Pokemon( id=94,   name='Gengar',            internal_name='GENGAR',       rarity=5).save()
    Pokemon( id=95,   name='Onix',              internal_name='ONIX',         rarity=3).save()
    Pokemon( id=96,   name='Drowzee',           internal_name='DROWZEE',      rarity=3).save()
    Pokemon( id=97,   name='Hypno',             internal_name='HYPNO',        rarity=3).save()
    Pokemon( id=98,   name='Krabby',            internal_name='KRABBY',       rarity=2).save()
    Pokemon( id=99,   name='Kingler',           internal_name='KINGLER',      rarity=4).save()
    Pokemon( id=100,  name='Voltorb',           internal_name='VOLTORB',      rarity=3).save()
    Pokemon( id=101,  name='Electrode',         internal_name='ELECTRODE',    rarity=5).save()
    Pokemon( id=102,  name='Exeggcute',         internal_name='EXEGGCUTE',    rarity=3).save()
    Pokemon( id=103,  name='Exeggutor',         internal_name='EXEGGUTOR',    rarity=4).save()
    Pokemon( id=104,  name='Cubone',            internal_name='CUBONE',       rarity=3).save()
    Pokemon( id=105,  name='Marowak',           internal_name='MAROWAK',      rarity=4).save()
    Pokemon( id=106,  name='Hitmonlee',         internal_name='HITMONLEE',    rarity=4).save()
    Pokemon( id=107,  name='Hitmonchan',        internal_name='HITMONCHAN',   rarity=3).save()
    Pokemon( id=108,  name='Lickitung',         internal_name='LICKITUNG',    rarity=3).save()
    Pokemon( id=109,  name='Koffing',           internal_name='KOFFING',      rarity=3).save()
    Pokemon( id=110,  name='Weezing',           internal_name='WEEZING',      rarity=4).save()
    Pokemon( id=111,  name='Rhyhorn',           internal_name='RHYHORN',      rarity=3).save()
    Pokemon( id=112,  name='Rhydon',            internal_name='RHYDON',       rarity=4).save()
    Pokemon( id=113,  name='Chansey',           internal_name='CHANSEY',      rarity=4).save()
    Pokemon( id=114,  name='Tangela',           internal_name='TANGELA',      rarity=3).save()
    Pokemon( id=115,  name='Kangaskhan',        internal_name='KANGASKHAN',   rarity=5).save()
    Pokemon( id=116,  name='Horsea',            internal_name='HORSEA',       rarity=3).save()
    Pokemon( id=117,  name='Seadra',            internal_name='SEADRA',       rarity=4).save()
    Pokemon( id=118,  name='Goldeen',           internal_name='GOLDEEN',      rarity=3).save()
    Pokemon( id=119,  name='Seaking',           internal_name='SEAKING',      rarity=4).save()
    Pokemon( id=120,  name='Staryu',            internal_name='STARYU',       rarity=2).save()
    Pokemon( id=121,  name='Starmie',           internal_name='STARMIE',      rarity=4).save()
    Pokemon( id=122,  name='MrMime',            internal_name='MR_MIME',      rarity=4).save()
    Pokemon( id=123,  name='Scyther',           internal_name='SCYTHER',      rarity=3).save()
    Pokemon( id=124,  name='Jynx',              internal_name='JYNX',         rarity=3).save()
    Pokemon( id=125,  name='Electabuzz',        internal_name='ELECTABUZZ',   rarity=3).save()
    Pokemon( id=126,  name='Magmar',            internal_name='MAGMAR',       rarity=3).save()
    Pokemon( id=127,  name='Pinsir',            internal_name='PINSIR',       rarity=2).save()
    Pokemon( id=128,  name='Tauros',            internal_name='TAUROS',       rarity=3).save()
    Pokemon( id=129,  name='Magikarp',          internal_name='MAGIKARP',     rarity=2).save()
    Pokemon( id=130,  name='Gyarados',          internal_name='GYARADOS',     rarity=5).save()
    Pokemon( id=131,  name='Lapras',            internal_name='LAPRAS',       rarity=4).save()
    Pokemon( id=132,  name='Ditto',             internal_name='DITTO',        rarity=5).save()
    Pokemon( id=133,  name='Eevee',             internal_name='EEVEE',        rarity=2).save()
    Pokemon( id=134,  name='Vaporeon',          internal_name='VAPOREON',     rarity=4).save()
    Pokemon( id=135,  name='Jolteon',           internal_name='JOLTEON',      rarity=4).save()
    Pokemon( id=136,  name='Flareon',           internal_name='FLAREON',      rarity=5).save()
    Pokemon( id=137,  name='Porygon',           internal_name='PORYGON',      rarity=4).save()
    Pokemon( id=138,  name='Omanyte',           internal_name='OMANYTE',      rarity=3).save()
    Pokemon( id=139,  name='Omastar',           internal_name='OMASTAR',      rarity=5).save()
    Pokemon( id=140,  name='Kabuto',            internal_name='KABUTO',       rarity=3).save()
    Pokemon( id=141,  name='Kabutops',          internal_name='KABUTOPS',     rarity=5).save()
    Pokemon( id=142,  name='Aerodactyl',        internal_name='AERODACTYL',   rarity=4).save()
    Pokemon( id=143,  name='Snorlax',           internal_name='SNORLAX',      rarity=3).save()
    Pokemon( id=144,  name='Articuno',          internal_name='ARTICUNO',     rarity=5).save()
    Pokemon( id=145,  name='Zapdos',            internal_name='ZAPDOS',       rarity=5).save()
    Pokemon( id=146,  name='Moltres',           internal_name='MOLTRES',      rarity=5).save()
    Pokemon( id=147,  name='Dratini',           internal_name='DRATINI',      rarity=3).save()
    Pokemon( id=148,  name='Dragonair',         internal_name='DRAGONAIR',    rarity=4).save()
    Pokemon( id=149,  name='Dragonite',         internal_name='DRAGONITE',    rarity=4).save()
    Pokemon( id=150,  name='Mewtwo',            internal_name='MEWTWO',       rarity=5).save()
    Pokemon( id=151,  name='Mew',               internal_name='MEW',          rarity=5).save()


if __name__ == '__main__':
    DB(wipe=True)
    insert_pokemon()



```

## Python links

- Learn Python: https://pythonbasics.org/
- Python Tutorial: https://pythonprogramminglanguage.com
