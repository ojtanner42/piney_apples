# Quality of life: modern conveniences for the port

Goal: the conveniences later action RPGs made standard, added to the port as
choices made in code. Each is off the original game's path, so each is a
setting, and what the original did stays the default where it changes play.
None changes the save format: what the port keeps of its own goes in files
beside the save (as `settings.toml` does).

## Order

1. Baseline: `cargo build`, the tests that need no disc.
2. Pace: game speed (hold or toggle 2x / 4x), instant or faster text with
   auto-advance, faster menu animations, shorter load fades, the menus'
   cursors remembered.
3. The battle hotbar (below).
4. Saving: autosave into slots of its own (rotating) on entering a Root
   Town and on gating out; saving from a Root Town without logging out.
5. The field helpers: the auto Fairy's Orb, the auto Fortune Wire, the
   sprint toggle (below).
6. Shops and items: buying and selling in quantities, equipment compared,
   items sorted and filtered, who can equip a piece shown, the item box
   reached from the field (a setting).
7. Combat: target cycling on the right stick with the target's health,
   damage numbers (on / off, larger), party AI presets, the bracelet's
   infection as a number.
8. Dungeons and the gate: a floor's chests and portals counted, a run toggle
   and faster walking in the Root Towns, back to the Root Town from a
   cleared dungeon's last room, the Chaos Gate's recent and favourite words.
9. Members and the party: friendship levels shown; the last party invited
   again at the Chaos Gate in one choice; which members want which items
   in a trade.
10. The .hack conveniences: logging in and out and the gate's transfer
    shortened; a Data Drain's result shown before the drain; the Virus Cores
    held against what each gate hack needs; the Grunty foods and the
    evolutions they lead to, shown at feeding; Kite's equipment kept in sets
    and changed in one press; an item that does not fit offered to the item
    box; the camera's options (following behind Kite, speed, inverted
    axes); items held past the stack limit, or a larger item box (a
    setting).
11. Presentation: widescreen without stretching, the menus and windows kept
    in proportion, and resolution (in part already: `--render-scale`); full
    button remapping.
12. Skipping in-engine event scenes (the script run fast, its flags all
    set).
13. Quick save and load anywhere.
14. The second list (below), placed into the steps above as each is
    designed.

The field map's changes come later.

### Not to be made

Decided against (2026-10-08): the party's status always on screen with a
low-HP warning; treasure, portals and the goal marked on the maps (the auto
Fairy's Orb stands in); a gate history of cleared areas and treasure left;
a "what next" hint from the event flags; an unread-mail badge in the field
and a list of the story's mail; text size and window opacity; the assists
(more experience or gold, no traps, easier Data Drain); anything taken from
.hack//G.U. Last Recode (the four parts as one continuous game, a higher
level cap, a photo mode); 60 fps with frames interpolated; skipping the
intro and the logos. From the second list: the Chaos Gate's word
autocomplete; fountains healing with no menu; a symbol's or statue's text
shortened; what a magic portal holds hinted; the summary after a fight; the
victory pose shortened; the members' chatter set less often; a trade log;
list cursors wrapping round; vibration strength; a theatre of the event
scenes; a screenshot key.

## The second list

Agreed 2026-10-08. *check*: the game may already do some of it; look first.

The ALTIMIT desktop:
- Connect into the Root Town and server last used, past the login's steps.
- A quick save on the desktop to the slot last used, past the slot list.
- Mail sorted by sender or date; all marked read.
- Old mail archived or deleted.
- News and the BBS open on the newest unread post.
- A save slot shows where, Kite's level, the party, the play time, the part
  (*check*).
- The card backed up before each save, the last few kept.
- The card exported to a PCSX2 memory card (*check*: import is there).

The Chaos Gate and travel:
- An area's level, element and field type shown before the warp (*check*).
- A random area word within a level range chosen.
- Gating out from anywhere in a field with no foe near.
- The dungeon's stairs and floor change shortened or skipped.
- The Grunty summoned and left faster, and ridden faster.

The field and the dungeon:
- Breakable objects broken on one press, past the "break it?" menu.
- Untrapped chests opened on one press, past the menu.
- The dungeon's floor number on screen.

Combat:
- "Triangle: Data Drain" shown when a foe's Protect Break opens, past the
  menu.
