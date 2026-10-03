# Web UI preferences

## Tools

- Use Tailwind CSS for styling.
- Prefer shadcn/ui components built on Base UI when available and suitable.
- Use Radix-based components when the needed Base UI implementation is unavailable or does not meet the requirements.
- Check actual component support instead of assuming interchangeability.
- In existing projects, reuse the established component foundation. Do not migrate primitives solely to satisfy this preference.
- Add specialized libraries only when needed.
- Reuse the project's icon set and notification components. Do not add a second library for the same purpose without a concrete benefit.

## Accessibility and forms

- Use semantic elements: buttons for actions, links for navigation, and labeled controls for input. Do not recreate their behavior with clickable divs.
- Give icon-only controls an accessible name; hide decorative icons from assistive technology.
- Preserve visible keyboard focus. For modal dialogs, use the component primitive's focus management and restore focus to an appropriate element on close.
- Provide keyboard and ordinary tap/click alternatives to gesture interactions.
- Associate field errors with their inputs, preserve non-sensitive input on failure, and explain how to correct the error. Do not disable pasting into password or verification fields.
- Announce meaningful asynchronous status changes when useful, without moving focus or announcing every background refresh.

## Mobile browser behavior

- Choose viewport sizing for the surface: dynamic viewport units can suit an app shell, while small viewport units can keep a full-height section stable. Avoid fixed heights that clip content when browser chrome or the keyboard changes.
- Account for safe-area insets around edge-aligned controls. Keep focused inputs and primary actions reachable when the keyboard opens.
- Preserve browser zoom. Where small input text causes unwanted focus zoom, adjust the input typography rather than disabling zoom.
- Set appropriate input types, input modes, autocomplete, and enter-key hints for the field's purpose.
- Design for touch and mouse together. Gate hover-only enhancements by input capability; do not infer touch support from screen width.
- Scope touch-action, overscroll, and text-selection restrictions to the interaction that needs them. Preserve useful browser behavior elsewhere.
- Check affected layouts with long content and narrow viewports. Use a real device when keyboard, touch, or browser behavior is material; report when those checks remain unverified.

## Styling and component consistency

- Reuse existing semantic tokens for color, spacing, typography, radius, and motion. Add tokens for recurring needs rather than creating a parallel theme.
- Let parent layouts control spacing between siblings; prefer gap for flex/grid layouts when it fits.
- Use the existing class-merging and variant utilities when extending components. Introduce a typed variant API only when the component has meaningful variants.
- Preserve the project's Tailwind version and theme setup unless a migration is requested. Dark mode and the visual palette are product decisions.

## Motion

- Give motion a purpose such as feedback, orientation, or explaining a state change. Keep frequent interactions fast and avoid delaying input or navigation.
- Prefer CSS for simple transitions. Add a motion library when gestures, layout transitions, or coordinated exits justify it; reuse an existing solution first.
- Reuse motion tokens and name the properties being transitioned instead of using transition: all.
- Prefer transform and opacity when suitable. When layout or paint animation is necessary, check its performance rather than assuming it is inexpensive.
- Let rapidly repeated or reversed interactions continue from their current state. Anchor popover motion to its trigger and preserve coherent enter/exit paths.
- Include a reduced-motion alternative that preserves the information conveyed. Decorative movement should not be required to understand or operate the interface.
- Keep content available if animation or JavaScript fails. Avoid scroll hijacking or hiding essential content behind a reveal.

## Quality criteria

- Design mobile-first, then adapt deliberately to larger screens.
- Support touch, keyboard navigation, visible focus, and accessible names.
- Handle long text, small viewports, scrolling, and safe-area insets.
- Avoid horizontal overflow and controls that become difficult to use when the layout narrows.
- Keep spacing, typography hierarchy, and component behavior consistent within the product.
- Reuse existing components before creating near-duplicates.
- Make loading, empty, error, success, and disabled states intentional.
- Keep common actions easy to find. Add filters and secondary controls only when they help a real workflow.
- Use animation for feedback or orientation, respecting reduced motion and performance constraints.

## Visual direction

Do not impose Runa's visual identity on other products.

Colors, typography, density, illustration, and visual style should follow the product's audience, brand, and explicit design direction.
