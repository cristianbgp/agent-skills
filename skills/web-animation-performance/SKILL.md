---
name: web-animation-performance
description: Design performant web animations and diagnose stutter, delayed interactions, excessive rendering work, or memory pressure in existing motion. Use when implementing animation, gestures, or scroll effects, or profiling their performance. Applies to CSS, browser animation APIs, and JavaScript libraries without requiring a particular framework.
---

# Web animation performance

Preserve the intended interaction while reducing unnecessary browser work. A smooth recording on one desktop is evidence for that configuration, not a guarantee for every device.

For new motion, follow **Design and build**. For an existing performance problem, start with **Diagnose and improve**. Use the browser-work guide below in either case. This skill is self-contained and does not require an animation library.

## Design and build

1. Identify what the movement communicates and when it occurs. Consider repeated input, navigation, loading, scrolling, and reduced motion. Keep essential controls responsive throughout.
2. Inspect the project's existing components, animation tools, and motion tokens. Reuse them when suitable. Do not replace a working library merely to prefer another execution engine.
3. Choose the smallest implementation that preserves the behavior. CSS transitions suit simple state changes; CSS keyframes suit prescribed sequences; WAAPI suits browser-managed playback with programmatic control. Use a library when its gesture, layout, spring, or coordination features are needed.
4. Plan the work per frame: which properties change, what must be measured, what descendants are affected, and whether animation overlaps heavy main-thread work. Prefer compositor-friendly changes when they produce the intended result.
5. Implement interruption, reversal, cleanup, and a reduced-motion alternative with the interaction. Remove event listeners and cancel obsolete work when the owning surface is disposed.
6. Verify the interaction in realistic surrounding content. Profile when it involves continuous movement, large surfaces, measurements, or concurrent heavy work. For a small local transition, a focused visual and interaction check may be sufficient.

Do not animate just to demonstrate a technique. Avoid turning a small interaction into a new animation framework or a project-wide refactor.

## Diagnose and improve

1. Reproduce the symptom with the relevant content size, viewport, browser, and input. Establish whether the issue is dropped frames, delayed input, incorrect timing, visual discontinuity, or resource use. Ask only for missing information that changes the investigation.
2. Capture a representative baseline with the browser's performance tools when available. Look for long tasks, style recalculation, forced layout, paint, and costly layer composition. Use framework profiling if repeated component renders appear involved.
3. Map the evidence to a likely cause using the guide below. Source inspection can identify a risk; it cannot establish its runtime cost by itself.
4. Make a focused change tied to that cause. Preserve geometry, hit targets, document flow, focus behavior, and the product's visual intent.
5. Repeat the same interaction under comparable conditions. Compare rendering work and responsiveness, then check interruption and reduced motion. Stop when the requested behavior is correct and the observed bottleneck is resolved; do not keep optimizing unrelated code.

If browser access or representative hardware is unavailable, make a bounded code-level assessment, label the cause as a hypothesis, and state the measurement needed to confirm it. Do not invent timings, frame rates, or a successful device check.

## Browser-work guide

### Separate rendering cost from animation scheduling

Ask both what changes on screen and what drives those changes. Updating a cheap property through a JavaScript frame loop still depends on main-thread availability. CSS or WAAPI can let eligible animations proceed in the compositor, but acceleration depends on the browser, values, and implementation.

Do not infer acceleration solely from a library name or assume a library's shorthand properties use the same execution path across versions. Inspect the actual animation and profile the case that matters.

### Geometry and document flow

Prefer transform and opacity for visual movement and fading when appropriate. A transform changes appearance without reserving new layout space: replacing an expanding panel's height with scale may distort text, overlap content, or leave the wrong space behind.

When surrounding content must reflow, keep the required layout behavior. Consider isolating the affected region or measuring start/end geometry and animating an inversion when that preserves the interaction. Measurements and visual correction have costs too. Use containment only when its sizing, clipping, and positioning consequences fit the component.

### Measurements and style invalidation

Avoid repeatedly interleaving geometry reads and DOM writes across elements. Gather the required measurements before applying the associated updates where possible. A scheduled callback alone does not prevent forced layout after a preceding write.

Inspect effects, observers, gesture callbacks, and third-party components together: individually small read/write sequences can become expensive in aggregate.

Keep rapidly changing values close to their consumers. A custom property updated on an ancestor can expand style invalidation through inheritance. Distinguish per-frame animation state from ordinary theme tokens; do not remove useful CSS variables wholesale. Local variables, non-inheriting registered properties, or direct property updates are alternatives to evaluate, not automatic performance guarantees.

### Framework work

Avoid using component state as a per-frame position buffer when it causes unnecessary rendering. Use the existing animation system's mutable values or a narrowly owned DOM update when appropriate. Keep semantic state in the framework and prevent competing writers from fighting over the same property.

### Paint, layers, and memory

Judge effects by their affected area, complexity, and frequency. A local color transition and a full-screen effect have different costs. Large blur regions, duplicated ticker content, and many promoted layers deserve particular scrutiny.

Use will-change for an observed issue where the hint helps. Scope it to the relevant properties and elements, allow preparation time when possible, and release temporary hints after use. Do not promote every element or apply GPU tricks globally.

### Scrolling and visibility

For ordinary positioning during scroll, consider native sticky or fixed positioning before a JavaScript synchronization loop. For progress-linked effects, evaluate native scroll timelines against browser support and fallback needs.

Use visibility observation for entrance triggers or pausing off-screen decorative loops when useful. It is not a frame-accurate scroll-progress source. Preserve the user's scroll control and make essential content available without the effect.

### Perceived responsiveness

Check rapid reversal and repeated activation, not just one clean playback. Snapshot-based view transitions may suit navigation but need special care for interactions that must retarget continuously. Choose based on the required behavior rather than a blanket ranking of APIs.

## Verification and response

Match checks to the change. Exercise relevant states, content sizes, and input methods; include a representative mobile device when GPU, memory, touch, or browser-specific behavior is material. Desktop CPU throttling does not reproduce all of those limits.

Report briefly:

- What was built or the observed symptom and cause.
- The implementation choice or focused fix and why it fits.
- What was actually checked, including comparable before/after evidence when measured.
- Any remaining hypothesis, device limitation, or trade-off.

If asked only for a review, provide findings and suggested changes without editing the implementation. Do not claim a fixed frame rate or assign a performance grade from source inspection alone.

## Background

The decision model is informed by [The Web Animation Performance Tier List](https://motion.dev/magazine/web-animation-performance-tier-list), [browser animation guidance](https://web.dev/articles/animations-guide), and [layout measurement guidance](https://web.dev/articles/avoid-large-complex-layouts-and-layout-thrashing). These links provide background; all operating instructions are above. Check current official documentation when a decision depends on browser support or a library version.
