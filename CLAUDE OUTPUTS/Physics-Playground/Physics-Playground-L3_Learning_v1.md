# Learning: Level 3, where the graph becomes a formula

Over coffee, here is what happened and why.

## Step 1: The approach, and why

Level 1 was feeling. Level 2 was measuring. Level 3 had to introduce equations to someone who has never been asked to use one, without the usual result, which is a page of symbols and a learner who quietly leaves.

My starting question was: what is a formula *for*? Not what it is. The honest answer is prediction. A formula lets you know something you have not measured. So every lesson is built to end on that moment: you predict a thing nobody has shown you, press Test, and the world agrees or disagrees.

That gave me one loop, repeated eight times:

1. **Measure.** Collect dots, as in Level 2.
2. **Say the rule in words.** "The train covers the same distance every second."
3. **Fit one number.** The formula appears with a slider. Slide it until the line runs through your own dots.
4. **Predict and test.** Use the formula on a case you did not measure. Then run it.

The formulas appear as words with a number in them, "distance = 2.0 × time", and only afterwards as the scientist's shorthand, d = v × t. The symbols arrive as an abbreviation of something the learner already built.

The eight lessons are ordered by the *shape* of the formula, not by topic: multiply (speed, spring, density), divide (seesaw), multiply by time (gravity adds speed), time times itself (falling distance), divide by a hidden quantity (force and mass), and square root (pendulum). By the end the learner has met the five or six shapes that cover most of school physics.

## Step 2: Roads not taken

- **Start with F = ma and explain the letters.** The standard textbook order. Rejected. It asks for trust before giving a reason. Here the learner sees their dots, sees a line miss them, and fixes the line. The formula is something they made.
- **Automatic curve fitting.** One button, best-fit line, done. Easier and more accurate. Rejected because dragging the slider and watching the line swing through the dots *is* the lesson. It teaches what the number in a formula does. A fit button teaches that computers know things.
- **Multiple-choice quizzes, as in Levels 1 and 2.** Dropped for this level. Recognising the right answer is weaker than producing a number and having it checked against the world.
- **Algebra: rearranging formulas.** "Solve for time." Real physics needs it. Parked for a Level 4, because it is a separate skill and it is where many learners fall off. Level 3 only ever runs a formula forwards.
- **Two numbers to fit at once** (a slope and a starting value). More realistic. Rejected: one knob is findable by feel, two knobs is a search problem.
- **More topics** (waves, circuits, energy). Electricity was never introduced in Levels 1 or 2, so a formula for it would have no dots behind it. Every Level 3 formula stands on something the learner has already touched.

## Step 3: How the pieces connect

Under the eight lessons there is one engine. Each lesson supplies only four things: a scene that produces measurements, a formula with one adjustable number, a question to predict, and its words. The engine does everything else: the table, the graph, the slider, the fit message, the arithmetic helper, the test, the result, the narration.

That is why the lessons feel identical in rhythm. It is also why adding a ninth would be an afternoon and not a week.

The table has a third column that Level 2 did not: "your formula says." Next to each thing you measured sits what your current formula claims. Slide the number and that column moves toward the measured one. It is the fit, shown as arithmetic instead of geometry, for people who trust numbers more than pictures.

When a prediction is wrong, the page tells you which kind of wrong. If your formula was good and your sum was off, it says so. If your formula was off, it sends you back to the dots. Those are different mistakes with different fixes, and confusing them is how people decide they are "bad at physics."

Narration was built in from the start this time, with the same pipeline as before: the page is the script, clips are generated from it, and each clip is transcribed back and compared.

## Step 4: Tools, methods, frameworks

- **Modeling Instruction** is the teaching framework this level borrows most from. Developed by David Hestenes and colleagues at Arizona State, it has students collect data, find the pattern, and write the equation themselves before anyone names a law (Wells, Hestenes and Swackhamer, 1995). The "fit the number to your dots" step is that method shrunk to a slider.
- **Words before symbols.** The order "say it, then write it, then abbreviate it" follows the concrete-to-abstract progression that Bruner described, and that maths teaching calls concrete, pictorial, abstract. Level 1 was the concrete stage, Level 2 the pictorial, Level 3 the abstract.
- **One shared engine** rather than eight bespoke lessons. The discipline of fitting every topic to "one number, one prediction" forced good choices. The seesaw became "distance = number ÷ weights," which is a cleaner first meeting with inverse proportion than the usual two-sided equation.
- **An end-to-end robot test.** A script played all eight lessons as a learner would: measured, fitted, predicted wrong on purpose, read the feedback, then predicted right. All eight passed both paths. This is the test I would least want to skip, because the lesson logic has many steps and each one can break the next.
- **Real constants.** Earth's gravity is 9.8, Mars 3.7, the Moon 1.6. The pendulum uses the true formula, so a 4 m pendulum takes 4.01 s, and "4.00" is accepted because the pass rule allows a small margin.

