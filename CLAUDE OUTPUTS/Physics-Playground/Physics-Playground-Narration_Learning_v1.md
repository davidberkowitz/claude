# Learning: giving the playground a voice

Over coffee, here is what happened and why.

## Step 1: The approach, and why

"Add voice narration" sounds like one feature. It is really three decisions: what gets read, who reads it, and when it plays.

**What gets read.** Everything a non-reader would otherwise miss: the lesson title and big idea, the try-this list, the what-you-saw explanation, the quiz question with its three answers, and the feedback after answering. That is five clips per lesson, plus a welcome and a "not quite" for each level. Ninety-nine clips, about 23 minutes of audio.

**Who reads it.** A recorded voice, generated once with Google Gemini's text-to-speech and shipped with the page as small MP3 files. Not the phone's built-in robot voice, which varies wildly by device.

**When it plays.** Two ways. Every section has a Listen button for people who want one thing read. And there is a "Read to me" switch for a child who cannot read yet: with it on, opening a lesson reads the title, the idea and the things to try, and tapping a quiz answer speaks the feedback.

My starting point was the audience. Level 1 was pitched at "lowest level," which includes kids who cannot read the try-this list. For them the narration is not an accessibility extra. It is the only way in.

## Step 2: Roads not taken

- **The browser's built-in speech.** Zero files, zero cost, works offline. Rejected as the main voice because quality is a lottery: lovely on one phone, a 1990s robot on another, and silent in some embedded views. I kept it as the fallback: if a recorded clip fails to load, the page speaks the text with the device voice instead of going quiet.
- **ElevenLabs.** You have it connected and its voices are arguably the best available. I did not use it because it spends your credits per generation and returns two takes per clip by default, so 99 clips is roughly 200 paid generations I had not been asked to buy. Gemini was already wired in for the images. If you want a more characterful voice, this is the upgrade path, and the clip list is ready to feed to it.
- **One long audio file per lesson.** Simpler to produce. Rejected because a learner wants "read me that bit," and seeking around inside a two-minute file is fiddly on a phone.
- **Auto-reading everything, including the explanation.** Rejected on teaching grounds. "What you saw" is a spoiler if it plays before the child has poked the sim. So Read-to-me reads the setup and stops. The explanation waits for a tap.
- **Narrating the live captions.** The sims describe themselves as they run ("Balanced. Everyone is pulling, nobody moves"). Those sentences are assembled on the fly from many pieces, so they cannot be pre-recorded as single clips. Left unvoiced. This is the biggest gap for a true non-reader.

## Step 3: How the pieces connect

There is a chain with four links, and each one feeds the next.

1. **The page is the script.** I did not retype any narration text. A script opened both pages in a headless browser and pulled every title, list and explanation straight out of the running lessons. So the voice cannot drift from the words on screen.
2. **A manifest maps each clip to its words.** One file name per piece of text, like `gravity-saw.mp3`. Units were spelled out for speech at this stage ("4 m" became "4 metres").
3. **Generate, then check.** Each clip was generated, converted to MP3, and then sent back to a different Gemini model to be transcribed. The transcript was compared word by word with the intended text.
4. **The page asks for clips by the same names.** The Listen button for gravity's explanation asks for `gravity-saw.mp3`. Same naming rule on both sides, so nothing needs a lookup table.

The player itself is small: one clip at a time, tap again to stop, starting a new clip stops the old one, and a short queue so Read-to-me can chain two clips.

## Step 4: Tools, methods, frameworks

- **Gemini text-to-speech** for the voice, one consistent voice across both levels.
- **ffmpeg** to convert and level the audio. Every clip was normalised to the same loudness, so a quiet sentence and a loud one do not make a kid grab the volume.
- **Speech-to-text as a test.** This is the method worth remembering. I cannot listen to audio. But I can have a second model listen and write down what it heard, then diff that against the script. It turns "does the audio say the right thing" from an unanswerable question into a checkable one.
- **Playwright** to test the behaviour: play, stop, switch, chain, speak quiz feedback, carry the setting across lessons, and confirm all 99 files load and have real length.
- **Mayer's modality principle** shaped the design: people learn better from pictures plus spoken words than pictures plus printed words, because eyes and ears carry separate loads (Mayer, *Multimedia Learning*, 2009). The flip side, his redundancy principle, says identical text and narration together can hurt fluent readers. That is why narration is opt-in per section and not forced on.

## Step 5: Tradeoffs

- **Recorded over live.** Consistent quality on every device. The cost: 8 MB of audio in the repo, and any wording change to a lesson now means regenerating that clip, or the voice and the text disagree.
- **A synthetic voice over a human one.** Done in minutes for nothing. Less warmth and less character than a person reading to a child, and no control over emphasis.
- **Plain delivery.** The voice reads in its default manner. I could not give it a style direction, for the reason in Step 6.
- **Opt-in over always-on.** Respects readers and public settings. A non-reading child needs someone to flip the switch once. It stays on after that.

