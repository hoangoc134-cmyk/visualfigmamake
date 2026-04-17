# Complete Folder Structure

Detailed breakdown of the project architecture and file organization.

## Directory Tree

```
portfolio/
├── src/                          # Source code
│   ├── app/                      # Application code
│   │   ├── components/           # Reusable React components
│   │   │   ├── Navbar.tsx        # Fixed navigation header with routing
│   │   │   ├── Hero.tsx          # Homepage hero section with large typography
│   │   │   ├── ProjectCard.tsx   # Individual project card with image & hover effects
│   │   │   ├── ProjectGrid.tsx   # Grid layout with category filtering
│   │   │   ├── Footer.tsx        # Site footer with links & newsletter
│   │   │   ├── figma/            # Figma-specific components
│   │   │   │   └── ImageWithFallback.tsx
│   │   │   └── ui/               # Shadcn UI components (pre-installed)
│   │   │       ├── dialog.tsx
│   │   │       ├── calendar.tsx
│   │   │       ├── button.tsx
│   │   │       └── ... (30+ components)
│   │   ├── pages/                # Route page components
│   │   │   ├── HomePage.tsx      # Main landing page (Hero + Grid)
│   │   │   └── ProjectDetailPage.tsx  # Individual project view
│   │   ├── data/                 # Data layer
│   │   │   └── projects.ts       # Project data, types, and utility functions
│   │   └── App.tsx               # Root component with BrowserRouter
│   └── styles/                   # Global styles
│       ├── fonts.css             # Google Fonts imports (Syne, Outfit)
│       ├── theme.css             # Design tokens, CSS variables, base styles
│       ├── index.css             # Global CSS imports
│       └── tailwind.css          # Tailwind directives
├── public/                       # Static assets (auto-created on build)
│   └── (add images here)
├── .gitignore                    # Git ignore rules
├── package.json                  # Dependencies and scripts
├── pnpm-lock.yaml                # Lockfile for pnpm
├── vite.config.ts                # Vite configuration
├── tsconfig.json                 # TypeScript configuration
├── postcss.config.mjs            # PostCSS configuration
├── README.md                     # Project documentation
├── DEPLOYMENT.md                 # Deployment guide
└── FOLDER_STRUCTURE.md           # This file
```

## File Descriptions

### Core Application Files

#### `src/app/App.tsx`
- **Purpose**: Application root component
- **Responsibilities**:
  - Sets up React Router (BrowserRouter)
  - Defines routes (homepage, project detail)
  - Wraps entire app with Navbar and Footer
- **Key Features**: Client-side routing, layout consistency

#### `src/app/pages/HomePage.tsx`
- **Purpose**: Main landing page
- **Components Used**: Hero, ProjectGrid
- **Data**: Imports projects and categories from `data/projects.ts`
- **Route**: `/`

#### `src/app/pages/ProjectDetailPage.tsx`
- **Purpose**: Individual project showcase
- **Features**:
  - Dynamic routing via slug
  - Project details (description, challenge, solution)
  - Image gallery
  - Previous/Next project navigation
  - Back to home link
- **Route**: `/project/:slug`

### Components

#### `src/app/components/Navbar.tsx`
- **Type**: Layout component
- **Features**:
  - Fixed positioning
  - Logo linking to homepage
  - Navigation links with underline hover effect
  - Responsive (hidden on mobile, visible on desktop)
- **Styling**: Backdrop blur, transparent background

#### `src/app/components/Hero.tsx`
- **Type**: Presentational component
- **Features**:
  - Large typographic headline (4rem - 8rem)
  - Tagline/description
  - Generous spacing
- **Purpose**: Visual impact and brand identity

#### `src/app/components/ProjectCard.tsx`
- **Type**: Interactive component
- **Props**: `slug`, `title`, `category`, `image`, `index`
- **Features**:
  - Square aspect ratio image
  - Hover scale effect (105%)
  - Staggered fade-in animation
  - Links to project detail page
- **Animations**: CSS keyframe fadeInUp with delay

#### `src/app/components/ProjectGrid.tsx`
- **Type**: Layout + Logic component
- **Features**:
  - Category filtering (state management)
  - Responsive grid (1-4 columns)
  - Sticky filter bar
  - Dynamic project rendering
- **Props**: `projects`, `categories`

#### `src/app/components/Footer.tsx`
- **Type**: Layout component
- **Sections**:
  - About info
  - Navigation links
  - Social links
  - Newsletter signup
  - Copyright
- **Layout**: 4-column grid on desktop, stacked on mobile

### Data Layer

