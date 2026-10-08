# Quality of life: modern conveniences for the port

Goal: the conveniences later action RPGs made standard, added to the port as
choices made in code. Each is off the original game's path, so each is a
setting, and what the original did stays the default where it changes play.
None changes the save format: what the port keeps of its own goes in files
beside the save (as `settings.toml` does).

## Order

1. Baseline: `cargo build`, the tests that need no disc.
2. Game speed (hold or toggle 2x / 3x) and faster text and menus.
3. The battle hotbar (below).
4. Autosave into a slot of its own: on entering a Root Town, on gating out.
5. Skipping in-engine event scenes (the script run fast, its flags all set).
6. Quick save and load anywhere.

The field map's changes come later.

## The battle hotbar

The game casts a skill or spell only from the menu (triangle, PERSONAL,
Skills, the skill, TARGET), and the battle runs on underneath. The hotbar
casts from the pad.

### Buttons

The field's buttons (`ccThGameCtrl`, `saveData.assignPAD` +0x8404 on, the
camera's `camType` pages in field-ui.md "ControllerMenu"):

| button | field use |
| --- | --- |
| cross | action: attack, talk, take (+0x8404) |
| circle | cancel |
| triangle | PERSONAL menu (+0x8406) |
| square | CHAT (+0x8408) |
| start | OPTION (+0x840a) |
| select | the map's mode (+0x840c) |
| L1, R1 | A types: rotate the camera; B types: L1 resets it, R1 zooms |
| R2 | A types: reset the camera; B types: zoom |
| L2 | both types: change the view |
| L3, R3 | nothing in the field (no reads found in the port's field, camera, map or menu code) |
| D-pad | walk, as the left stick |

Hold to open: **L2 for skills, R2 for spells.**

- L2's view change is the field's least used button; it moves to L3.
- R2 is the camera reset (A) or zoom out (B); it moves to R3. A click of a
  stick is fine for a press now and then; it is poor for a hold, which is
  why L3 and R3 are not the hotbar's.
- The two can be changed in the port's settings, and the moves undone.

To be confirmed in play: that nothing in a battle, a boss's camera
(`bosscam.rs` reads L2 and R2) or an event reads L2 or R2 in a way the
hotbar breaks. While a hotbar is held, the port hands the field no L2 / R2.

### Play

- Holding L2 or R2 in a field or dungeon, with no menu open and Kite free to
  act, opens that bar: eight slots drawn around the pad's layout, the D-pad's
  four on the left and triangle, circle, cross, square on the right, each with
  its button and the skill's name beside it.
- While the bar is open the battle slows (not stopped): the world steps one
  frame in four (a setting); the bar and the pad run every frame. A frame
  stepped is the same frame as before, so replays and pad logs still hold.
- A slot's button: the target step (below). Releasing the hold first closes
  the bar with nothing cast.
- A slot greyed out: its skill not on Kite's equipment now, too little SP, an
  item none of which is left, or the menu's own check
  (`ccCheckSkillUseful`, `ccCheckItemUseful`) says no. The binding stays; it
  comes back with the equipment or the item.
- Kite's own only. The members' skills stay CHAT's.

### Targets

The second press. The bar shows the target chosen, the same cursor the game
draws on a target:

- an attack: the enemy already targeted, else the nearest;
- a support spell or item (healing, raising, buffs, curing): the party member
  with the least HP in proportion, the dead first for a revive;
- left and right (D-pad or stick) step through the candidates, enemies or the
  party by the skill's target type (`ccCheckTargetTypeId`);
- the slot's button again, or cross, casts; circle goes back to the bar.

Casting goes through the same request as the menu's (`ccSkillRequest`,
`ccUseItemRequest`), so cost, range, the members' chat and every rule are
the game's.

### Assigning

- In the Skills menu, select on a skill opens the slot picker: the bar it
  belongs on (skills or spells, by the skill's kind) with its eight slots;
  the slot's button binds it.
- A slot already bound asks first, in the game's own dialog: "Replace
  <old> with <new>?" OK / Cancel.
- The menu's help line carries the hint: "SELECT: assign to hotbar".
- The bindings are kept per save slot in a file beside the card, not in the
  save: the save stays as the game made it.

### Items

Items share the bars: in the Items menu, select on a usable item opens the
same picker. Healing and curing items go by default on the spell bar (R2),
next to the healing spells. A slot holding an item shows its count. One path
assigns both, so a player can put Health Drinks and Repth on one bar.

### The look

Everything the hotbar draws is the game's own: its menu window and frame
(`ccMenuWindow`), its font, its cursor and its colours, the button marks the
menus already draw for the pad, and the target cursor of the battle. Nothing
new is painted. The art is read from the disc at run time, as all the port's
is; none is put in the repository (plans/release.md).

### Checks

- The cast a hotbar makes against the same cast from the menu: the same
  request, the same SP taken, the same result.
- A pad log of a fight with the bar replayed to the same end.
- The slowdown: the frames stepped while held, one in four.
- Shots of the bar, the picker, the overwrite dialog and the hint, for a look
  in play against the menus beside them.
