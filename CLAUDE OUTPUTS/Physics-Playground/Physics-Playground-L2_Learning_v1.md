# Learning: Level 2, where the playground gets a ruler

Over coffee, here is what happened and why.

## Step 1: The approach, and why

Level 1 was about feeling physics. Level 2 had a narrower job: get someone from "the ball on carpet stops sooner" to "here is a graph that says so," without an equation in sight.

My starting question was what the smallest honest step up from Level 1 is. The answer is not algebra. It is the act of writing a number down. So every Level 2 lesson has the same three things that Level 1 did not: a measuring tool in the scene (ruler, stopwatch, scale, thermometer, measuring jug, oscilloscope), a table that fills in as you measure, and a graph that draws itself from that table.

The order of the nine lessons is the order in which graph-reading skills stack:

1. Ruler and stopwatch: a measurement is a pair of numbers, and a pair is a dot.
2. Match the graph: read a position graph by walking it.
3. Speed up, slow down: a different graph of the same motion, and the first look at area.
4. Dropping and timing: your first real experiment with a surprising result.
5. Stretch a spring: a straight line means a rule, and the rule has a limit.
6. Swing timer: which things do not matter. Controlling variables.
7. Heat it up: a graph with flat parts that mean something.
8. Weigh it, dunk it: a graph with a dividing line that predicts.
9. See the sound: a graph of something you cannot see at all.

The first three teach the language. The next five use it to find something out. The last one shows the language reaching past things you can watch.

## Step 2: Roads not taken

- **Adding graphs to the Level 1 sims.** The cheap option: bolt a chart onto each of the ten existing lessons. Rejected, because most Level 1 sims were designed for feel, not for measurement. The magnet sim has nothing worth graphing at this level. Measurement lessons need scenes built around a measuring tool.
- **Free-form graphing tool.** "Pick any two quantities and plot them." Powerful, and what real lab software does. Rejected for the same reason as the big sandbox in Level 1: a beginner needs each graph to have one obvious story.
- **Showing the equation after the graph.** Tempting in the spring lesson especially. I held the line. The text says "every 100 g adds 2 cm," which is the rule in words. That is the bridge to Level 3, and crossing it early would have broken the brief.
- **A charting library (Chart.js, D3).** Rejected. The graphs here redraw sixty times a second alongside the scene, share its colors, and need odd extras like a dividing line with a shaded side. A forty-line hand-written graph function did all of it and stays in sync by construction.
- **Sandbagging the data with fake measurement noise.** Real measurements scatter. I considered adding jitter so learners would meet error bars. Parked: scatter is a real idea but it is a second idea, and each lesson gets one.

## Step 3: How the pieces connect

Each lesson is two canvases side by side (stacked on a phone): the scene on the left, the graph on the right. They are drawn in the same animation frame from the same numbers, so the dot on the graph and the ball in the scene cannot disagree.

Under them sits the data table. The table is the hinge between the two pictures. The scene produces a row, the row becomes a dot. I wanted that chain visible, because "where do graphs come from" is the actual lesson.

One shared graph function draws every chart: gridlines, axis labels, tick numbers, and helper methods for points, lines, shaded areas and reference lines. Nine lessons, one grammar. Once a learner has read one of these graphs, the other eight look familiar.

## Step 4: Tools, methods, frameworks

- **Kinesthetic graphing** (lesson 2) comes straight from physics education research. Motion-detector labs where students walk to match a graph are among the best-documented interventions for graph reading (Thornton and Sokoloff, 1990, *American Journal of Physics*). Dragging a walker with your thumb is the phone version.
- **The classic misreadings** drove the quiz design. Students reliably read a graph as a picture of the path, and confuse the height of a line with its slope (McDermott, Rosenquist and van Zee, 1987; Beichner, 1994). The quiz distractors are those exact mistakes: "sloping down means going backwards" on the speed graph is the trap, and the lesson exists to spring it.
- **Controlled-variable experiment** (lesson 6): change one thing, hold the others. The pendulum is the standard vehicle because two of its three obvious knobs do nothing, which is a better surprise than any knob that does something.
- **A palette validator.** The chart colors were run through a script that checks color-blind separation and contrast, in light and dark. My first picks failed (the teal read as grey, the amber was too pale on white). The validator caught what my eye did not.
- **Playwright** drove every lesson headlessly: pressed the buttons, held the hold-buttons, dragged the walker, waited for the pot to boil, and screenshotted each result.

