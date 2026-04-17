# Quick Start Guide

Get up and running in 5 minutes.

## Prerequisites

- Node.js 18 or higher
- pnpm (recommended) or npm

## Installation

```bash
# 1. Navigate to project
cd portfolio

# 2. Install dependencies (if not already installed)
pnpm install

# 3. Start development (in Figma Make environment)
# The dev server is already running - just make changes!
```

## Project Overview

This is a **portfolio website** featuring:
- Homepage with filterable project grid
- Individual project detail pages
- Responsive design
- Smooth animations

## Key Files to Know

```
src/app/
├── App.tsx                    # Main app with routing
├── data/projects.ts           # Edit project data here
├── components/                # Reusable UI components
└── pages/                     # Page components
```

## Making Changes

### Add a New Project

Edit `src/app/data/projects.ts`:

```typescript
{
  id: 13,
  slug: 'my-new-project',
  title: 'My New Project',
  category: 'Branding',
  image: 'https://your-image-url.jpg',
  description: 'Description...',
  gallery: ['img1.jpg', 'img2.jpg', 'img3.jpg']
}
```

### Change Colors

Edit `src/styles/theme.css`:

```css
:root {
  --background: #ffffff;  /* Change to your color */
  --foreground: #000000;
}
```

### Update Typography

Edit `src/styles/fonts.css` to import different fonts:

```css
@import url('https://fonts.googleapis.com/css2?family=YourFont:wght@400;700&display=swap');
```

Then update components with new font families.

### Modify Layout

Edit components in `src/app/components/`:
- `Navbar.tsx` - Navigation bar
- `Hero.tsx` - Homepage hero
- `ProjectGrid.tsx` - Project grid layout
- `Footer.tsx` - Site footer

## Common Tasks

### Filter Projects by Category

Click category buttons on homepage - it's already working!

### Navigate to Project Details

Click any project card to view full details.

### Go Back Home

Click logo or "Back to Work" link.

## Deployment

### Deploy to Vercel (Easiest)

```bash
# 1. Install Vercel CLI
npm i -g vercel

# 2. Login
vercel login

# 3. Deploy
vercel

# 4. For production
vercel --prod
```

See `DEPLOYMENT.md` for detailed instructions.

## File Structure

```
src/
├── app/
│   ├── components/     # UI components
│   ├── pages/          # Route pages
│   ├── data/           # Project data
│   └── App.tsx         # Main app
└── styles/             # Global styles
```

## Component Hierarchy

```
App
├── Navbar (fixed header)
├── Routes
│   ├── HomePage
│   │   ├── Hero
│   │   └── ProjectGrid
│   │       └── ProjectCard (12 instances)
│   └── ProjectDetailPage
└── Footer
```

## Responsive Breakpoints

- Mobile: < 768px
- Tablet: 768px - 1024px
- Desktop: 1024px+

## Tech Stack

- **React 18** - UI library
- **TypeScript** - Type safety
- **Tailwind CSS 4** - Styling
- **React Router 7** - Routing
- **Vite 6** - Build tool
- **Lucide React** - Icons

## Need Help?

- Check `README.md` for full documentation
- See `DEPLOYMENT.md` for deployment guides
- Review `FOLDER_STRUCTURE.md` for architecture details

## Next Steps

1. ✅ Customize project data in `data/projects.ts`
2. ✅ Update colors/fonts to match your brand
3. ✅ Add your own images
4. ✅ Test responsive design
5. ✅ Deploy to Vercel

## Tips

- **Images**: Use consistent aspect ratios
- **Content**: Keep descriptions concise
- **Performance**: Optimize images before uploading
- **SEO**: Add meta tags for better discoverability
- **Testing**: Check on mobile, tablet, and desktop

## Example Workflow

```bash
# 1. Make changes to data/projects.ts
# 2. Preview changes in browser
# 3. Happy with changes? Deploy:
vercel --prod
```

That's it! You're ready to go. 🚀
