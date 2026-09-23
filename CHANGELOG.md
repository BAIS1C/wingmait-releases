# Wing Mait changelog (public)

All times SGT (UTC+8). Earlier builds: see the GitHub releases list.

## 0.9.5-beta.3, Beta 0.95 hotfix 2 (2026-09-24)

- Fixed: revive lines while you were alive, when the mortar sight or the big map covered the minimap.
- Fixed: the same contact being called twice as it moves from one compass direction to the next.
- Combat callouts are muted while the big map is open; fire solutions still speak.
- Sgt Bravo 4 now speaks the full fire solution.

## 0.9.5-beta.2, Beta 0.95 hotfix (2026-09-23)

- Fixed: moving the radio sliders or clicking presets could queue test lines that kept playing. Only one preview plays at a time now, and each new one interrupts the last; real callouts are never cut off by a preview.
- Fixed: picking a new character in the voice dropdown takes effect straight away, instead of waiting for the old voice's queued lines.
- CLEAR now sits apart from the radio presets, with a tooltip; it resets the radio effect to clean (0/0).

## 0.9.5-beta.1, "Beta 0.95" (2026-09-23)

### Highlights
- Radio comms now has two sliders: Voice distortion and Static (0 to 100 each), with presets Clear, Comms, Field and Hell, and a live preview when you release a slider. Signal quality still wanders within each line; an anti-mud guard ducks static under the voice, cuts low rumble and keeps noise at least 6 dB below speech. Both sliders at 0 is a clean bypass. Applies to every voice, character packs and Kokoro alike.
- Every voice line is now loudness-normalised to one level before any radio effect, at playback and in the shipped media (pack spread cut from about 8 dB to about 0.1 dB).
- Settings: an "i" explainer on every settings row, in all five languages (non-English text is machine translated and awaiting native review).
- Military comms voice bank (military digits, NATO alphabet, radio prowords) promoted into six of seven character packs; the spoken fire solution from the Wing Mait map and mortar calculator is live for those characters. Sgt Bravo 4 has 3 lines pending and stays silent for fire solutions until they ship.
- Occasional "Break" / "Over" radio words on quiet-time callouts (about 1 in 20; never under load, never on spotted callouts).
- New Stats screen (replaces Ledger): session and all-time views, JSON and Excel export, full screen, and OBS stat pins that render chosen tiles as a Browser Source overlay. "Stats powered by Everywear ID".

### Honest status of Stats
- The screen, local recorder and exports are in. The on-screen stat readers are still calibrating against recorded gameplay (best so far: control holder 87.5% exact, HOT ZONE banner 81%; cash and team scores lower). Until a reader reaches 97% accuracy its tile shows "Calibrating" instead of a number. Evidence crops are kept locally so sessions recorded now can be re-read by a later build.

### Not claimed
- Unsigned installer (SmartScreen will warn). No anti-cheat certification. Live in-game mortar callouts from the map remain coming soon. Leaderboards and Everywear ID sign-in are not in this build.
## 0.9.0-beta.9 (2026-09-23)

### Highlights
- Detector now supports proportional 16:9 WARDOGS windows from 1920x1080 through 3840x2160, including 2560x1440, normalised into the existing 4K-derived detection geometry.
- Radio comms voice treatment: every character can be heard Clear or on Radio, with wandering signal quality, static, crackle, dropouts and a detuned high-band whine.
- New military comms voice bank (military digits, NATO alphabet, radio prowords) rendering for all seven characters.
- Voiced fire-solution wiring for the Wing Mait mortar calculator and map (grid, bearing and elevation in mils, ending "Adjust accordingly"); it switches on when the comms voice bank ships in the next update.
- New device sounds: rubber-keycap button press and release, a long drawer slide woosh, and a "Say again" menu item that replays the last callout.
- Self-downed false holds fixed (82 confirmed false "callouts held" events traced to a hue-only test), full-map classification, minimap north resolution, and measured distance scale all landed since beta.2.

### New in beta.9
- Runtime radio comms treatment for every voice; Kokoro Radio now plays the clear bank through the same treatment.
- New UI sounds; lamp sound removed; Clear/Radio setting enabled for character voices; Say again; fail-closed voiced fire solution; military comms bank render tooling.

### Coming soon
- Live mortar callouts read from the in-game map (right-click target, coordinates, bearing, elevation in mils).
- Voice callouts in more languages.

