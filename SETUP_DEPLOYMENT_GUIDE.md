# Portfolio Setup & Deployment Guide

## 🎯 Quick Start (5 Minutes)

### Step 1: Install Dependencies
```bash
cd "c:\Users\usrer\OneDrive\Documents\Projects\profile"
npm install
```

### Step 2: Start Development Server
```bash
npm run dev
```
Visit `http://localhost:5173` in your browser.

### Step 3: Make Changes
- Edit portfolio content in `src/App.vue`
- Modify component styles in individual `.vue` files
- Changes auto-reload in the browser

## 📝 Customization Guide

### Update Your Information

#### 1. Hero Section Headline
In `src/App.vue`, update the HeroSection component:

**Before:**
```typescript
// Build scalable web experiences
// with modern technology
```

**After:**
```typescript
// Your custom headline
// on multiple lines
```

#### 2. Experience Timeline
In `src/App.vue`, modify the `experiences` array:

```typescript
const experiences = [
  {
    id: 1,
    company: 'Your Company Name',
    position: 'Your Job Title',
    period: 'Start Date – End Date',
    description: 'Brief description of role',
    highlights: [
      'Achievement or responsibility 1',
      'Achievement or responsibility 2',
      'Achievement or responsibility 3',
    ],
    technologies: ['React', 'Next.js', 'TypeScript'],
  },
  // Add more experiences...
]
```

#### 3. Projects Showcase
Update the `projects` array in `src/App.vue`:

```typescript
const projects = [
  {
    id: 1,
    title: 'Project Title',
    description: 'What does this project do?',
    tags: ['React', 'TypeScript', 'AWS'],
    highlights: [
      'Key accomplishment or feature',
      'Technical achievement',
      'Business impact',
    ],
    link: 'https://project-url.com', // Optional
  },
  // Add more projects...
]
```

#### 4. Social Links
Update these components with your profiles:

**Navigation.vue** (Header):
```typescript
href="https://linkedin.com/in/your-username/"
href="mailto:your-email@gmail.com"
```

**Footer.vue**:
```typescript
href="https://github.com/your-username"
href="https://twitter.com/your-handle"
href="https://linkedin.com/in/your-username/"
```

#### 5. Contact Info
Update email and phone in:
- `src/components/Navigation.vue` - Get in Touch button
- `src/components/Footer.vue` - Footer links
- `index.html` - Meta description

### Customize Colors & Design

#### Theme Colors
Edit `tailwind.config.ts`:

```typescript
colors: {
  // Brand Colors - Vercel Design
  ink: '#171717',        // Change primary text color
  'success': '#0070f3',  // Change accent color
  'canvas': '#ffffff',   // Change background
  // ... add custom colors
}
```

#### Button Styles
Edit `src/assets/tailwind.css`:

```css
.btn-primary {
  @apply px-6 py-3 bg-ink text-white font-medium rounded-full;
  /* Adjust rounded-full to rounded-md for square buttons */
}
```

#### Typography
Update font families in `tailwind.config.ts`:

```typescript
fontFamily: {
  'sans': ['Your Custom Font', '-apple-system', /* ... */],
  'mono': ['Your Mono Font', 'monospace'],
}
```

## 🚀 Building & Deployment

### Build for Production
```bash
npm run build
```
Creates optimized files in the `dist/` folder.

### Preview Production Build
```bash
npm run preview
```

### Deployment Options

