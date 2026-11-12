# Learning: adding energy and wave lessons to a Level 3 that already existed

Over coffee, here is what happened and why.

## Step 1: The approach, and why

The ask was narrow: take the two lessons I had drafted, energy from height and ripples in a tank, and put them into the Level 3 that was already shipped, with narration.

The shipped Level 3 has a strict loop. Measure dots, say the rule in words, fit one number so a line runs through the dots, then predict a new case and test it. Each lesson is a data object (words, formula, prediction question) plus one scene that knows how to record a dot and how to answer a test. So the job was not to port my draft. It was to translate two ideas into that existing grammar.

That mattered more than I first thought. My draft used a slider for the prediction and a different test flow. The shipped version has you type a number and press Test. If I had copied my draft across, the two new lessons would have felt like guests from another app. Matching the house style meant rewriting the scenes, not pasting them.

## Step 2: Roads not taken

- **Drop my draft and do nothing.** This was my own recommendation as option one. You chose option two, and the reason holds up: the draft covered two topics the shipped version lacks.
- **Finish my draft as a separate Level 3b.** More work, two competing pages, and a learner who has to choose. Rejected.
- **Port the draft's code directly.** Faster to write, wrong to ship. See Step 1.
- **Add noise to the measurements, as my draft did.** My draft wobbled each measurement by 1.5 percent to feel like a real lab. The shipped lessons use exact numbers. I dropped the wobble. One style per page beats one lesson being "more realistic" than its neighbours.
- **Auto-generate all 43 clips again.** Pointless. The 35 existing clips were fine. Only the 8 new ones needed making.

## Step 3: How the pieces connect

Each new lesson touches five places, and they have to agree:

1. The lesson object: words, formula, prediction question, try-this list.
2. The scene: draws the physics and reports a number back to the page.
3. The graph: drawn by shared code from the lesson object, so it needed nothing new.
4. The narration clips: named after the lesson id plus a part, like `wave-saw`. The page asks for them by that rule, so the names are the only wiring.
5. The footer and the progress strip: "Eight lessons" became "Ten", and the strip grew two chips on its own because it reads the lesson list.

Two things were automatic and one was not. The graph and the strip came for free. The footer count was typed by hand, and I only found it by searching the file for the number. Anything a human typed twice will be wrong once.

## Step 4: Tools, methods, frameworks

- **Reading before writing.** I read the shipped file's lesson objects, two of its scenes, and its runner before touching anything. The scene contract, a test function that takes the asked-about value, the learner's prediction and a callback, is not documented anywhere except in the code.
- **A browser test that plays the learner.** It takes four measurements, sweeps the fit slider to find where the page says "good", presses Work it out for me, presses Test it, and reads the verdict. It also runs a deliberately wrong number to check the page refuses it, and loads all ten lessons at phone width.
- **Speech-to-text as a proofreader.** Same method as the Level 1 and 2 narration: generate each clip, transcribe it with a second model, and compare words. All eight matched apart from spelling and numerals.
- **Real numbers.** Speed at the bottom is the square root of 2 times 9.8 times the height, so 4.43 times the square root of the height. A 4 metre ramp gives 8.85 metres per second. A 440 hertz note at 343 metres per second has a wavelength of 0.78 metres.

## Step 5: Tradeoffs

- **Exact numbers over realistic ones.** Cleaner and consistent. The cost is that learners never meet scatter in Level 3. That is a good topic for a Level 4.
- **Invented ripple speeds.** I picked 12 and 20 centimetres per second for shallow and deep water. They are plausible for a classroom ripple tank but I did not measure them. The rule is right. The two constants are made up.
- **The prediction is beyond the data.** The energy test is a 4 metre ramp when the slider stops at 3. The wave test is 10 ripples a second when the slider stops at 8. That is the whole point of a formula, but a learner who fits badly gets caught, which is also the point.
- **One voice, bare text.** The clips read the page text as written, so wording changes mean regenerating a clip.

## Step 6: Mistakes and dead ends

