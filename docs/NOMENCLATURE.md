# Chronica Solis: Eclipse — Nomenklatura

## Waluta

| W kodzie | Opis |
|----------|------|
| `teeth` | Zęby — waluta (drop z wrogów) |
| `player_teeth` | Zęby gracza (GameState.player_teeth) |

**NIGDY:** souls, orbs, gold.

---

## Statystyki gracza (obecnie)

| Statystyka | Komponent | Zmienne |
|------------|-----------|---------|
| HP | StatSheet | max_hp, current_hp |
| Stamina | StaminaComponent | max_stamina, current |
| Poise | PoiseComponent | max_poise, current |

Pozostałe statystyki (str, dex, arc, fth, vig, end) — do implementacji w innym systemie.

---

## Zapis i stan gry (GameState)

| Zmienna | Typ | Opis |
|---------|-----|------|
| player_teeth | int | Zebrane zęby |
| last_checkpoint | Vector2 | Pozycja ostatniego checkpointu |
| last_room_path | String | Ścieżka sceny przy zapisie (do Wczytaj grę) |
| defeated_bosses | Array[String] | ID pokonanych bossów |
| pending_teeth | Dictionary | {position, amount} — teeth do odebrania przy ciele |
| DEFAULT_SPAWN | Vector2 | Pozycja respawnu gdy brak checkpointu |

---

## EventBus — sygnały

| Sygnał | Parametry |
|--------|-----------|
| enemy_died | enemy: Node, position: Vector2, teeth: int |
| boss_defeated | boss: Node, position: Vector2 |
| room_transition_requested | room_path: String, spawn_position: Vector2 |
| player_died | position: Vector2 |

---

## Dane wrogów (data/enemies/*.json)

| Pole | Opis |
|------|------|
| hp | Maksymalne HP |
| damage | Obrażenia hitboxa |
| speed | Prędkość ruchu |
| teeth_drop | Ilość teeth przy śmierci |
| detection_range | Zasięg wykrycia gracza |
| attack_range | Zasięg ataku |
| patrol_range | Zakres patrolu |
| status_effect | (opcjonalnie) Bleed, Madness, Necrotic, Petrify — **nieużywane w EnemyAI** |

Boss dodatkowo: phase_thresholds, speed_per_phase, attack_cooldowns.

**Uwaga (audyt):** Pole `status_effect` (np. "Bleed" w effossus.json) istnieje w JSON, ale EnemyAI.gd go nie odczytuje ani nie stosuje — brak systemu statusów.

---

## Statusy (chronicalore)

Bleed, Poison, Corruption, Petrify, Burn, Frostbite, Parasitic, Necrotic, Mutagenic, Madness

---

## Klasy (chronicalore)

| Lore (łacina) | Dla gracza |
|---------------|-------------|
| Pellio | Skinner |
| Servus | Thrall |
| Sarcinator | Stitcher |
| Custos | Ward |
| Speculator | Snooper |

Szczegóły w chronicalore.md.

---

## Przykładowe bronie (osteo-metal)

Falx Ossium, Falx Cinerea, Ironclad Hammer, Necrotic Whip, Voidtwin Blades

---

## Łacińskie nazwy (świat)

Magnum Horreum, Membrana Humana, Maszyneria