#### Option 1: Vercel (Recommended)
1. Push project to GitHub
2. Go to [vercel.com](https://vercel.com)
3. Click "New Project"
4. Import your repository
5. Click "Deploy" (Vercel auto-detects Vue)

```bash
# Or deploy via CLI
npm install -g vercel
vercel
```

#### Option 2: Netlify
```bash
npm run build
# Drag dist/ folder to netlify.com
# Or use Netlify CLI:
npm install -g netlify-cli
netlify deploy
```

#### Option 3: AWS Amplify
```bash
npm run build
npm install -g @aws-amplify/cli
amplify init
amplify add hosting
amplify publish
```

#### Option 4: GitHub Pages
```bash
# Edit vite.config.ts
export default defineConfig({
  base: '/repository-name/',
  // ...
})

npm run build
# Push dist/ to gh-pages branch
```

## 🧪 Development Workflow

### Commands
```bash
npm run dev           # Start dev server
npm run build         # Build for production
npm run preview       # Preview production build
npm run type-check    # Check TypeScript errors
npm run lint          # Run linters (ESLint, Prettier)
npm run format        # Format code with Prettier
```

### Hot Module Replacement (HMR)
- Changes to `.vue` files auto-reload
- Changes to `tailwind.css` auto-apply
- Component state is preserved during reload

### Debugging
1. Open DevTools (F12)
2. Use Vue DevTools extension (installed)
3. Check Console for errors
4. Use Network tab to verify API calls

## 🌐 Domain Setup

### Connect Custom Domain

#### Vercel
1. Go to project Settings → Domains
2. Add custom domain
3. Follow DNS instructions
4. Wait 2-24 hours for DNS propagation

#### Netlify
1. Go to Domain Management
2. Add custom domain
3. Update DNS or use Netlify nameservers

### DNS Configuration
Update your domain registrar:
- CNAME: `your-domain.com` → `your-deployment-url`
- Or use the nameservers provided by your host

## 📱 Testing

### Browser Testing
- Chrome/Chromium: `npm run dev` → F12
- Firefox: `npm run dev` → Ctrl+Shift+K
- Safari: `npm run dev` → Cmd+Option+I

### Mobile Testing
```bash
# Get your local IP
ipconfig getifaddr en0  # macOS
ipconfig              # Windows

# Visit http://<your-ip>:5173 on your phone
```

### Lighthouse Audit
1. Open DevTools (F12)
2. Click "Lighthouse"
3. Click "Generate report"
4. Check Performance, Accessibility, SEO scores

### Keyboard Navigation
- Tab: Move between elements
- Shift+Tab: Move backward
- Enter: Activate button/link
- Space: Activate button
- Escape: Close menu

### Screen Reader Testing
- Windows: NVDA (free)
- macOS: VoiceOver (Cmd+F5)
- iOS: VoiceOver (Settings → Accessibility)
- Android: TalkBack (Accessibility → TalkBack)

## 🔒 Security & Performance

### Security Checklist
- [ ] Remove console logs in production
- [ ] Use HTTPS (enforced on Vercel/Netlify)
- [ ] Validate all links and social URLs
- [ ] Check for sensitive data in code
- [ ] Review dependencies: `npm audit`

### Performance Optimization
- [ ] Minimize bundle size: `npm run build --report`
- [ ] Lazy load images if added
- [ ] Use preconnect for external fonts
- [ ] Monitor Core Web Vitals

## 📊 Analytics

### Add Google Analytics
Update `index.html`:
```html
<script async src="https://www.googletagmanager.com/gtag/js?id=GA_MEASUREMENT_ID"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'GA_MEASUREMENT_ID');
</script>
```

### Add Schema Markup
Update `src/App.vue` or create a schema component:
```json
{
  "@context": "https://schema.org",
  "@type": "Person",
  "name": "Rushabh Dedhia",
  "url": "https://your-domain.com",
  "jobTitle": "Lead Frontend Engineer",
  "sameAs": [
    "https://linkedin.com/in/rushabh-dedhia-ab108314b/"
  ]
}
```

## 🐛 Troubleshooting

### Issue: Port 5173 already in use
```bash
# Kill the process or use a different port
npm run dev -- --port 3000
```

### Issue: CSS not loading
```bash
# Restart dev server
npm run dev
# Clear browser cache (Ctrl+Shift+Delete)
```

### Issue: Build fails
```bash
# Check for TypeScript errors
npm run type-check

# Clear node_modules and reinstall
rm -r node_modules package-lock.json
npm install
npm run build
```

### Issue: Styles look wrong
- Check if Tailwind CSS is properly imported in `main.ts`
- Verify `tailwind.config.ts` is in root directory
- Clear browser cache and hard refresh (Ctrl+F5)

### Issue: Images not showing
- Use absolute paths: `/image.png` (from public/)
- Use imports: `import image from '@/assets/image.png'`
- Check image dimensions are specified

## 📚 Resources

- [Vue 3 Documentation](https://vuejs.org/)
- [Tailwind CSS v4 Docs](https://tailwindcss.com/)
- [Vite Documentation](https://vitejs.dev/)
- [Web Design Guidelines](https://vercel.com/design)
- [WCAG 2.1 Accessibility](https://www.w3.org/WAI/WCAG21/quickref/)

## 🎓 Next Steps

1. ✅ Install and run locally
2. ✅ Update your information
3. ✅ Customize colors and design
4. ✅ Test on mobile devices
5. ✅ Run Lighthouse audit
6. ✅ Deploy to production
7. ✅ Set up custom domain
8. ✅ Monitor analytics

## 📞 Support

If you encounter issues:
1. Check the [Vue 3 Docs](https://vuejs.org/)
2. Search [Tailwind Discord](https://discord.com/channels/618022840208744448)
3. Check component comments for implementation details
4. Review the compliance document: `WEB_GUIDELINES_REVIEW.md`

---

**Version**: 1.0
**Last Updated**: June 30, 2026
**Status**: Production Ready
