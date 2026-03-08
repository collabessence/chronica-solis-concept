# Chronica Solis: Eclipse — Architektura techniczna

## Silnik

- Godot 4.6
- GDScript
- Renderer: gl_compatibility (2D pixel art)
- Viewport: 576×324, stretch canvas_items + expand

---

## Stan projektu

- **StartMenu** — ekran startowy (Rozpocznij, Wczytaj grę, Ustawienia)
- **main.tscn** — RoomBase, Player, Checkpoint, HUD, PauseMenu, DeathOverlay
- **Mechanika** — HitboxComponent, HurtboxComponent, ParryComponent, StatSheet, StaminaComponent, PoiseComponent
- **Systemy** — GameState, EventBus, SaveSystem, SettingsManager
- **Assets** — tile, player, checkpoint, ikony HUD, efekty (generate_assets.py)

---

## Struktura projektu

```
res://
├── scenes/
│   ├── ui/              StartMenu, HUD, PauseMenu, DeathOverlay, SettingsMenu
│   ├── world/           main.tscn, RoomBase.tscn, Checkpoint.tscn
│   └── player/          Player.tscn
├── scripts/
│   ├── Bootstrap.gd
│   ├── combat/          HitboxComponent.gd, HurtboxComponent.gd, ParryComponent.gd
│   ├── stats/           StatSheet.gd
│   ├── player/          StaminaComponent.gd, PoiseComponent.gd
│   └── systems/         GameState.gd, EventBus.gd, SaveSystem.gd, SettingsManager.gd
├── data/enemies/        test_enemy.json, boss.json, crawler.json, ...
├── assets/
│   ├── icons/           teeth, hp_heart, stamina, poise (HUD)
│   ├── tiles/           tile_floor, tile_wall, tile_floor_dark, tile_rust_floor, tile_metal_plate, checkpoint_flag
│   ├── player/          player_idle.png
│   ├── audio/           attack, hit, parry, death, checkpoint, pickup (.wav)
│   ├── effects/         hit_slash, parry_spark, blood_splash
│   ├── concept/         concept art (wszystkie pliki w jednym folderze)
│   └── ui/              game_theme.tres, menu_background.png
├── docs/                LORE.md, GAMEPLAY.md, ASSETS.md, ...
└── tools/               generate_assets.py, pixel_utils.py, generate_sfx.py
```

---

## Autoloady (Project Settings)

| Nazwa | Typ | Opis |
|-------|-----|------|
| GameState | scripts/systems/GameState.gd | player_teeth, last_checkpoint, last_room_path, defeated_bosses, pending_teeth |
| EventBus | scripts/systems/EventBus.gd | Sygnały globalne |
| SaveSystem | scripts/systems/SaveSystem.gd | save(), load_game(), save_with_position(pos, room_path) → user://save.json |
| SettingsManager | scripts/systems/SettingsManager.gd | master_volume, fullscreen. load_settings(), save_settings() → user://settings.json |

---

## Zasady kodu

1. **class_name** + komentarz po polsku na początku skryptu
2. **Sygnały** (EventBus) zamiast bezpośrednich referencji między niezwiązanymi węzłami
3. **Dane** w .json (data/enemies/) lub Resource — nie na twardo w kodzie
4. **Komponenty** (Hitbox, Hurtbox, Stamina, Poise) jako osobne węzły/skrypty
5. **Typowanie:** Jawny typ przy Variant. Unikać Unicode (→, —) w komentarzach.

---

## EventBus — sygnały

| Sygnał | Parametry | Odbiorcy |
|--------|-----------|----------|
| enemy_died | enemy, position, teeth | GameState |
| boss_defeated | boss, position | GameState |
| room_transition_requested | room_path, spawn_position | (do implementacji) |
| player_died | position | GameState |

---

## Dokumentacja

| Plik | Zawartość |
|------|-----------|
| docs/README.md | Spis dokumentów |
| docs/chronicalore.md | Lore — timeline, kasty, klasy, statusy, fabuła |
| docs/AUDIT.md | Audyt stanu projektu |
| docs/ARCHITECTURE.md | Ten plik |
| docs/NOMENCLATURE.md | teeth, HP, Stamina, statystyki |
| docs/GAMEPLAY.md | Inspiracje, mechaniki |
| docs/ASSETS.md | Styl, ścieżki assetów |
| docs/PROMPT_GODOT_SPECJALISTA.md | Prompt dla agenta |