## Step 6: Mistakes and dead ends

1. **The narrator read its own stage directions.** My first prompt was "Read this aloud in a warm, friendly voice, like a teacher: ..." followed by the lesson text. The test clip came back nearly three times too long. I transcribed it, and the voice had cheerfully read the instruction out loud, then the lesson. A shorter "Say warmly:" prefix did the same. Sending only the bare text fixed it. If I had not checked the length and the transcript of one clip before making 99, every clip would have opened with a paragraph of directions.
2. **I misread the audio format.** I assumed the service returned raw sound samples and told the converter so. It actually returned a complete WAV file. The result still played, which is what made it dangerous. Reading the format label the service sent back, instead of assuming, sorted it out.
3. **False alarms from spelling.** Two clips "failed" the transcript check. The voice was right; the transcriber had written "one meter" where the script said "1 metre," and "waterline" for "water line." I diffed the words on every lower-scoring clip to confirm all differences were spelling or numerals. A check is only as good as its idea of "the same."
4. **Where to put the switch.** I first planned the Read-to-me toggle in the sticky top bar. On a phone that bar is already full. It went under each lesson title instead, next to the first Listen button, where a parent will see it.

## Step 7: Pitfalls for next time

- **Test one before you make a hundred.** Batch generation multiplies whatever is wrong with the first item.
- **Browsers will not play sound until the person taps something.** Read-to-me cannot start itself on first page load. It starts on the tap that turns it on, and on each lesson tap after that. Design for it instead of fighting it.
- **Text-to-speech models read what you send.** Treat the input as the script, the whole script, and nothing but the script.
- **Units and symbols need spelling out.** "4 m" might be read as "four em" or "four metres." Decide it yourself.
- **Audio and text are now coupled.** Keep the clip list (the manifest in this folder) with the project, so a text edit has an obvious matching regeneration step.
- **Have a fallback that degrades gracefully.** A missing file should produce a lesser voice, not silence.

## Step 8: What an expert sees that a beginner misses

A beginner adds a Play button. An expert asks what the audio is *for* at each point and lets that decide the behaviour. Setup is read automatically because it is needed to start. The explanation is not, because hearing it early destroys the discovery. Quiz feedback is spoken only in Read-to-me mode, because a reader finds it redundant and a non-reader finds it essential.

The other thing an expert notices is the verification loop. Audio is the classic "looks fine in the code, broken in reality" medium. Building a way to check content you cannot perceive directly, by round-tripping it through transcription, is what separates "I generated 99 files" from "I know what 99 files say."

## Step 9: Lessons for completely different projects

- **Round-trip to verify.** Translate and translate back. Summarise and expand. Speak and transcribe. When you cannot inspect an output directly, convert it back to a form you can compare.
- **Make the source of truth do the work.** The page was the script. Wherever two things must agree, a price list and a website, a contract and its summary, generate one from the other instead of typing both.
- **Suspicious numbers are free tests.** A 17-word sentence taking 20 seconds was the whole clue. Know roughly what the answer should look like before you look at it.
- **Decide when not to help.** The most useful design choice here was something the narration does not do: read the answer before the child has played.

## Image prompts

No new images were needed for this change. If you want an illustration for a "now with narration" announcement:

Nano Banana (NB2):

```
A child wearing oversized headphones sits cross-legged on a rug, grinning at a small round robot that is reading aloud from an open picture book, with a red ball, a magnet and a spring floating out of the book's pages. Rendered in a warm flat-vector children's science picture-book style with soft paper texture, bold simple shapes and thick clean outlines, with soft diffused daylight. The composition is a medium eye-level view with the child on the left and the robot on the right. Color palette emphasizes deep teal, warm amber, cream and coral. The mood is cosy and curious.
```

Midjourney:

```
child in oversized headphones sitting cross-legged on a rug, small round robot reading aloud from an open picture book, red ball magnet and spring floating out of the pages, flat vector children's science picture book, paper texture, thick outlines, deep teal warm amber cream coral palette, soft daylight, cosy curious mood --ar 16:9 --stylize 150 --v 7
```

## Epistemic check

Verified by test: all 99 clips load and have real duration; play, stop, switching, chaining, quiz feedback and the saved setting behave as designed on both levels at phone width; every clip's transcript matches its script apart from spelling and numeral differences. Not verified: how the voice actually sounds. No one has listened to it. Tone, pacing and pronunciation of words like "inertia" should be spot-checked by ear. The transcription check used a second Gemini model, so it is a cross-check within one vendor, not an independent one.

References: Mayer, R. (2009) *Multimedia Learning*, 2nd ed., Cambridge University Press, modality and redundancy principles; Google, Gemini API speech generation documentation.

Attribution: David Berkowitz, with research from Anthropic Claude, images from Google Gemini Nano Banana and narration from Google Gemini text-to-speech.