Real numbers are used throughout: gravity is 9.81, the pendulum times match the textbook formula (2.01 s at 1 m), a 4 m drop takes 0.90 s. Level 1 could fake its physics. Level 2 cannot, because the learner is reading the numbers.

## Step 5: Tradeoffs

- **Clean data over realistic data.** Dots land exactly on the line. Good for seeing the rule, bad for learning that real data scatters.
- **Nine guided experiments over an open lab.** Each graph has fixed axes chosen so the story fits. The learner never chooses a scale, which is itself a graph skill left for later.
- **Compressed time in the heat lesson.** Real ice takes many minutes to melt. Here the whole heating curve fits in under two minutes. The shape is right and the durations are not. The flat parts sit at exactly 0 and 100, which is the point.
- **Words like "packed-in" give way to units.** Level 2 uses metres, seconds, grams, millilitres and degrees. That costs a little friendliness and buys the ability to read a real axis.

## Step 6: Mistakes and dead ends

1. **The spring broke its own ruler.** At the heaviest loads the spring stretched past the end of the 40 cm ruler and off the canvas, and off the top of the graph. I capped the load so the overstretch is visible but stays on the page. Lesson: test the extremes of every slider, not just the middle.
2. **Water under ice at minus twenty.** The pot showed liquid water beneath the ice cubes before any melting had happened. A learner would never have forgiven that in a lesson about melting. The water level now grows only as the ice melts. Spotted in the phone screenshot.
3. **A thermometer hiding behind the stopwatch.** Two instruments, same corner. Moved one.
4. **A test that lied.** My first automated check of the gas pedal reported the car never moved. The button was fine. The test was pressing at a spot that had scrolled off screen. A failing test is a claim about the test as much as the code. Check both.
5. **A control whose name contained a decimal point.** The burner's "high" setting was labelled internally as 2.2, and the dot made it unfindable by the test script. Renamed to "high." Names are for finding things, so keep them boring.
6. **An interruption mid-build.** One reply was cut off partway through reviewing screenshots. I picked up from the files on disk: the app was written, six of nine lessons were verified, three were not. Having the work saved in files rather than in my head made the restart cheap.

## Step 7: Pitfalls for next time

- **Label the axes in the learner's words and the scientist's units together.** "position (m)", not "x". The axis label is the first thing a beginner reads and the first thing an expert forgets to write.
- **One graph, one y-axis.** It is tempting to overlay position and speed. Two scales on one chart is the most common way charts mislead. Use a toggle or two charts.
- **The table matters as much as the graph.** Skip it and graphs look like magic. Show it and they look like bookkeeping, which is what they are.
- **Make hold-buttons work for thumbs and keyboards.** A press-and-hold control needs to handle the finger sliding off, the page losing focus, and the space bar.
- **Distractors should be real misconceptions.** A quiz with silly wrong answers teaches nothing. One with the tempting wrong answer teaches the lesson a second time.

## Step 8: What an expert sees that a beginner misses

A beginner sees nine graphs. An expert sees four different kinds of graph meaning, introduced one at a time: slope means rate (lessons 1 to 3), area means accumulation (3), straight means proportional (5), and flat means something is happening that the axis does not show (7). Lesson 8 adds a fifth: a line that divides a plane into two outcomes. That is the quiet curriculum underneath the playful one.

The expert also notices what the pendulum lesson is really for. It is not about pendulums. It is the first time the learner finds out that a measurement can tell you something does not matter. Null results are half of science and almost never taught.

## Step 9: Lessons for completely different projects

- **Show where the number comes from.** Scene, then row, then dot. Any dashboard, report or pitch gets more trust when the reader can trace a figure back to the thing it measures.
- **Teach the reading before the writing.** People walked graphs before being asked to interpret one. In any new notation, a spreadsheet, a contract, a codebase, let people operate it before asking them to analyze it.
- **A flat line is information.** The heating curve's plateaus are where the interesting physics is. In business charts too, the stretch where the metric did not move despite effort is often the story.
- **Pick the surprise, then build backwards.** Four times the height, twice the time. Heavy bob, same swing. Every lesson was designed from its surprise outward. A presentation or an article can be built the same way.

