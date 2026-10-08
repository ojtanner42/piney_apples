---
number: 383
title: The game's speed: Tab runs The World at x2 or x4, held at x1 while a movie or stream plays
date: 2026-10-08
area: engine, build, test
files: crates/piney-game/src/main.rs, crates/piney-game/src/mode.rs, crates/piney-game/src/session.rs, crates/piney-game/src/area.rs, crates/piney-game/src/world.rs, crates/piney-game/src/desktop.rs, crates/piney-game/src/toppage.rs, crates/piney-game/src/console.rs, README.md, plans/qol.md
---

# 383. The game's speed: Tab runs The World at x2 or x4, held at x1 while a movie or stream plays

The first of the conveniences in plans/qol.md, and not the game's: the port
can run The World faster than the PS2 did. `App::tick` counted vertical
blanks at 59.94 a second and ran a game frame each `frameRate` of them, at
most `MAX_CATCH_UP` (4) a tick. The speed multiplies both: the blanks
counted are 59.94 x speed a second, and the catch-up limit is 4 x speed, so
at x4 a slow tick can still make up its frames. Nothing inside a frame
changes. Each frame reads one pad and steps the mode once, as before, so a
pad log is a list of the same frames at any speed, and `--replay` of a run
recorded at x2 plays the same game at x1.

Tab steps 1, 2, 4 and back to 1 (the console takes Tab for completion while
it is open, and the console's keys are handled first, so the two do not
meet). `--speed N` and the console's `speed N` set it; the window's title
carries "(x2)" or "(x4)". Tab is not on the port's keyboard pad (arrows, Z X
A S, Q W, 1 2, Enter, Backspace, C V, I J K L), so no game button moved.

## Held at 1 under a movie or stream

The sound runs on the output device's clock, not the game's: `Audio::frame`
only hands the driver the frame's requests. A PSS movie
(`movie::Playing`) shows each picture for two game frames and starts its
sound once with the first, so at x2 the pictures would run ahead of their
sound. The same holds for the in-engine streams with voices. So the mode
says when it plays one: `Mode::real_time`, false by default, true for
`Session` while the title waits on a movie or its opening stream, or the
desktop, top page, world or area plays a stream (the area's Data Drain movie
too). Each mode's `streaming()`, kept for tests until now, is now built
for the game. While it is true the tick runs at x1.

## Checked

The build, clippy and rustfmt are clean. `cargo test -p piney-game`: 239
pass and 10 fail, the 10 being those that fail without the disc's data in
`work/` (the dressing, ocarina, Fairy's Orb, card and tornado tests) and
`webp::tests::frames_timed_on_the_game_clock`, which writes under
`/mnt/data/claude/scratch` and fails where that does not exist; all ten
failed the same before the change. `console::tests::tab_completes_the_commands`
now lists `speed`.

**Still unknown:** the speed has not been played with a disc: whether x4
holds its frames on an ordinary GPU (each frame is still drawn, since a frame
may sample the one before), how the sound effects bunch up at x4, and
whether any other sound is tied to the game's frames in a way that drifts.
