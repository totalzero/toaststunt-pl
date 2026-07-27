# Guide: Building Your Own MOO World From Scratch

*This is an original, hands-on guide written directly for this ToastStunt fork (not a translation of an external source) -- the English-language counterpart to [PORADNIK-BUDOWY-SWIATA.md](PORADNIK-BUDOWY-SWIATA.md), the Polish version of this same guide. Both versions build the same kind of world with the same MOO mechanics; only the example content (room names, NPCs, item flavor text) differs to read naturally in each language. Code blocks (commands, property names, verb names, MOO program fragments) are meant to be copied as-is.*

This guide answers the question "I already have a running, empty server -- now what?". It walks, step by step, through one continuous worked example, showing how to build a real, playable slice of a world: from the first `@dig`, through dozens of interconnected rooms, items and NPCs, all the way to special effects like locks, a day/night cycle, an economy, and simple quests. Everything uses one coherent setting -- but every technique shown here carries over 1:1 to any other theme (a modern city, a spaceship, whatever you like).

## Who this guide is for, and what it assumes

I'm assuming:

- You already have a running ToastStunt server with a loaded database (e.g. `toastcore.db`) -- if not, start with the [Getting Started Guide](https://lisdude.com/moo/toaststunt_newbie.txt), which walks through compiling the server and logging in for the first time. (A Polish translation, expanded with extra detail, also lives in this repo as [PRZEWODNIK-DLA-POCZATKUJACYCH.md](PRZEWODNIK-DLA-POCZATKUJACYCH.md).)
- You have a player account with builder (Generic Builder) or programmer permissions -- see `help @programmer` if you need to grant yourself or someone else that status.
- You know the basics of MOO syntax (variables, `if`/`for`, calling verbs), or you're willing to glance at the [ToastStunt Programmer's Manual](https://github.com/lisdude/toaststunt-documentation/blob/master/manual/toaststunt-programmers-manual.md) along the way -- this guide explains each new piece of the language the first time it shows up, but it isn't a full syntax course from zero.

I'm not assuming anything beyond that. In particular, I'm not assuming you're building on a live, production server -- quite the opposite: in Chapter 2, the very first thing we do is set up a safe place to experiment.

## How to use this guide

Each chapter assumes the previous ones have been worked through -- the world is built incrementally, the same way you'd actually do it. The code in the blocks is meant to be pasted into your MOO client (telnet/MUD client) exactly as written -- anywhere you need to substitute your own object number or name, the text right before the code block says so clearly.

Table of contents:

1. [World concept](#chapter-1-world-concept)
2. [Setting up your builder's workshop](#chapter-2-setting-up-your-builders-workshop)
3. [Your first room, by hand](#chapter-3-your-first-room-by-hand)
4. [Building the whole map](#chapter-4-building-the-whole-map)
5. [Items](#chapter-5-items)
6. [NPCs and dialogue](#chapter-6-npcs-and-dialogue)
7. [Atmosphere effects](#chapter-7-atmosphere-effects)
8. [Locks, secrets and traps](#chapter-8-locks-secrets-and-traps)
9. [Economy](#chapter-9-economy)
10. [A simple quest system](#chapter-10-a-simple-quest-system)
11. [In-game help for your own content](#chapter-11-in-game-help-for-your-own-content)
12. [Testing and where to go next](#chapter-12-testing-and-where-to-go-next)

## Chapter 1: world concept

Before you type your first `@dig`, it's worth writing down (on paper, or in a text file next to your terminal) the answer to three questions: **where** does this happen, **who** lives here, and **what can the player actually do here**. Skip this and you'll easily end up with ten nameless "rooms" with no character. Below is the answer to those three questions for the example we'll build throughout this guide -- treat it as a template to fill in with your own idea (a modern-day city, a spaceship, whatever), not as the one true answer.

### Name and tone

Our example world is **Ravenhill Vale** -- a small, half-isolated land: a village in a valley, the forest surrounding it, a river with a mill, hills with an abandoned mine, and an old barrow (burial mound) hiding something older than the village itself. This is a deliberately modest scale -- **one village plus four neighboring areas**, not an entire continent. That's what makes it realistic to actually build within this guide (30-40 rooms) while still leaving room for items, NPCs and effects, instead of drowning in geography alone.

Tone: low, "earthy" fantasy without a lot of flashy magic -- closer to folk tales and ballads than to an epic. I picked this tone on purpose: it doesn't require inventing a whole cosmology or pantheon to work, while still giving us a pretext for everything we want to show off in later chapters (a locked door, something in the woods, a mound nobody visits).

If you'd rather build something completely different -- a modern city, a space station, whatever -- the structure below (regions -> locations -> hooks for NPCs/quests) carries over directly; only the names and descriptions change.

### Geography: five regions

| # | Region | Character | Approximate room count |
|---|--------|-----------|------------------------|
| 1 | Ravenford (village) | the heart of the world: market, inn, smithy, temple, houses | ~10 |
| 2 | Whispering Oak Forest | wilderness north of the village, paths, a hermit's hut | ~7 |
| 3 | The River and Raven Bridge | eastern border, fisherfolk, a water mill | ~5 |
| 4 | Ravenhill Barrow | an old burial mound to the south, an internal "mini-dungeon" | ~8 |
| 5 | The Hills and the Abandoned Mine | terrain to the west, a bandit camp, a crystal grotto | ~7 |

Total: about 37 rooms -- within the 20-50 bracket we set out to build, with margin left over to add something in later chapters (a secret passage, an extra room for a quest) without going over the upper limit.

The exact room-by-room list, with connections, is in Chapter 4 -- for now this is just the skeleton we'll refer back to when designing items and NPCs.

### Factions and story hooks

Four groups/characters we'll build the later chapters around (NPCs in Chapter 6, economy in Chapter 9, quests in Chapter 10):

- **The Ravenford Council of Elders** -- runs the village, based out of the Elder's House. Source of the player's first tasks.
- **The Priests of the Three Moons** -- a small temple in the village, who know about the barrow and about what's better left undisturbed. Source of lore and of the quest in Chapter 4/10.
- **The Hermit of the Whispering Oak Forest** -- a neutral character on the fringe, trades in herbs/information, an alternate source of hints.
- **The Hill Bandits** -- antagonists occupying the abandoned mine, a source of conflict/danger in Chapter 5 (items -- e.g. stolen goods) and Chapter 8 (locks/traps -- their camp is guarded).

You don't need to know the details yet -- they'll come together naturally in later chapters, as we add NPCs and quests. What matters right now is having these four "hooks" in place, so that later rooms, items and characters aren't random, but add up to a coherent whole.

### Porting this to your own theme

If you're building something other than a fantasy village, the same template works like this:

1. Pick a scale you'll actually finish -- one city district, one ship, one base, not "the whole world." 20-50 rooms is a good, proven size for a first project.
2. Split it into 3-6 regions/zones with clearly different characters (as above: village / forest / river / barrow / hills) -- this naturally prevents monotonous descriptions.
3. For each region, write down a rough room count -- it doesn't need to be exact, it's just a budget so the whole project doesn't spiral out of control.
4. List 3-5 factions/characters who'll be the source of NPCs and quests -- a player will always remember a place through its characters more than through the room descriptions alone.

With that on paper, let's move on to Chapter 2 -- preparing the safe place where we'll actually build it.

## Chapter 2: setting up your builder's workshop

### Don't build on a production database

Before you type anything, make sure you're connected to a database you can break with impunity. If you just set up your server following the Getting Started Guide, you're probably running a fresh `toastcore.db` on your own machine -- an ideal place, since you're the only player and the only wizard on it. If instead you have access to an already-running, shared MOO (say, as a builder on someone else's server), **don't experiment with the techniques in this guide there without the admins' permission** -- asking for a separate test database, or at least an isolated area to build in, is good practice, not excessive caution.

The simplest approach if you're building for yourself: copy a fresh `toastcore.db` into its own working directory and run a second, local server on a different port, dedicated to working through this guide. Nothing you build here needs to ever reach a production server -- this is a practice range. If you later want to move a finished piece of the world onto a real MOO, `@dump`/`@create ... with create` (see `help @dump`) lets you export objects into a format you can paste in elsewhere.

### Permissions: builder or programmer

Most of this guide (digging rooms, creating items from ready-made classes) only needs **builder** status (Generic Builder) -- that's what gives you access to `@dig`, `@create`, `@recycle` and friends. To write your own verbs (which we start doing from Chapter 5 onward) you need **programmer** status (Generic Programmer), which includes builder permissions and adds the ability to write code.

If you're a wizard on your own test server (most likely, if you followed the Getting Started Guide), just grant it to yourself:

```
@programmer me
```

(or `@programmer <your-player-name>`, if you'd rather spell it out). If you're building on someone else's server, ask a wizard to run the same command on your account -- see `help @programmer` for their side of the process.

### Object quota -- check this before you start

Every new programmer gets a default limit of **7 objects** (the `size_quota` property) -- meaning that without raising the limit, you won't even finish a single region of our map, let alone the whole ~37 rooms plus items and NPCs. Wizards are the exception -- they aren't limited by quota at all.

Check your current limit:

```
@quota me
```

If you're building as a regular programmer (not a wizard), ask a wizard to raise your limit before going further -- to, say, 100, with margin for the whole example in this guide plus your own experiments:

```
@quota <your-player-name> 100
```

(only a wizard can run this command -- see `help @quota`). If you're a wizard building on your own test server, you can skip this step.

While building, it's worth occasionally checking how many objects you've used:

```
@count
```

and the full list of everything you've created so far shows up via:

```
@audit
```

Both commands will come in handy especially in Chapter 4, where we create dozens of objects back to back.

### Naming convention

MOO doesn't have named constants -- every object you create gets a number (e.g. `#1503`), not a name you can refer to in code. That means **you have to keep your own notes** on which number is which location, or you'll lose track after the twentieth `@dig`.

Recommended convention for this guide:

- Every location gets a full, descriptive, player-visible name (e.g. `"Ravenford Market Square"`) -- that's what goes into `@dig`/`@rename` and what players actually see.
- In parallel, keep a table **outside of MOO**, in a plain text file: region / location name / object number / connections. We build exactly this table together in Chapter 4 -- treat it as a template.
- For your own object classes (custom parents, which we start creating from Chapter 5 onward) a thematic prefix in the name works well, e.g. `"Ravenford Chainmail"` instead of just `"Chainmail"` -- makes it easier to find "your" objects later with `@audit` or `@find`, especially as the database grows.
- Write verb names as single English words, same as the rest of the ToastCore database (`take`, `drop`, `read`) -- that's the engine-wide convention; if you'd also like to add Polish aliases alongside them (this fork supports it), see [TWORZENIE-TRESCI-PO-POLSKU.md](TWORZENIE-TRESCI-PO-POLSKU.md) (in Polish).

With permissions, a quota, and a notebook ready, we can dig the first room -- Chapter 3.

## Chapter 3: your first room, by hand

We start at the heart of our world -- Ravenford Market Square. This will be the only room in the whole guide that we build step by step with a full explanation of every command; from Chapter 4 on we already know what we're doing, so the pace picks up.

### Digging the room

```
@dig "Ravenford Market Square"
```

The server will respond with something like:

```
Ravenford Market Square created as #1500.
```

**Your number will be different** -- every database has a different object counter state, so yours might be `#88`, `#3502`, whatever. For the rest of this chapter I'll use `#1500` as the example -- wherever you see it, substitute your own number. (This is exactly what the notebook from Chapter 2 is for -- write it down now.)

This form of `@dig` (without `to`) creates a room **connected to nothing** -- it floats in limbo, exactly as `help @dig` says (`help @dig` if you want a refresher on the syntax). That's deliberate: we build connections (exits) systematically for the whole map in Chapter 4, instead of doing it piecemeal.

### Moving there

The new room doesn't have any entrance yet, so normal walking won't get you there -- we teleport with `@move`:

```
@move me to #1500
```

You should see the room's name and (for now) an empty, default description.

### Describing the room

The description is the single most important thing a player sees at every location -- worth spending time on. We set it with `@describe`:

```
@describe here as "Uneven cobblestones, worn smooth by a thousand feet. A stone well with a weathered shingle roof stands at the center. A handful of empty wooden stalls stand around it -- the market doesn't start until morning. From the square you can see the inn, the smithy, and paths leading off toward the forest and the hills."
```

I used `here` because we're already standing in the room after `@move` -- you can also give the number directly (`@describe #1500 as "..."`). Type `look` to see the effect.

Technically, `@describe` just sets the `.description` property on the object -- `@describe here as "..."` is shorthand for `@set here.description to "..."`. Worth knowing, because in Chapter 7 we'll be reading and modifying that property from code (e.g. so the description changes with the time of day).

Notice something important in the description text: it mentions "paths leading off toward the forest and the hills," even though those exits don't physically exist yet. That's deliberate -- a room's description is the best place to *foreshadow* where a player can go, before they even check the exit list. Keep that in mind when writing descriptions for the rest of the map in Chapter 4.

### Your first custom verb: `listen`

Before we move on to building the rest of the map, let's see the full code-writing cycle on something small -- a verb that adds a bit of atmosphere when a player types `listen` while standing in the square.

We create a new verb on our room:

```
@verb #1500:"listen hark" none none none
```

`none none none` means a command verb with no arguments at all -- the player just types `listen`, with no object named (see `help @verb` for a refresher on what `dobj`/`prep`/`iobj` mean; there's also a shorthand `tnt` for `this none this` there, but that's something different -- it marks a verb that is **not** called as a player command at all, only from code, and we'll use that later, e.g. with the NPCs in Chapter 6). We give it two names at once (`listen` and `hark`) purely as an example of adding a synonym -- feel free to add more the same way for your own verbs.

Now we enter code-editing mode:

```
@program #1500:listen
```

The server switches into line-input mode. Type (each line separately, Enter after each one):

```
sounds = {"The inn's sign creaking in the wind.", "A dog barking somewhere.", "Someone's footsteps crossing the square and fading into a side alley.", "Silence -- not even the well creaks."};
player:tell(sounds[random(length(sounds))]);
.
```

The final, lone period ends programming mode and installs the verb (exactly as `help @program` describes). If the server reports a syntax error, go back into `@program #1500:listen` and fix it.

Type `listen` in-game a few times -- you should get a different, random message each time. This is the simplest possible example of interactivity: a variable (here: the local variable `sounds`) plus a verb that reacts to a player command. We'll repeat exactly this pattern -- a variable/property holding data, plus a verb that reads it -- throughout the rest of the guide, just on progressively more interesting examples: items (Chapter 5), NPCs (Chapter 6), and atmosphere effects (Chapter 7).

### What's next

We now have one fully described, mildly interactive room. In Chapter 4 we do the same thing systematically for the rest of the map -- this time with a ready-made table of locations and full `@dig` sequences, instead of explaining every step from scratch.

## Chapter 4: building the whole map

### Direction convention

This fork recognizes Polish direction names alongside the standard English abbreviations -- `polnoc`/`n`, `poludnie`/`s`, `wschod`/`e`, `zachod`/`w`, and so on (you can verify this yourself -- it's a table baked into `$string_utils`, used among other things to generate exits). Since this is the English guide, every `@dig` below uses the standard English direction words, in the same dual-name form shown in `help @dig`'s own example (`west,w|east,e,out`) -- the player will be able to type either the full word or the abbreviation.

### How we work: dig, then walk, then dig further

`@dig` **does not move you** into the newly dug room -- you stay where you were, and the new room is just connected by an exit. To keep digging *from* the new room, you have to actually walk into it -- through the very exit you just created. That's actually a good thing: it means you immediately verify the exit works exactly the way it will for a player.

The command sequences below assume you run them one after another, in the order given, starting out standing in the Market Square (`#1500` in our example from Chapter 3 -- **substitute your own number**). After every `@dig` followed by a "walk" instruction, type the given direction as a normal movement command.

### The full map -- reference table

Before we start digging, here's the entire skeleton at once -- worth copying into the notebook from Chapter 2 and filling in the real object numbers as you build.

**Region 1: Ravenford** (village, the heart of the world)

| Location | Connection | Note |
|---|---|---|
| Ravenford Market Square | (start, built in Chapter 3) | hub of the whole region |
| The Broken Horseshoe Inn | west of the Square | quest starting point, see Chapter 10 |
| Born's Forge | north of the Square | the smith NPC lives here later, Chapter 6 |
| Ravenford North Gate | north of the Forge | exit to Region 2 (forest) |
| Temple Lane | east of the Square | |
| Temple of the Three Moons | east of Temple Lane | source of barrow lore |
| Temple Graveyard | south of the Temple | |
| Elder Bramwell's House | northwest of the Square | source of the first quests |
| Old Mara's Herb Cottage | west of the Elder's House | sells herbs/potions, Chapter 9 |
| Ravenford South Gate | south of the Square | exit to Region 3 (river) |

**Region 2: Whispering Oak Forest**

| Location | Connection | Note |
|---|---|---|
| Forest Edge | north of the North Gate | |
| Forest Spring | east of Forest Edge | dead end, good for an atmosphere detail |
| Thicket | north of Forest Edge | |
| Hermit's Hut | west of the Thicket | hermit NPC, Chapter 6 |
| Clearing of the Mushroom Ring | north of the Thicket | magical detail, Chapter 8 |
| Bear Cave | north of the Clearing | dead end/danger |
| Old Lightning-Split Oak | east of the Clearing | landmark, hook for Chapter 8 (secret) |

**Region 3: The River and Raven Bridge**

| Location | Connection | Note |
|---|---|---|
| Riverbank | south of the South Gate | |
| Fisherman's Dock | east of the Riverbank | |
| Water Mill | west of the Riverbank | |
| Raven Bridge | south of the Riverbank | |
| Far Riverbank | south of Raven Bridge | exit to Region 4 (barrow) |

**Region 4: Ravenhill Barrow** (mini-dungeon)

| Location | Connection | Note |
|---|---|---|
| Barrow Entrance | south of the Far Riverbank | |
| Barrow Passage | down from the Barrow Entrance | |
| First Crypt | east of the Passage | |
| Second Crypt | west of the Passage | hidden connection to Region 5, Chapter 8 |
| Trap Hall | south of the Passage | physical trap, Chapter 8 |
| Guardian's Chamber | south of the Trap Hall | guardian NPC/mini-boss, Chapter 6 |
| Treasure Vault | down from the Guardian's Chamber | locked, Chapter 8 |
| Secret Passage | (hidden exit from the Second Crypt) | leads to Region 5 |

**Region 5: The Hills and the Abandoned Mine**

| Location | Connection | Note |
|---|---|---|
| Foot of the Hills | west of the Secret Passage | |
| Mountain Trail | north of the Foot of the Hills | |
| Hilltop | north of the Mountain Trail | dead end, viewpoint/atmosphere |
| Abandoned Mine Entrance | south of the Foot of the Hills | |
| Mine -- First Level | down from the Mine Entrance | |
| Crystal Cave | east of the First Level | treasure/economy, Chapter 9 |
| Mine -- Second Level (Bandit Camp) | down from the First Level | antagonists' base, Chapters 6 and 8 |

Total: 10 + 7 + 5 + 8 + 7 = **37 rooms**, matching the plan from Chapter 1.

### Building Region 1 (the rest of the village)

We assume you're standing in the Market Square (`#1500` in the example). Run these in order:

```
@dig west,w|east,e to "The Broken Horseshoe Inn"
@dig north,n|south,s to "Born's Forge"
```

Walk `north` to enter the Forge, and dig the gate onward from there:

```
@dig north,n|south,s to "Ravenford North Gate"
```

Go back to the Square (`south`, `south`) and dig the eastern branch:

```
@dig east,e|west,w to "Temple Lane"
```

Walk `east` into Temple Lane, and dig further:

```
@dig east,e|west,w to "Temple of the Three Moons"
```

Walk `east` into the Temple and dig the graveyard:

```
@dig south,s|north,n to "Temple Graveyard"
```

Go back to the Square (`north`, `west`, `west` -- or just use `@move me to #1500` if you'd rather not count steps) and dig the remaining two branches:

```
@dig northwest,nw|southeast,se to "Elder Bramwell's House"
```

Walk `northwest` into the Elder's House and dig the herbalist's cottage:

```
@dig west,w|east,e to "Old Mara's Herb Cottage"
```

Go back to the Square and dig the south gate -- our exit from the village toward the river:

```
@dig south,s|north,n to "Ravenford South Gate"
```

Region 1 done -- 10 locations, all connected. Check `@count`, you should now have around 11 objects (10 rooms + exits are counted separately from rooms, so the exact number will be higher -- `@audit` will show the full list).

### Building Region 2 (Whispering Oak Forest)

Walk into the North Gate (from the Forge: `north`) and dig further into the forest:

```
@dig north,n|south,s to "Forest Edge"
```

Walk `north`, and from Forest Edge dig two branches:

```
@dig east,e|west,w to "Forest Spring"
```

Go back (`west`) to Forest Edge and continue deeper into the forest:

```
@dig north,n|south,s to "Thicket"
```

Walk `north` into the Thicket and dig the hermit's hut plus the path onward:

```
@dig west,w|east,e to "Hermit's Hut"
```

Go back (`east`) to the Thicket:

```
@dig north,n|south,s to "Clearing of the Mushroom Ring"
```

Walk `north` into the Clearing and dig the last two rooms of the region:

```
@dig north,n|south,s to "Bear Cave"
```

Go back (`south`) to the Clearing:

```
@dig east,e|west,w to "Old Lightning-Split Oak"
```

Region 2 done -- 7 locations.

### Building Region 3 (The River and Raven Bridge)

Go back to the Square and walk out through the South Gate (`south`, `south`):

```
@dig south,s|north,n to "Riverbank"
```

Walk `south` to the Riverbank and dig three branches:

```
@dig east,e|west,w to "Fisherman's Dock"
```

Go back (`west`):

```
@dig west,w|east,e to "Water Mill"
```

Go back (`east`):

```
@dig south,s|north,n to "Raven Bridge"
```

Walk `south` onto the Bridge and dig the far bank:

```
@dig south,s|north,n to "Far Riverbank"
```

Region 3 done -- 5 locations.

### Building Region 4 (Ravenhill Barrow)

Walk `south` from the Far Riverbank and dig the barrow entrance:

```
@dig south,s|north,n to "Barrow Entrance"
```

Walk `south` and head underground:

```
@dig up,u|down,d to "Barrow Passage"
```

(notice that here the exit *down* leads to the new room, so the exit pair is `up,u|down,d` -- from the passage you go back `up`, not `north`; directions don't have to follow surface geography once you're building something underground).

Walk `down` into the Passage and dig three branches plus the guardian's chamber in a straight line:

```
@dig east,e|west,w to "First Crypt"
```

Go back (`west`):

```
@dig west,w|east,e to "Second Crypt"
```

Go back (`east`):

```
@dig south,s|north,n to "Trap Hall"
```

Walk `south` and keep digging deeper:

```
@dig south,s|north,n to "Guardian's Chamber"
```

Walk `south` and dig the vault beneath the chamber:

```
@dig down,d|up,u to "Treasure Vault"
```

The last room of this region -- the **Secret Passage** -- we deliberately don't dig now. It's a hidden connection between the Second Crypt and Region 5, which requires an exit-hiding mechanism (the exit object exists, but isn't visible in a normal `look`) -- that's exactly the material of Chapter 8. Just make a note that the Second Crypt will need this connection, and we'll come back to it in Chapter 8.

Region 4 done -- 7 of the 8 planned locations (the last one waits for Chapter 8).

### Building Region 5 (The Hills and the Abandoned Mine)

By design, this region connects to the rest of the map through the Secret Passage from Region 4 -- since that doesn't exist yet, for now we'll build Region 5 as a separate, temporarily disconnected group of rooms (`@dig` without `to`), and it'll get its connection after Chapter 8. Good moment for a reminder: a room with no entrance isn't a bug -- it's a normal, transitional state during construction.

```
@dig "Foot of the Hills"
```

Write down the number the server returns, and walk there by hand: `@move me to <number>`.

```
@dig north,n|south,s to "Mountain Trail"
```

Walk `north`:

```
@dig north,n|south,s to "Hilltop"
```

Go back to the Foot of the Hills (`south`, `south` -- or `@move`):

```
@dig south,s|north,n to "Abandoned Mine Entrance"
```

Walk `south` and head down into the mine:

```
@dig down,d|up,u to "Mine -- First Level"
```

Walk `down` and dig the last two locations:

```
@dig east,e|west,w to "Crystal Cave"
```

Go back (`west`):

```
@dig down,d|up,u to "Mine -- Second Level (Bandit Camp)"
```

Region 5 done -- 7 locations, isolated from the rest of the map for now (deliberately, see above).

### Descriptions

Every room above now has a name and connections, but still a default (empty) description. The pattern from Chapter 3 (`@describe here as "..."`) is identical for each of them -- instead of writing out 36 more examples, treat this as an exercise: walk the whole map and describe at least the locations that'll matter in later chapters (the Inn, the Forge, the Temple, the Hermit's Hut, the Clearing of the Mushroom Ring, the Guardian's Chamber, the Bandit Camp -- all of them come back up when we get to items, NPCs, or effects). You can fill in the rest whenever you like -- an empty description doesn't get in the way of further mechanical work.

### What's next

We now have the skeleton of the whole world -- 36 rooms built, plus one (the Secret Passage) deferred to Chapter 8, and all of Region 5 waiting to be spliced into the rest of the map. In Chapter 5 we start filling these locations with content: items the player can pick up, use, and (sometimes) eat.

## Chapter 5: items

### Four standard classes

`help @create` lists four ready-made "standard classes" you can inherit from right away: `$note`, `$letter`, `$thing` and `$container`. Each is useful for something different:

- `$thing` -- the most general class. It can be picked up, dropped, carried. The base for anything that doesn't fit the other three.
- `$note` -- an item with text to read (the `.text` property, a list of lines). Ideal for notes, scraps of writing, little messages.
- `$letter` -- similar to `$note`, but intended for the mail system (an addressee, the ability to send it) -- for this guide we'll mostly stick to `$note`.
- `$container` -- an item you can put other items into (`put X in Y`) and take them out of (`take X from Y`). It also has built-in support for an optional lock (the `.key` property) -- we'll use that in Chapter 8.

### First item: a note in the Hermit's Hut

Walk to the Hermit's Hut (Chapter 4, Region 2) and create a note there:

```
@create $note named "faded note,note"
```

The server returns the new object's number (say, `#1540` -- substitute your own). Describe it from the outside and set the text to read:

```
@describe #1540 as "A scrap of parchment, covered in unpracticed handwriting."
@set #1540.text to {"If you're reading this, the hermit must have let you stay.", "The Three Moons see more than the priests care to admit -- ask about the Barrow.", "-- H."}
```

The new object is still in your inventory (`@create` doesn't automatically place it in the room) -- drop it wherever it should lie:

```
drop faded note
```

Any player who walks into the Hermit's Hut can now pick up the note (`take note`) and read it (`read note`) -- both verbs are already there, inherited from `$note`.

### A container: the chest in the Vault

Walk to the Treasure Vault (Region 4) and create a lockable (not locked yet -- that's Chapter 8) chest there:

```
@create $container named "old iron-bound chest,chest,coffer"
@describe here as "A heavy oak chest bound in iron, dark with damp."
drop old iron-bound chest
```

You can put a first "treasure" inside right away -- for now, a plain `$thing`:

```
@create $thing named "handful of old silver coins,coins,silver"
@describe here as "A handful of coins, tarnished black with age, bearing the profile of a ruler nobody remembers anymore."
put coins in chest
```

A player who makes it to the Vault can `open chest`, `look in chest` and `take coins from chest` -- again, all of this mechanics is already built into `$container`, we haven't written a single line of code for it.

### A custom class: edible items

No standard class handles eating -- a good excuse to show how to build **your own parent class**, which later items of the same kind will inherit from (here: every future meal in the game, without rewriting the code each time).

We create the class (not a specific item -- a prototype the others will inherit from):

```
@create $thing named "Class: Edible Item,edible class"
```

For children of this class to be creatable, it has to be **fertile** -- otherwise `@create` with this parent will refuse to work (`help @chmod` if you want a refresher on what the permission bits mean):

```
@chmod #1550 +f
```

(again: `#1550` is the example number, yours will be different -- this one's worth noting in your notebook under the name `$edible`, we'll use it again).

Now we add the verb `eat`, which will work on every item inheriting from this class:

```
@verb #1550:"eat" this none none
```

```
@program #1550:eat
if (this.location != player)
player:tell("You need to pick that up first.");
else
player:tell("You eat ", this.name, ". ", (this.taste_desc || "It tastes fine enough."));
player:notify_others(player.name + " eats " + this.name + ".");
this:recycle();
endif
.
```

A few new things in this code, explained: `this` is always the object the verb was invoked on (here: the specific meal); `player` is the player who issued the command; `this.location != player` checks whether the item is actually in the player's hands (and not, say, still lying in the room); `this.taste_desc || "..."` is the "default value if the property is empty/unset" pattern, which we'll use again several times in later chapters; `this:recycle()` destroys the item after it's eaten -- an eaten loaf of bread shouldn't stay in your inventory.

Notice that `eat` refers to the property `taste_desc`, which the `$edible` class doesn't have yet -- let's add it, with a sensible default of an empty string:

```
@property #1550.taste_desc "" rc
```

(`rc` are the property's permissions -- readable and chown-owned, i.e. standard, see `help @property`).

Now we create a specific item inheriting from this class -- a loaf of bread in the Inn:

```
@create #1550 named "loaf of dark rye bread,bread,loaf"
@describe here as "A still-warm loaf of dark rye, smelling faintly of caraway."
@set here.taste_desc to "A crisp crust and warm, dense crumb -- the best bread in the whole valley."
```

(I used `here`, so make sure you're standing right where the new object is -- `@create` leaves it in your inventory, so `here` doesn't behave here the way it did in Chapter 3; give the number directly if you'd rather: `@describe #1551 as "..."`).

Drop the bread in the Inn, and try `eat bread` -- you should see the taste description, and the item vanish from your inventory.

### Why this pays off

We'll repeat this same pattern -- a parent class with shared logic, plus many lightweight "children" that differ only in property values -- a few more times: for keys in Chapter 8, and for goods for sale in Chapter 9. Instead of writing the `eat` verb from scratch for every new meal in the game, all you need is another `@create #1550 named "..."` and two or three properties set. That's the essence of object-oriented programming in MOO, and the single biggest productivity lever when building a larger world.

Scatter a few of your own edible items around the world as an exercise (say, whatever's out during market day in the Square, or something the hermit offers) -- in Chapter 6 we start populating this world with characters, who'll be handing these items out, selling them, and talking about them.

## Chapter 6: NPCs and dialogue

### What an NPC is in MOO

MOO doesn't have a separate "type" for a non-player character (NPC) -- it's just a regular object (most often inheriting from `$thing`) that looks and behaves like a character because we wrote its description and the verbs that react to player commands ourselves. It isn't a logged-in player, and it doesn't do anything "on its own" unless we explicitly plan for that -- either through verbs invoked on demand (e.g. `talk to the smith`), or through a self-rescheduling background task (`fork`) that occasionally does something without the player's involvement. We'll build both mechanisms on one example, then replicate it for the rest of the cast.

### A custom class: $npc

Like in Chapter 5, we start with a fertile parent class. Create it anywhere (e.g. in the Square) and note the number as `$npc`:

```
@create $thing named "Class: NPC,npc class"
@chmod #1560 +f
```

Two properties every NPC of this class will need -- a list of lines to say from time to time, and a "cheat sheet" of answers to questions:

```
@property #1560.chatter {} rc
@property #1560.responses [] rc
@property #1560.heartbeat_task 0 rc
```

`responses` will be a map (the MOO data type written `[key -> value, ...]`) pairing a keyword with an answer -- e.g. `["barrow" -> "Don't go there after dark, lad."]`. `heartbeat_task` stores the number of the currently scheduled background task, so we can later stop it (`kill_task`) instead of leaving it running forever, e.g. once the NPC gets recycled.

### The dialogue verb: `ask`

```
@verb #1560:"ask talk" any about any
```

```
@program #1560:ask
topic = strsub(iobjstr, " ", "");
if (topic in mapkeys(this.responses))
this:announce_line(this.responses[topic]);
else
this:announce_line(this.responses["_default"] || "...just shrugs.");
endif
.
```

(`this:announce_line` doesn't exist yet -- let's add it right away, so we don't repeat the same `player:tell`/`announce` in every subsequent NPC verb):

```
@verb #1560:announce_line this none this
```

```
@program #1560:announce_line
text = args[1];
player:tell("\"", text, "\" says ", this.name, ".");
.
```

The command a player types looks like this: `ask smith about barrow` or `talk smith about barrow` (both verb names work the same way, since they're just aliases of the same verb). `about` is one of the prepositions built into the engine -- `help prepositions` shows the full recognized list.

### Random background lines (`fork`)

For an NPC to occasionally speak up on its own (not just in response to a question), we need a task that reschedules itself into the future. This is the first use of `fork` in this guide -- the full syntax is described in the [ToastStunt Programmer's Manual](https://github.com/lisdude/toaststunt-documentation/blob/master/manual/toaststunt-programmers-manual.md); here we just show a working pattern:

```
@verb #1560:heartbeat this none this
```

```
@program #1560:heartbeat
this.heartbeat_task = 0;
if ((this.chatter != {}) && (random(4) == 1))
this.location:announce(this.name, " says: \"", this.chatter[random(length(this.chatter))], "\"");
endif
fork task_id (30 + random(60))
this:heartbeat();
endfork
this.heartbeat_task = task_id;
.
```

```
@verb #1560:start this none this
```

```
@program #1560:start
if (this.heartbeat_task == 0)
this:heartbeat();
endif
.
```

```
@verb #1560:stop this none this
```

```
@program #1560:stop
if (this.heartbeat_task != 0)
kill_task(this.heartbeat_task);
this.heartbeat_task = 0;
endif
.
```

Each call to `:heartbeat` has a one-in-four chance of saying a random line to the whole room (`this.location:announce(...)`, the same built-in method used for connection messages back in Chapter 3), and then **schedules its own next call** 30-90 seconds later (`30 + random(60)`), remembering the scheduled task's number in `.heartbeat_task`. `:stop` kills that scheduled task -- **always call `:stop` before `@recycle`-ing such an NPC**, otherwise the scheduled task will be orphaned (it'll try to invoke a verb on an object that no longer exists, and fail with an error in the server log -- better to avoid that entirely).

### Our first NPC: Born the Smith

```
@create #1560 named "Born the Smith,smith,born"
@describe here as "A broad-shouldered man with hands like beams, in a leather apron scarred by sparks. He watches the forge as if it were the most precious thing he owns."
@set here.chatter to {"Mind the sparks if you come closer.", "Good steel takes patience, same as a good life."}
@set here.responses to ["barrow" -> "Don't go there after dark, lad. The priests know something, but they won't say.", "_default" -> "The smith mutters something under his breath and goes back to work."]
```

Start his background chatter (typing this as him -- that is, invoking the verb on the object you just created, which is still in your inventory, so you can refer to it by name):

```
smith:start()
```

Wait a minute in the Forge and try `ask smith about barrow`.

### The rest of the cast

We repeat this same three-part pattern (the `$npc` class + `@create #1560 named "..."` + setting `.chatter`/`.responses` + `:start()`) for the remaining characters from Chapter 1:

- **Elder Bramwell** (the Elder's House) -- `.responses` includes a hint about the first quest (we expand on it in Chapter 10).
- **The Hermit** (the Hermit's Hut) -- neutral, cryptic answers; knows about the `note` from Chapter 5, since he wrote it himself.
- **The Barrow Guardian** (the Guardian's Chamber, Region 4) -- instead of random lines, `.responses["_default"]` can warn the player against going any further -- in Chapter 8 we'll give him a real passage-blocking mechanic.
- **The Hill Bandits** (Region 5) -- a few instances of the same class with more hostile `.chatter`, e.g. `"You didn't see us."`, `"This ain't a place for you."`.

You don't need to write a single new line of code for any of these characters -- all the programming effort went into the `$npc` class; every subsequent character is just data (a description plus two lists of text). Same productivity lever as with the edible items in Chapter 5, just at a larger scale.

In Chapter 7 we turn to something else: effects that don't belong to any single object, but to the whole world -- time of day and weather.

## Chapter 7: atmosphere effects

### One object holding the whole world's state

Time of day and weather aren't properties of a single room -- they're global state that many rooms should be able to read. Instead of duplicating it everywhere, we create one clock object and refer back to it from wherever it's needed:

```
@create $thing named "World Clock,clock,world clock"
@property #1575.time_of_day "morning" rc
@property #1575.weather "clear" rc
@property #1575.tick_task 0 rc
```

(`#1575` is, again, an example number -- substitute your own). This object never needs to be "seen" by a player -- it's purely a technical state store, so don't worry that it's still sitting in your inventory.

### A self-rescheduling task: `:tick`

The same `fork`/`kill_task` pattern as the NPCs in Chapter 6, except this time the task advances the time of day and rolls the weather instead of speaking lines:

```
@verb #1575:tick this none this
```

```
@program #1575:tick
this.tick_task = 0;
cycle = {"morning", "day", "evening", "night"};
now = 1;
for i in [1..length(cycle)]
if (cycle[i] == this.time_of_day)
now = i;
endif
endfor
this.time_of_day = cycle[(now % length(cycle)) + 1];
roll = random(10);
if (roll <= 2)
this.weather = "rain";
elseif (roll == 3)
this.weather = "fog";
else
this.weather = "clear";
endif
fork task_id (300)
this:tick();
endfork
this.tick_task = task_id;
.
```

```
@verb #1575:start this none this
```
```
@program #1575:start
if (this.tick_task == 0)
this:tick();
endif
.
```
```
@verb #1575:stop this none this
```
```
@program #1575:stop
if (this.tick_task != 0)
kill_task(this.tick_task);
this.tick_task = 0;
endif
.
```

Every call to `:tick` moves `.time_of_day` one step around the cycle morning->day->evening->night->morning..., rolls a new `.weather` (20% chance of rain, 10% chance of fog, otherwise clear), and reschedules itself 300 seconds (5 minutes) later -- often enough for a player to notice the change within a reasonable play session, but not so often it floods the server with tasks.

To be able to refer to the clock from anywhere in the database without remembering its number, we corify it (requires wizard permissions -- `help @corify` for a refresher):

```
@corify clock as world_clock
```

From now on `$world_clock` works everywhere, just like `$room` or `$thing`. Let's start the clock:

```
$world_clock:start()
```

### Wiring room descriptions to the clock's state

This is the most interesting part of this chapter: we want `look` in an outdoor room to append a sentence about the time of day and weather to the description we already wrote in Chapter 4 -- without rewriting that description every time. The [ToastStunt Programmer's Manual](https://github.com/lisdude/toaststunt-documentation/blob/master/manual/toaststunt-programmers-manual.md) describes exactly this pattern (look for its section on object-oriented programming and the `pass()` function): every object has a `:description()` verb that by default returns `this.description`, and `look` calls that verb (it doesn't read the property directly). If we override `:description()` on a child object, we can call the original version via `pass()` and append something of our own.

We're overriding `:description()` not on one room, but **on `$room` itself** -- the parent of literally every location in the whole database, including all 36+ rooms from Chapter 4. That's a deliberate decision, not a mistake: it means we write this code once, and it works everywhere. To avoid tacking weather onto the interior of the Forge or a crypt in the Barrow, we add a switch that each room has to explicitly turn on:

```
@property $room.outdoors 0 rc
```

```
@verb $room:description this none this
```

```
@program $room:description
desc = pass();
if (!this.outdoors)
return desc;
endif
if (typeof(desc) == STR)
desc = {desc};
endif
return {@desc, "", this:weather_desc()};
.
```

```
@verb $room:weather_desc this none this
```

```
@program $room:weather_desc
tod = $world_clock.time_of_day;
weather = $world_clock.weather;
tod_lines = ["morning" -> "The morning sun is only just climbing above the rooftops.", "day" -> "The sun stands high, the day is in full swing.", "evening" -> "The sky is turning orange -- evening is coming on.", "night" -> "It's dark, with only the stars (and maybe the moon) giving any light at all."];
line = tod_lines[tod];
if (weather == "rain")
line = line + " A thin rain is falling.";
elseif (weather == "fog")
line = line + " A thick fog hangs over the ground.";
endif
return line;
.
```

(indexing the map `tod_lines[tod]` assumes `tod` is always one of the map's four keys -- which it is, since we control the possible values of `.time_of_day` ourselves in `:tick`, so we don't need to additionally handle a missing key here).

Now turn the effect on for a few outdoor locations -- e.g.:

```
@set #1500.outdoors to 1
```

(the Square), and likewise for Forest Edge, the Riverbank, the Foot of the Hills, and other "under the open sky" locations from Chapter 4. Leave indoor and underground locations (the Inn, the Forge, the whole Barrow, the mine interior) at the default `.outdoors` of `0` -- weather has no business there.

Type `look` in the Square at different times (or just wait through a few `:tick` cycles) -- the description should now end with a changing line about time of day and weather, while the description text itself from Chapter 3 stays untouched.

### The same pattern elsewhere

Exactly this technique -- overriding `:description()`, calling `pass()` for the original text, appending something of your own -- works on any object, not just `$room`: an NPC could look different depending on whether they're currently working (Born the Smith could have "currently working at the forge" appended during the day, and "asleep on a pallet in the corner" at night). I'll leave that as an exercise -- you already have the whole pattern you need.

In Chapter 8 we go back to something more tangible: locks, keys, and that unfinished Secret Passage from Chapter 4.

## Chapter 8: locks, secrets and traps

### Key expressions -- how locking works in MOO

Before we lock our first object, it's worth understanding the mechanism: any object can be "locked" against a **key expression** -- a logical expression made of objects joined by the operators `&&` (and), `||` (or) and `!` (not). The expression is checked against a specific player (more precisely: the player and everything they're carrying) -- if it comes out true, the player can use the object. `help keys` has the full, formal description; a few examples will do for us here:

- `key` -- true if the candidate *is* the object `key`, **or is carrying it**.
- `me` -- true only for you yourself.
- `key || guardian` -- true for someone carrying `key`, **or** for the `guardian` itself.
- `! coffin` -- true for anyone who is *not* carrying `coffin`.

### Locking the chest in the Vault

In Chapter 5 we created an `old iron-bound chest` in the Vault, open to anyone. Time to fix that. First we need a physical key:

```
@create $thing named "rusty iron key,key"
@describe here as "A heavy, badly rusted key. Someone must have lost it here a long time ago."
```

Leave it in the Guardian's Chamber (Chapter 4) -- a player has to get past the guardian to find it, which is already a small challenge on its own (and in Chapter 6 the guardian already got a warning line about it).

Now we lock the chest -- for containers we use **`@lock_for_open`**, not plain `@lock` (that one controls something else -- whether the container can be picked up/moved at all; `help @lock_for_open` if you want to check the difference):

```
@lock_for_open chest with key
```

Try `open chest` now without the key in your inventory -- the server refuses. Pick up the `rusty iron key` and try again -- it should work. Removing the lock is `@unlock_for_open chest`.

### A compound expression: locking the passage to the Vault

The Vault (Chapter 4) connects to the Guardian's Chamber via a "down" exit. Let's lock that exit itself with a compound expression -- letting through anyone carrying the key, **or** the guardian itself (say, if he needs to go back down there to patrol):

```
@lock #<down-exit-number> with key || guardian
```

You'll find the exit's number with the `@exits` command, standing in the Guardian's Chamber -- it lists all the conventional exits from the current room along with their object numbers (`help @exits`).

### A hidden passage between Region 4 and Region 5

In Chapter 4 we put off the Secret Passage -- the connection between the Second Crypt and the Foot of the Hills. We now have both rooms dug, so we can use the **third form** of `@dig` -- linking two already-existing rooms by object number (`help @dig`, the form with `to <number>`):

Standing in the Second Crypt:

```
@dig west,w to <number of the Foot of the Hills>
```

This creates an exit from the Second Crypt to the Foot of the Hills (one-way -- if you want passage in both directions, repeat the operation the other way while standing at the Foot of the Hills, linking `to <number of the Second Crypt>`).

The exit already works, but it's still just as visible on `look`/`@exits` as any other -- nothing "secret" about it yet. To hide it, we use the `.obvious` property, which the built-in exit-listing mechanism in `$room` checks (exactly the same code we overrode in Chapter 7 for `.outdoors` -- this time we don't need to override anything, `.obvious` is already handled by the database):

```
@exits
@property #<new-exit-number>.obvious 0 rc
```

(the first command is just `@exits`, to read off the newly created exit's number). From now on the exit won't show up in the room's exit list, but a player who types `west` while standing in the Second Crypt will still be moved -- exactly how a secret passage should work.

To give the player any chance of finding it, let's add a hint through a simple search verb in the same room:

```
@verb #<Second Crypt>:"search" none none none
```
```
@program #<Second Crypt>:search
player:tell("You search the walls... and feel a draft from the west, where the stones look loose.");
.
```

(Note: the `player:tell` above doesn't spell out the `west` command directly -- that's deliberate, the player still has to connect "a draft from the west" with trying to go west themselves. How much to hint, and how much to leave for discovery, is a design decision, not a technical one).

### Teleport: the ring of toadstools in the Clearing

The Clearing of the Mushroom Ring (Region 2) now gets its "magical detail," foreshadowed back in Chapter 1 -- a passage into a small, isolated pocket of the world. First, a new room (we budgeted for this back in Chapter 1 -- room number 38, still under 50):

```
@dig "The Other Side of the Ring"
```

Now our own fertile teleport class -- the same class-plus-instances pattern as Chapters 5 and 6:

```
@create $thing named "Class: Teleport,teleport class"
@chmod #<class> +f
@property #<class>.destination #-1 rc
```

```
@verb #<class>:"enter" this none none
```
```
@program #<class>:enter
if (!valid(this.destination))
player:tell("Nothing happens.");
return;
endif
player:tell("The world spins for a moment...");
this.location:announce(player.name, " vanishes into thin air!");
move(player, this.destination);
player.location:announce(player.name, " appears out of nowhere!");
.
```

Two instances, each pointing at the other -- exactly like the two ends of one exit, just implemented as items instead of exits:

```
@create #<class> named "ring of toadstools,ring"
@set #<ring1>.destination to <number of The Other Side of the Ring>
drop ring of toadstools
```

Walk to "The Other Side of the Ring" and repeat it the other way:

```
@create #<class> named "ring of toadstools,ring"
@set #<ring2>.destination to <number of the Clearing of the Mushroom Ring>
drop ring of toadstools
```

Type `enter ring` in the Clearing -- you should land on the other side, and be able to come back the same way.

### A trap: the Trap Hall

The last effect in this chapter uses `:enterfunc()` -- a verb that `$room` (or more precisely, the whole mechanism behind the built-in `move()` function) automatically calls on any room something enters, with the arriving object as the argument. By overriding it (with `pass()`, so we don't lose the default arrival messages), we can add a side effect:

```
@verb #<Trap Hall>:enterfunc this none this
```
```
@program #<Trap Hall>:enterfunc
who = args[1];
pass(who);
if (is_player(who) && (random(2) == 1))
who:tell("Click! You step on a loose flagstone -- a net of stone weights drops from the ceiling and shoves you backward!");
this:announce(who.name, " triggers a trap and gets shoved back!");
move(who, <number of the Barrow Passage>);
endif
.
```

A one-in-two chance of triggering (`random(2) == 1`) makes the trap non-deterministic -- a player might walk through fine the first time and get caught the second, which is more convincing than a rigid, always-the-same block. `is_player(who)` makes sure the trap doesn't fire on every dropped item or NPC that happens to pass through.

### What's next

We now have the full set of "tangible" mechanics: locks, keys, secrets, teleports, traps -- and along the way we finished off the map from Chapter 4 (the Secret Passage and The Other Side of the Ring). In Chapter 9 we add the last big piece missing for full gameplay: a way to buy and sell things.

## Chapter 9: economy

### Currency: a number, not an item

The simplest and most reliable way to handle currency in MOO is a plain number in a player property, not a physical "coin" item that has to be carried, picked up, and watched for duplication. We add a property to `$player` -- same as `.outdoors` on `$room` in Chapter 7, we do it once, on the shared parent, and **every** player in the database (present and future) gets it automatically, defaulting to 0:

```
@property $player.coppers 0 rc
```

For testing purposes, give yourself some money:

```
@set me.coppers to 20
```

### A custom class: shopkeeper

A shopkeeper is an NPC with special trading verbs -- easiest to build as a **child of the `$npc` class** from Chapter 6, rather than starting from scratch. This is the first case in this guide where one of our own classes inherits from another of our own classes, not directly from a standard one -- the chain looks like this: `$thing -> $npc -> $shopkeeper -> (specific shopkeepers)`.

```
@create $npc named "Class: Shopkeeper,shopkeeper class"
@chmod #<class> +f
@property #<class>.stock {} rc
```

`.stock` will be a list of maps, one map per item for sale: name, aliases, price and description. Two verbs for browsing and buying:

```
@verb #<class>:"pricelist" none from this
```
```
@program #<class>:pricelist
player:tell(this.name, " has for sale:");
for item in (this.stock)
player:tell("  ", item["name"], " -- ", item["price"], " coppers");
endfor
.
```

```
@verb #<class>:"buy" any from this
```
```
@program #<class>:buy
text = dobjstr;
for item in (this.stock)
if ((text == item["name"]) || (text in item["aliases"]))
if (player.coppers < item["price"])
player:tell("You can't afford that -- you need ", item["price"], " coppers, and you have ", player.coppers, ".");
else
player.coppers = player.coppers - item["price"];
new = create($thing, player);
new.name = item["name"];
new.aliases = item["aliases"];
new.description = item["description"];
player:tell("You buy ", item["name"], " for ", item["price"], " coppers.");
this.location:announce(player.name, " buys ", item["name"], " from ", this.name, ".");
endif
return;
endif
endfor
player:tell("We don't have anything like that for sale. Try 'pricelist'.");
.
```

Command syntax: `buy potion from shopkeeper` -- `from` is a standard, built-in preposition (`help prepositions`), so it works right away.

And the reverse verb, selling -- the player hands over an item they're actually carrying, the shopkeeper pays a flat amount for it (unless the item has its own `.sale_value` property):

```
@verb #<class>:"sell" any to this
```
```
@program #<class>:sell
if ((dobj == $failed_match) || !valid(dobj) || (dobj.location != player))
player:tell("You're not carrying anything like that.");
return;
endif
if ($object_utils:has_property(dobj, "sale_value"))
value = dobj.sale_value;
else
value = 1;
endif
player.coppers = player.coppers + value;
player:tell("You sell ", dobj.name, " for ", value, " coppers.");
dobj:recycle();
.
```

### A specific shopkeeper: Old Mara

We come back to the herbalist's cottage from Chapter 1/4, flagged from the start as a source of trade:

```
@create #<class> named "Old Mara,mara,herbalist"
@describe here as "An elderly woman with nimble fingers, hung all over with bundles of dried herbs."
@set here.stock to [["name" -> "small vial of potion", "aliases" -> {"vial", "potion"}, "price" -> 3, "description" -> "A cloudy, greenish liquid with a sharp smell."], ["name" -> "bundle of dried herbs", "aliases" -> {"bundle", "herbs"}, "price" -> 1, "description" -> "A handful of assorted herbs, tied together with string."]]
```

Start her background chatter, same as with the smith in Chapter 6 (Mara inherits `:start`/`:stop`/`:heartbeat` from `$npc`, even though she's also a shopkeeper):

```
mara:start()
```

Try `pricelist from mara`, then `buy potion from mara` (with at least 3 coppers), and finally `sell small vial of potion to mara`, to see the full trade cycle in both directions.

### What's next

We have items, NPCs, atmosphere, locks, and now an economy -- only one thing left: a reason for the player to visit all of it in a particular order. In Chapter 10 we tie several of these mechanics together into a simple, tracked quest.

## Chapter 10: a simple quest system

### Quest state: a map on the player

Same as currency in Chapter 9, quest state is a property on `$player` -- shared by every player, added once:

```
@property $player.quests [] rc
```

An empty map by default means "the player hasn't started any quest yet." The key is the quest's name (a string), the value is its status -- in our example, that'll be `"active"` and `"done"`; a missing key means "not started." Same key-checking pattern as `.responses` on the NPCs in Chapter 6:

```
if ("barrow" in mapkeys(player.quests))
state = player.quests["barrow"];
else
state = "new";
endif
```

### Quest: the Signet of the Barrow

Our quest ties together three mechanics from earlier chapters: dialogue with an NPC (Chapter 6), an item locked away in the Vault (Chapter 8), and a currency reward (Chapter 9). First, the quest item -- add it alongside the `handful of old silver coins` in the Vault:

```
@create $thing named "old gold signet ring,signet"
@describe here as "A heavy signet ring engraved with a crest nobody in the village recognizes anymore."
drop old gold signet ring
```

Now two verbs on Elder Bramwell (Chapter 6) -- these are verbs **on this one specific instance**, not on the whole `$npc` class, since they only concern him, not every NPC in the game:

```
@verb elder:"quest" this none this
```
```
@program elder:quest
if ("barrow" in mapkeys(player.quests))
state = player.quests["barrow"];
else
state = "new";
endif
if (state == "new")
player.quests["barrow"] = "active";
this:announce_line("There's an old signet ring of our family resting in the Barrow to the south. The priests are too afraid to go, but someone has to recover it. Bring it to me, and you won't go unrewarded.");
elseif (state == "active")
this:announce_line("I'm still waiting on that signet from the Barrow.");
elseif (state == "done")
this:announce_line("Thank you again for the signet. Well done.");
endif
.
```

(`this:announce_line` is the same helper verb from Chapter 6, inherited from `$npc` -- we don't need to write it again).

```
@verb elder:"return handover" any to this
```
```
@program elder:return
if ("barrow" in mapkeys(player.quests))
state = player.quests["barrow"];
else
state = "new";
endif
if ((dobj == $failed_match) || !valid(dobj) || (dobj.location != player))
player:tell("You're not carrying anything like that.");
elseif (state != "active")
this:announce_line("I never asked you for anything like that.");
elseif (!("signet" in dobj.aliases))
this:announce_line("That's not what I was looking for.");
else
dobj:recycle();
player.quests["barrow"] = "done";
player.coppers = player.coppers + 15;
this:announce_line("Thank you, at last we can breathe easy. Here -- 15 coppers for you.");
this.location:announce(player.name, " hands something to Elder Bramwell.");
endif
.
```

Command syntax for the player: `quest elder`, to accept (or be reminded of) the quest, and `return signet to elder`, to finish it.

### Why quest state, and not just checking whether you're carrying the item

We could check only "does the player have the signet in their inventory," with no `.quests` property at all -- for a single quest that would even work. But a status property has two advantages that only show up once you have more than one quest: first, a quest can be "done" even though the item itself vanished long ago (it got recycled once handed in) -- without a separate status there'd be no way to tell "never started" from "already done." Second, `.quests` is one shared map you can easily add more quests to (a new key, a new pair of verbs) without touching any existing code -- the same reason the shopkeeper's `.stock` from Chapter 9 is a list, not a separate property per item.

As an exercise, try adding a second quest using mechanics from earlier chapters -- say, the Priests of the Temple of the Three Moons (Chapter 1) asking you to deal with the bandits at the Camp (Chapter 6), or to investigate the Clearing of the Mushroom Ring (Chapter 8).

### What's next

The whole mechanical skeleton of the world is done: map, items, NPCs, atmosphere, locks, economy, and a quest tying them all together. In Chapter 11 we wire up the last, easy-to-skip piece -- in-game help, so a player who ends up in our world without this guide in hand has a chance of finding their own way around.

## Chapter 11: in-game help for your own content

### How `help` works in this fork

The `help <topic>` command searches several "help databases" in order: the player themself and their ancestors (up to `$player`), and, if the player is standing in a room, that room and its ancestors too (up to `$room`), and finally, always, the main `$help` database. Each of these objects can have a `.help` property, whose value is a help-database object (or a list of such objects) -- in any such database, a help topic is simply a property named after the topic, whose value is the text (a string for one line, a list of strings for several).

That means we can add help **specific to our world**, which only shows up while the player is actually in it -- we don't need to add anything to the main, server-wide help database at all.

### A help database of our own

A new help database is just a regular object inheriting from Generic Help Database (`#30`):

```
@create #30 named "Help Database: Ravenhill Vale,valley help database"
@corify valley help database as valley_help
```

Each topic is one property -- the property name has to be a valid MOO identifier (no spaces), so a player will type e.g. `help barrow`, not `help old barrow`:

```
@property $valley_help.valley {"Ravenhill Vale is a small land: the village of Ravenford, the Whispering Oak Forest surrounding it, the River and Raven Bridge, an old Barrow to the south, and the Hills with an abandoned mine to the west."} rc
@property $valley_help.barrow {"An old burial mound south of the river. The guardian at the entrance warns newcomers away -- apparently not without reason. Inside lies a locked Treasure Vault."} rc
@property $valley_help.shop {"Old Mara in her cottage sells goods. 'pricelist from mara' shows what's on offer, 'buy <item> from mara' buys it, 'sell <item> to mara' sells her something from your inventory."} rc
@property $valley_help.quests {"Ask Elder Bramwell in the Elder's House about 'quest' if you're looking for something to do around here."} rc
```

### Wiring it into the help system

For these topics to be visible through `help`, we add our database to the `.help` property on `$room` -- same as `.outdoors` in Chapter 7 and `.coppers` in Chapter 9, we do it once, on the shared parent, so it works automatically in every room of the whole world (not just our 38 locations):

```
@property $room.help {} rc
```

(if the server tells you `$room` already has a `.help` property, skip this step -- some database might already define it; we continue regardless of the outcome). Next, we append our database to the list, instead of overwriting it -- in case something was already there:

```
@set $room.help to {@$room.help, $valley_help}
```

Standing anywhere in our world, type `help barrow` or `help shop` -- you should see the matching property's content. Outside our world (in another part of the database) these topics won't be visible -- exactly as it should be.

### Alternative: adding to the main help database

If you'd rather your topics be available everywhere, not just in your world, you can instead add them directly to the main `$help` database (the same one behind `help @dig` or `help movement`) -- the same per-topic-property mechanism, just on the `$help` object instead of our own database. For content specific to one self-contained world (like ours), a separate database wired to `$room` is usually the better choice -- it doesn't mix in with server-wide help.

### What's next

The whole world -- map, items, NPCs, atmosphere, locks, economy, a quest, and now help -- is complete and ready to explore. In Chapter 12, the last one, we run through a testing checklist for the whole thing and gather pointers on where to go next.

## Chapter 12: testing and where to go next

### Checklist -- walk the whole world

Before you call the world done (even if it's only your own test server), it's worth going through everything you've built systematically -- it's easy to typo an object number, or miss a step that only shows up in actual use, not while writing the code:

- **Map**: walk all 38 locations in both directions on every exit -- a missing return exit is the most common mistake with manual `@dig`. The `@dig` in Chapter 4 created both directions at once, but if you tweaked anything by hand afterward, it's easy to forget the other side.
- **Descriptions**: check that every location mentioned in Chapters 5-10 (anywhere an item, NPC or mechanic lives) has a description other than the empty default.
- **NPCs**: for each one, `ask <npc> about <topic>` for at least one topic from their `.responses`, and check that `:start()` was actually called (see below for how to check without guessing).
- **Items**: `eat bread` (or whatever edible item you made), `open`/`close`/`take from` on the chest in the Vault (before and after getting the key).
- **Economy**: a full cycle of `pricelist from mara` -> `buy ... from mara` -> `sell ... to mara`, checking that `.coppers` actually changes.
- **Quest**: `quest elder` (new), `quest elder` again (active -- different text), get the signet, `return signet to elder` (reward), `quest elder` again (done -- a third text variant).
- **Locks and secrets**: try opening the chest without the key (should fail), with the key (should work); walk through the Secret Passage even though it doesn't show up in the exit list; enter the ring of toadstools and come back.
- **Trap**: walk into the Trap Hall several times in a row -- you should see both outcomes (triggered and not), since the chance is random.
- **Help**: `help valley`, `help barrow`, `help shop`, `help quests`, standing anywhere in our world.

### Cleaning up after yourself: background tasks

Every NPC and `$world_clock` has its own self-rescheduling background task (Chapters 6 and 7). To check what's currently running in the background (useful if you suspect something looped incorrectly, or that you forgot to stop something), type:

```
queued_tasks()
```

It returns a list of every scheduled task -- including the ones created by `fork` in our `:heartbeat`/`:tick` verbs. If you want to do a thorough cleanup before a longer break (or before recycling an NPC -- **always** `<npc>:stop()` before `@recycle`, as reminded in Chapter 6), you can stop a specific task with `kill_task(<task-number>)`.

### Common pitfalls (not the programmed kind, this time)

- **Object numbers in this guide are examples.** Every `#1500`, `#1550`, `#1560`, `#1575` and so on in the text is a placeholder -- yours will be different. If you're copying code block by block, double-check each time that you've substituted the right number (or, where possible, refer to objects by name while you're carrying them or standing in them, as many of the examples above do).
- **`this none this` (`tnt`) doesn't mean "a command with no arguments."** It marks a verb meant to be called only from code, never directly by a player -- a genuine no-argument command uses `none none none` (Chapter 3 has the full explanation of the difference).
- **A forgotten `:start()`.** A freshly created NPC or `$world_clock` doesn't do anything on its own until you call `:start()` on it -- easy to forget, since the code compiles fine and looks finished.
- **`@create` doesn't put the object in a room.** The new object lands in your inventory -- remember `drop` if it's meant to lie in a specific place (Chapter 5 points this out at the very first note).
- **Quota limit.** If the server starts refusing `@create`/`@dig` partway through building, go back to Chapter 2 -- you've probably hit your `.size_quota`.

### Summary: what we actually built

- 38 locations across 5 regions, fully connected (including one hidden and one teleport connection).
- Four of our own fertile parent classes: `$edible` (Chapter 5), `$npc` (Chapter 6), the teleport class (Chapter 8), and `$shopkeeper` inheriting from `$npc` (Chapter 9).
- Six extensions of shared base classes (`$room`, `$player`) with new properties and verbs, working automatically across the whole database: `.outdoors` + `:description()` (Chapter 7), `.coppers` (Chapter 9), `.quests` (Chapter 10), `.help` (Chapter 11).
- One global state object (`$world_clock`) with a self-rescheduling background task.
- A full economic cycle, and one quest tying together dialogue, a lock, and a reward.
- A help database of our own, visible only within our world.

No single piece of this is complicated -- all the value comes from how they're wired together.

### Where to go next

A few natural directions to grow this further, each building on something you already have:

- **More quests** -- you already have the whole pattern from Chapter 10, more of them is mostly content, not new code.
- **A combat system** -- this guide deliberately skips it (it's a big topic on its own), but `random()`, properties on the player (like `.coppers`/`.quests`), and the `:enterfunc()`/action-verb techniques from Chapter 8 are exactly the tools it would need.
- **Guilds/factions** -- the Council of Elders and the Bandits from Chapter 1 are a ready-made starting point; a map property similar to `.quests`, just tracking a player's affiliation, would go the same direction.
- **NPCs with real "artificial intelligence"** -- `:heartbeat` from Chapter 6 can be extended to patrol between rooms (`move(this, ...)` instead of just `:announce()`), not just speak random lines in place.
- **Deeper help integration** -- Chapter 11 shows the minimum; Generic Help Database (`#30`, the parent of our `$valley_help`) also supports topics in the form `{"*forward*", ...}` and `{"*subst*", ...}`, useful once you have more content.
- **WAIFs instead of properties on objects** -- for data structures more complex than simple maps/lists (e.g. an elaborate quest inventory), the [WAIF Programmers' Manual](http://ben.com/MOO/waif-progman.html) shows a lighter-weight alternative to full MOO objects.
- **Running a production server** -- once you decide something from this guide is worth showing to other players, `help @quota`, `help @make-player` and the rest of the built-in help topics cover backups, player accounts, and running the server long-term.

For the full, formal reference on the language and every builtin function we used along the way (`fork`, `pass`, maps, `random`, `move` and the rest), see the [ToastStunt Programmer's Manual](https://github.com/lisdude/toaststunt-documentation/blob/master/manual/toaststunt-programmers-manual.md) -- this guide showed them in action, on one concrete example, but the manual is the ultimate source of truth on the syntax and semantics of the MOO language.
