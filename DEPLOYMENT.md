# Deployment Guide

Complete guide for deploying the Alex Rivers Portfolio to production.

## Quick Deploy to Vercel

### Option 1: GitHub + Vercel (Recommended)

1. **Push to GitHub**
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin <your-github-repo-url>
   git push -u origin main
   ```

2. **Deploy on Vercel**
   - Go to [vercel.com](https://vercel.com)
   - Click "New Project"
   - Import your GitHub repository
   - Vercel auto-detects Vite configuration
   - Click "Deploy"
   - Done! 🎉

### Option 2: Vercel CLI

```bash
# Install Vercel CLI
npm i -g vercel

# Login
vercel login

# Deploy
vercel

# Production deployment
vercel --prod
```

## Environment Configuration

No environment variables required for basic deployment. The site works out of the box.

### Optional: Custom Domain

1. Go to your Vercel project settings
2. Navigate to "Domains"
3. Add your custom domain
4. Update DNS records as instructed
5. SSL automatically provisioned

## Build Settings

Vercel automatically detects these settings:

- **Framework Preset**: Vite
- **Build Command**: `vite build`
- **Output Directory**: `dist`
- **Install Command**: `pnpm install`
- **Node Version**: 18.x

### Manual Configuration (if needed)

Create `vercel.json` in project root:

```json
{
  "buildCommand": "pnpm build",
  "outputDirectory": "dist",
  "framework": "vite",
  "rewrites": [
    {
      "source": "/(.*)",
      "destination": "/index.html"
    }
  ]
}
```

## Alternative Hosting Platforms

### Netlify

1. Push to GitHub
2. Go to [netlify.com](https://netlify.com)
3. Click "New site from Git"
4. Configure:
   - **Build command**: `pnpm build`
   - **Publish directory**: `dist`
5. Deploy

Create `netlify.toml`:
```toml
[build]
  command = "pnpm build"
  publish = "dist"

[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200
```

### GitHub Pages

1. Install gh-pages:
   ```bash
   pnpm add -D gh-pages
   ```

2. Update `package.json`:
   ```json
   {
     "scripts": {
       "deploy": "vite build && gh-pages -d dist"
     },
     "homepage": "https://yourusername.github.io/repo-name"
   }
   ```

3. Update `vite.config.ts`:
   ```typescript
   export default defineConfig({
     base: '/repo-name/',
     // ... other config
   })
   ```

4. Deploy:
   ```bash
   pnpm deploy
   ```

### Cloudflare Pages

1. Push to GitHub
2. Go to [pages.cloudflare.com](https://pages.cloudflare.com)
3. Connect your repository
4. Configure:
   - **Build command**: `pnpm build`
   - **Build output directory**: `dist`
5. Deploy

## Performance Optimization

### Image Optimization

Replace Unsplash URLs with optimized images:

1. Download and compress images
2. Place in `public/images/`
3. Update `src/app/data/projects.ts`:
   ```typescript
   image: '/images/project-1.jpg'
   ```

### Bundle Size

Check bundle size:
```bash
pnpm build
ls -lh dist/assets/
```

Optimize if needed:
- Use dynamic imports for large components
- Lazy load images
- Remove unused dependencies

### Lighthouse Score

Target scores:
- Performance: 90+
- Accessibility: 95+
- Best Practices: 100
- SEO: 100

## CI/CD Pipeline

### GitHub Actions

Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: pnpm/action-setup@v2
        with:
          version: 8
      - uses: actions/setup-node@v3
        with:
          node-version: 18
          cache: 'pnpm'
      - run: pnpm install
      - run: pnpm build
      - uses: amondnet/vercel-action@v20
        with:
          vercel-token: ${{ secrets.VERCEL_TOKEN }}
          vercel-org-id: ${{ secrets.ORG_ID }}
          vercel-project-id: ${{ secrets.PROJECT_ID }}
```

## Post-Deployment

### Verify Deployment

- [ ] Homepage loads correctly
- [ ] All project cards are visible
- [ ] Clicking a project navigates to detail page
- [ ] Navigation works (back button, next/previous)
- [ ] Category filters work
- [ ] Images load properly
- [ ] Responsive on mobile/tablet
- [ ] Animations run smoothly

### SEO Setup

1. **Add sitemap**: Create `public/sitemap.xml`
2. **robots.txt**: Create `public/robots.txt`
3. **Meta tags**: Add to each page
4. **Analytics**: Add Google Analytics or Plausible

### Monitoring

- Set up Vercel Analytics
- Monitor Core Web Vitals
- Track error rates
- Check uptime

## Troubleshooting

### Build Fails

```bash
# Clear cache and reinstall
rm -rf node_modules pnpm-lock.yaml
pnpm install
pnpm build
```

### Routing Issues (404 on refresh)

Make sure your hosting platform is configured for SPA routing:
- Vercel: Automatically handled
- Netlify: Add `_redirects` file
- Others: Configure rewrite rules

### Images Not Loading

- Check image URLs are accessible
- Verify CORS settings
- Use relative paths for local images

### Slow Performance

- Enable compression (gzip/brotli)
- Add CDN for static assets
- Optimize images (WebP format)
- Enable caching headers

## Security

- All dependencies are up-to-date
- No environment variables exposed
- CSP headers recommended
- HTTPS enforced

## Rollback

If deployment has issues:

```bash
# Vercel
vercel rollback

# Or via dashboard: Deployments > Previous Deployment > Promote to Production
```

## Support

For deployment issues:
- Vercel Docs: https://vercel.com/docs
- Netlify Docs: https://docs.netlify.com
- GitHub Issues: Create issue in repository
