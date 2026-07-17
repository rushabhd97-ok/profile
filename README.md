# Portfolio Website

A modern personal portfolio website built with Vue 3, TypeScript, and Vite. This project showcases my professional experience, featured projects, technical skills, and contact information in a clean and responsive layout.

## Overview

This portfolio is designed to act as my polished online presence as a developer and professional. It includes:

- A fixed navigation bar with smooth section scrolling
- A hero section with personal introduction and call-to-action
- Experience, projects, and skills sections
- A downloadable resume feature
- Responsive layout for desktop and mobile devices

## Tech Stack

- Vue 3
- TypeScript
- Vite
- Vue Router
- Pinia
- CSS with custom design styling

## Project Structure

```text
src/
├── App.vue                # Main app shell and page composition
├── main.ts                # Application entry point
├── assets/                # Global styles and visual assets
├── components/            # Reusable UI sections and layout components
│   ├── ButtonLink.vue
│   ├── ExperienceSection.vue
│   ├── FooterNote.vue
│   ├── HeroSection.vue
│   ├── Navigation.vue
│   ├── ProjectsSection.vue
│   ├── SectionHeading.vue
│   ├── SkillsSection.vue
│   └── icons/             # SVG icon components
├── router/                # Application routes
├── stores/                # Pinia state stores
└── views/                 # Page-level views
```

## Main Components

- Navigation: sticky top navigation with menu toggle and resume download
- HeroSection: introduction area with branding and call-to-action
- ExperienceSection: timeline-style work history display
- ProjectsSection: featured project cards
- SkillsSection: categorized skill overview
- FooterNote: contact and closing footer content

## Getting Started

### Prerequisites

- Node.js 24 or newer
- npm

### Installation

```bash
npm install
```

### Run locally

```bash
npm run dev
```

The development server will start and you can view the site in your browser.

### Build for production

```bash
npm run build
```

## Available Scripts

```bash
npm run dev       # Start local development server
npm run build     # Build for production
npm run preview   # Preview the production build
npm run type-check # Run TypeScript checks
npm run lint      # Run linting checks
npm run format    # Format source files
```

## Resume Download

The site includes a Resume button that downloads a PDF from the public folder. I make sure the PDF file is placed in the public directory before deployment.

## Deployment

This project is deployed on the platform:

- GitHub Pages - https://rushabhd97-ok.github.io/profile/

## GitHub Showcase Notes

This repository is well-suited for showcasing my work through:

- Clean Vue 3 component architecture
- Responsive UI implementation
- TypeScript-based frontend development
- Modern Vite-based workflow
- Professional portfolio presentation

## License

This project is for personal and portfolio use.
