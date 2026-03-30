<div align="center">

# Daemon Swords 3 Endless

**A Procedurally Generated Action Roguelike with Deterministic Voice & Narrative**

*Powered by ZeroBytes Position-is-Seed — Infinite Dungeons, Voices, and Stories from a Single Seed*

[![TypeScript](https://img.shields.io/badge/TypeScript-5.8-blue.svg)](https://www.typescriptlang.org/)
[![React](https://img.shields.io/badge/React-19-61dafb.svg)](https://reactjs.org/)
[![Tauri](https://img.shields.io/badge/Tauri-2-ffc131.svg)](https://tauri.app/)
[![Vite](https://img.shields.io/badge/Vite-6.4-646cff.svg)](https://vitejs.dev/)

</div>

---

## Overview

Daemon Swords 3 Endless is an action roguelike where you play as a sentient daemon blade seeking hosts to possess and enemies to slay. Every room, enemy, voice, dialogue line, and adventure chronicle entry is deterministically generated from world coordinates using the **ZeroBytes** family of procedural systems. The same seed produces the same world, the same enemies, the same voices, the same story — across sessions, across machines, zero storage.

### The ZeroBytes Principle

> *"The coordinate IS the seed. Zero bytes store infinity."*

Eight ZeroBytes-compatible systems work together:

| Layer | System | Purpose |
|-------|--------|---------|
| ZeroBytes | `proceduralGen.ts` | Room, tile, enemy generation from coordinates |
| Zero-Field | `zeroField.ts` | Corruption gradients, affinity territory fields |
| Zero-Quadratic | `zeroQuadratic.ts` | Enemy social bonds (allied/rival pairs) |
| Zero-Cubic | `zeroCubic.ts` | Triangle formation dynamics (three-entity emergent behaviour) |
| ZeroResponse | `speech/` | Deterministic NPC dialogue from spawn position + class |
| ZeroVoice | `voice/` | Deterministic voice identity (26 Kokoro voices, gender pools) |
| ZeroLog | `zerolog/` | Structured event capture (17 event types) |
| ZeroLogENH | `zerolog-enh/` | Narrative prose generation from event logs |

---

## Features

### Core Gameplay
- **Possess Hosts** — Take control of enemies to fight for you
- **6 Weapon Types** — Sword, Daggers, Trident, Halberd, Chain, Lightning Rod
- **6 Affinities** — Goblin, Skeleton, Demon, Beast, Ghost, Elemental
- **Level Up System** — Gain XP, unlock charge attacks and special abilities
- **Passive Upgrades** — Damage, Speed, HP, Cooldown, Light Radius, Stamina

### Infinite Procedural Dungeons
- **Endless exploration** — Rooms generate on-demand as you explore in any direction
- **8 room types** — Spawn, Combat, Boss, Treasure, Puzzle, Secret, Rest, Empty
- **Dynamic corridors** — Automatically connect adjacent rooms
- **Floor transitions** — Stairs up and down between floors
- **6 character classes** — Warrior, Mage, Rogue, Paladin, Necromancer, Ranger
- **5 rarity tiers** — Common, Uncommon, Rare, Epic, Legendary
- **Procedural names** — Generated from syllable combinations
- **40+ body parts** — Mix and match heads, torsos, arms, legs, weapons
- **Color tinting** — Unique skin, hair, and armor colours per enemy

### Zero-Field: Territorial Warfare
- **Corruption field** — Multi-scale noise field tinted into floor/wall rendering, cleansed by boss kills
- **Affinity territories** — Six competing scalar fields determine regional dominance
- **Territory defence buffs** — Enemies in home territory gain up to 1.4x damage reduction with visible shield ring
- **Field-driven spawning** — Dynamic spawns gravitate to affinity field peaks

### Zero-Quadratic & Zero-Cubic: Social Dynamics
- **Enemy social bonds** — Allied pairs flank together, rivals maintain distance
- **Triangle formations** — Allied trios coordinate in equilateral formation with synchronised 70% windup attacks
- **Parry hesitation** — Stunning a triangle member causes partners to briefly hesitate

### ZeroResponse: NPC Speech
- **Deterministic dialogue** — Every enemy speaks class-appropriate lines derived from spawn position
- **7 creature profiles** — Goblin (erratic), Skeleton (duty-bound), Demon (imperious), Beast (primal), Ghost (mournful), Elemental (impersonal), Boss (commanding)
- **Billions of combinations** — 10-13 templates x 20-31 vocabulary pools per class
- **Speech bubbles** — Floating text with semi-transparent background, auto-truncation

### ZeroVoice: Deterministic Voice Identity
- **26 Kokoro base voices** — 14 female (American + British), 12 male
- **Gender-filtered pools** — Deterministic gender from spawn coordinates
- **Voice blending** — Two voices interpolated with pitch and energy scaling
- **Voice tags** — Muted subtitle showing assigned voice name on speech bubbles

### KokoroTTS: Real-Time Speech Synthesis
- **ONNX Runtime** — int8-quantised KokoroTTS model (~88 MB) via Tauri Rust backend
- **eSpeak-NG phonemisation** — Text to IPA to Kokoro tokens
- **Zero-Quadratic arc properties** — Curve warp, spectral skew, harmonic blend shape voice interpolation
- **First-run asset download** — Model, voices, and eSpeak-NG downloaded on first launch with progress UI
- **Web Audio API playback** — 24 kHz mono PCM played through browser audio
- **Async non-blocking** — Synthesis runs off main thread, text appears immediately, audio follows

### ZeroLog & ZeroLogENH: Adventure Chronicle
- **17 event types** — Kills, boss defeats, possession, floor transitions, NPC speech, upgrades, reforges, affinity changes, corruption cleansing, cache looting, saves, deaths
- **Chapter system** — Each floor is a chapter, auto-incremented on descent
- **Narrative prose** — Events transformed into immersive dungeon chronicle sentences via deterministic template + vocabulary pool selection
- **Persistent across sessions** — Log saved/loaded with game state
- **Download as .txt** — Full chronicle exportable at death screen
- **Ctrl+F11 overlay** — Live parchment-style narrative view (last 20 entries)

### Debug Tools
- **Ctrl+F9** — Debug console overlay (colour-coded log/warn/error capture)
- **Ctrl+F10** — TTS test key (sends "hello world" to synthesis engine)
- **Ctrl+F11** — Adventure chronicle overlay

---

## Controls

| Key | Action |
|-----|--------|
| WASD | Move host |
| Mouse | Aim |
| Left Click | Attack (hold to charge at level 2+) |
| Right Click | Special attack (level 3+) |
| Space | Ping for nearby hosts (when grounded) |
| E | Interact (Forge, Inverter) |
| F | Release host |
| 1-3 | Select upgrade |
| F5 | Quick Save |
| F9 | Quick Load |
| Ctrl+F9 | Debug console |
| Ctrl+F10 | TTS test |
| Ctrl+F11 | Adventure chronicle |

---

## Installation

### Desktop App (Tauri)

Download the latest MSI or NSIS installer from the releases. On first launch, the TTS engine downloads ~106 MB of voice assets automatically.

---

### ZeroBytes Salt Allocation

All procedural systems use independent salt values to ensure decorrelation:

| Range | System |
|-------|--------|
| `0 - 250000` | Core ZeroBytes (stats, appearance, rooms, spawns, loot, features) |
| `300000 - 450000` | Zero-Field (corruption, 6 affinity territories) |
| `500000` | Zero-Quadratic (enemy social bonds) |
| `600000` | Zero-Cubic (triangle formations) |
| `0x700001 - 0x700006` | ZeroVoice (voice A/B, blend, pitch, energy, gender) |

---

## Save Data

```typescript
interface SaveData {
  version: number;
  worldSeed: number;
  floor: number;
  roomX: number;
  roomY: number;
  killCount: number;
  cleansingEvents: CleansingEvent[];
  adventureLog: LogEntry[];
  currentChapter: number;
  logSequence: number;
  blade: { level, xp, totalXp, weaponType, affinity, affinityStrength, passiveStats };
  possessedHost?: { type, health, maxHealth, stamina, maxStamina, affinity, color, puppetState, colors, proceduralData };
  timestamp: number;
}
```

---

## Changelog

### v0.8.4 — Caffeinated Speed Tuning
- Caffeinated enemy speed 6x (720 units/s, 3.6x player speed)
- Detection/chase range 9x (2700px — full screen awareness)

### v0.8.2 — Difficulty Modes (Stage 12)
- Journalist mode (default): all multipliers 1.0, current casual gameplay
- Caffeinated mode: 2x enemy speed, 2x attack rate, 3x detection/chase range
- Data-driven multiplier system via DIFFICULTY_CONFIGS (extensible for future modes)
- Difficulty toggle on main menu with Cinzel-styled UI
- Persisted in save data and localStorage across sessions

### v0.8.1 — Chronicle Modal
- Chronicle button in bottom-right, pulses gold after save or new chapter
- Full centered modal overlay replaces old corner panel and death-only download
- Scrollable narrative log with chapter dividers, Cinzel serif font
- Download .txt button accessible anytime (not just on death)
- Click-outside-to-close, Ctrl+F11 toggle preserved

### v0.8.0 — Main Menu & Title Screen
- Dark fantasy main menu with animated dust particles and fog effects
- Cinzel serif typography, aged gold palette, gothic atmosphere
- New Game / Continue / Settings menu with keyboard navigation
- Continue button only appears when save data exists
- Menu displays after TTS setup, before gameplay begins
- Staggered fade-in entrance animations

### v0.7.3 — Stage 10 Polish
- Pure art rendering for heads, torsos, weapons (tint overlay removed)
- Fix: sword orientation corrected via imageRotation field
- Head sizes increased 20% for better proportion with torso textures
- Fix: espeak-ng terminal no longer flashes on Windows (CREATE_NO_WINDOW)
- Fix: TTS subprocess focus theft and stuck keyboard input resolved

### v0.7.2 — Rayman-Style Puppet Rendering
- Arms and legs hidden (transparent) for floating-limb silhouette
- Hands and feet render as black gloves/boots
- Head offsets nudged down to close gap with torso art
- Part offset field now applied in renderer (was previously ignored)

### v0.7.1 — Art Assets, Dungeon Connectivity Fix
- 27 hand-painted character textures (heads, torsos, weapons) replace procedural shapes
- Asset pipeline: 2048px PNGs resized to spec, converted to .webp (348KB total)
- Image preloader with seamless procedural-shape fallback
- Canvas renderer uses drawImage with multiply-tint for color system
- Fix: dungeon corridors now connect center room to all 4 neighbors (star topology)
- Fix: spawn room no longer isolated — sequential-pair corridor bug replaced with adjacency check

### v0.7.0 — ZeroLog & ZeroLogENH Adventure Chronicle
- 17 event types captured into structured log lines
- Deterministic narrative prose via ZeroLogENH engine
- Chapter system (each floor = one chapter)
- Ctrl+F11 parchment-style chronicle overlay
- Download Chronicle button at death screen (.txt export)
- Adventure log persisted in save data

### v0.6.0 — Debug Console, Bug Fixes, TTS Hardening
- Ctrl+F9 debug console overlay (200-entry ring buffer)
- Ctrl+F10 TTS test key
- Fix: lucide-react Map import shadowing (black screen fix)
- Fix: ATTRACTED state preservation (possession restored)
- Fix: listen() guard for TTS init
- Fix: resumeAudioContext() on mousedown
- Fix: cleansingEvents added to GameState interface
- TTS setup screen with download progress and Skip TTS button

### v0.5.0 — KokoroTTS ONNX Backend
- Real-time NPC speech synthesis via Tauri Rust backend
- ~88 MB int8-quantised KokoroTTS model with first-run download
- eSpeak-NG phonemisation pipeline
- Zero-Quadratic arc-aware voice blending
- Web Audio API playback (24 kHz mono)

### v0.4.0 — Initial Migration to Daemon Swords 3 Endless
- ZeroResponse NPC speech system (7 creature profiles, billions of combinations)
- ZeroVoice deterministic voice assignment (26 Kokoro voices)
- ZeroSystems Stage 2 (territory buffs, triangle formations, field-driven spawning, corruption cleansing)
- Full PuppetJSX v2 ZeroBytes procedural generation
- Tauri desktop build with MSI/NSIS installers

### v1.0.0 — Original Release
- Core gameplay mechanics
- 6 weapon types
- Hand-crafted dungeon layouts
- Basic enemy AI

---

## Credits

- **Game Design & Development** — React + TypeScript + Vite + Tauri
- **Procedural Systems** — ZeroBytes position-is-seed architecture
- **TTS Engine** — KokoroTTS ONNX (int8-quantised)
- **Phonemisation** — eSpeak-NG
- **AI Assistance** — Claude (Anthropic)

---

## License

MIT License — See LICENSE file for details

---

<div align="center">

**"The blade remembers. The dungeon is eternal. The chronicle endures."**

*Enter a seed. Explore forever. Download your story.*

</div>

## 📚 Citation

### Academic Citation

If you use this codebase in your research or project, please cite:

```bibtex
@software{daemon_swords_3_endless,
  title = {Daemon Swords 3 Endless: you play as a sentient daemon blade seeking hosts to possess and enemies to slay. Every room, enemy, voice, dialogue line, and adventure chronicle entry is deterministically generated from world coordinates using the ZeroBytes family},
  author = {[Drift Johnson]},
  year = {2025},
  url = {https://github.com/MushroomFleet/Daemon-Swords-3-Endless},
  version = {1.0.0}
}
```

### Donate:


[![Ko-Fi](https://cdn.ko-fi.com/cdn/kofi3.png?v=3)](https://ko-fi.com/driftjohnson)