- How long a Protect Break lasts, shown.
- The conditions' icons with their time left.
- Cross held keeps attacking.
- The next foe targeted after a kill.
- The camera turned to the target in a fight.
- A skill's range shown while its target is chosen.
- A level up's stat changes listed.
- The members' HP and SP as numbers in CHAT.
- A log of the chat and the system's messages, to scroll back.

ALTIMIT's News as the players' own web sites:
- A bestiary filled in as foes are met: level, element, weaknesses, drains.
- An item book filled in as items are had: effects, where found, trade
  value.
- Every item a Data Drain gives, and those drained.
- A completion page: areas visited, rare items, members met.

Items and equipment:
- Items' descriptions with their numbers (HP, SP, stats).
- "Heal the party" outside a fight, with the cheapest items that do it.
- Items marked favourite or locked: not sold or traded by accident.
- "Sell all junk", sparing the locked and those a trade wants.
- A shop shows how many are held and whether one is worn.
- The compare shows the skills a piece gives and those lost (in .hack the
  skills are the equipment's).
- Kite's best equipment for a stat chosen (attack, defence, an element).
- The item box sorted.
- An item given to a member from the shop.

Members and the party:
- Any member with an address invited from the gate or PERSONAL (*check*).
- A member's level and equipment seen before the invitation.
- Gifts given and friendship's progress, per member.

The Grunty:
- Each Grunty's hunger, foods eaten and evolution's progress.

Menus and controls:
- A held direction scrolls faster the longer it is held.
- L1 / R1 page every long list (*check*).
- The routine "are you sure?" prompts skipped (a setting per kind).
- The mouse and keyboard in the menus.
- Button marks for Xbox and Nintendo pads, drawn in the game's style (new
  art, the plan's one exception).
- A pad plugged in during play taken up at once.

Event scenes:
- The last lines read again (a backlog).
- A pause in the in-engine scenes.

Sound and the system:
- Voices' and battle chatter's volumes apart.
- A pause when the window loses focus.

## The field helpers

Each can be turned on and off in the game's OPTION menu (a row of its
own, in the menu's style, beside the game's rows) and is kept in
`settings.toml`; all three are on in a fresh settings file. Each goes
through the game's own use of the item, so what it does, costs and
shows is the game's.

### The auto Fairy's Orb

On entering a field, or a new floor of a dungeon, with a Fairy's Orb (13/2)
in Kite's items and the map not yet whole, one is used as from TARGET:
`ccUseItemRequest(plw, -, 13/2)`, its sound, its line, `ShowMap` until it
answers (map.md "ShowMap: the Fairy's Orb"), one orb taken.

- Not where it would be wasted: a field already shown (`mapFlag` set), a
  dungeon floor already seen whole, a town, an event area with a story map
  of its own (`ShowMap` answers 1 at once there), a floor entered while a
  fight holds its rooms.
- Not while an event holds the field or the menus are banned
  (`menu_ban`); it waits for the area's fade in to end.

### The auto Fortune Wire

The action button on a trapped box (base type 0x8000, menu 33 "Risky
Treasure"):

- With a Fortune Wire (13/0) in Kite's items, the wire is used first, as
  from TARGET: its sound, `effRemoveTrap`, a popup "Used a Fortune Wire.
  Disarmed trap." in the game's message window, `EntryAffect(box, plw,
  12)`; then the box opens as an untrapped one.
- With none, a warning in the game's dialog before the menu: "This box is
  trapped. You have no Fortune Wire." with Open anyway / Leave it. Open
  anyway goes on to the game's own menu 33.

### The sprint toggle

A button (the port's settings; by default L3, which the field does not
read) toggles running: with it on, any push of the stick or the D-pad
runs at full speed whatever the tilt, so a keyboard and the D-pad run too.
A small mark in the game's style shows it on. In the Root Towns the run
may go faster still (a setting, the town walk's speed scaled).

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

- A tap keeps the button's own use; a hold (a setting, by default 8
  frames) opens the bar. So L2 still changes the view and R2 still resets
  (A) or zooms (B), on release of a tap. Nothing moves.
- L3 and R3 stay free: a click of a stick is fine for a press now and then
  and poor for a hold. L3 takes the sprint toggle.
- The two can be changed in the port's settings.
- The B types zoom while R2 is held, which a tap cannot give. With a B
  type the spells' bar defaults to R3 held instead, or the player picks
  another button.

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
