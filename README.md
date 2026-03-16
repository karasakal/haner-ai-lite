# 🧠 Haner AI Free — Enemy AI for Unity

[![Unity](https://img.shields.io/badge/Unity-2021.3%2B-black?logo=unity)](https://unity.com)
[![License](https://img.shields.io/badge/License-MIT-green)](#license)
[![Asset Store](https://img.shields.io/badge/Pro%20Version-$59.99-7c3aed)](https://assetstore.unity.com)
[![Publisher](https://img.shields.io/badge/Publisher-Haner%20Games-purple)](https://hanergames.com.tr)

> Free, single-script enemy AI for Unity. 8 states, FOV + hearing + touch perception, basic cover, NavMesh movement. Great starting point — upgrade to [Haner AI Pro](https://assetstore.unity.com) when you need more.

---

## What's Included

| Feature | Free | [Pro — $59.99](https://assetstore.unity.com) |
|---------|:----:|:----:|
| States | **8** | 14 |
| Vision (FOV) | Single ray | 3-ray LOS, peripheral, motion bonus |
| Hearing | Tag overlap | ISoundSource interface, suppressor, tag filter |
| Touch sense | ✓ | ✓ |
| Scent / trail | ✗ | ✓ wind direction, time-decay |
| Awareness Score | ✗ | ✓ 0–100, 4 AlertPhase levels |
| Behaviour Tree | ✗ | ✓ full abort system (Self / LowerPriority / Both) |
| Emotional system | ✗ | ✓ Morale / Fear / Anger → accuracy & speed |
| Cover | Nearest tag | ✓ scored selection + peek & shoot |
| Squad system | ✗ | ✓ 6 roles, leader election, flanking, pincer |
| LOD optimisation | ✗ | ✓ 4 tiers, NavMesh quality scaling |
| Movement backend | NavMesh | NavMesh + Rigidbody (switchable) |
| Hit zones | ✗ | ✓ Head ×2.5, Limb ×0.6, armour |
| C# Events | 2 | 18 |
| Files | 1 script | 10 scripts |

---

## Quick Start

```
1. Copy Assets/HanerAIFree/ into your project
2. Haner AI Free → ▶ Build Demo Scene
3. Window → AI → Navigation → Bake
4. ▶ Play
```

---

## Setup

Add `HanerAIFree` to a NavMeshAgent GameObject:

```csharp
// Assign in Inspector:
// targetLayers    → layers the AI treats as threats
// obstacleLayers  → layers that block vision rays
// patrolWaypoints → patrol route transforms
```

---

## API

```csharp
// Give the AI a target
ai.SetTarget(playerTransform);

// Alert to a position (heard something)
ai.Alert(noisePosition);

// Deal damage
ai.TakeDamage(25f);

// Events
ai.OnDeath   += () => HandleKill();
ai.OnDamaged += (dmg) => SpawnHitEffect();

// Read state
AIState s = ai.CurrentState;
float   h = ai.HealthNorm;   // 0–1
```

---

## States

`Idle` → `Patrol` → `Investigate` → `Alert` → `Combat` → `TakeCover` → `Retreat` → `Dead`

---

## Inspector Fields

| Field | Description |
|-------|-------------|
| `targetLayers` | Layers treated as threats |
| `obstacleLayers` | Layers that block LOS rays |
| `fieldOfView` | Vision cone angle (30–360°) |
| `visionRange` | Vision distance |
| `hearingRadius` | Hearing radius |
| `soundTriggerTag` | Tag that triggers hearing (e.g. `Player`) |
| `touchRadius` | Proximity trigger radius |
| `attackRange` | Fire range |
| `attackCooldown` | Time between shots |
| `retreatHPPct` | HP% threshold that triggers retreat (0–1) |
| `coverTag` | Tag of cover objects |
| `coverSearchRadius` | How far to search for cover |

---

## Known Limitations vs Pro

**Single-ray vision** — partial cover is not handled correctly. An agent can see through a half-open door. Pro uses 3 parallel rays (head/body/low).

**Tag-based hearing** — no loudness, no suppressor support, no sound type filtering. Pro uses the `ISoundSource` interface — any object can emit calibrated sound.

**Nearest-cover selection** — the agent picks the closest cover object regardless of whether it actually blocks the threat. Pro scores by LOS quality, protection angle, and occupancy.

**No squad awareness** — when an agent dies, no other agent knows. Pro broadcasts `AllyDown` to the squad and lowers morale.

**Flat accuracy** — every shot has the same spread. Pro accuracy is modified by the emotional state: a frightened agent fires faster but less accurately.

---

## Support

- **Bug reports:** [github.com/karasakal/haner-ai-free/issues](https://github.com/karasakal/haner-ai-free/issues)
- **Pro version:** [hanergames.com.tr](https://hanergames.com.tr)
- **Email:** info@hanergames.com.tr

---

## License

MIT — free for personal and commercial use.

© 2026 Haner Games — hanergames.com.tr
