# com.kruty1918.vfx

Reusable VFX layer extracted from Moyva: `VfxPool` (pooled spawn, budgets,
per-key cooldown), `VfxEffect`, `VfxDefinitionRegistry`, `VfxQualityState`,
`VfxRendererFlash`, `VfxUnitSnapshotStore`, and contracts (`VfxSpawnRequest`,
`IVfxSpawner`, `IVfxService`, `VfxEffectRule`, `VfxBudgetSettings`).

Host provides: event-id constants, the JSON/serialized catalog
(`VfxCatalogConfig`-like), domain event wiring (e.g. `GameplayVfxService`),
and quality-profile mapping.

## Install (Unity Package Manager)

Package Manager → **+** → **Add package from git URL**:

```
https://github.com/kruty1918dev-ai/com.kruty1918.vfx.git
```

or in `Packages/manifest.json`:

```json
"com.kruty1918.vfx": "https://github.com/kruty1918dev-ai/com.kruty1918.vfx.git#v0.1.0"
```

The repository is private — Git credentials (PAT / Git Credential Manager)
are required on every machine that resolves the package.

## API surface

| Type | Purpose |
|---|---|
| `IVfxService` / `IVfxSpawner` | Spawn requests routed through budgets, cooldowns and quality scaling |
| `VfxSpawnRequest` | Spawn descriptor (effect id, position, parent, overrides) |
| `VfxPool` / `VfxEffect` | Pooled effect lifecycle |
| `VfxDefinitionRegistry` | Effect-id → prefab/config lookup |
| `VfxQualityState` / `VfxBudgetSettings` | Quality scaling and per-frame spawn budgets |
| `VfxRendererFlash` | Hit feedback flashes on renderers |
| `VfxUnitSnapshotStore` | Last-known visual state for effects anchored to units |

## Model

Pool-first spawning keeps allocations flat; the host owns which domain event
maps to which effect id — the package stays game-agnostic.