## Image prompts

Markers in the page: the hero sits in the "Level 2: measure it" card on lesson 1, and each lesson's picture sits above its title. All ten were generated with Nano Banana (NB2, model `gemini-3.1-flash-image`, 16:9) using the same shared style clause as Level 1:

```
Rendered in a warm flat-vector children's science picture-book style with soft paper texture, bold simple shapes, thick clean outlines, no text, no letters, no numbers, no equations. Soft diffused daylight. Color palette emphasizes deep teal, warm amber, cream and coral. The mood is curious and playful.
```

Nano Banana scene sentences:

```
A child and a small round robot at a workbench covered with a tape measure, a stopwatch, a kitchen scale and a thermometer, pinning a hand-drawn graph with a rising line onto a corkboard behind them. The composition is a wide landscape at table height, child slightly left of center.
```
```
A toy train running along a straight track laid beside a long wooden ruler with evenly spaced marks, while a small robot holds up a big round stopwatch. The composition is a wide side view at track level.
```
```
A child walking back and forth across a chalk-marked line on a playground while a friend on a bench draws a wiggly line on a big sheet of paper on an easel. The composition is a wide side view.
```
```
A small red car on a straight road with a dashboard dial glowing in the corner, speed streaks behind it, with a long paper strip unrolling from its rear showing a rising and falling line. The composition is a wide side view.
```
```
A child on a tall ladder dropping a red ball past a wall-mounted measuring tape, with a robot at the bottom holding a stopwatch, the ball frozen mid-fall. The composition is a tall side view cropped to a wide frame.
```
```
A coiled metal spring hanging from a hook with a stack of round weights pulling it down, a ruler fixed beside it showing how far it has stretched. The composition is a straight-on close-up.
```
```
A grandfather clock pendulum and a child's long swing ride side by side, both caught mid-swing, with a robot timing them on a stopwatch. The composition is a wide side view.
```
```
A glass pot of ice cubes melting on a small stove with a tall thermometer standing in it and gentle steam starting to rise, a notebook beside it with a stepped rising line. The composition is a medium straight-on view at counter height.
```
```
A kitchen scale with a stone on it next to a tall measuring jug of water with a wooden block floating and the water level clearly raised, a rubber duck waiting on the counter. The composition is a straight-on close-up.
```
```
A child singing into a microphone connected to a boxy old oscilloscope screen showing a glowing wavy line, a robot pointing at one wave on the screen. The composition is a medium side view.
```

Midjourney, hero (for publication use NBP for the hero instead):

```
child and small round robot at a workbench with tape measure, stopwatch, kitchen scale and thermometer, pinning a hand-drawn rising line graph to a corkboard, flat vector children's science picture book, paper texture, thick outlines, deep teal warm amber cream coral palette, soft daylight, wide landscape --ar 16:9 --stylize 200 --v 7
```

Midjourney, lesson set (swap in each scene clause above):

```
[scene], flat vector children's science picture book illustration, paper texture, bold simple shapes, thick clean outlines, no text, deep teal warm amber cream coral palette, soft diffused daylight, playful curious mood --ar 16:9 --stylize 150 --v 7
```

## Epistemic check

Numbers in the sims were checked against standard results: free-fall time from 2 m is 0.64 s and from 4 m is 0.90 s; a 1 m pendulum has a 2.01 s period; water is 1 g per mL; melting and boiling points are 0 and 100 °C at sea level; piano range is about 27.5 to 4,186 Hz. The spring's elastic limit and the heating durations are invented for the model, and the text does not claim otherwise. I did not triangulate with Gemini or ChatGPT on this run; the content is introductory and the checks above were done against known values.

References: Thornton, R. & Sokoloff, D. (1990) "Learning motion concepts using real-time microcomputer-based laboratory tools," *American Journal of Physics* 58; McDermott, L., Rosenquist, M. & van Zee, E. (1987) "Student difficulties in connecting graphs and physics," *American Journal of Physics* 55; Beichner, R. (1994) "Testing student interpretation of kinematics graphs," *American Journal of Physics* 62.

Attribution: David Berkowitz, with research from Anthropic Claude and images from Google Gemini Nano Banana.
