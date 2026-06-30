# Design Tokens Reference

This document provides a quick reference of all design tokens used in the portfolio, derived from the Vercel design language and Tailwind CSS v4 configuration.

## 🎨 Color Palette

### Primary Colors
- **Ink** - `#171717` - Used for headings, text, primary buttons
- **Ink Soft** - `#4d4d4d` - Secondary text, descriptions
- **Ink Mute** - `#888888` - Tertiary text, captions

### Surface Colors
- **Canvas** - `#ffffff` - Card backgrounds, modals
- **Canvas Soft** - `#fafafa` - Page background (default)
- **Canvas Soft 2** - `#f5f5f5` - Inset regions, hover states

### Border & Dividers
- **Hairline** - `#ebebeb` - Card borders, dividers
- **Hairline Strong** - `#a1a1a1` - Stronger dividers

### Interactive & Semantic
- **Success/Link** - `#0070f3` - Links, primary CTA, focus rings
- **Success Deep** - `#0761d1` - Pressed/visited link state
- **Success Light** - `#d3e5ff` - Background for badges

### Feedback Colors
- **Error** - `#ee0000` - Destructive actions
- **Error Soft** - `#f7d4d6` - Error backgrounds
- **Error Deep** - `#c50000` - Pressed error state
- **Warning** - `#f5a623` - Caution/pending status
- **Warning Soft** - `#ffefcf` - Warning background
- **Warning Deep** - `#ab570a` - Pressed warning state

### Brand Gradient
A three-pair multi-stop gradient used at hero scale:
```
linear-gradient(
  135deg,
  #007cf0 0%,    /* Blue (develop start) */
  #00dfd8 25%,   /* Cyan (develop end) */
  #7928ca 50%,   /* Violet (preview start) */
  #ff0080 75%,   /* Pink (preview end) */
  #f9cb28 100%   /* Amber (ship end) */
)
```

Individual gradient stops available as:
- **Cyan** - `#50e3c2`
- **Violet** - `#7928ca`
- **Pink** - `#ff0080`
- **Amber** - `#f9cb28`

## 📝 Typography

### Font Families
- **Sans (Display, Body, Nav)**: Inter, -apple-system, BlinkMacSystemFont, Segoe UI, sans-serif
- **Mono (Code, Labels, Captions)**: JetBrains Mono, monospace

### Font Scale & Hierarchy

| Token | Size | Weight | Line Height | Letter Spacing | Usage |
|-------|------|--------|-------------|----------------|-------|
| `display-xl` | 48px | 600 | 48px | -2.4px | Hero headline |
| `display-lg` | 32px | 600 | 40px | -1.28px | Section headlines |
| `display-md` | 24px | 600 | 32px | -0.96px | Card headlines |
| `display-sm` | 20px | 600 | 28px | -0.6px | Subsection titles |
| `body-lg` | 18px | 400 | 28px | 0px | Lead paragraphs |
| `body-md` | 16px | 400 | 24px | 0px | Default body text |
| `body-md-strong` | 16px | 500 | 24px | 0px | Emphasized body |
| `body-sm` | 14px | 400 | 20px | -0.28px | Secondary text, nav |
| `body-sm-strong` | 14px | 500 | 20px | -0.28px | Nav CTA, emphasis |
| `caption` | 12px | 400 | 16px | 0px | Footer, badges |
| `caption-mono` | 12px | 400 | 16px | 0px | Section eyebrows |
| `code` | 13px | 400 | 20px | 0px | Code snippets |
| `button-md` | 14px | 500 | 20px | 0px | Small buttons |
| `button-lg` | 16px | 500 | 24px | 0px | Marketing CTAs |

### Typography Principles
- Negative tracking on display sizes (aggressive -2.4 to -0.6px)
- Sentence-case headlines with period punctuation
- Font weight capped at 600 (never 700+)
- Mono font for technical elements only

## 📏 Spacing System

### Base Unit
**4px** - All spacing values are multiples of 4px

### Spacing Tokens

| Token | Value | Usage |
|-------|-------|-------|
| `xxs` | 4px | Minimal gaps, inline spacing |
| `xs` | 8px | Tight spacing, badge padding |
| `sm` | 12px | Component gaps, button groups |
| `md` | 16px | Standard padding, card interior |
| `lg` | 24px | Section gaps, list spacing |
| `xl` | 32px | Header spacing, large gaps |
| `2xl` | 40px | Major section dividers |
| `3xl` | 48px | Large component spacing |
| `4xl` | 64px | Section top/bottom padding |
| `5xl` | 96px | Hero section spacing |
| `6xl` | 128px | Full-width section gaps |
| `section` | 192px | Hero bands, major section dividers |

### Layout Spacing Patterns
- **Section padding**: 64px-96px top/bottom (lg to 5xl)
- **Hero padding**: 192px top/bottom for gradient breathing room
- **Card interior**: 16px-24px (md to lg)
- **Inline gaps**: 12px-24px between siblings
- **Component clusters**: 12px between related items

## 🎯 Border Radius

| Token | Value | Usage |
|-------|-------|-------|
| `none` | 0px | No rounding |
| `xs` | 2px | Minimal curves |
| `sm` | 4px | Subtle rounding |
| `md` | 8px | Standard cards, buttons |
| `lg` | 12px | Larger components |
| `xl` | 16px | Feature sections |
| `2xl` | 20px | Oversized elements |
| `full` | 9999px | Pills, circles |

### Component Patterns
- **Buttons**: `rounded-full` for pills, `rounded-md` for square buttons
- **Cards**: `rounded-md` for standard cards
- **Inputs**: `rounded-md` for form fields
- **Interactive**: `rounded-md` for general interactive elements

## 🌫️ Elevation & Shadows

