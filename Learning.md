# Learning: turning a phonics worksheet into a game plan

Over coffee, here's what happened and why.

## Step 1: The approach, and why

The starting point was a photo of a "Phonics Search: Short i" worksheet. My first move was not to brainstorm mechanics. It was to ask what the worksheet already *is*. It is a hidden-object puzzle (Highlights Hidden Pictures, basically) plus a word list plus one target sound. That means the game is already there in skeleton form. The job was to find what the paper can't do and build around those gaps.

The paper can't make sound. That is a big deal, because the entire lesson is a sound (/i/). And the paper gives no reason to care about finding a lid. So the plan adds exactly two things: audio-first decoding (hear, blend, then find) and a character who needs the objects. Everything else hangs off those two.

I also noticed the worksheet is black and white. That handed me the reward mechanic for free: finding an object colors it in. No points, no stars. The page itself becomes the progress bar. The best mechanics usually come from the material, not from a list of "gamification techniques."

## Step 2: Roads not taken

- **Straight digitization.** Tap twelve words on a screen. Rejected because it's the paper with worse ergonomics. If a digital version isn't better than paper, don't build it.
- **Printable plus camera.** Kid circles on real paper, phone checks it. I liked this because it keeps crayons involved. Rejected because detecting scribbles on a crowded doodle field is flaky, and you lose the audio loop, which is the entire point.
- **Voice-first.** Kid says "pig" instead of tapping. Pedagogically the strongest option. Rejected for now because speech recognition on four-year-olds is bad, and a false "wrong" is worse than no voice at all. Parked as a later phase.
- **Creative mode.** Build your own scene. Fun, zero decoding. Parked as an unlockable reward.

The pattern: each rejection was "good idea, wrong moment," not "bad idea." That distinction matters when you revisit a plan later.

## Step 3: How the pieces connect

The plan has a spine: core loop → story arc → build plan → risks. The loop comes first because everything else is a container for it. The story arc exists to give the loop twelve reasons to repeat. The build plan is just the loop made of real materials (SVG, recorded audio, local save). The risks section is a check: does anything in the build plan threaten the loop? (Yes: cutting the sound lens for scope would reintroduce the worksheet's picture-ambiguity problem.)

The twelve words got sorted into four scenes of three by asking "where would these objects plausibly live together?" Wig, lid, bin → bedroom. Dig, pin, pig → garden. That's just grouping by setting, but it's what turns a list into a story.

## Step 4: Tools and frameworks

- **Science of Reading** (National Reading Panel 2000; Castles, Rastle & Nation 2018) decided the loop order: hear and blend *before* search, because blending onto letters is what builds word memory. Searching first would make this a vocabulary game, not a decoding game.
- **Hirsh-Pasek's four pillars** for educational apps (active, engaged, meaningful, socially interactive) were the checklist. The plan is weak on "socially interactive," which is honest: it leans on a parent co-playing.
- **Mayer's coherence principle** was the brake. It's the research-backed version of "don't add confetti that distracts from the lesson."
- **Feature-integration theory** (Treisman) justified the decoys: a search is harder when distractors share features with the target, so a pen next to a pin is the right kind of hard.

If I'd picked a pure game-design framework (say, Koster's theory of fun) instead of reading-science ones, the plan would have more mechanics and less pedagogy. For a learning product, pedagogy picks the mechanics, not the reverse.

## Step 5: Tradeoffs

- **Recorded audio over text-to-speech.** More expensive, more work, but TTS cannot say an isolated /i/ reliably. Here the expensive option is the only correct one.
- **No fail state.** Loses some tension. Gains a four-year-old who doesn't quit.
- **Single HTML page over a native app.** Loses app store discovery and some polish. Gains "works on grandma's phone tonight."
- **Twelve words, four scenes.** Could have been one big scene. Four small ones match attention span and give the story beats, at the cost of more art.

## Step 6: Mistakes and dead ends

Two things went sideways.

1. I tried to get a second opinion from Gemini via its API, as your preferences ask. The sandbox blocked the call because it would have sent an API key from a shell command. So the plan is single-source, and I said so in the artifact rather than pretending otherwise. The same block stopped me from generating the Nano Banana images, which is why the plan has prompts and markers instead of embedded pictures.
2. The repo had no ABOUT ME, PROJECTS, or TEMPLATES folders, so the "read these first" protocol couldn't run. I proceeded on your stated preferences alone.

