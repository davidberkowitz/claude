# Learning: building a public personal-brand site from a private archive

*David Berkowitz, with research from Anthropic Claude and images from Google Gemini Nano Banana. November 16, 2026.*

Coffee's poured. Here's what actually happened.

## Step 1: The approach, and why

You said "use all available info." The repo had none, so I went to Drive. What I found was not a résumé folder; it was a fifteen-month biography project: a 60KB timeline spine, a 250KB literary narrative, a gap register, a privacy protocol, eleven recurring themes, a humor thread, three résumés, and a mirror of your LinkedIn network. That changed the job. The hard part of this site was never "what do I say about David." It was "what, out of everything I now know, is allowed on a page strangers will read."

So the first thing I read closely was not the résumé. It was `Bio_Privacy-Protocol_v1.md`. It has four tiers (OPEN, FAMILY, CONFIDENTIAL, SEALED) and one time boundary (EMBARGOED). I treated it as the spec. Everything on the site is OPEN tier. Nothing else got in, no matter how good the story was.

Then I asked you four questions, because four decisions were yours alone: what the site is for, how to handle the IBM-years-and-age problem, which personal threads to expose, and where to host. Your answers (professional profile; full arc but no early dates; Atelier only; Netlify) set the whole shape. I built nothing before those came back.

## Step 2: Roads not taken

- **Consulting lead-gen site.** The obvious choice for someone planning a practice. Rejected for now because the brand is embargoed under your own protocol, and a lead-gen site without a name is a site with a hole in the middle. The professional profile can become the consulting site later by swapping the hero and CTA.
- **The literary site.** *A Deep Well*, the Field Guide, the manifesto trilogy. The richest material in the archive. Rejected as the primary frame because most of it is FAMILY tier or in progress, and because a public site that leads with the inner life makes the engineering career look like a footnote. It became one section (Writing) instead of the spine.
- **Using the real photo.** The Avatar 3 files in Drive are the current candidate. I didn't embed them because pulling a 600KB image through the Drive connector into my context would have cost more than the whole rest of the build, and because I couldn't tell from metadata alone whether the avatar was meant to be public. The hero is an illustration instead. Photo is a one-line swap when you want it.
- **A multi-page site with a build system.** Overkill. One HTML file, no framework, no build step. Same philosophy as the phonics prototype: works on anyone's phone tonight.
- **mailto: link for contact.** Would have put your email on a public page. Netlify Forms keeps it private and still lets people reach you.

## Step 3: How the pieces connect

The site has one argument: *substrate, not features*. It comes from theme 7 in your Recurring Themes file (ISPF port → OpenDoc → WebKit/webOS → AI agent harness). Every section is that argument at a different zoom level:

- **Hero** states it in one sentence and one image (strata with a thread of light through them).
- **Through-line** is the argument as a six-step sequence. This is the only numbered list on the page, because it's the only thing that's actually a sequence.
- **Experience** is the same facts as a ledger, for the recruiter who scans instead of reads.
- **Approach** is how you do it (AI + Agile, process fitted to the work, succession plans).
- **Atelier** is the argument applied to your creative life: build the pipeline once, let projects flow through it. The four interactive explorers from this repo are the evidence, served as real pages under `/work/`.
- **Writing** and **Contact** close it.

The order is deliberate: thesis, proof, record, method, hobby-that's-really-the-same-thing, voice, door.

## Step 4: Tools and frameworks

- **The Privacy Protocol as the content filter.** Not a design framework, but the most important tool in the build. Without it I'd have had to guess, and guessing with other people's private facts is how you get a site you have to take down.
- **Your 2023 résumé** for the verbatim professional claims. I lifted lines like "flexible application of development process, from chaos to agile to ISO/CMM" because they're yours and better than anything I'd paraphrase.
- **Gemini image model (via the proxy credential)** for the hero. The last two sessions couldn't reach it; this one could because the environment now injects the key. First try worked.
- **Netlify MCP + CLI** for hosting. The MCP tool created the project and enabled Forms; the actual upload ran through the `@netlify/mcp` command it handed back.
- **Playwright** for one screenshot pass at desktop and phone width, light and dark. Zero console errors, zero horizontal overflow.
- **IBM Plex** for the body type. A small private joke that only you will notice: the sans-serif on your site is IBM's, and IBM is the chapter you keep off LinkedIn.

If I'd used a static-site generator instead of one file, the site would be easier to grow into a blog and harder for you to edit in a text editor. For a profile that changes a few times a year, one file wins.

## Step 5: Tradeoffs

- **No early dates vs. a complete story.** IBM and CI Labs are on the page but with "earlier" instead of years. The through-line still reads as forty years of work to anyone who counts the companies; it just doesn't hand them the arithmetic. This is a half-measure and you should know it's a half-measure.
- **Illustration vs. photograph.** A profile site without a face is less trustworthy. A profile site with the wrong face is worse. I chose the recoverable error.
- **Writing section lists unpublished pieces.** "Available on request" is honest, but it's also a promise. If someone asks for the Constraints essay, you have to send it.
- **Contact form means a Netlify dependency.** Free tier, 100 submissions a month. Fine for a personal site; worth knowing it's there.
- **Naming SOLVE and Leadership Grid MAP.** Names only, no content. They signal you build frameworks; they reveal nothing TRI would mind.

