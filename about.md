# Pulse Macro v1.4.7

Pulse Macro combines a 240 Hz deterministic macro recorder/player, a 20-slot per-level library, playback auto-repair, and built-in Frame Windows for Geometry Dash 2.2081 / Geode 5.10.1 on Win64.

## v1.4.7

**Stable macro libraries.** Positive online/official Geometry Dash level IDs now identify the macro library. Raw `m_levelString` differences no longer create an apparently empty second library for the same level. On first access, legacy per-hash files are migrated per slot; duplicate legacy variants are retired as backups. Local/non-positive-ID levels remain content-keyed.

**Frame Window timing filter.** Macros still record every press and release. Frame Windows replays every transition too, but only measures inputs with independent timing meaning: every press, plus releases in ship, wave, and robot. Cube, ball, UFO, spider, and swing releases are replay-only. The local metric ends at the next meaningful timing for the same player. Analysis progress, histograms, circles, precision, and checkpoint planning use the filtered timing set. Analysis version 5 intentionally invalidates older widths so existing references can be re-analyzed with player-mode metadata learned during the opening baseline.

**Cleaner UI.** Pause → **Pulse** opens the macro library. The library has Record / Replace, Play, Save Now, Delete, Undo Delete, Files, Frame Windows, and Help. Frame Windows has a numbered Record → Analyze flow plus Results, Export, Settings, and How to use. The default normal counter is a transparent compact grouped display with a NaN-style palette; turn off **Minimal counter (NaN-style)** for the detailed panel.

**Analysis acceleration and safety.** Candidate trials restore verified native checkpoints near the exact shifted timing and fall back to earlier checkpoints or the level start if a snapshot is unreliable. Each direction stops at its first confirmed failed boundary. Unstable boundary confirmations continue conservatively with warnings. If every timing is already measured and only the final validation replay fails, the measurements are preserved with a prominent unverified warning instead of being discarded.

## v1.4.6 playback auto-repair

A reproducible playback death can trigger a bounded nearby-frame search. Pulse retries the original route first, then tests recent jump transitions at nearby 240 Hz offsets. A candidate only passes if the entire remaining macro survives. The center of the widest passing region is confirmed again, its full trajectory replaces stale recorded positions, and the original macro is kept as `.bak`.

## Usage

**F6** records Pulse plus the linked Frame Windows reference from the level start. **F8** saves. **F7** replays the selected slot. **F4** opens Frame Windows controls; **F3** toggles its counter. F5 is optional standalone Frame Windows recording. Practice checkpoints must be created after F6; leave practice before normal playback.

Keep analysis at native 240 Hz physics. Disable CBF Physics Bypass/subtick physics, TPS bypass, other replay bots, Lock Delta, and frame extrapolation during measurement. Pulse does not position-correct frame-window trials.

Standalone/core validation: 6/6 CTest suites pass. The included GitHub Actions workflow builds Win64 with Geode SDK 5.10.1. Native in-game behavior must still be validated with the resulting `.geode`; this source package is not a claim of live GD testing.
