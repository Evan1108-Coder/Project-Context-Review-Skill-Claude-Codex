# Design Lens — UI/Styling/Component Analysis

Use this lens when working on frontend features, UI changes, or design system work. Detects the visual and component patterns so new UI code matches existing conventions.

## What to Scan

### Styling Approach

Identify which system is in use (check config + actual usage):
- **Tailwind**: `tailwind.config.*` + class usage in templates
- **CSS Modules**: `*.module.css` files + import patterns
- **Styled Components / Emotion**: `styled.` or `css()` calls in source
- **SCSS/Sass**: `.scss` files + folder structure
- **Vanilla CSS**: Global stylesheets + class naming conventions
- **Utility-first custom**: Check for a custom utility class system

If Tailwind: read `tailwind.config.*` for custom theme values, plugins, content paths.
If CSS Modules: check naming convention (camelCase vs kebab-case class names).
If CSS-in-JS: check for a theme provider and token structure.

### Design Tokens / Theme

Look for centralized design values:
- CSS custom properties (`:root` block or `variables.css`)
- Theme object (JS/TS file exporting colors, spacing, typography)
- Token files (JSON/YAML design tokens)
- Tailwind theme extensions

Extract: color palette, spacing scale, typography scale, breakpoints, shadows, radii.

### Component Library

Identify the component approach:
- **External library**: MUI, Chakra, Radix, shadcn/ui, Ant Design, Headless UI
- **Custom components**: Check `components/` for shared primitives (Button, Input, Modal, etc.)
- **Hybrid**: External base + custom wrappers

For custom components, note:
- Props pattern (TypeScript interfaces? PropTypes? JSDoc?)
- Composition pattern (compound components, render props, slots)
- Where shared components live vs page-specific ones

### Layout Patterns

Sample 2-3 pages/routes and identify:
- Layout wrapper components (shell, sidebar, header)
- Grid system (CSS Grid, Flexbox patterns, framework grid)
- Responsive approach (breakpoints, container queries, fluid)
- Page structure conventions (where does main content start?)

### Asset Handling

- Where do images/icons live? (`public/`, `assets/`, `src/assets/`)
- Icon approach: SVG components, icon font, sprite, external CDN
- Image optimization: next/image, @nuxt/image, manual optimization

## Output Additions

```markdown
### Design System
- Styling: [approach] | Config: [file path]
- Tokens: [where defined] | [# colors, # spacing values, # breakpoints]
- Component library: [name or "custom"] | Location: [path]
- Icons: [approach] | Location: [path]

### UI Conventions
- Component file pattern: [e.g., PascalCase.tsx with co-located .module.css]
- Props pattern: [interface/type approach]
- Layout: [shell component path + structure]
- Responsive: [breakpoint strategy]

### To Add a New UI Component
- Create: [where]
- Style: [how — which tokens/classes to use]
- Export: [pattern]
- Test: [if UI tests exist, how]
```