#### `src/app/data/projects.ts`
- **Purpose**: Single source of truth for project data
- **Exports**:
  - `Project` interface (TypeScript type)
  - `projects` array (12 sample projects)
  - `categories` array
  - `getProjectBySlug()` utility
  - `getNextProject()` utility
  - `getPreviousProject()` utility
- **Data Structure**:
  ```typescript
  {
    id: number
    slug: string (URL-friendly)
    title: string
    category: string
    client?: string
    year?: string
    image: string (thumbnail)
    description: string
    challenge?: string
    solution?: string
    gallery: string[] (3 images)
  }
  ```

### Styles

#### `src/styles/fonts.css`
- **Purpose**: Web font imports
- **Fonts**:
  - Syne: Display font (400, 600, 700, 800)
  - Outfit: Body font (300, 400, 500, 600)
- **Source**: Google Fonts

#### `src/styles/theme.css`
- **Purpose**: Design system tokens
- **Contents**:
  - CSS custom properties (colors, spacing)
  - Dark mode variants
  - Tailwind theme integration
  - Base element styles (h1-h4, p, button, input)
- **Key Variables**:
  - `--background`, `--foreground`
  - `--primary`, `--secondary`
  - `--border`, `--radius`

#### `src/styles/tailwind.css`
- **Purpose**: Tailwind CSS directives
- **Contents**:
  ```css
  @import "tailwindcss";
  @import "./theme.css";
  @import "./fonts.css";
  ```

### Configuration Files

#### `package.json`
- **Dependencies**:
  - React 18.3.1
  - React Router 7.13.0
  - Tailwind CSS 4.1.12
  - Lucide React (icons)
  - Motion (animations)
  - 30+ UI libraries (pre-installed)
- **Scripts**:
  - `build`: Production build via Vite
  - (dev server managed by Figma Make)

#### `vite.config.ts`
- **Purpose**: Vite bundler configuration
- **Plugins**: React, Tailwind
- **Optimizations**: Code splitting, tree shaking

#### `tsconfig.json`
- **Purpose**: TypeScript compiler options
- **Config**: Strict mode, JSX support, module resolution

## Component Relationships

```
App.tsx (Router)
├── Navbar (always visible)
├── Routes
│   ├── HomePage
│   │   ├── Hero
│   │   └── ProjectGrid
│   │       └── ProjectCard (×12)
│   └── ProjectDetailPage
│       ├── Project Header
│       ├── Image Gallery
│       └── Navigation (Prev/Next)
└── Footer (always visible)
```

## Data Flow

```
projects.ts
    ↓
HomePage.tsx → ProjectGrid.tsx → ProjectCard.tsx
    ↓
User clicks card
    ↓
Navigate to /project/:slug
    ↓
ProjectDetailPage.tsx → getProjectBySlug(slug)
    ↓
Display project details
```

## Styling Architecture

```
Tailwind CSS (utility classes)
    +
theme.css (design tokens)
    +
fonts.css (typography)
    +
Inline styles (font-family overrides)
    =
Complete design system
```

## Responsive Breakpoints

- **Mobile**: < 768px (1 column grid)
- **Tablet**: 768px - 1024px (2 column grid)
- **Desktop**: 1024px - 1280px (3 column grid)
- **Large Desktop**: 1280px+ (4 column grid)

## Animation Strategy

1. **On Mount**: Staggered fadeInUp for project cards
2. **On Hover**: Scale transform for images
3. **On Click**: Smooth navigation transitions
4. **On Scroll**: Sticky category filter bar

## Best Practices Implemented

- ✅ Component composition over prop drilling
- ✅ TypeScript for type safety
- ✅ Centralized data management
- ✅ Responsive-first design
- ✅ Accessible HTML semantics
- ✅ Performance optimizations (lazy loading potential)
- ✅ Clean separation of concerns
- ✅ Reusable utility functions
- ✅ Consistent naming conventions
- ✅ Mobile-friendly navigation

## Adding New Features

### New Page
1. Create in `src/app/pages/NewPage.tsx`
2. Add route in `App.tsx`:
   ```tsx
   <Route path="/new" element={<NewPage />} />
   ```

### New Component
1. Create in `src/app/components/NewComponent.tsx`
2. Import where needed
3. Use TypeScript for prop types

### New Project
1. Add to `src/app/data/projects.ts`
2. Follow existing data structure
3. Component automatically renders it

### Style Customization
1. Edit `src/styles/theme.css` for global changes
2. Use Tailwind classes for component-specific styles
3. Add custom CSS in component `<style>` tags if needed