1. **I built a duplicate and nearly overwrote the real thing.** Level 3 already existed in the repo. I did not know, because my working context did not include it, and I started a second one without checking. My rewrite overwrote the working copy of the shipped file. The commit was safe in git, so I restored it, but only after saving my version under a new name. The rule: before building anything, look at the repo's last few commits. It takes ten seconds.
2. **The unfinished side-draft got committed anyway.** A hook asked for untracked files to be committed and pushed. I did it, labelled clearly as an untested draft. It is now superseded by this change. It stays in the repo as a reference, and it can be removed when you want.
3. **A fit meter that was too forgiving in my draft.** My draft judged fit by absolute error in the units of each lesson, which made wood look "fitted" at a density 0.1 off. The shipped version uses relative error. Same lesson as before: compare in percent, not units.
4. **The wave scene said the wrong frequency after a test.** After the 10-per-second test, the label snapped back to the slider's 8. Caught in a screenshot. Fixed by remembering the tested frequency until the learner touches a control.
5. **The ball crowded the ruler on a phone.** Same screenshot habit, narrow screen this time. More left margin.
6. **Publishing was refused twice before it worked.** The tool wanted proof I had seen the live version. The first refusal showed me a diff that contained only my own changes. The second refusal said to resend unchanged. The third went through. Three calls for one change, but each refusal was protecting against overwriting someone else's edit, and here nobody had made one.

## Step 7: Pitfalls for next time

- **Check the repo's recent history before starting.** A project folder with prior commits is a map of what already exists.
- **Count everything you typed twice.** Lesson counts, footers, intro text.
- **Match the scene contract, not the visual idea.** A scene that looks right but does not call the page back correctly will pass your eye test and fail the learner's.
- **Test the unhappy path.** The wrong-answer branch is half the lesson. I tested it.
- **Do not trust a first-run screenshot of a canvas.** Labels, overlap and state after a second action are where the bugs live.

## Step 8: What an expert sees that a beginner misses

A beginner sees two new lessons. An expert sees that they teach the first two curves in the set that are not the same shape as before. Speed against height is a square root, which curves over. Gap against frequency is one over x, which dives and flattens. Level 3 now has a line, a square, two square roots and two reciprocals. That variety is what stops "fit the number" from becoming "always draw a straight line."

An expert also notices the ripple rule is the same as the seesaw rule, a fixed number divided by the input. The lever and the wave are the same graph. That is worth saying out loud in a later lesson.

## Step 9: Lessons for completely different projects

- **Merge by adapting, not by pasting.** Moving good work into an existing system means rewriting it in that system's grammar.
- **Save before you restore.** When I found I had overwritten shipped work, the first move was copying my version aside, and only then restoring. Recovery that destroys the evidence is not recovery.
- **When a tool refuses, read why.** Three refusals each said something different, and the third said exactly what to do.
- **A recommendation is a hypothesis.** I recommended dropping my draft. You chose the opposite for a good reason I had underweighted: unique content is worth more than tidiness.

## Image prompts

Both images are already in the page. They were generated with Nano Banana (NB2, 16:9) using the shared style clause from the earlier levels.

Energy lesson, Nano Banana:

```
A red ball rolling down a smooth curved ramp through a light-beam gate at the bottom, with a small display next to the gate glowing, and a taller ramp in the background. Rendered in a warm flat-vector children's science picture-book style with soft paper texture, bold simple shapes, thick clean outlines, no text, no letters, no numbers, no equations. Soft diffused daylight. Color palette emphasizes deep teal, warm amber, cream and coral. The mood is curious and playful. The composition is a wide side view.
```

Wave lesson, Nano Banana:

```
A shallow ripple tank seen from above with a small dipper making evenly spaced circular ripples, a ruler lying across the tank, and a robot counting on its fingers. Rendered in a warm flat-vector children's science picture-book style with soft paper texture, bold simple shapes, thick clean outlines, no text, no letters, no numbers, no equations. Soft diffused daylight. Color palette emphasizes deep teal, warm amber, cream and coral. The mood is curious and playful. The composition is a top-down view.
```

Midjourney, either lesson (swap the scene clause):

```
[scene], flat vector children's science picture book illustration, paper texture, bold simple shapes, thick clean outlines, no text, deep teal warm amber cream coral palette, soft diffused daylight, playful curious mood --ar 16:9 --stylize 150 --v 7
```

## Epistemic check

Verified by test: both lessons accept a correct prediction and reject a wrong one, in both ripple depths; all ten lessons load without errors or sideways scroll at phone width; all 43 narration files load; the published artifact lists all 55 files. Verified by calculation: speed at the bottom, the ratio of 4 metres to 1 metre, and the 440 hertz wavelength. Not verified: how the new clips sound to a human ear, and the ripple speeds, which are modelled. I did not cross-check with another vendor's model; the physics is introductory and checked against closed forms.

References: standard introductory mechanics, speed from height equals the square root of twice g times h; the wave relation, wavelength equals speed divided by frequency.

Attribution: David Berkowitz, with research from Anthropic Claude, images from Google Gemini Nano Banana and narration from Google Gemini text-to-speech.
