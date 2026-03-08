# Chronica Solis: Eclipse — Assets i grafiki

## Concept Art — Brief

**Wyobraź sobie concept arty do najbardziej wynaturzonej podziemnej rasy ludzkiej.**

- **Nie zombie** — to żywi ludzie, zdegradowani przez wieki w ciemnościach. Karykatury samych siebie.
- **Regres ewolucyjny:** brak światła, kanibalizm, praca w kopalniach, Zamknięty Cykl — ciała zrosły się z narzędziami (Effossus), żebra innych jako „zbroja" (Canis Osteus).
- **Groteska:** przesadzone proporcje, asymetria, deformacje. Goya, Bosch — nie „cool monster", lecz upadła ludzkość.
- **Gore:** krew, osteo-metal (kość+żelazo), blizny, ciało jako surowiec. Purgatory, nie fantasy.
- **Bohater:** wyłom społeczeństwa — nie superbohater. Zdegradowany, ale żywy. Pellio, Servus, Custos — wyrzutki.

---

## Styl (Dead Cells)

- **Pixel art** dokładnie w stylu Dead Cells
- **Obrysy:** mocne, ciemne (outline ~12,10,14)
- **Akcenty:** nasycone kolory (czerwień, miedź, rdza)
- **Kontrast:** wysoki — czytelne sylwetki
- **Paleta:** ciemne szarości, brązy, rdza, verdigris, kości, metal (LORE.md)

---

## Stan obecny (wygenerowane w tools/generate_assets.py)

### Tiles (assets/tiles/)

| Plik | Opis | Użycie |
|------|------|--------|
| tile_floor.png | Podłoga (szarobrązowa) | level_tileset, RoomBase |
| tile_wall.png | Ściana (ciemna) | level_tileset, RoomBase |
| tile_floor_dark.png | Ciemniejsza podłoga | level_tileset, RoomBase |
| tile_rust_floor.png | Zardzewiała podłoga | level_tileset, RoomBase |
| tile_metal_plate.png | Metalowa płyta | level_tileset, RoomBase |
| tile_blood.png | Plama krwi | level_tileset |
| tile_salt.png | Sól (Magnum Horreum) | level_tileset |
| tile_cracked_wall.png | Pęknięta ściana | level_tileset |
| tile_grating.png | Kratownica metalowa | level_tileset |
| checkpoint_flag.png | Maszt z flagą | Checkpoint.tscn |
| level_tileset.tres | TileSet (sources 0–4) | RoomBase |

### Ikony (assets/icons/)

| Plik | Użycie |
|------|--------|
| teeth.png | HUD — licznik zębów |
| hp_heart.png | HUD — HP |
| stamina.png | HUD — Stamina |
| poise.png | HUD — Poise |
| skull_small.png | Dekoracja |
| parry.png | Parry |
| dash.png | Dash |
| attack.png | Atak |

### Player (assets/player/)

| Plik | Użycie |
|------|--------|
| player_idle.png | Player.tscn (Sprite2D) |

### Enemies (assets/enemy/)

| Plik | Użycie |
|------|--------|
| enemy_idle.png | Enemy.tscn (Effossus) |
| relictum_solis_idle.png | RelictumSolis.tscn |
| canis_osteus_idle.png | CanisOsteus.tscn |
| salsamentarius_idle.png | Salsamentarius |
| boss_fodinae_idle.png | BossFodinae.tscn |

### UI (assets/ui/)

| Plik | Opis |
|------|------|
| icon.png | Ikona gry (concept art: czaszka) |
| menu_background.png | Tło StartMenu |
| game_theme.tres | Theme UI (przyciski, panele, labele) |

### Efekty (assets/effects/)

| Plik | Opis | Użycie |
|------|------|--------|
| hit_slash.png | Efekt cięcia | (do podpięcia w HitboxComponent) |
| parry_spark.png | Iskra parry | (do podpięcia w ParryComponent) |
| blood_splash.png | Plama krwi | (do podpięcia przy trafieniu) |

### Concept art (assets/concept/)

| Plik | Opis |
|------|------|
| concept_gr_0.jpg – concept_gr_3.jpg | Referencje stylu |
| concept_su_1.jpg – concept_su_4.jpg | Referencje stylu |
| pellio_concept.png, vincti_bust_concept.png, … | Postacie, wrogowie, lokacje, broń, rekwizyty |

---

## Planowane (do wygenerowania / ręcznego stworzenia)

### Tiles (plan)

| Plik | Opis |
|------|------|
| tile_bones.png | Stos kości |
| tile_vent.png | Wlot/wylot rur |
| tile_corner_wall.png | Narożnik ściany |
| tile_pipe_h.png | Rura pozioma (32×16) |
| tile_pipe_v.png | Rura pionowa (16×32) |

### Ikony (plan)

| Plik | Użycie |
|------|--------|
| gear_cog.png | Maszyneria |
| death_skull.png | Śmierć |
| key_bone.png | Klucz z kości |
| map.png | Mapa |
| save_point.png | Punkt zapisu |

### Concept art — struktura (spłaszczona)

```
assets/concept/         # Wszystkie pliki graficzne w jednym folderze (bez podfolderów)
```

---

## Audio (SFX)

| Plik | Przypisanie |
|------|-------------|
| attack.wav | HitboxComponent |
| hit.wav | HurtboxComponent |
| parry.wav | ParryComponent |
| death.wav | StatSheet.died |
| checkpoint.wav | Checkpoint |
| pickup.wav | TeethPickup |

---

## Regeneracja (tools/)

```bash
pip install Pillow
python tools/generate_assets.py   # tiles, icons, player, enemies, checkpoint, menu, efekty
python tools/generate_sfx.py      # dźwięki
```
