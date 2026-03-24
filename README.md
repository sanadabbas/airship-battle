# Airship Battle — Space Conquest

A top-down 2D space battle game built in C++ with SFML.

## Features
- 5 ship types: Scout, Gunship, Dreadnought, Carrier, Miner
- LoL-style base structure: Outer Turrets → Inner Turrets → Shield Stations → Nexus
- Economy system: earn credits by destroying ships/structures, passive income
- Upgrade system: 6 upgrades per ship (damage, fire rate, shields, regen, speed, armor)
- AI opponents with patrol/chase/attack/retreat states, wave spawning
- Exploration: stars, planets, asteroid fields, nebulae, resource caches — discover them for credit bonuses
- Particle effects: explosions, debris, hit sparks
- Minimap, HUD with HP/shield bars, zone info

## Build Requirements
- C++17 compiler (g++ or clang++)
- SFML 2.6 (`libsfml-dev`)
- CMake 3.16+

## Build & Run
```bash
sudo apt install libsfml-dev cmake build-essential
mkdir build && cd build
cmake ..
make -j4
./AirshipBattle
```

## Controls
| Key | Action |
|-----|--------|
| W / Up | Thrust forward |
| S / Down | Thrust backward |
| A / Left | Turn left |
| D / Right | Turn right |
| Space / LCtrl | Fire |
| U | Open upgrade menu (near repair bay) |
| R | Repair hull at upgrade menu (50 credits) |
| ESC | Pause / close menus |
| 1-6 | Select upgrade |
| Enter | Confirm upgrade purchase |

## Ship Types
| Ship | HP | Shield | Speed | Role |
|------|----|--------|-------|------|
| Scout | 80 | 30 | 280 | Fast recon, long vision |
| Gunship | 150 | 60 | 180 | Balanced DPS |
| Dreadnought | 400 | 150 | 80 | Heavy siege |
| Carrier | 250 | 100 | 120 | Drone support |
| Miner | 120 | 20 | 150 | Passive credit income |

## Base Structure (per team)
Destroy in order:
1. **Outer Turrets** (3) — front line
2. **Inner Turrets** (3) — mid defense
3. **Shield Stations** (2) — protect the core
4. **Nexus** — win condition

The **Repair Bay** lets you upgrade your ship when nearby.

## Economy
- Kill credits: Scout 50, Gunship 80, Dreadnought 120, Carrier 100, Miner 60
- Structure kills: 40 credits each
- Passive income: +10 credits every 5 seconds
- Exploration discovery: 15–140 credits per zone
- Upgrades cost 150 credits each
- Hull repair: 50 credits (+50% HP)

## Project Structure
```
src/
├── main.cpp
├── Constants.h         — shared enums, balance values
├── Game.h / Game.cpp   — master loop, state machine, collision
├── entities/
│   ├── Entity.h        — base class (HP, shield, position)
│   ├── Ship.h          — player/AI ships, upgrades, rendering
│   ├── Structure.h     — bases, turrets, nexus
│   └── Projectile.h    — bullets
├── systems/
│   ├── EconomyManager.h
│   ├── World.h         — exploration zones, star generation
│   ├── ParticleSystem.h
│   └── AIController.h  — FSM AI (patrol/chase/attack/retreat)
└── ui/
    └── HUD.h           — bars, minimap, upgrade menu, notifications
```