## Step 5: Tradeoffs

- **Clean data again.** The dots sit exactly on the true line, so the right number makes a perfect fit. Real experiments never do this. It keeps the first meeting with formulas free of noise, at the price of hiding uncertainty for one more level.
- **Forwards only.** No rearranging. A learner can predict distance from time but is never asked for time from distance.
- **"Work it out for me" exists.** It shows the arithmetic and fills in the answer. A learner can lean on it every time. I judged that better than losing someone at the multiplication when the lesson is about the formula. It is a crutch on purpose.
- **Invented units of convenience.** The spring lesson says each weight pulls with 1 newton. A 100 g weight really pulls with 0.98. The text says "about."
- **Eight lessons, not ten.** Each takes longer than a Level 1 lesson because there are four steps. Fewer, deeper.

## Step 6: Mistakes and dead ends

1. **Four labels sat on top of each other.** On a phone, the seesaw's two readouts collided into one unreadable line. The train's "your prediction" flag ran off the right edge. The pendulum's length readout landed on a tick label. The spring's readout ran into its own hook. None of these showed in the logic test, which passed. All four showed in screenshots. A passing test and a readable screen are different claims.
2. **A typo I shipped earlier.** When adding narration I had edited the footer credit and dropped a comma: "Anthropic Claude images from." It was live on Levels 1 and 2. I found it while reusing that footer for Level 3 and fixed all three. Reuse is a good proof-reader.
3. **The pendulum prediction is 4.00 and the truth is 4.01.** With the slider's steps the best fit is exactly 2.00, but the real constant is 2.006. A strict equality check would have failed a correct learner. The pass rule is "within six percent," which is how a physicist would judge it anyway.
4. **Precise dragging on a touchscreen.** The seesaw needs the stack placed to within about half a centimetre. A thumb cannot do that. I added snap-to-half-centimetre and two nudge buttons. Any drag interaction that needs precision needs a fine-adjust control beside it.

## Step 7: Pitfalls for next time

- **Do not let the slider start at the answer.** Each one starts well off, so the first thing the learner sees is a line that misses.
- **Require a few dots before the fit counts.** With one dot, every line through it "fits." The page asks for three.
- **Say what kind of wrong.** "Incorrect" teaches nothing. "Your formula is fine, check your sum" teaches a lot.
- **Predict outside the measured dots when you can.** The pendulum lesson measures up to 2 m and asks about 4 m. That is where a formula earns its keep. Predicting between dots is only reading the graph.
- **Keep one colour for one meaning.** Teal is always "what you measured." Amber is always "what your formula says." The number in the formula is underlined in amber because it controls the amber line.

## Step 8: What an expert sees that a beginner misses

A beginner sees eight physics topics. An expert sees a tour of function shapes: proportional, inverse, quadratic, square root. Those few shapes describe an enormous share of the physical world, and recognising which one you are looking at from a handful of dots is a deeper skill than remembering any single law.

The expert also notices two lessons that quietly teach measurement by inference. In the force lesson you find a cart's mass without a scale. In the density lesson you find what a block is made of from a slope. Using a formula backwards, to learn a hidden thing from visible ones, is most of what experimental science does. The learner is doing it before anyone has called it that.

And the expert notices what the falling-distance lesson sets up: the fitted number is 4.9, and the previous lesson's was 9.8. Exactly half. That coincidence, pointed at but not fully explained, is the doorway to calculus.

## Step 9: Lessons for completely different projects

- **Lead with what the thing is for.** Formulas are for predicting. Budgets are for deciding. Style guides are for consistency. Teach or pitch the purpose first and the notation becomes a convenience instead of a barrier.
- **Let people turn the knob.** A model someone has tuned by hand is a model they understand and trust. This applies to a sales forecast as much as a spring.
- **Build one engine and many configurations.** Once the pattern is right, variety is cheap, and consistency comes for free.
- **Diagnose the error, not just its existence.** In code review, in editing, in coaching: "wrong" is the start of feedback, not the feedback.
- **Test the whole journey, including the wrong turns.** The deliberate wrong prediction was half the test. Most products are only ever tested on the path where the user does everything right.