### Shadow Definitions

| Level | CSS | Usage |
|-------|-----|-------|
| **0 - Flat** | None | Full-bleed sections, no elevation |
| **1 - Hairline** | `0 0 0 1px rgba(0,0,0,0.08)` inset | Card borders, default elevation |
| **2 - Subtle** | `0px 1px 1px rgba(0,0,0,0.05), 0px 2px 2px rgba(0,0,0,0.1)` | Slightly elevated cards |
| **3 - Soft Stack** | `0px 2px 2px rgba(0,0,0,0.1), 0px 8px 8px rgba(0,0,0,0.1)` | Feature cards |
| **4 - Float** | `0px 2px 2px rgba(0,0,0,0.1), 0px 8px 16px rgba(0,0,0,0.1)` | Pricing/callout cards |
| **5 - Modal** | `0px 1px 1px rgba(0,0,0,0.05), 0px 8px 16px rgba(0,0,0,0.1), 0px 24px 32px rgba(0,0,0,0.15)` | Modals, dropdowns |

### Shadow Principles
- Stacked shadows (multiple offsets) not single heavy drop-shadow
- Always paired with inset hairline border for edge definition
- Never use `box-shadow: 0 10px 30px rgba(...)` style shadows

## 📱 Responsive Breakpoints

| Name | Width | Design Pattern |
|------|-------|----------------|
| Mobile | < 600px | Single column, full-width, hamburger nav |
| Tablet | 600–959px | 2-up grids, responsive nav |
| Desktop | 960–1199px | 3-up grids, full sidebar navigation |
| Wide | 1200–1399px | Full horizontal nav, max container 1400px |
| Ultra-wide | ≥ 1400px | Content centered at 1400px, bands full-width |

### Responsive Patterns
- **Grid**: 1-up → 2-up → 3-up at breakpoints
- **Padding**: Mobile 12px → Tablet/Desktop 24px
- **Font sizes**: Slightly smaller on mobile, scale up on desktop
- **Touch targets**: Minimum 44×44px on mobile, standard on desktop

## 🎨 Component Utilities

### Button Variants

**Primary Button** (`.btn-primary`)
```css
background: #171717 (ink)
color: white
padding: 12px 24px (md spacing)
border-radius: 9999px (full)
font-weight: 500
font-size: 16px (button-lg)
```

**Secondary Button** (`.btn-secondary`)
```css
background: #ffffff (canvas)
border: 1px #ebebeb (hairline)
color: #171717 (ink)
Same padding/radius/weight as primary
```

**Small Button** (`.btn-small`)
```css
Same as primary but:
padding: 8px 16px (xs spacing)
border-radius: 6px (md)
font-size: 14px (button-md)
```

### Card Component (`.card`)
```css
background: #ffffff (canvas)
border: 1px #ebebeb (hairline)
border-radius: 8px (md)
padding: 16px (md)
box-shadow: 0px 1px 1px rgba(0,0,0,0.05), 
            0px 2px 2px rgba(0,0,0,0.1)
```

### Focus Styles
```css
focus-visible:ring-2                    /* 2px ring width */
focus-visible:ring-offset-2             /* 2px gap from element */
focus-visible:ring-success              /* #0070f3 blue */
```

## 🎯 Animation Properties

### Preferred Animation
- **Properties**: `transform` and `opacity` only
- **Reason**: GPU-accelerated, smooth performance
- **Avoid**: `transition: all` (list specific properties)

### Example Animations
- Button hover: `transition-all`
- Link hover: `transition-colors`
- Card elevation: `transition-shadow`
- Menu open: `transition-transform`

### Reduced Motion
Support `prefers-reduced-motion: reduce`:
```css
@media (prefers-reduced-motion: reduce) {
  * {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

## 🔐 Accessibility Tokens

### Focus Indicators
- Ring width: 2px
- Ring offset: 2px
- Ring color: #0070f3 (success/link blue)
- Never use `outline: none` without replacement

### Color Contrast
- **Normal text**: 4.5:1 minimum
- **Large text**: 3:1 minimum
- **UI components**: 3:1 minimum

### Touch Targets
- **Minimum size**: 44×44px (mobile)
- **Ideal size**: 48×48px (comfortable touch)
- **Minimum spacing**: 8px between targets

## 📐 Layout Container

### Max Width
- **Desktop**: 1400px (`max-w-container`)
- **Legacy**: 1200px (older pages)
- **Center**: Horizontal auto margins

### Padding
- **Mobile**: 16px (md)
- **Tablet**: 24px (lg)
- **Desktop**: 24px-32px (lg-xl)

## 🎓 Usage Guidelines

### When to Use Each Color

**Ink (#171717)**
- Primary headlines
- Primary body text
- Primary button background
- Icon colors

**Success (#0070f3)**
- Links
- Focus rings
- Primary CTA button text (on ink)
- Accent elements

**Canvas Soft (#fafafa)**
- Default page background
- Hover states on light backgrounds

**Canvas (#ffffff)**
- Card backgrounds
- Modal backgrounds
- Input fields

**Hairline (#ebebeb)**
- Card borders
- Divider lines
- Input borders

### When to Use Each Font Size

**Display XL (48px)**
- Only for hero headline

**Display LG (32px)**
- Section main headings

**Display MD (24px)**
- Card/feature headings

**Body LG (18px)**
- Lead paragraphs under headings

**Body MD (16px)**
- Default body text
- Large buttons

**Body SM (14px)**
- Secondary text
- Navigation items
- Small buttons

**Caption (12px)**
- Footer text
- Badge labels
- Fine print

---

**Reference**: Derived from DESIGN.md and tailwind.config.ts
**Version**: 1.0
**Last Updated**: June 30, 2026
