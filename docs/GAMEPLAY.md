# Chronica Solis: Eclipse — Gameplay

## Inspiracje

- **Blasphemous** — ciężki combat, parry, kary za błędy, wall-cling, gore
- **Hollow Knight** — precyzyjny ruch, responsywne sterowanie, odkrywanie mapy
- **Dead Cells** — styl graficzny (pixel art, płynne animacje, ciemna paleta z mocnymi akcentami)

---

## Ruch gracza

| Mechanika | Sterowanie | Opis |
|-----------|------------|------|
| Chodzenie | A/D, strzałki | move_left, move_right |
| Skok | Spacja | jump |
| Dash | Shift | Krótki dystans, iframes, koszt staminy (20) |
| Wall-cling | Przy ścianie + kierunek w stronę ściany | Spowolniony opad. Używa move_left/move_right. |

---

## Combat

| Element | Sterowanie | Opis |
|---------|------------|------|
| Atak | Z | Hitbox przed graczem, koszt staminy (15) |
| Parry | E | Okno ~0.2s, odbicie trafienia, bonus staminy (15) |
| Iframes | — | Niewrażliwość po trafieniu (~0.5s), miganie sprite |
| Stamina | — | Regeneracja 20/s, zużycie przy dash i ataku |
| Poise | — | Odbiera poise_damage, przy zerze → stagger (0.5s) |

---

## Śmierć i checkpointy

- **Śmierć:** Strata teeth, respawn przy last_checkpoint (lub DEFAULT_SPAWN) po 2s.
- **Checkpoint:** Area2D — zapis pozycji i scene_file_path, SaveSystem.save_with_position()
- **Odzyskiwanie:** TeethPickup (do implementacji) — spawnuje przy ciele po śmierci (gdy amount > 0).

---

## Waluta

- **Zęby (teeth):** Drop z wrogów (Enemy 5, Boss 50, Crawler 2). Nigdy souls, orbs, gold.
- **HUD:** Licznik "Teeth: %d" z GameState.player_teeth

---

## Room transitions (do implementacji)

- Przejścia między pokojami (main ↔ Level02 ↔ Level03)
- RoomTransition (Area2D) emituje room_transition_requested
- TransitionOverlay: fade to black → change_scene → ustaw player.global_position → fade in

---

## Zrealizowane elementy

1. ✓ Ruch gracza (chodzenie, skok, dash, wall-cling)
2. ✓ Combat loop (atak, hitboxy, iframy, parry, stamina, poise)
3. ✓ RoomBase (TileMap + Floor, WallLeft, WallRight)
4. ✓ Checkpoint + zapis (last_checkpoint, last_room_path)
5. ✓ HUD (HP, stamina, poise, teeth)
6. ✓ PauseMenu, DeathOverlay
7. ✓ StartMenu, SettingsMenu

---

## Brakuje (audyt)

| Kategoria | Brak |
|-----------|------|
| **Wrogowie** | Enemy, Boss, Crawler, AI |
| **Room transitions** | Przejścia między poziomami, TransitionOverlay |
| **TeethPickup** | Odzyskiwanie teeth przy ciele |
| **Audio** | Muzyka w tle, muzyka per poziom/boss |
| **Wizualne** | Prawdziwe animacje (osobne klatki), zróżnicowane poziomy |
| **Gameplay** | Mapa, sklep, ekonomia teeth, ekwipunek, efekty statusowe |
| **Progresja** | Warunek zwycięstwa, ekran końcowy |
| **UX** | Tutorial, przypisywanie klawiszy, wiele slotów zapisu |