## Image prompts

Markers in the page: the hero sits in the "Level 3: write the rule" card on lesson 1, and each lesson's picture sits above its title. All nine were generated with Nano Banana (NB2, model `gemini-3.1-flash-image`, 16:9) with the same shared style clause as the earlier levels:

```
Rendered in a warm flat-vector children's science picture-book style with soft paper texture, bold simple shapes, thick clean outlines, no text, no letters, no numbers, no equations. Soft diffused daylight. Color palette emphasizes deep teal, warm amber, cream and coral. The mood is curious and playful.
```

Nano Banana scene sentences:

```
A child and a small round robot stand at a big green chalkboard, the child drawing a smooth rising curve through a row of chalk dots while the robot holds up a ball and a stopwatch. The composition is a wide landscape at eye level, child slightly left of center.
```
```
A red toy train rolling along a straight track past a row of small flags planted at perfectly equal spacing, with a robot beside the track clicking a stopwatch. The composition is a wide side view at track level.
```
```
A brass spring scale hanging from a wooden hook with a lumpy paper bag hanging from it, a child crouching to read where the pointer sits against a row of tick marks. The composition is a straight-on close-up.
```
```
Three cubes of exactly the same size, one pale wood, one cream wax and one black rubber, in a clear water tank seen from the side, the wood floating high, the wax floating low and the rubber resting on the bottom. The composition is a straight-on cutaway side view.
```
```
A large grey elephant sitting close to the middle of a long wooden seesaw, perfectly balanced by a tiny mouse sitting far out at the other end. The composition is a wide side view at ground level.
```
```
A small robot standing at the foot of a cliff aiming a handheld speed radar gun up at a red ball that is falling past the cliff face, with motion streaks above the ball. The composition is a wide side view.
```
```
A red ball dropped from the top of a tall stone tower, shown as six frozen copies of the same ball down the side of the tower, each gap between copies bigger than the one above it. The composition is a tall side view cropped to a wide frame.
```
```
A small wooden cart with three little spinning propeller fans mounted on top, loaded with two bricks, rolling along a straight track on a workbench while a child watches. The composition is a wide side view at track level.
```
```
A very long pendulum with a heavy brass ball hanging from the ceiling of a tall round hall, swinging slowly above a patterned floor while a child and a robot look up at it. The composition is a wide low-angle view.
```

Midjourney, hero (for publication use NBP for the hero instead):

```
child and small round robot at a big green chalkboard, child drawing a smooth rising curve through a row of chalk dots, robot holding a ball and a stopwatch, flat vector children's science picture book, paper texture, thick outlines, deep teal warm amber cream coral palette, soft daylight, wide landscape --ar 16:9 --stylize 200 --v 7
```

Midjourney, lesson set (swap in each scene clause above):

```
[scene], flat vector children's science picture book illustration, paper texture, bold simple shapes, thick clean outlines, no text, deep teal warm amber cream coral palette, soft diffused daylight, playful curious mood --ar 16:9 --stylize 150 --v 7
```

## Epistemic check

Verified by test: all eight lessons complete the full loop in a browser, on both the wrong-prediction and right-prediction paths; no script errors; no sideways scroll at phone width; all 35 narration clips load, and their transcripts match the script apart from spelling and numerals. Constants were checked against standard values: g is 9.8 on Earth, 3.7 on Mars and 1.6 on the Moon; a 1 m pendulum has a 2.01 s period; pine is about 0.5 g/mL.

Not verified: how the narration sounds. And one image was not inspected for physical accuracy beyond a glance: an elephant and a mouse on a seesaw is a cartoon of the lever law, not a diagram of it.

Simplifications a physicist would flag: the pendulum formula is the small-swing approximation; "weight" in grams is used where "mass" is correct, with the proper word introduced in the density lesson; the carts have no friction. No Gemini or ChatGPT triangulation on the physics this run. The content is standard and the numbers were checked against known values.

References: Wells, M., Hestenes, D. & Swackhamer, G. (1995) "A modeling method for high school physics instruction," *American Journal of Physics* 63; Bruner, J. (1966) *Toward a Theory of Instruction*, Harvard University Press; NASA planetary fact sheets for surface gravity.

Attribution: David Berkowitz, with research from Anthropic Claude, images from Google Gemini Nano Banana and narration from Google Gemini text-to-speech.
