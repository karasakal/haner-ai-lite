# Changelog — Haner AI Free

## [1.0.0] — 2026

### Added
- HanerAIFree.cs: single-script AI with 8 states
- States: Idle, Patrol, Investigate, Alert, Combat, TakeCover, Retreat, Dead
- Vision: FOV cone with single-ray LOS
- Hearing: tag-based proximity overlap
- Touch: configurable radius proximity trigger
- Cover: tag-based nearest cover search
- Burst fire with configurable cooldown
- Retreat on low HP threshold
- NavMesh movement with per-state speeds
- OnDeath / OnDamaged C# events
- HanerAIFreeBuilder: one-click demo scene
