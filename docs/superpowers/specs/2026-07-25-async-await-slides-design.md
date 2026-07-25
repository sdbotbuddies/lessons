# Async/Await Explainer Slides — Design

## Purpose

Lesson 11 (`lesson11-spike-prime-python.html`) uses `async`/`await` in every code
example, but never explains *why* those keywords exist. Kids are new to the
concept. This adds a short, visual, kid-friendly detour that builds intuition
before the existing code-heavy `runloop` slide (`id="s7"`).

## Placement

Three new slides, inserted immediately before `id="s7"` (after the current
`id="s6b"` — Setup: Program Slots). `s7` itself is unchanged; it already
covers the `runloop`/`await` code pattern and now serves as the payoff after
the new slides build the intuition.

## Analogy

Making breakfast: microwaving oatmeal + toasting bread.

- **Sync (blocking):** stand and stare at the microwave until it dings, only
  then start the toaster. Nothing else happens while waiting.
- **Async (non-blocking within one wait):** start the microwave, start the
  toaster, set the table while both run, come back and check on each when
  it's ready.

## Slides

### Slide A — "The Slow Way (Sync)"
- New `slide-label`: "Async vs. Sync — Part 1"
- Cartoon: kid character stares at a spinning/glowing microwave, arms
  crossed, bored/impatient expression (droopy eyes, single motion-line
  "sigh"). Toaster sits cold and untouched off to the side (grayed out,
  no motion). A wall clock ticks forward exaggeratedly. No table-setting
  happens until the microwave dings.
- Copy: plain language — the computer does ONE thing, waits until it's
  *totally* finished, then moves to the next thing. Nothing else happens
  in between.
- Visual register: playful/exaggerated — googly eyes, blush cheeks, bold
  outlines, warm-toned palette consistent with the rest of the deck but
  bouncier motion than the existing `wf-scene` animation. Built in pure
  CSS/SVG (no external images/libraries), own keyframe set (not reusing
  `wf-*` classes, since this needs a more expressive/cartoony feel).

### Slide B — "The Smart Way (Async)"
- `slide-label`: "Async vs. Sync — Part 2"
- Cartoon: same kid starts the microwave (spins, glows) AND the toaster
  (heating glow) at the same time, then hops/bounces off to set the table.
  Both appliances animate independently and finish on their own timeline:
  microwave dings with a little burst/sparkle + "DING!" pop-text, toaster
  pops with toast flying up + "POP!" pop-text. Kid ends with a proud grin,
  arms out, breakfast ready — clearly faster than Slide A's timeline.
- Copy: you start a task, and *while it's working* you go do something
  else — you just come back and check on it when it's done.

### Slide C — "Connecting It to Your Code"
- `slide-label`: "From Breakfast to Python"
- Two-column layout:
  - Left: breakfast steps as a simple numbered list (start microwave →
    start toaster → set table → check microwave → check toaster), styled
    like the existing `checklist`/`check-row` pattern.
  - Right: matching SPIKE code snippet (`async def main():` /
    `await motor.run(...)` / `await sound.beep(...)`) styled with the
    existing `.code-block` component, with simple connective arrows/labels
    tying specific breakfast steps to specific code lines.
- Two callout boxes (styled like the existing yellow "🔑 remember" callout
  on `s7`):
  - **`async def main():`** — this label goes on the recipe card itself;
    it tells the hub "this set of steps has waiting parts, get ready to
    juggle." Without it, `await` can't be used inside at all.
  - **`await` (used when calling)** — this goes on the *specific* step
    where pausing is OK: "wait right here until the microwave dings — but
    I don't need to wait like that for setting the table."
- Small note: `await` only ever appears inside an `async def` function —
  they're a package deal.

## Animation Technique

Pure CSS (`@keyframes`) with inline SVG/HTML shapes for the characters and
appliances — same technology as the existing `wf-scene` animated workflow
slide, but a distinct, more expressive/playful visual style: bouncier
easing, exaggerated character expressions (googly eyes, blush, motion
lines), onomatopoeia pop-text ("DING!", "POP!"), and small celebratory
details (steam wisps, flying toast, sparkle bursts) to make it visually fun
for kids. No JS libraries, no external image assets — self-contained in the
existing single-file HTML lesson, consistent with the rest of the deck.

## Non-goals

- No changes to `s7` or any other existing slide content.
- No interactivity beyond the existing slide nav (no click-to-play, no
  sound).
- No new external dependencies (fonts, JS libraries, images).

## Testing / Verification

- Open the lesson in a browser, click through all slides including the 3
  new ones, confirm animations loop smoothly and slide counter updates
  correctly (deck grows from 18 → 21 slides).
- Visual check only (no automated tests for this static HTML deck).
