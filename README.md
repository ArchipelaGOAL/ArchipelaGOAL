# ArchipelaGOAL II - Jak 2 Archipelago Mod

This is a modded version of the OpenGOAL decompilation project for Jak 2, integrating **Archipelago multiworld randomizer** functionality. It implements comprehensive Archipelago support for randomizing and tracking Jak 2 missions and items.

## 📝 Short Summary of Features

### **Core Archipelago Integration**

- **Memory Communication System**: Implements a shared memory structure (`ap-info-jak2`) that communicates game state with the Archipelago client
- **Mission Tracking**: Tracks completion of 70 main missions and 24 side missions
- **Item Reception System**: Handles receiving randomized items from other Archipelago worlds
- **Route Management**: Controls access to different city areas based on received items

## 🎯 Key Features

### 1. **Mission & Side Mission Tracking**

- Automatically tracks when missions are completed via `ap-mission-checked!`
- Side missions tracked separately via `ap-side-mission-checked!`
- Mission IDs are written to shared memory for the AP client to read

### 2. **Item Reception System** (`ap-item-received!`)

The mod can receive and process the following items:

**Weapons & Mods:**

- Scatter Gun (Red)
- Blaster Mod (Yellow)
- Vulcan Barrel (Blue)
- Peace Maker (Dark)

**Security Passes:**

- Red Security Pass
- Green Security Pass
- Yellow Security Pass
- Purple Security Pass (Palace)
- Black Security Pass (Weapons Factory)
- Air Train Pass

**Dark Jak Powers:**

- Dark Jak transformation
- Dark Bomb
- Dark Blast
- Dark Invincibility
- Dark Giant

**Equipment & Upgrades:**

- Jetboard
- Titan Suit
- Seal of Mar
- Rift Rider
- Gun Speed Upgrade
- Gun Ammo Upgrade
- Gun Damage Upgrade

**Story Items:**

- Mountain Lens
- Mountain Gear
- Mountain Shard
- Ruby Key
- Heart of Mar
- Time Map
- Precursor Stone
- Life Seed

### 3. **City Area Access Control**

Routes between city areas are controlled by received items:

- `ap-route-slums-to-port?`
- `ap-route-slums-to-stadium?`
- `ap-route-slums-to-market?`
- `ap-route-port-to-stadium?`
- `ap-route-port-to-market?`
- `ap-route-market-to-stadium?`
- `ap-route-slums-to-landing?`
- `ap-route-slums-to-nest?`

### 4. **UI Updates**

- Visual indicators for received items
- In-game text notifications when items are received
- Mission tree segmented by level, opening nodes based on items
- All receivable items have corresponding UI elements

### 5. **Bug Fixes & Logic Improvements**

- Fixed vehicle training closure issues
- Air train logic corrections at Nest
- Fortress and sewer level loading fixes
- Mountain temple door modifications
- Tomb poles, water sections, and boss fights adjusted
- Strip Mine, Dig Site, and Drill Platform mission fixes
- Purple pass delay fix
- Talker spawn removals from cutscenes
- Side mission logic improvements

## 📂 File Structure

### **Archipelago-specific files:**

```
goal_src/jak2/pc/features/
├── archipelago.gc       # Main AP autosplitter/tracking
├── ap-struct.gc        # AP item reception & mission checking
└── ap-struct-h.gc      # AP structure definitions
```

### **Modified core files:**

- `task-control.gc` - Mission completion hooks
- `game-task.gc` - Task system modifications
- `warp-gate.gc` - Area transition logic
- Various level-specific scene and obs files

## 🚀 Entry Points

### 1. **Memory Interface** (Version 1)

- Struct at `*ap-info-jak2*` contains all tracking data
- Version field ensures compatibility with AP client
- End marker "end" for memory boundary detection

### 2. **Mission Completion Hook**

- Integrated into `task-control.gc`
- Automatically calls `ap-mission-checked!` on task completion
- Tracks both main and side missions

### 3. **Item Reception**

- `ap-item-received!` function processes incoming items
- Spawns appropriate talkers with confirmation messages
- Adds items to inventory using game-task-node commands

## 🎮 Usage

This mod is designed to work with the Archipelago multiworld system:

1. **Game Communication**: The game communicates with an external Archipelago client via shared memory
2. **Mission Tracking**: Mission completions are automatically tracked and sent to the AP server
3. **Item Reception**: Items from other worlds are received and integrated into the game
4. **Progressive Unlocks**: City areas and content unlock based on received items rather than normal progression

## 🔧 Technical Details

- **Memory Version**: 2 (must match `expected_memory_version` in MemoryReader.py of Archipelago)
- **Mission Capacity**: 70 main missions, 24 side missions
- **Shared Memory Structure**: Uses arrays for tracking checked missions
- **Item Integration**: Uses existing game-task-node-command system for adding items
- **Talker System**: Each item spawns a talker with appropriate dialogue

## 📈 Development Progress

### Accomplished Tasks

- [x] Complete mission tree segmentation system
- [x] All items have corresponding UI elements
- [x] Side mission and collectible tracking implementation
- [x] Extensive bug fixes for mission logic across all levels
- [x] Proper talker spawns for all receivable items
- [x] Debug information system for tracking AP checks

### Known Areas of Work

- Collectibles (orbs, skull gems) tracking integration
- Further refinement of mission dependencies
- Additional route logic for late-game areas(?)

## 🔗 Integration with Archipelago

This mod allows Jak 2 to participate in Archipelago multiworld randomizers. Players can:

- Send Jak 2 mission completions as checks to other worlds
- Receive items from other games that unlock Jak 2 content
- Experience a randomized progression through Haven City
- Play cooperatively with friends in other games

## 🛠️ Building the Mod

To compile the goalc compiler with Archipelago support:

```bash
# Configure the build
cmake -B build

# Build goalc
cmake --build build --target goalc --config Release
```

The compiled goalc will be available at:
`build/goalc/Release/goalc.exe`

---

*This mod is built on top of the OpenGOAL project and the OpenGOAL-Mods base template.*