### Since 0.9.0-beta.2 (the last public build)

Beta.2 (2026-09-20) was the last build the public download page pointed at. Everything below shipped, or was architected, after that cut.

#### Detection and capture
- Operator position tracking (`OperatorTracker`) so bearing and distance are measured from the operator's own fix instead of the crop centre.
- Self-downed detection rebuilt from a colour/proximity test to a shape test (hollow ring plus interior squiggle, white-arrow-absence check, team-colour inference, two-tick hysteresis), fixing 82 confirmed false "callouts held" holds measured from one live session.
- Map-screen state detection (in-game vs. map open) and an unmeasured hot-zone detector, pending real capture evidence.
- Heading reader and minimap-north resolution from compass OCR plus the player chevron's screen angle, gated on three agreeing samples within 12 degrees.
- Explicit Fixed or Follow minimap orientation setup, replacing an automatic estimator that missed a real fixed frame in internal testing; an unset config now fails closed with a setup prompt rather than guessing.
- Measured minimap distance scale wired into the distance provider (2.56 / 1.71 / 0.853 / 0.427 metres per native pixel across the minimap's four zoom steps, one disc-measured and three ladder-derived); distance now reports to the nearest 10 metres with a Measured/Derived confidence tag.
- Full-map classification against the three bundled tactical maps (Bakurani, Ozeti, Zestafona), gated on score, lead margin and two consecutive agreeing reads; selected map now binds into the artillery solver, and changing maps clears mortar and target points.
- Direct WARDOGS capture (Windows Graphics Capture, GDI fallback) confirmed as the sole recognition input; OBS is not required for callouts and remains available only as an optional stream-overlay presentation surface.
- Black-box marker proposal layer: a colour and geometry pre-filter that proposes small, flat-colour HUD marker candidates before the existing template matcher classifies them, rejecting map borders, score-panel colour washes and unrelated HUD colour noise.
- Big-map and a separate generic 3D spotting surface wired end to end in source (capture, template match, geometry, strict voice-media receipt), both fail-closed and off by default; no admitted exemplars exist yet, so neither surface emits a live observation today.
- Opt-in low-magazine warning: detector logic and fail-closed states for a threshold of 2 or 3 rounds, defaulting off; architecture and handover only, no voice media promoted yet.
- Multi-resolution detector normalisation: proportional 16:9 windows from 1920x1080 to 3840x2160 (including 2560x1440) are now supported in source, resampled into the existing 3840x2160 detection geometry rather than requiring a manual resolution picker. Beta.9 is the first installer to carry it; native 4K remains the most tested setup.

#### Callouts and doctrine
- Callout pacing tightened after playtest feedback: smaller queue, longer minimum intervals, a per-minute speaking budget, and no repeat of identical spoken text inside a suppression window.
- Doctrine rules implemented: enemy-spotted lines take priority under load and hold that priority for 6 seconds after speaking; character flavour tails are capped at roughly 1 in 20 utterances instead of baked into every line; the operator's own downed state goes fully silent apart from one optional "hold on" line, with no engine chatter while down.
- Numeric bearing and distance for spotted contacts where the selected voice pack has the numbers rendered; downed teammates always keep compass-word callouts.
- In-game chat is never spoken aloud, at any callout detent.
- Downed-teammate rings are classified separately from a generic "spotted" contact.
- Pickup speech limited to one call per local downed incident, and phrase-variant rotation so the same line variant does not repeat back to back.
- Fixed-phrase callouts (for example "hold on") that a voice pack does not actually contain now log and report as a failed speak instead of a false "dispatched" line.

#### Voice and audio
- All seven character packs (Captain Discount, Colonel Hantuto, Commander Kaira, Corporal Tuppence, General Attitude, Lt Verenas, Sgt Bravo 4) ship as Ogg Vorbis, 1,509 phrases per character, 10,563 files total, cutting combined pack size from roughly 1.35 GB to about 213 MB.7 build.
- Playback-truth instrumentation added to the audio thread, distinguishing "dispatched" from "actually queued and played." This traced an in-game silence report to a missing "hold on" media file in the shipped packs; the resolver no longer claims speech it did not produce.
- A 25-id equal-semantic voice addendum (hold-on, downed states, generic and specific vehicle sightings, a first-run calibration and FAQ sequence) rendered and QC'd for all seven characters, 175 files, automated audio QC clean; not yet merged into a shipping phrase pack as of beta.8.
- New in beta.9: a runtime comms treatment selectable per voice, Clear or Radio. On Radio, signal quality wanders from mild to heavily distorted within a single line, with static, crackle, dropouts and a detuned high-band whine, band-limited like a real field radio.
- New in beta.9: a military comms voice bank (military digits, NATO phonetic alphabet, radio prowords) rendering for all seven characters, feeding the mortar fire-solution line below.

#### Device and UI
- Compact chassis default window size (400x600, 320x480 minimum) and a reliable corner-resize fix; only an unversioned legacy default window size migrates automatically, any size a player already chose is preserved.
- New in beta.9: rubber-keycap device button sounds for press and release, and a long drawer slide woosh.
- New in beta.9: a "Say again" device menu item that replays the last callout.

#### Mortar and maps
- Full-map classification auto-selects the matching tactical map and binds it into the artillery solver's coordinate validation; changing maps clears any in-progress mortar or target point.
- New in beta.9: a voiced fire-solution line for the mortar calculator and map. It speaks the target grid, bearing and elevation in mils, ending "Adjust accordingly," and stays silent until the military comms voice bank has finished rendering for the selected character.
- A live, in-game, screen-read mortar targeting flow (watching the big map for a right-click and reading the resulting coordinates automatically) is the next planned feature; it is not implemented in this build. See "Not claimed."

#### Licensing and install
- Beta.7: production NSIS build with a fully verified 10,563-file Ogg voice tree, installed silently as an update with the licence key, activation instance, expiry and validation timestamp all confirmed unchanged before and after.
- Beta.8: black-box detector build installed and, after native testing, accepted as ready to move toward public beta launch; licence and config preservation re-verified on that update.
- Beta.8 pinned as the launch-candidate revision across the desktop, website and root repositories.
- Beta.9 supersedes beta.8 as the public build.

#### Website and guides
- Getting-started guide and a how-it-works section added to the site, alongside a build-line indicator for the current download.
- Download page wired to the hosted public GitHub release, and a Lemon Squeezy checkout overlay embedded on the pricing call to action.
- Localisation fixes for the guide language switcher and its content-security-policy allowances across five locales.
- Field Notes build-blueprint library published: a five-module WARDOGS build plan with field-plan diagrams, served through a versioned library manifest.

### Compatibility boundary
- No CUDA, DirectML or other vendor-specific GPU dependency; NVIDIA, AMD and Intel are not separate code paths.
- Source now supports proportional 16:9 WARDOGS windows from 1920x1080 through 3840x2160, including 2560x1440, normalised into the existing 4K-derived detection geometry. This is proven at the source and automated-unit-test level as of 2026-09-23 only; it has not been verified with a native live 1080p or 1440p capture, an installed build, or gameplay accuracy comparison against the 4K path.
- Ultrawide, 16:10, stretched, letterboxed, sub-1080p and above-4K layouts remain fail-closed, by design, rather than warped into a false match.
- Wing Mait reads visible pixels through supported Windows capture APIs only. It never injects into, reads memory from, hooks the renderer of, or modifies WARDOGS, and it never sends input.
- No claim is made about anti-cheat policy, every Windows/GPU/audio-device combination, HDR, multi-monitor layouts, exclusive-fullscreen capture, or performance across DLSS/DLAA modes beyond our own test machines.

### Not claimed
- The installer is not code-signed. Windows SmartScreen will warn on first run; this is expected for an unsigned beta, not a corruption or security failure.
- Wing Mait's observation-only design is not an anti-cheat certification and is not a guarantee against future WARDOGS anti-cheat policy or engine changes.
- The mortar fire-solution voice line is silent until the military comms voice bank finishes rendering for the selected character; the calculator and map remain usable without it.
- Live, in-game, screen-read mortar callouts, triggered automatically by watching the map for a right-click target, are coming soon and are not in this build; today's mortar flow is the calculator and map path only.
- Big-map and 3D spotting are wired in source but remain silent: no admitted exemplars exist yet for either surface.
- The low-magazine warning is architecture only in this build; no voice media has been promoted for it.
- Multi-resolution support has not been proven with a native, installed, live-game capture at 1080p or 1440p; only 3840x2160 has installed, native acceptance behind it as of beta.8.
