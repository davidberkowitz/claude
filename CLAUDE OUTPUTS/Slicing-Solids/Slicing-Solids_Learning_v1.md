# Learning: building "Slab Limit", a slicing-to-the-limit explorer

Coffee version of what happened and why.

## Step 1: The approach, and why

The prompt was eight words: "slicing a solid into thinner and thinner pieces, build an interactive environment to explore." The first decision was what the *object of study* is. It is not the 3D picture. It is the sentence "volume = limit of a sum of slab volumes," and the thing worth exploring is how the sum approaches the limit: how fast, from which side, and when it hits exactly.

So the page has one state (solid, cross-section shape, sampling rule, N) and three views of that same state: the rotating stack, the Riemann rectangles, and the error-versus-N chart. Everything is computed live from the same little model function, `stack()`, so the three views cannot disagree. That is the architecture in one sentence: one truth, three windows.

I started from the readout, not the 3D view. If you can't say what numbers a tool should print at N = 1, 8, 1024, you don't know what the tool is for.

## Step 2: Roads not taken

- **WebGL / Three.js for the 3D stack.** Prettier shading. Rejected because every slab is a convex prism, so its silhouette is just the convex hull of its two projected faces. A 30-line hull routine on a 2D canvas gives a rotating, exploding stack with no library and no load-time risk. Shaders would have cost a day and bought lighting I don't need.
- **Showing f(x) with rectangles under it.** This is the textbook picture, but it is wrong for this task. The slab volume is A(x)·Δx, not f(x)·Δx. Plotting A(x) = c·f(x)² makes each rectangle's area literally equal to a slab's volume, so the "area under the curve" sentence is exactly true.
- **Trapezoid or Simpson as "slab rules."** Faster convergence, but a trapezoid slab is a frustum, not a flat-sided prism. The page is about replacing slabs with prisms; keeping only rules that correspond to a physical prism (edge, midpoint, inscribed, circumscribed) keeps the picture honest.
- **Infinite-N "reveal" animation that morphs into the smooth solid.** Tempting and dishonest. The whole epistemic point is that no slab ever has zero thickness. The auto-refine button stops at 512 on purpose.
- **A torus or a vase with a non-single-valued profile.** Breaks the "one radius per x" model. Parked.

## Step 3: How the pieces connect

Controls set state. `stack()` turns state into an array of slab sizes plus a sum. The three canvases each read that array: the 3D view draws prisms from it, the 2D view draws rectangles from it, the convergence chart runs `stack()` for 20 values of N and 5 rules to draw its curves. The readout prints the sum, the closed-form exact value, and the gap. Hovering a rectangle sets one index and both the rectangle and the prism light up copper, which is the visual proof that they are the same object.

Order on the page: stack first (the thing you asked about), numbers beside it (the claim), rectangles and error chart below (the why and the how fast), prose last (what to try, where it misleads, references).

## Step 4: Tools, methods, frameworks

- **Closed-form exact volumes** for every solid (4/3, 1/3, 2, 1/2, 3/4, 0.535π) so "exact" means exact, not "a bigger Riemann sum." The bell curve is the one exception; its integral needs erf, so it is computed by Simpson's rule at 4000 intervals and labelled with its erf formula.
- **Cavalieri's principle** as the reason a cross-section dropdown is cheap: changing disk to square multiplies every volume by a constant. One dropdown, four solids per profile.
- **Painter's algorithm + convex hull** for the 3D view. Works because the slabs are convex and strung along one line, so sorting by depth is enough.
- **Node for verification before publishing.** I extracted the model into a test script and checked every solid against its closed form, plus the special cases I was about to claim in the prose. That caught a real error (next section).
- **Playwright screenshots** at desktop/light and phone/dark, one pass, to catch overflow and label collisions.

If I'd chosen a charting library for the two 2D plots, the log-log reference slopes and the "drop points below 1e-12" logic would have been fights with the library's axis model. Hand-drawn canvas was shorter.

## Step 5: Tradeoffs

- **Faceted silhouettes.** Circles are 40-gons. At N = 1024 nobody can tell; at N = 1 you can if you squint. I took that over smooth ellipse math that only works for disks.
- **Recomputing the convergence chart on every hover.** About 150k function evaluations per render. Simple code over a cache; still instant on a phone.
- **Five rules, not more.** Each rule is a physical prism. I sacrificed trapezoid's 1/N² for a cleaner story.
- **Short prose.** The user's preference is brevity, so the notes are bullets, and the deeper material lives in the references.

## Step 6: Mistakes and dead ends

- **I wrote "edge rules fall like 1/N" and it was false for the default solid.** The sphere is symmetric, so the left-edge sum equals the right-edge sum, equals their average, which is the trapezoid rule, which is 1/N². The test script showed left and midpoint errors both quartering as N doubled. The fix was to make the claim specific (cone, horn: 1/N) and turn the exception into a "things to try" bullet. The mess became content.
- **My own test was wrong once.** I compared the vase against π·0.535 instead of π·(0.535π) and saw a constant error of 3.6 and briefly believed the model was broken. Always check the test before you check the code.
- **The vase surprised me.** For N ≥ 3 every rule is exact to machine precision, because A(x) is a trig polynomial over a full period and equally spaced samples integrate those exactly once N exceeds the top frequency. The convergence chart was silently dropping those points; now it says so on the chart.
- **Label collision.** The "1/N²" reference label landed on the "1024" tick. Moved reference labels to the middle of their lines.

## Step 7: Pitfalls to watch for

- Decide what "exact" means before writing a single pixel. If the reference value is itself an approximation, every error you print is a lie of unknown size.
- Symmetric test cases hide first-order errors. Test convergence rates on something lopsided (a cone) before stating a rate.
- A hover that triggers a full recompute is fine until it isn't. Measure before caching, but know where the cache would go.
- Do not let the picture promise more than the math. Pulling slabs apart is a visual aid only, and the page says so.

## Step 8: What an expert notices

- The paraboloid is exact under the midpoint rule at every N because A(x) is linear. A beginner sees a coincidence; an expert sees the midpoint rule's error term, which is proportional to A″.
- The 1/N² rate for the sphere needs A to be smooth, not f. f(x) = √(1−x²) has infinite slope at the ends, which would wreck a surface-area computation, but A = π(1−x²) is a parabola. The page says this because it is the single most common confusion in this chapter.
- Volume converges under slicing; surface area does not. The staircase never flattens. That is why arc length and surface area need frustums, and why Gabriel's horn can have finite volume and infinite area.

## Step 9: Lessons for other projects

- **One model, many views.** Whenever two displays can disagree, they eventually will. Derive both from one function.
- **Turn the exception into the lesson.** The sphere's "wrong" convergence rate became the best bullet on the page. When a test contradicts your prose, the prose is usually what needs to change.
- **Verify the claim, not the code.** I didn't test that the hull routine works; I tested that the cylinder is exact at N = 1 and that the sphere with square sections is 16/3. Test the sentences you are about to publish.
- **Cheap geometry beats heavy libraries when the shapes are convex.** Convex hull plus painter's order is a trick that generalizes to a lot of "stack of simple things" visualizations.

## Triangulation

Gemini and ChatGPT were queried through their APIs to cross-check the five closed-form volumes and the convergence orders. See the chat recap for whether those calls succeeded; the numeric checks above were done locally in Node regardless.

## Image prompts

Markers for where each image would go in the page are listed in the chat recap along with the Midjourney and Nano Banana prompts.
