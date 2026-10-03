# Web UI preferences

## Tools

- Use Tailwind CSS for styling.
- Prefer shadcn/ui components built on Base UI when available and suitable.
- Use Radix-based components when the needed Base UI implementation is unavailable or does not meet the requirements.
- Check actual component support instead of assuming interchangeability.
- In existing projects, reuse the established component foundation. Do not migrate primitives solely to satisfy this preference.
- Add specialized libraries only when needed.

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
