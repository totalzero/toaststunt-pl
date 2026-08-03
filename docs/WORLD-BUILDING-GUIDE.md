# Guide: Building Your Own MOO World From Scratch

*This is an original, hands-on guide written directly for this ToastStunt fork (not a translation of an external source) -- the English-language counterpart to [PORADNIK-BUDOWY-SWIATA.md](PORADNIK-BUDOWY-SWIATA.md), the Polish version of this same guide. Both versions build the same kind of world with the same MOO mechanics; only the example content (room names, NPCs, item flavor text) differs to read naturally in each language. Code blocks (commands, property names, verb names, MOO program fragments) are meant to be copied as-is.*

This guide answers the question "I already have a running, empty server -- now what?". It walks, step by step, through one continuous worked example, showing how to build a real, playable slice of a world: from the first `@dig`, through dozens of interconnected rooms, items and NPCs, all the way to special effects like locks, a day/night cycle, an economy, and simple quests. Everything uses one coherent setting -- but every technique shown here carries over 1:1 to any other theme (a modern city, a spaceship, whatever you like).

## Who this guide is for, and what it assumes

I'm assuming:

- You already have a running ToastStunt server with a loaded database (e.g. `toastcore.db`) -- if not, start with the [Getting Started Guide](https://lisdude.com/moo/toaststunt_newbie.txt), which walks through compiling the server and logging in for the first time. (A Polish translation, expanded with extra detail, also lives in this repo as [PRZEWODNIK-DLA-POCZATKUJACYCH.md](PRZEWODNIK-DLA-POCZATKUJACYCH.md).)
- You have a player account with builder (Generic Builder) or programmer permissions -- see `help @programmer` if you need to grant yourself or someone else that status.
- You know the basics of MOO syntax (variables, `if`/`for`, calling verbs), or you're willing to glance at the [ToastStunt Programmer's Manual](https://github.com/lisdude/toaststunt-documentation/blob/master/manual/toaststunt-programmers-manual.md) along the way -- this guide explains each new piece of the language the first time it shows up, but it isn't a full syntax course from zero.

I'm not assuming anything beyond that. In particular, I'm not assuming you're building on a live, production server -- quite the opposite: in Chapter 2, the very first thing we do is set up a safe place to experiment.

**One important, easy-to-miss fact about this specific fork, verified by actually running every example in this guide on a live server rather than just reading the source:** this is a Polish-localized fork, and the localization goes deeper than the bundled database content -- the *engine itself* (the C++ command parser) only recognizes Polish prepositions and a couple of Polish pronouns. This is true no matter what language you write your own room names, descriptions, or dialogue in. Concretely: the special words for "myself" and "here" are `ja` and `tu` (not `me`/`here`), and the engine's built-in preposition table is Polish-only (`jako` not `as`, `za pomoca` not `with`, `w` not `in`, `z` not `from`, `o`/`dla` not `about`/`for`, `u`/`do` not `to`/`at`). You'll also see the server's own system messages (errors, confirmations) in Polish throughout, regardless of what language your content is in -- that's normal, not a sign anything is broken. Every command shown in this guide already accounts for this and uses the words that actually work; a callout box at the end of Chapter 2 covers the specifics in one place.

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

**Note**: this five-region split isn't just an organizing device for this guide's prose -- toaststunt-pl now ships a built-in `.region_name` property on every room that maps onto exactly this split in the running game (it groups the built-in `walk`/`idz`/`mapa` commands by area). Details and an example are in Chapter 12.

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

### IMPORTANT: special words and prepositions in this fork

Before you start typing commands -- as flagged in the introduction, this fork translates more than just the bundled database content; several things are baked directly into the engine (C++), not the database. That means the usual English MOO habits won't work here, and **I verified this live on a running server** before writing it down:

- The special words meaning "myself" and "my current location" are **`ja`** and **`tu`**/**`tutaj`** -- not the English `me`/`here`. E.g. `@move ja to #1500` works; `@move me to #1500` returns `Nie widze tu "me".` ("I don't see 'me' here.")
- The basic prepositions the engine uses to match command arguments are also Polish: `jako` (not `as`), `za pomoca`/`przy uzyciu`/`uzywajac` (not `with`), `w`/`wewnatrz` (not `in`), `z`/`spod` (not `from`), `u`/`do` (not `to`), `o`/`dla` (not `about`/`for`), plus `na`, `nad`, `przez`, `pod`, `za`, `obok`, `ze` -- `help prepositions` shows the full list. This applies both to built-in commands (`@describe X jako "..."`, not `@describe X as "..."`) and to **verbs we write ourselves** -- e.g. `@verb object:"thing" any about any` fails outright with `"about" is not a valid preposition.` when you try to create it; you have to use `any o any`.
- The specifier words inside the `@verb` command itself (`none`, `this`, `any`) **stay in English** -- those aren't prepositions, they're separate `@verb` syntax, and work exactly as `help @verb` describes.
- Calling a verb in the form `object:verb()` (e.g. `smith:start()`) **is not a normal player command at all** -- it's a MOO language expression, so it always needs to be prefixed with `;` (shorthand for `eval`, see `help eval`). What's more, inside `eval`, names like `smith` **are not matched against objects the way they are in ordinary commands** -- they're treated as plain MOO variables, so `;smith:start()` fails with "variable not found". Inside `eval`, use the object's number directly (`;#1561:start()`) -- the exception is `$name` references (like `$room` or `$world_clock`), which work directly in `eval` because `$name` is part of the language's own syntax, not an ordinary variable.
- `@set object.property do value` (note: `do`, not `to`) has **its own simplified value parser** -- it handles strings, numbers, and simple lists/maps, but not nested structures (e.g. a list of maps, `{[...], [...]}`) -- those need `;` (eval) with the object's number, for the same reason as above.
- A handful of admin commands (`@move`, `@dig`, `@corify`) happen to accept **both** `to`/`do` (or `jako`/`as`) in their own code -- that's the exception, not the rule; don't assume it for other commands or your own verbs without checking. `@set` specifically does **not** belong to that group -- it requires `do`, not `to` (verified live), even though it might intuitively seem similar to `@move`. Two commands go the other way and specifically require **English** `me` when referring to yourself -- `@quota` and `@programmer` (most likely an oversight from this fork's original translation pass, not a deliberate choice) -- both are used correctly below, but it's a good demonstration that **every** command is worth checking individually rather than assuming consistency across the whole database.

Every example in the rest of this guide already accounts for all of this -- but if you're ever comparing against an English-language MOO tutorial from somewhere else, this is exactly the kind of detail that will trip you up.

With permissions, a quota, and a notebook ready, we can dig the first room -- Chapter 3.

## Chapter 3: your first room, by hand

We start at the heart of our world -- Ravenford Market Square. This will be the only room in the whole guide that we build step by step with a full explanation of every command; from Chapter 4 on we already know what we're doing, so the pace picks up.

### Digging the room

```
@dig "Ravenford Market Square"
```

The server will respond with something like (remember, per the callout above, actual system messages are in Polish regardless of your content's language -- "utworzony" means "created"):

```
Ravenford Market Square (#1500) utworzony.
```

**Your number will be different** -- every database has a different object counter state, so yours might be `#88`, `#3502`, whatever. For the rest of this chapter I'll use `#1500` as the example -- wherever you see it, substitute your own number. (This is exactly what the notebook from Chapter 2 is for -- write it down now.)

This form of `@dig` (without `to`) creates a room **connected to nothing** -- it floats in limbo, exactly as `help @dig` says (`help @dig` if you want a refresher on the syntax). That's deliberate: we build connections (exits) systematically for the whole map in Chapter 4, instead of doing it piecemeal.

### Moving there

The new room doesn't have any entrance yet, so normal walking won't get you there -- we teleport with `@move`:

```
@move ja to #1500
```

You should see the room's name and (for now) an empty, default description.

### Describing the room

The description is the single most important thing a player sees at every location -- worth spending time on. We set it with `@describe`:

```
@describe tu jako "Uneven cobblestones, worn smooth by a thousand feet. A stone well with a weathered shingle roof stands at the center. A handful of empty wooden stalls stand around it -- the market doesn't start until morning. From the square you can see the inn, the smithy, and paths leading off toward the forest and the hills."
```

I used `tu` ("here") because we're already standing in the room after `@move` -- you can also give the number directly (`@describe #1500 jako "..."`). Type `look` to see the effect.

Technically, `@describe` just sets the `.description` property on the object -- `@describe tu jako "..."` is shorthand for `@set tu.description do "..."` (note: `do`, not `to` -- `@set` is one of the commands that does *not* accept the English word, see the callout in Chapter 2). Worth knowing, because in Chapter 7 we'll be reading and modifying that property from code (e.g. so the description changes with the time of day).

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

Go back to the Square (`south`, or just `@move ja to #1500` if you'd rather not count steps) and dig the eastern branch:

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

Go back to the Square (`west`, `west`, or just use `@move ja to #1500` if you'd rather not count steps) and dig the remaining two branches:

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

Region 1 left you in the Square -- walk into the North Gate (`north` to the Forge, then `north` again to the Gate -- or `@move ja to <the North Gate's number from your notebook>`) and dig further into the forest:

```
@dig north,n|south,s to "Forest Edge"
```

Walk `north`, and from Forest Edge dig two branches:

```
@dig east,e|west,w to "Forest Spring"
```

Still standing in Forest Edge (you dug Forest Spring from the outside, you never walked in), continue deeper into the forest:

```
@dig north,n|south,s to "Thicket"
```

Walk `north` into the Thicket and dig the hermit's hut plus the path onward:

```
@dig west,w|east,e to "Hermit's Hut"
```

Still standing in the Thicket (same situation as with Forest Spring):

```
@dig north,n|south,s to "Clearing of the Mushroom Ring"
```

Walk `north` into the Clearing and dig the last two rooms of the region:

```
@dig north,n|south,s to "Bear Cave"
```

Still standing in the Clearing (didn't walk into the Cave):

```
@dig east,e|west,w to "Old Lightning-Split Oak"
```

Region 2 done -- 7 locations.

### Building Region 3 (The River and Raven Bridge)

Go back to the Square (`@move ja to #1500` is simplest, since it's several steps from the Clearing) and walk out through the South Gate (`south`):

```
@dig south,s|north,n to "Riverbank"
```

Walk `south` to the Riverbank and dig three branches:

```
@dig east,e|west,w to "Fisherman's Dock"
```

Still on the Riverbank (didn't walk into the Dock):

```
@dig west,w|east,e to "Water Mill"
```

Still in the same spot:

```
@dig south,s|north,n to "Raven Bridge"
```

Walk `south` onto the Bridge and dig the far bank:

```
@dig south,s|north,n to "Far Riverbank"
```

Region 3 done -- 5 locations.

### Building Region 4 (Ravenhill Barrow)

You're still on Raven Bridge (you never stepped onto the Far Bank) -- walk `south` to get there, and dig the barrow entrance:

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

Still standing in the Passage (didn't walk into the First Crypt):

```
@dig west,w|east,e to "Second Crypt"
```

Still in the Passage:

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

Write down the number the server returns, and walk there by hand: `@move ja to <number>`.

```
@dig north,n|south,s to "Mountain Trail"
```

Walk `north`:

```
@dig north,n|south,s to "Hilltop"
```

Go back to the Foot of the Hills (`south` -- or `@move`):

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

Still on the First Level (didn't walk into the Cave):

```
@dig down,d|up,u to "Mine -- Second Level (Bandit Camp)"
```

Region 5 done -- 7 locations, isolated from the rest of the map for now (deliberately, see above).

### Descriptions

Every room above now has a name and connections, but still a default (empty) description. The pattern from Chapter 3 (`@describe tu jako "..."`) is identical for each of them -- instead of writing out 36 more examples, treat this as an exercise: walk the whole map and describe at least the locations that'll matter in later chapters (the Inn, the Forge, the Temple, the Hermit's Hut, the Clearing of the Mushroom Ring, the Guardian's Chamber, the Bandit Camp -- all of them come back up when we get to items, NPCs, or effects). You can fill in the rest whenever you like -- an empty description doesn't get in the way of further mechanical work.

### What's next

We now have the skeleton of the whole world -- 36 rooms built, plus one (the Secret Passage) deferred to Chapter 8, and all of Region 5 waiting to be spliced into the rest of the map. In Chapter 5 we start filling these locations with content: items the player can pick up, use, and (sometimes) eat.

## Chapter 5: items

### Four standard classes

`help @create` lists four ready-made "standard classes" you can inherit from right away: `$note`, `$letter`, `$thing` and `$container`. Each is useful for something different:

- `$thing` -- the most general class. It can be picked up, dropped, carried. The base for anything that doesn't fit the other three.
- `$note` -- an item with text to read (the `.text` property, a list of lines). Ideal for notes, scraps of writing, little messages.
- `$letter` -- similar to `$note`, but intended for the mail system (an addressee, the ability to send it) -- for this guide we'll mostly stick to `$note`.
- `$container` -- an item you can put other items into (`put X w Y`) and take them out of (`take X z Y`). It also has built-in support for an optional lock (the `.key` property) -- we'll use that in Chapter 8.

### First item: a note in the Hermit's Hut

Walk to the Hermit's Hut (Chapter 4, Region 2) and create a note there:

```
@create $note named "faded note,note"
```

The server returns the new object's number (say, `#1540` -- substitute your own). Describe it from the outside and set the text to read:

```
@describe #1540 jako "A scrap of parchment, covered in unpracticed handwriting."
@set #1540.text do {"If you're reading this, the hermit must have let you stay.", "The Three Moons see more than the priests care to admit -- ask about the Barrow.", "-- H."}
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
@describe chest jako "A heavy oak chest bound in iron, dark with damp."
drop old iron-bound chest
```

You can put a first "treasure" inside right away -- for now, a plain `$thing`. A freshly created container starts out **closed**, so we open it first (verified live: `put` into a closed container just fails):

```
@create $thing named "handful of old silver coins,coins,silver"
@describe coins jako "A handful of coins, tarnished black with age, bearing the profile of a ruler nobody remembers anymore."
open chest
put coins w chest
```

A player who makes it to the Vault can `open chest`, `look w chest` and `take coins z chest` -- again, all of this mechanics is already built into `$container`, we haven't written a single line of code for it (remember Chapter 2's rule -- this fork's built-in prepositions are Polish, `w`/`z`, not English `in`/`from`).

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
this.location:announce_all_but({player}, player.name + " eats " + this.name + ".");
recycle(this);
endif
.
```

A few new things in this code, explained: `this` is always the object the verb was invoked on (here: the specific meal); `player` is the player who issued the command; `this.location != player` checks whether the item is actually in the player's hands (and not, say, still lying in the room); `this.taste_desc || "..."` is the "default value if the property is empty/unset" pattern, which we'll use again several times in later chapters; `this.location:announce_all_but({player}, ...)` tells everyone else in the room (but not the player themselves -- they already saw their own `player:tell`) -- `:announce` from Chapter 3 tells *everyone* with no exceptions, `:announce_all_but` lets you skip someone; `recycle(this)` destroys the item after it's eaten -- an eaten loaf of bread shouldn't stay in your inventory. **Note:** it has to be `recycle(this)` (the builtin function), not `this:recycle()` (a verb call) -- the latter is verified live to silently do nothing and just return 0.

Notice that `eat` refers to the property `taste_desc`, which the `$edible` class doesn't have yet -- let's add it, with a sensible default of an empty string:

```
@property #1550.taste_desc "" rc
```

(`rc` are the property's permissions -- readable and chown-owned, i.e. standard, see `help @property`).

Now we create a specific item inheriting from this class -- a loaf of bread in the Inn:

```
@create #1550 named "loaf of dark rye bread,bread,loaf"
@describe bread jako "A still-warm loaf of dark rye, smelling faintly of caraway."
@set bread.taste_desc do "A crisp crust and warm, dense crumb -- the best bread in the whole valley."
```

(I used the item's own name, `bread`, not `tu` -- **`@create` leaves the new object in your inventory, not in the room, and `tu` always means the room, never an item in your hands, no matter where you're standing** -- verified live: using `tu` here silently describes the room instead of the item, which is easy to miss because `@describe` still reports "Opis ustawiony." either way. For freshly created items in your inventory, use their name or alias instead -- or the number directly, if you'd rather: `@describe #1551 jako "..."`).

Drop the bread in the Inn, and try `eat bread` -- you should see the taste description, and the item vanish from your inventory.

### Why this pays off

We'll repeat this same pattern -- a parent class with shared logic, plus many lightweight "children" that differ only in property values -- a few more times: for keys in Chapter 8, and for goods for sale in Chapter 9. Instead of writing the `eat` verb from scratch for every new meal in the game, all you need is another `@create #1550 named "..."` and two or three properties set. That's the essence of object-oriented programming in MOO, and the single biggest productivity lever when building a larger world.

Scatter a few of your own edible items around the world as an exercise (say, whatever's out during market day in the Square, or something the hermit offers) -- in Chapter 6 we start populating this world with characters, who'll be handing these items out, selling them, and talking about them.

## Chapter 6: NPCs and dialogue

### What an NPC is in MOO

MOO doesn't have a separate "type" for a non-player character (NPC) -- it's just a regular object (most often inheriting from `$thing`) that looks and behaves like a character because we wrote its description and the verbs that react to player commands ourselves. It isn't a logged-in player, and it doesn't do anything "on its own" unless we explicitly plan for that -- either through verbs invoked on demand (e.g. `talk to the smith`), or through a self-rescheduling background task (`fork`) that occasionally does something without the player's involvement. We'll build both mechanisms on one example, then replicate it for the rest of the cast.

### A custom class: $npc

Like in Chapter 5, we start with a fertile parent class. Create it anywhere (e.g. in the Square):

```
@create $thing named "Class: NPC,npc class"
@chmod #1560 +f
```

This time we actually corify it (not just jot the number down like `$edible` in Chapter 5) -- in Chapter 9 we'll build a class that inherits from this one via `@create $npc named ...`, so `$npc` needs to be a real reference, not just a name in our heads:

```
@corify #1560 jako npc
```

(for the rest of this chapter we still use the number `#1560` directly -- it works identically to `$npc`, just two ways of writing the same object).

Two properties every NPC of this class will need -- a list of lines to say from time to time, and a "cheat sheet" of answers to questions:

```
@property #1560.chatter {} rc
@property #1560.responses [] rc
@property #1560.heartbeat_task 0 rc
```

`responses` will be a map (the MOO data type written `[key -> value, ...]`) pairing a keyword with an answer -- e.g. `["barrow" -> "Don't go there after dark, lad."]`. `heartbeat_task` stores the number of the currently scheduled background task, so we can later stop it (`kill_task`) instead of leaving it running forever, e.g. once the NPC gets recycled.

### The dialogue verb: `ask`

```
@verb #1560:"ask talk" any o any
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

The command a player types looks like this: `ask smith o barrow` or `talk smith o barrow` (the verb name can be English or Polish -- that's just an alias -- but the preposition has to be `o`, not the English `about`; reminder from the Chapter 2 callout: this fork's built-in prepositions are Polish, `help prepositions` shows the full list).

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
@describe smith jako "A broad-shouldered man with hands like beams, in a leather apron scarred by sparks. He watches the forge as if it were the most precious thing he owns."
@set smith.chatter do {"Mind the sparks if you come closer.", "Good steel takes patience, same as a good life."}
@set smith.responses do ["barrow" -> "Don't go there after dark, lad. The priests know something, but they won't say.", "_default" -> "The smith mutters something under his breath and goes back to work."]
```

Walk to the Forge (`@move ja to <Forge's number from your notebook>`) and drop him there -- that's his intended spot:

```
drop smith
```

Start his background chatter. Calling a verb in the form `object:verb()` **is not a normal player command** -- per the Chapter 2 callout, it's a MOO expression, so it needs `;` (eval), and inside `eval` a bare name like `smith` doesn't get matched to an object -- you need the object's number instead:

```
;#1561:start()
```

Wait a minute in the Forge and try `ask smith o barrow`.

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

From now on `$world_clock` works everywhere, just like `$room` or `$thing`. Let's start the clock -- remember the `;` before the verb call (per the Chapter 2 callout: `object:verb()` needs `eval`); unlike `smith` in Chapter 6, `$world_clock` works here directly, because `$name` syntax is part of the language itself, not an ordinary variable:

```
;$world_clock:start()
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
@set #1500.outdoors do 1
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

In Chapter 5 we created an `old iron-bound chest` in the Vault, open to anyone. Time to fix that. First we need a physical key -- create it standing in the Vault, next to the chest (`@move ja to <the Vault's number>` if you're not already there):

```
@create $thing named "rusty iron key,key"
@describe key jako "A heavy, badly rusted key. Someone must have lost it here a long time ago."
```

The new key is now in your inventory -- **leave it there for now** (don't drop it yet), because `@lock_for_open` needs to find it, and key expressions match objects the same way ordinary commands do: you have to be carrying it or standing in the same room as it (verified live: if the key is sitting in a different room than the one you run the command in, `@lock_for_open` reports "Nie mozna znalezc obiektu o nazwie 'key'" -- "cannot find an object named 'key'").

Now we lock the chest -- for containers we use **`@lock_for_open`**, not plain `@lock` (that one controls something else -- whether the container can be picked up/moved at all; `help @lock_for_open` if you want to check the difference):

```
@lock_for_open chest za pomoca key
```

(note: `help @lock_for_open`'s own syntax example still shows the English `with` -- that's a stale bit of help text that slipped through an earlier audit; the word that actually works is `za pomoca`, per the Chapter 2 callout).

Now move the key to its intended home -- the Guardian's Chamber (Chapter 4) -- and drop it there: a player has to get past the guardian to find it, which is already a small challenge on its own (and in Chapter 6 the guardian already got a warning line about it). The chest was opened back in Chapter 5 and has stayed open ever since -- open/closed is separate from locked/unlocked, so close it now before you leave with the key, otherwise the demonstration below won't work (the chest will just be "already open" no matter what):

```
close chest
@move ja to <the Guardian's Chamber's number>
drop key
```

Go back to the Vault and try `open chest` without the key in your inventory -- the server refuses. Go back for the key, take it, bring it back, and try again -- it should work. Removing the lock is `@unlock_for_open chest`.

### A compound expression: locking the passage to the Vault

The Vault (Chapter 4) connects to the Guardian's Chamber via a "down" exit. Let's lock that exit itself with a compound expression -- letting through anyone carrying the key, **or** the guardian itself (say, if he needs to go back down there to patrol). If you already built the Guardian as an exercise from Chapter 6's "rest of the cast," use him -- if not, walk to the Guardian's Chamber and build a minimal version now, just enough for this example (same `$npc` pattern as the smith, without `.chatter`/`:start()`, since all we need here is the object itself for the key expression):

```
@create #1560 named "Barrow Guardian,guardian"
@describe guardian jako "A silent, armored shape that doesn't take its eyes off you."
drop guardian
```

Standing in the Guardian's Chamber:

```
@lock #<down-exit-number> za pomoca key || guardian
```

You'll find the exit's number with the `@exits` command, standing in the Guardian's Chamber -- it lists all the conventional exits from the current room along with their object numbers (`help @exits`).

### A hidden passage between Region 4 and Region 5

In Chapter 4 we put off the Secret Passage -- the connection between the Second Crypt and the Foot of the Hills. We now have both rooms dug, so we can use the **third form** of `@dig` -- linking two already-existing rooms by object number (`help @dig`, the form with `to <number>`):

Standing in the Second Crypt:

```
@dig west,w to <number of the Foot of the Hills>
```

This creates an exit from the Second Crypt to the Foot of the Hills (one-way -- if you want passage in both directions, repeat the operation the other way while standing at the Foot of the Hills, linking `to <number of the Second Crypt>`).

The exit already works, but an ordinary player trying `@ways` (the "what are the obvious exits from here" hint command) will still see it as plainly as any other -- nothing "secret" about it yet. (Plain `look` in this fork doesn't show an exit list at all, by the way -- it's `@ways`, not `look`, that matters here.) To hide it, we use the `.obvious` property, which the built-in `$room:obvious_exits()` mechanism checks (a similar kind of mechanism to the one we overrode in Chapter 7 for `.outdoors` -- this time we don't need to override anything, `.obvious` is already handled by the database):

```
@exits
@set #<new-exit-number>.obvious do 0
```

(the first command is just `@exits`, to read off the newly created exit's number -- **note**: every new exit already has an `.obvious` property, defaulting to true, so we use `@set`, not `@property` -- the latter returns "already exists", verified live). From now on an ordinary player won't see this exit via `@ways`, but anyone who types `west` while standing in the Second Crypt will still be moved -- exactly how a secret passage should work. (As the owner/wizard, `@exits`/`@ways` still show you everything, hidden exits included -- that's a deliberate convenience for builders, not a bug; to verify the hiding itself, check from an ordinary player's perspective, or directly via `;room:obvious_exits()`.)

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
@set #<ring1>.destination do <number of The Other Side of the Ring>
drop ring of toadstools
```

Walk to "The Other Side of the Ring" and repeat it the other way:

```
@create #<class> named "ring of toadstools,ring"
@set #<ring2>.destination do <number of the Clearing of the Mushroom Ring>
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
@set ja.coppers do 20
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
@verb #<class>:"pricelist" none z this
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
@verb #<class>:"buy" any z this
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
move(new, player);
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

Command syntax: `buy potion z shopkeeper` -- `z` is this fork's standard, built-in preposition for "from" (`help prepositions`; reminder from Chapter 2: this fork's engine recognizes Polish prepositions, not English ones).

Notice `move(new, player)` right after `create($thing, player)` -- **the second argument to `create()` is the new object's owner, not its location** (verified live: without that `move`, the purchased item exists, is owned by the player, but sits nowhere -- `.location` is `#-1`/`$nothing` -- so the player doesn't actually have it in hand, even though the "You buy..." message implies success). `create()` doesn't raise any error if you forget the `move` -- an easy trap.

And the reverse verb, selling -- the player hands over an item they're actually carrying, the shopkeeper pays a flat amount for it (unless the item has its own `.sale_value` property):

```
@verb #<class>:"sell" any do this
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
recycle(dobj);
.
```

### A specific shopkeeper: Old Mara

We come back to the herbalist's cottage from Chapter 1/4 (`@move ja to <its number from your notebook>`), flagged from the start as a source of trade:

```
@create #<class> named "Old Mara,mara,herbalist"
@describe mara jako "An elderly woman with nimble fingers, hung all over with bundles of dried herbs."
```

`.stock` is a list of maps -- in MOO, lists are `{...}` and maps are `[...]`, so "a list of maps" looks like `{[...], [...]}`. That's a fairly complex literal, and **`@set` has its own simplified value parser that can't handle this kind of nesting** (verified live: `@set mara.stock do {[...], [...]}` fails with "Nie mozna sparsowac" even though the syntax is valid MOO). Instead we use `;` (eval), which runs the real language compiler -- and in eval, as you'll remember from Chapter 7, names like `mara` don't work (they're not variables), so we need the object's number:

```
;#<Mara's number>.stock = {["name" -> "small vial of potion", "aliases" -> {"vial", "potion"}, "price" -> 3, "description" -> "A cloudy, greenish liquid with a sharp smell."], ["name" -> "bundle of dried herbs", "aliases" -> {"bundle", "herbs"}, "price" -> 1, "description" -> "A handful of assorted herbs, tied together with string."]};
drop mara
```

Start her background chatter, same as with the smith in Chapter 6 (Mara inherits `:start`/`:stop`/`:heartbeat` from `$npc`, even though she's also a shopkeeper) -- remember `;` and the object number, same reasons as with the smith:

```
;#<Mara's number>:start()
```

Try `pricelist z mara`, then `buy potion z mara` (with at least 3 coppers), and finally `sell small vial of potion do mara`, to see the full trade cycle in both directions.

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
@describe signet jako "A heavy signet ring engraved with a crest nobody in the village recognizes anymore."
drop old gold signet ring
```

Now two verbs on Elder Bramwell (Chapter 6) -- these are verbs **on this one specific instance**, not on the whole `$npc` class, since they only concern him, not every NPC in the game. The syntax is `this none none` (dobj=elder, no preposition, no iobj) -- **not** `this none this`: since `prep` is `none`, the player can never physically supply an iobj, so an `iobj=this` requirement could never be satisfied -- verified live that this exact mistake makes the command always fail with "I don't understand", no matter what's typed. This is the same mistake Chapter 3 warned about (tnt/`this none this` is for verbs that are **not** called as a command), just applied the wrong way round:

```
@verb elder:"quest" this none none
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
@verb elder:"return handover" any do this
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
recycle(dobj);
player.quests["barrow"] = "done";
player.coppers = player.coppers + 15;
this:announce_line("Thank you, at last we can breathe easy. Here -- 15 coppers for you.");
this.location:announce(player.name, " hands something to Elder Bramwell.");
endif
.
```

Command syntax for the player: `quest elder`, to accept (or be reminded of) the quest, and `return signet do elder`, to finish it.

### Why quest state, and not just checking whether you're carrying the item

We could check only "does the player have the signet in their inventory," with no `.quests` property at all -- for a single quest that would even work. But a status property has two advantages that only show up once you have more than one quest: first, a quest can be "done" even though the item itself vanished long ago (it got recycled once handed in) -- without a separate status there'd be no way to tell "never started" from "already done." Second, `.quests` is one shared map you can easily add more quests to (a new key, a new pair of verbs) without touching any existing code -- the same reason the shopkeeper's `.stock` from Chapter 9 is a list, not a separate property per item.

As an exercise, try adding a second quest using mechanics from earlier chapters -- say, the Priests of the Temple of the Three Moons (Chapter 1) asking you to deal with the bandits at the Camp (Chapter 6), or to investigate the Clearing of the Mushroom Ring (Chapter 8).

### What's next

The whole mechanical skeleton of the world is done: map, items, NPCs, atmosphere, locks, economy, and a quest tying them all together. In Chapter 11 we wire up the last, easy-to-skip piece -- in-game help, so a player who ends up in our world without this guide in hand has a chance of finding their own way around.

## Chapter 11: in-game help for your own content

### How `help` works in this fork

The `help <topic>` command searches several "help databases" in order: the player themself and their ancestors (up to `$player`), and, if the player is standing in a room, that room and its ancestors too (up to `$room`), and finally, always, the main `$help` database. Each of these objects can have a `.help` property, whose value is a help-database object (or a list of such objects) -- in any such database, a help topic is simply a property named after the topic, whose value is the text (a string for one line, a list of strings for several).

Ideally we'd want help **specific to our world**, wired to `$room` the way `.outdoors` was in Chapter 7, so it would only show up while the player is actually here. Live-testing that ran into a real obstacle (see below), so we end up wiring it to `$player` instead -- help will work everywhere, not just in our world, but the mechanism is identical, and that's still better than nothing.

### A help database of our own

A new help database is just a regular object inheriting from Generic Help Database (`#30`). We avoid a colon in the name -- `@create`/`@rename` have a special, "non-preferred" `name:alias` syntax where the colon acts as a separator, so `"Help Database: Ravenhill Vale,..."` would get cut into "Help Database" as the name and "Ravenhill Vale" as a separate alias (verified live -- harmless, but not the intended result):

```
@create #30 named "Ravenhill Vale Help Database,valley help database"
@corify valley help database as valley_help
```

Each topic is one property -- the property name has to be a valid MOO identifier (no spaces), so a player will type e.g. `help barrow`, not `help old barrow`:

```
@property $valley_help.valley {"Ravenhill Vale is a small land: the village of Ravenford, the Whispering Oak Forest surrounding it, the River and Raven Bridge, an old Barrow to the south, and the Hills with an abandoned mine to the west."} rc
@property $valley_help.barrow {"An old burial mound south of the river. The guardian at the entrance warns newcomers away -- apparently not without reason. Inside lies a locked Treasure Vault."} rc
@property $valley_help.shop {"Old Mara in her cottage sells goods. 'pricelist z mara' shows what's on offer, 'buy <item> z mara' buys it, 'sell <item> do mara' sells her something from your inventory."} rc
@property $valley_help.quests {"Ask Elder Bramwell in the Elder's House about 'quest' if you're looking for something to do around here."} rc
```

### Wiring it into the help system

`$room` seems like the natural place -- but it turns out **Generic Editor (`#50`) already has its own, local `.help` property** (it uses it for help within the line editor), and it happens to be -- surprisingly -- a descendant of `$room`. MOO won't let you add a property at a parent if some descendant already defines it locally (`@property $room.help {} rc` returns "Wlasciwosc jest juz zdefiniowana na jednym lub wiecej potomkach" -- "This property is already defined on one or more descendants"). This restriction has been baked into this fork's database from the start, so anyone taking this route hits the exact same wall.

Fortunately, `$player` already has a `.help` property (defined by the base database -- confirmed via `@check-prop`), so we just need to append to it. Same as `.stock` on Old Mara in Chapter 9, `@set` can't handle the `{@list, item}` splice syntax -- that needs `;` (eval):

```
;$player.help = {@$player.help, $valley_help};
```

Standing anywhere, type `help barrow` or `help shop` -- you should see the matching property's content. Unlike the original plan, these topics are now available to every player everywhere, not just in our world -- in your own project, if you care about a tighter scope, the fix is a custom class in between `$room` and your locations (e.g. `$valley_room`), where you can safely add `.help` without the Generic Editor conflict.

### Alternative: adding to the main help database

Since `$player.help` is already global anyway, you could just as easily add our topics directly to the main `$help` database (the same one behind `help @dig` or `help movement`) -- the same per-topic-property mechanism, just on the `$help` object instead of our own database, with the same end result. The advantage of keeping a separate database (`$valley_help`) instead of writing straight into `$help` is organization -- it's easier to find and manage topics specific to our world when they live in one object of their own, instead of mixed in with hundreds of server-wide help topics.

### What's next

The whole world -- map, items, NPCs, atmosphere, locks, economy, a quest, and now help -- is complete and ready to explore. In Chapter 12, the last one, we run through a testing checklist for the whole thing and gather pointers on where to go next.

## Chapter 12: testing and where to go next

### Checklist -- walk the whole world

Before you call the world done (even if it's only your own test server), it's worth going through everything you've built systematically -- it's easy to typo an object number, or miss a step that only shows up in actual use, not while writing the code:

- **Map**: walk all 38 locations in both directions on every exit -- a missing return exit is the most common mistake with manual `@dig`. The `@dig` in Chapter 4 created both directions at once, but if you tweaked anything by hand afterward, it's easy to forget the other side.
- **Descriptions**: check that every location mentioned in Chapters 5-10 (anywhere an item, NPC or mechanic lives) has a description other than the empty default.
- **NPCs**: for each one, `ask <npc> o <topic>` for at least one topic from their `.responses`, and check that `:start()` was actually called (see below for how to check without guessing).
- **Items**: `eat bread` (or whatever edible item you made), `open`/`close`/`take z` on the chest in the Vault (before and after getting the key).
- **Economy**: a full cycle of `pricelist z mara` -> `buy ... z mara` -> `sell ... do mara`, checking that `.coppers` actually changes.
- **Quest**: `quest elder` (new), `quest elder` again (active -- different text), get the signet, `return signet do elder` (reward), `quest elder` again (done -- a third text variant).
- **Locks and secrets**: try opening the chest without the key (should fail), with the key (should work); walk through the Secret Passage even though it doesn't show up in the exit list; enter the ring of toadstools and come back.
- **Trap**: walk into the Trap Hall several times in a row -- you should see both outcomes (triggered and not), since the chance is random.
- **Help**: `help valley`, `help barrow`, `help shop`, `help quests`, standing anywhere in our world.

### Bonus: built-in navigation (`walk`/`idz`, `mapa`)

Every fresh toaststunt-pl now ships four extra player commands by default -- no code required on your part, they already live on `$player`:

- **`walk <place>` / `idz <place>`** -- automatically walks to any previously visited location by name (or part of its name), one exit per second. Typed with no argument, it shows a numbered list of known places -- typing just the number also works as a pick.
- **`map <place>` / `mapa <place>`** -- same lookup, but instead of walking, it prints the exit sequence to type by hand (e.g. `Droga do "Rynek w Kruczym Brodzie": n e n`).
- **`stop` / `przerwij`** -- interrupts a walk started by `walk`/`idz`.

These work automatically because every room your character visits registers itself on the player's "known places" list on the way in (a hook in `$room:enterfunc`). You can use this in place of manually walking the **Map** checklist item above -- `idz`-ing to each of the 38 locations in turn is faster than typing individual directions.

To make use of the five regions from Chapter 1 (instead of one long list of all 38 locations at once), set `.region_name` on the rooms of each region, e.g.:

```
;$string_utils:name_and_number(#1500)
;#1500.region_name = "Kruczy Brod"
```

(repeat for a representative room in each of the five Chapter 1 regions -- rooms with no value set simply fall into one shared, unnamed region together, so nothing breaks if you skip some). A player standing in a given region then sees only that region's known places in `walk`/`mapa`, instead of the whole Valley at once.

Note that the command names themselves stay as shown above (`walk`/`idz`, `map`/`mapa`, `stop`/`przerwij`) regardless of which language you're playing in -- same rule as every other bilingual command pair in this fork.

### Cleaning up after yourself: background tasks

Every NPC and `$world_clock` has its own self-rescheduling background task (Chapters 6 and 7). To check what's currently running in the background (useful if you suspect something looped incorrectly, or that you forgot to stop something), type (remember the `;` -- this is a builtin function, not a player command, same pattern as `object:verb()` in Chapter 6):

```
;queued_tasks()
```

It returns a list of every scheduled task -- including the ones created by `fork` in our `:heartbeat`/`:tick` verbs. If you want to do a thorough cleanup before a longer break (or before recycling an NPC -- **always** `<npc>:stop()` before `@recycle`, as reminded in Chapter 6), you can stop a specific task with `;kill_task(<task-number>)`.

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
- A help database of our own, wired to `$player.help` (available everywhere -- `$room.help` turned out to be blocked by a property Generic Editor already defines, see Chapter 11).

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
