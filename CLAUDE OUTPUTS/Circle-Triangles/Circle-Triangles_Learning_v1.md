# Learning: building "Triangle Limit", the circle-by-triangles explorer

Coffee version, shorter than the Slab Limit debrief because most of the scaffolding was reused.

## Step 1: The approach, and why

The ask was "a similar app for filling in a circle with triangles." The word that mattered was *similar*. Slab Limit's whole value is the one-model, three-views structure, so I kept it: one `geom(N)` function returns every number, and the fan, the unrolled strip, the readout and the error chart all read from it.

The one design decision that was new: which second view earns its place. For slabs it was the Riemann rectangles. For triangles it is the unrolled strip, the "pizza slice" rearrangement where N triangles alternate up and down to form a parallelogram that straightens into a πr by r rectangle. That picture is the proof; the fan is just the setup.

## Step 2: Roads not taken

- **A 3D view.** Tempting for family resemblance, but the problem is flat. A 3D fan would be decoration.
- **Polygons by perimeter instead of area.** Archimedes bounded π with perimeters. Area is the better match for the slicing page (sum of pieces → limit), and area is what the strip picture proves. The perimeter story is noted in the "things to try" bullet, with the correction that the inscribed area sits below his lower bound.
- **Letting the user set the radius.** It only rescales every number by r². Fixing r = 1 makes the π estimate fall straight out of the area.
- **Generic "any polygon" or triangles from an off-center point.** Breaks the shared-height argument that makes the total equal ½ · perimeter · h. Not worth it.

## Step 3: How the pieces connect

Controls set N, mode, spread. `geom(N)` gives base and height for inscribed and circumscribed triangles, their totals, and the blend. The fan draws N triangles from those; the strip draws the same N triangles in a row, alternating orientation; the readout prints the totals and colors the π digits that match; the chart plots the three error series. Hovering a triangle in either picture highlights it in both, which is the visual claim that the two pictures contain the same objects.

## Step 4: Tools, methods, frameworks

- **Archimedes, Measurement of a Circle, Prop. 1** supplies the equation the page is built around: area = ½ · circumference · r.
- **Taylor series of sin and tan** give the error rates: inscribed π − 2π³/(3N²), circumscribed π + π³/(3N²). The ratio of errors is exactly ½ in the limit, which the Node check confirmed (0.521, 0.505, 0.501, 0.500 at N = 12, 24, 48, 96).
- **Richardson extrapolation** gives the blend (1 in + 2 out) ÷ 3 that cancels the 1/N² term. Checked: error 4.8e−7 at N = 96, so six correct decimals.
- **Playwright** for one desktop light and one phone dark render.

## Step 5: Tradeoffs

- **Strip packing for large N.** A single row of 1024 triangles is unreadable, so above 48 the strip wraps into rows and gives up the dashed πr × r target rectangle. The rectangle is the point of the view, so this is a real cost, paid only where the picture would be unreadable anyway.
- **Both-mode hover.** In "both" mode hovering picks the inscribed triangle only. Picking both would need two highlights and more explanation than it is worth.
- **Fixed r = 1.** Loses the "areas scale with r²" lesson, gains a direct π readout.

## Step 6: Mistakes and dead ends

- **I wrote "about seven decimals" for the blend at N = 96.** The check gave six. Fixed before publishing. Same lesson as last time: test the sentence, not the code.
- **I was about to say Archimedes' bounds match the page's totals.** They match only on the circumscribed side, because he used perimeters and circumscribed area equals half the circumscribed perimeter. The inscribed area is lower than his lower bound. The bullet now says so.
- **The strip canvas was square and two-thirds empty**, and its dimension label sat on the dashed rectangle. Changed the aspect ratio, centered the strip vertically, and moved the label below the taller of the triangle and the rectangle.

## Step 7: Pitfalls to watch for

- Area and perimeter polygons are different approximations with different constants. Do not mix a perimeter bound with an area total in one sentence.
- Alternating-orientation packing needs an offset of half a base per triangle, not a full base. Off by that factor and the strip is twice too long.
- Hit-testing a fan by angle is easy; hit-testing a circumscribed fan needs the half-step phase shift, or hover lands on the neighbor.

## Step 8: What an expert notices

- The circumscribed error is always half the inscribed error, so the simple average of the two is still first order in 1/N². Only the 1:2 weighting cancels. A beginner averages; an expert matches coefficients.
- Here the perimeter converges and in Slab Limit the surface area did not. The difference is whether the pieces' *directions* converge, not just their positions. That is the single most transferable idea in the pair of pages.
- Using the computer's `sin` to estimate π is circular. Archimedes avoided it by iterating square roots from the hexagon. The page says so rather than pretending.

## Step 9: Lessons for other projects

- **Reuse the structure, not the surface.** The second page shares tokens, type and layout with the first, but every view was re-chosen for the new subject.
- **Find the picture that is also the proof.** The unrolled strip does more than the formula does.
- **When a historical claim sounds too neat, check the quantity.** "Matches Archimedes" was almost right, which is the most dangerous kind of wrong.
