# Rushabh Dedhia Portfolio Website

A modern, responsive portfolio website built with Vue 3, Tailwind CSS v4, and following Vercel's design language.

## 🚀 Quick Start

### Prerequisites
- Node.js 20.19.0 or ≥22.12.0
- npm or yarn

### Installation

```bash
# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview
```

The portfolio will be available at `http://localhost:5173`

## 📁 Project Structure

```
src/
├── components/
│   ├── Navigation.vue          # Responsive navbar with smooth scroll
│   ├── HeroSection.vue         # Hero with animated gradient
│   ├── ExperienceSection.vue   # Timeline of work experience
│   ├── ProjectsSection.vue     # Showcase of featured projects
│   ├── SkillsSection.vue       # Technical skills and expertise
│   └── Footer.vue              # Footer with links and info
├── assets/
│   ├── tailwind.css            # Tailwind v4 imports and custom utilities
│   └── main.css                # Additional base styles
├── App.vue                     # Main portfolio application
└── main.ts                     # Application entry point
```

## 🎨 Design System

The portfolio follows Vercel's design language with:

### Colors
- **Primary**: `#171717` (Ink) - Main text and primary actions
- **Surface**: `#fafafa` (Canvas Soft) - Page background
- **Accent**: `#0070f3` (Success/Link Blue) - CTA and interactive elements
- **Gradient**: Multi-stop mesh (cyan → blue → magenta → amber)

### Typography
- **Display**: Custom geometric sans (Inter) - Headlines with negative tracking
- **Body**: Inter (14-18px) - Content and descriptions
- **Code**: JetBrains Mono - Technical labels and code blocks

### Spacing System
- Base unit: 4px
- Tokens: `xxs` (4px) → `5xl` (96px)
- Section padding: 192px (vertical) for major sections

### Components
- Buttons: Pills (primary/secondary) and small squares
- Cards: Subtle shadows with hairline borders
- Forms: Proper labels and accessibility attributes
- Interactive: Focus rings and smooth transitions

## ✨ Features

### Responsive Design
- Mobile-first approach
- Breakpoints: 600px (mobile), 960px (desktop), 1400px (ultra-wide)
- Touch-friendly touch targets (44×44px minimum)

### Performance
- Optimized animations (transform/opacity only)
- Lazy loading ready
- Prefers-reduced-motion support

### Accessibility (WCAG AA)
- Semantic HTML (`<button>`, `<a>`, `<label>`)
- ARIA labels on icon buttons
- Focus-visible states on all interactive elements
- Color contrast ratios > 4.5:1 for text
- Keyboard navigation support

### SEO
- Semantic HTML structure
- Meta tags for social sharing
- Proper heading hierarchy
- Structured data ready

## 🛠️ Technologies

- **Framework**: Vue 3 (Beta)
- **Build Tool**: Vite 8
- **Styling**: Tailwind CSS v4
- **Language**: TypeScript
- **Routing**: Vue Router 5
- **State**: Pinia 3
- **Linting**: ESLint + Prettier + Oxlint
- **Type Checking**: vue-tsc

## 📝 Content Sections

### 1. Hero Section
- Eye-catching headline with animated gradient background
- Professional summary
- Call-to-action buttons (Email, LinkedIn)
- Quick stats: 6+ years, 50+ projects, 3 teams led

### 2. Experience Timeline
- 3 major positions with numbered timeline
- Detailed descriptions and highlights
- Technology stack for each role
- Company and period information

### 3. Projects Showcase
- Featured projects with descriptions
- Highlighted key achievements
- Technology tags
- Links to project details

### 4. Skills & Expertise
- 6 skill categories
  - Frontend Frameworks
  - Languages & Core
  - Data Visualization
  - Testing & DevOps
  - Backend & Databases
  - Tools & Platforms
- Stats cards
- Visual hierarchy with badge styling

### 5. Navigation
- Sticky header with smooth scrolling
- Mobile hamburger menu
- Direct links to sections
- CTA button

### 6. Footer
- Quick links to social profiles
- Company mentions
- Tech stack highlights
- Contact information

## 🎯 Customization

### Update Resume Content

Edit `src/App.vue` and modify:

```typescript
const experiences = [
  {
    id: 1,
    company: 'Your Company',
    position: 'Your Position',
    period: 'Date Range',
    description: 'Description',
    highlights: ['Achievement 1', 'Achievement 2'],
    technologies: ['Tech1', 'Tech2'],
  },
]

const projects = [
  {
    id: 1,
    title: 'Project Name',
    description: 'Description',
    tags: ['React', 'TypeScript'],
    highlights: ['Highlight 1', 'Highlight 2'],
  },
]
```

### Customize Colors

Update `tailwind.config.ts` theme colors:

```typescript
colors: {
  ink: '#171717',
  success: '#0070f3',
  // ... add your colors
}
```

### Update Social Links

Edit components to update:
- LinkedIn URL in `Navigation.vue` and `Footer.vue`
- Email address in `Navigation.vue`
- Twitter/GitHub links in `Footer.vue`

## 🌐 Deployment

### Vercel (Recommended)
```bash
npm run build
# Push to GitHub and connect to Vercel
```

### Other Platforms
```bash
npm run build
# Deploy the `dist` folder
```

## 📊 Browser Support

- Chrome/Edge: Latest 2 versions
- Firefox: Latest 2 versions
- Safari: Latest 2 versions
- Mobile browsers: iOS Safari 14+, Chrome Android

## 📱 Mobile Optimization

- Responsive breakpoints at 600px, 960px, 1200px, 1400px
- Touch-friendly navigation
- Optimized images and lazy loading
- Reduced animations on low-end devices

## ♿ Accessibility

The portfolio meets WCAG 2.1 AA standards:
- ✅ Semantic HTML
- ✅ ARIA labels and roles
- ✅ Keyboard navigation
- ✅ Color contrast (4.5:1+)
- ✅ Focus indicators
- ✅ Reduced motion support

## 🔍 SEO Features

- Meta descriptions and open graph tags
- Semantic HTML with proper heading hierarchy
- Accessible images with alt text
- Mobile-first responsive design
- Fast page load times

## 📄 License

This portfolio is open source and available under the MIT License.

## 👤 Contact

- Email: rushabh.lucifer@gmail.com
- LinkedIn: [linkedin.com/in/rushabh-dedhia-ab108314b](https://linkedin.com/in/rushabh-dedhia-ab108314b)
- Phone: +91 86528 21301

---

Built with ❤️ using Vue 3, Tailwind CSS v4, and inspired by Vercel's design language.
