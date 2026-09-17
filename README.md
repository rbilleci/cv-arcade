# Richard Billeci — Career Playthrough

An 8-bit side-scrolling platformer that plays through my CV, one world per role, from Commerce One in 1999 to Mambu today, with a bonus stage for independent projects. It runs itself as a demo; press a key at any time to take the controls.

**Play:** open `index.html` in a browser. No build step, no dependencies, no network calls.

## Controls

| Key | Action |
| --- | --- |
| `←` `→` / `A` `D` | Move (takes over from autoplay) |
| `Space` / `↑` / `W` | Jump |
| `Enter` | Toggle autoplay |
| `R` | Restart |
| `M` | Toggle sound |

Touch controls appear on phones and tablets. Browsers block audio until the first key press or tap, so the demo runs silently until you interact; the SOUND button shows the current state and your choice is remembered.

## How it works

Everything lives in a single `index.html`:

- The `WORLDS` array at the top is the CV: company, role, years, a colour theme and the milestones. Each milestone becomes a `?` block; hitting it shows the achievement.
- Levels are generated from that data with a seeded random generator, so layouts are stable between visits. Add `?seed=3` to the URL for a different layout.
- The autoplayer is not a recording. Every frame it reads the tiles ahead (walls, gaps, bugs, unhit blocks) and derives inputs, so it survives regenerated levels and hands over cleanly when a human presses a key.
- Sprites and tiles are drawn procedurally on a 384×216 canvas and scaled with `image-rendering: pixelated`; the HUD and cards are DOM elements sized in `rem` off the same scale factor.
- Music and sound effects are synthesized with the Web Audio API, no audio files. Each world's theme defines a tempo, scale, root note, chord progression and lead voice; a small step sequencer derives bass, pad, lead and drums from that. Music ducks while a milestone card is showing.

Enemies are bugs. Stomping them counts as bugs fixed.

## Local development

```sh
python3 -m http.server 8000
# open http://localhost:8000
```

## Licence

Code is MIT licensed (see `LICENSE`). The CV content — names, roles, milestones — is © Richard Billeci and not covered by the MIT licence. The *Press Start 2P* font is bundled under the SIL Open Font License (`fonts/OFL.txt`).
