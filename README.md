# Alex Rivers Portfolio

A minimal, editorial-style portfolio website built with React, TypeScript, and Tailwind CSS. Features bold typography, clean spacing, and smooth animations.

## Features

- 🎨 **Bold Typography** - Syne for headings, Outfit for body text
- 🖼️ **Image-Focused Layout** - Square thumbnails with hover effects
- 🔄 **Client-Side Routing** - React Router for seamless navigation
- 📱 **Fully Responsive** - Mobile-first design
- ✨ **Smooth Animations** - Fade-in, hover, and transition effects
- 🚀 **Production Ready** - Optimized for Vercel deployment

## Tech Stack

- **Framework**: React 18.3.1
- **Build Tool**: Vite 6.3.5
- **Routing**: React Router 7.13.0
- **Styling**: Tailwind CSS 4.1.12
- **Language**: TypeScript
- **Icons**: Lucide React

## Project Structure

```
src/
├── app/
│   ├── components/          # Reusable UI components
│   │   ├── Navbar.tsx       # Fixed navigation header
│   │   ├── Hero.tsx         # Homepage hero section
│   │   ├── ProjectCard.tsx  # Individual project card
│   │   ├── ProjectGrid.tsx  # Grid layout with filtering
│   │   └── Footer.tsx       # Site footer
│   ├── pages/               # Route pages
│   │   ├── HomePage.tsx     # Main landing page
│   │   └── ProjectDetailPage.tsx  # Project detail view
│   ├── data/                # Data and types
│   │   └── projects.ts      # Project data & utilities
│   └── App.tsx              # Root component with routing
└── styles/
    ├── fonts.css            # Font imports (Syne, Outfit)
    └── theme.css            # Design tokens & variables
```

## Getting Started

### Prerequisites

- Node.js 18+ 
- pnpm (recommended) or npm

### Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd code
```

2. Install dependencies:
```bash
pnpm install
```

3. Start development server:
```bash
pnpm dev
```

The site will be available at the preview URL provided by Figma Make.

### Build for Production

```bash
pnpm build
```

## Design System

### Typography

- **Display Font**: Syne (weights: 400, 600, 700, 800)
- **Body Font**: Outfit (weights: 300, 400, 500, 600)

### Spacing Scale

- Container max-width: 1800px
- Grid gap: 8 (2rem)
- Section padding: 6 (1.5rem)
- Vertical spacing: 12, 16, 20, 32

### Color Palette

- Background: `#fafafa`
- Text: Black with opacity variations (100%, 60%, 40%)
- Borders: `black/5`
- Accents: Pure black

### Animations

- Fade-in on scroll: `fadeInUp` with staggered delays
- Hover scale: Images scale to 105% on hover
- Transition duration: 300ms (UI), 700ms (images)

## Routing

- `/` - Homepage with project grid
- `/project/:slug` - Individual project detail pages

## Deployment on Vercel

### Method 1: Via Vercel Dashboard

1. Push code to GitHub
2. Import project in [Vercel Dashboard](https://vercel.com)
3. Vercel auto-detects Vite config
4. Deploy!

### Method 2: Via Vercel CLI

```bash
npm i -g vercel
vercel login
vercel
```

### Build Configuration

Vercel automatically detects the Vite build:
- **Build Command**: `vite build`
- **Output Directory**: `dist`
- **Install Command**: `pnpm install`

No additional configuration needed!

## Customization

### Adding New Projects

Edit `src/app/data/projects.ts`:

```typescript
{
  id: 13,
  slug: 'your-project-slug',
  title: 'Your Project Title',
  category: 'Editorial', // or Book, Branding, Campaign, Animation, Personal
  client: 'Client Name',
  year: '2026',
  image: 'https://your-image-url.jpg',
  description: 'Brief description...',
  challenge: 'The challenge...',
  solution: 'The solution...',
  gallery: [
    'image1.jpg',
    'image2.jpg',
    'image3.jpg'
  ]
}
```

### Changing Fonts

Update `src/styles/fonts.css` with your Google Fonts import, then update the `fontFamily` inline styles in components.

### Modifying Theme

Edit design tokens in `src/styles/theme.css` for colors, spacing, and other CSS variables.

## Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

## License

This project is for demonstration purposes.

## Credits

- Design inspiration: Tommy Parker (tommyparker.co.uk)
- Images: Unsplash
- Fonts: Google Fonts