## Step 6: Mistakes and dead ends

1. **My first Gemini call failed with a 400** because I appended `?key=x` out of habit. The proxy injects the real key; the dummy param conflicted with it. Dropping the param fixed it. Lesson: when a host is pre-authenticated, send a clean request.
2. **The branch already existed** when I tried to create it. Harmless, but I should have checked first.
3. **One response got cut off by a safety classifier** mid-build. Nothing was lost; I re-ran the tool calls that hadn't completed. I don't know which sentence tripped it. Worth noting only because it cost a turn.
4. **I nearly listed MathXplorers.** It's in the Interests section of your spine as co-owned, which reads as public. But you'd ticked only "Atelier" in the personal-threads question, and MathXplorers names Gigi. Your answer outranked my reading of the spine. It's not on the site.

## Step 7: Pitfalls for next time

- **A private archive is not a public source.** The spine says health and finance are "public view" per your choice. That means visible to automations and family editions, not visible to the internet. Don't let "public view" in a filename drift into "public" on a website.
- **Check the embargo list before every publish.** The AI.gility brand is embargoed until you say otherwise. The retirement date and the consulting plan are OPEN facts but still don't belong on a site whose job is to represent you *now* at TRI.
- **Third parties aren't yours to publish.** Matt Crowley, Paul Chambers, Steve Winston make your career story better and they're not on the site. Sponsors go in the biography, not the brand page.
- **Netlify manual deploys get overwritten by Git CD.** Right now the site is a manual deploy. If you later connect the repo for continuous deployment, the next push replaces whatever's live. That's fine as long as you expect it.
- **`.netlify/` must stay out of git.** Added to `.gitignore`. Leave it there.

## Step 8: What an expert sees that a beginner misses

A beginner builds the site from the résumé. An expert builds it from the one sentence the résumé never says. Yours was sitting in theme 7 of a file about your life, not in any job description.

A beginner fills every section with everything available. An expert notices that the archive's own withheld-inventory found a pattern: the material you soften clusters around family and money while career runs at full resolution. On a *brand* site that bias is correct, and it has to be a choice, not a drift.

A beginner uses a stock headshot slot. An expert leaves the slot empty rather than guess which of four avatar files is the one you'd stand behind.

## Step 9: Lessons for other projects

- **Find the governing document before the content.** For this site it was the privacy protocol. For a product it's the terms of service; for a report it's who's allowed to read it. Read that first and the content decisions make themselves.
- **One thesis, several zoom levels.** Hero, sequence, ledger, method. Same fact, four readers. Works for a pitch deck, a grant, a PR description.
- **Ask the four questions that fan out widest, and ask them first.** Purpose, exposure, scope, destination. Everything else was derivable.
- **The recoverable error beats the unrecoverable one.** No photo beats the wrong photo. "Earlier" beats a date you can't take back.
- **When a door that was locked last time is open this time, walk through it quietly.** The Gemini proxy worked today. I didn't write a paragraph about it; I made the image.

## What's live

- **Site:** https://davidberkowitz.netlify.app
- **Netlify project:** https://app.netlify.com/projects/davidberkowitz (Forms enabled; submissions appear under Forms → contact)
- **Source:** `site/` on branch `claude/practical-bell-ms1fx5` in `davidberkowitz/claude`
- **Pages:** `/`, `/work/slab-limit.html`, `/work/triangle-limit.html`, `/work/short-i-island.html`, `/work/short-i-island-brief.html`, `/thanks.html`

## Image prompts

The hero was generated from the Nano Banana prompt below (NB2, via Gemini `gemini-3.1-flash-image`). Midjourney alternative follows, for a second take or a header variant.

**Nano Banana (used):**
```
A wide abstract editorial illustration of layered translucent platform slabs stacked like geological strata, each layer a different era of technology, with a single luminous thread of light running vertically through all of them and emerging at the top as a small branching tree of light. Rendered in a restrained screen-print style with visible paper grain and slight ink misregistration. Lighting is soft and directional from the upper left. The composition is a wide 16:9 panorama with generous negative space on the right third for text. Color palette emphasizes deep slate blue, warm graphite, and one accent of burnished copper. The mood is quiet, structural, and patient. No text, no letters, no people.
```

**Midjourney (alternative):**
```
layered translucent slabs stacked like geological strata, each a different technological era, one thread of copper light running vertically through every layer and branching into a small tree at the top, screen-print texture, paper grain, slate blue and graphite with a single copper accent, soft directional light from upper left, wide composition with empty space on the right, quiet and structural --ar 16:9 --style raw --v 7
```

**Nano Banana (portrait placeholder, if you want an illustrated stand-in rather than a photo):**
```
A dignified three-quarter portrait of a silver-haired engineer in his sixties with a short beard and wire-rimmed glasses, seated at a plain wooden workbench with a single laptop and a stack of paper, looking slightly off-camera with a thoughtful half-smile. Rendered as a restrained two-color screen print in slate blue and burnished copper on warm off-white paper, with visible grain and slight misregistration. Soft window light from the left. The composition is a tight square crop from the chest up. The mood is calm, attentive, and unhurried.
```