## Step 7: Pitfalls for next time

- **Picture-naming is the silent killer of phonics worksheets.** "Lid" drawn as a jar, "tin" as a can, "win" as a ribbon. A kid who decodes perfectly fails anyway. Any picture-based phonics product needs a way to hear the intended label.
- **Dialect can contradict your lesson.** Pin/pen merger speakers don't hear the contrast you're teaching. Check your minimal pairs against the dialect of your audience.
- **Don't reuse scanned worksheet art.** It's almost certainly copyrighted. Redraw.
- **Test the blend step for skipping.** Kids will rush any gate between them and the fun part. Instrument it.

## Step 8: What an expert sees that a beginner misses

A beginner sees twelve words and designs twelve mini-games. An expert sees one loop and asks how to make it worth repeating twelve times. Repetition is the product; variety is the wrapper.

A beginner adds rewards (stars, badges). An expert makes the reward *be* the content: the page coloring in. Extrinsic rewards fade; visible progress on the thing itself doesn't.

A beginner picks mechanics first, then checks pedagogy. An expert lets the learning science constrain the mechanics, then makes those constraints feel like play.

## Step 9: Lessons for other projects

- **Start by naming what the source already is.** A worksheet is a game. A spreadsheet is a database. A memo is a decision. Half the design is recognizing the existing shape.
- **Find the one thing the current medium can't do.** Paper can't make sound. That one gap drove the whole plan. Most "digital transformations" fail because they digitize the parts that already worked.
- **"Good idea, wrong moment" is a separate bin from "bad idea."** Keep a parking lot. Half of a plan's value is what it deliberately defers.
- **Make the progress indicator out of the work itself.** Whether it's a coloring page, a build log, or a sales pipeline, visible state beats a score.
- **When a check fails, say so in the deliverable.** The blocked Gemini call went into the plan as a sentence, not into a footnote nobody reads.

## Addendum: the ten images

You asked for ten images. The raw Gemini API was blocked (credential in a shell command), so I routed through the ElevenLabs connector, which runs the same Nano Banana 2.1 model. That worked. What did not work was pulling the finished files back into the sandbox: the proxy refuses the storage host. So the plan links to the images instead of embedding them.

Lesson: when one door is locked, check whether a connector already in the room goes to the same place. And when you can generate but not retrieve, link, say why, and move on rather than burning time on a workaround.

## Addendum: "product, mobile and web"

Two words from you changed nine rows of the plan. That is the point of asking open questions early: "product" pulls in COPPA, store categories, monetization and a parent account, none of which a one-kid prototype needs. "Mobile and web" settles the stack (one web codebase wrapped for the stores) and forces scene density to scale with screen width.

Lesson: the cheapest design decisions are the ones made before anything is built. Ask the two or three questions whose answers fan out the widest, and ask them first.

## Addendum: the prototype

**Approach.** One HTML file, no framework, no build step. Twenty doodles are hand-written SVG paths in a 100-unit box, laid on a 4 by 5 grid with a little jitter so it looks drawn, not placed. Each object is a config entry, so a new scene is a new list, not new code.

**Roads not taken.** Drag-to-blend was the plan. I shipped tap-in-order instead: a four-year-old's drag on a phone is unreliable, and the plan already named tap as the fallback. Recorded audio was out of reach in a sandbox, so the browser's own voice stands in. It says whole words fine and isolated sounds badly ("ih" is a coin flip). That is the single biggest gap between this proto and the product.

**What connects to what.** The hint ladder, decoy message, press-and-hold sound lens, and parent stats all hang off one round object. If you add a scene, none of them change.

**Mistakes.** My first headless test failed twice for reasons that were not bugs: the test page lacked the artifact's hidden-element reset, and the pulsing tile never looked "stable" to the test tool. Lesson: when a test fails, first ask whether the test or the thing is wrong. I fixed the first by adding the reset to the page anyway, which is the right call for a file that may be opened outside the artifact viewer.

**What an expert sees.** The parental gate is a two-second hold, not a math question. Store reviewers accept both; a hold is faster to build and harder for a kid to stumble through by accident. Also: no fail state anywhere. A wrong tap names the object and replays both words. That is the lesson, not a penalty.

**Next.** Record a human voice for 12 words and 9 phonemes, test with three kids, then scene 2.
