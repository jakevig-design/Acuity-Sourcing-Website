# Acuity Sourcing Website - Build Instructions for Claude Code

## Overview
This guide provides step-by-step instructions for building and deploying the Acuity Sourcing website using Claude Code. The site consists of two HTML files with integrated CSS and is ready for immediate deployment.

## Files Included
- `acuity-homepage.html` — Main landing page with hero, services, and methodology
- `acuity-portfolio.html` — Portfolio page with case studies organized by service type

## Prerequisites
- Node.js 18+ (for local development server)
- A modern web browser (Chrome, Firefox, Safari, or Edge)
- Git (optional, for version control)
- SSH/FTP access to your hosting provider (for deployment)

## Local Development

### 1. Set Up a Local Directory
```bash
mkdir acuity-sourcing
cd acuity-sourcing
```

### 2. Add the HTML Files
Place both `acuity-homepage.html` and `acuity-portfolio.html` in the project directory.

### 3. Start a Local Development Server
Option A (Node.js with http-server):
```bash
npm install -g http-server
http-server
```

Option B (Python 3):
```bash
python3 -m http.server 8000
```

Option C (Node.js with live-server for auto-reload):
```bash
npm install -g live-server
live-server
```

### 4. Test Locally
Open your browser and navigate to:
- Homepage: `http://localhost:8000` (or `http://localhost:8080` for http-server)
- Portfolio: `http://localhost:8000/acuity-portfolio.html`

Verify all links work:
- Navigation links in header
- Service card links to portfolio sections
- Footer email and LinkedIn links

## Deployment

### Option 1: Vercel (Recommended for Static Sites)
1. Initialize git repository:
   ```bash
   git init
   git add .
   git commit -m "Initial Acuity Sourcing website"
   ```

2. Push to GitHub:
   ```bash
   git remote add origin https://github.com/yourusername/acuity-sourcing.git
   git branch -M main
   git push -u origin main
   ```

3. Connect to Vercel:
   - Visit https://vercel.com
   - Sign in with GitHub
   - Click "New Project"
   - Select the acuity-sourcing repository
   - Vercel will auto-detect it as a static site
   - Click "Deploy"

4. Configure custom domain:
   - In Vercel dashboard, go to Settings > Domains
   - Add your domain (acuitysourcing.com)
   - Follow DNS instructions from your domain registrar

### Option 2: GoDaddy Hosting (Current Provider)
1. Connect to your GoDaddy hosting via FTP:
   - Use FileZilla or your preferred FTP client
   - Server: ftp.yourdomain.com
   - Username/Password: From GoDaddy account
   - Port: 21 (standard FTP)

2. Upload files:
   - Navigate to the public_html directory
   - Upload `acuity-homepage.html` as `index.html` (this becomes the homepage)
   - Upload `acuity-portfolio.html` in the same directory

3. Update links:
   - If deploying to a subdirectory, update all relative links
   - Example: `acuity-portfolio.html` → `portfolio/index.html`

4. Test the live site:
   - Visit https://acuitysourcing.com
   - Check all navigation and links work

### Option 3: Manual Deployment to Any Web Host
1. Connect via SSH:
   ```bash
   ssh username@yourdomain.com
   ```

2. Navigate to web root:
   ```bash
   cd public_html
   # or /var/www/html depending on your host
   ```

3. Upload files:
   ```bash
   scp acuity-homepage.html username@yourdomain.com:~/public_html/index.html
   scp acuity-portfolio.html username@yourdomain.com:~/public_html/portfolio/index.html
   ```

4. Verify deployment:
   - Visit your domain
   - Test all internal links
   - Check mobile responsiveness

## Build Configuration

### For Vercel (vercel.json)
If you want to customize the Vercel build, create a `vercel.json` file:

```json
{
  "buildCommand": "",
  "outputDirectory": "",
  "env": {},
  "headers": [
    {
      "source": "/(.*)",
      "headers": [
        {
          "key": "Cache-Control",
          "value": "public, max-age=3600, must-revalidate"
        }
      ]
    }
  ]
}
```

### For GoDaddy/Traditional Hosting
No build configuration needed. Files are served as-is.

## File Structure

```
acuity-sourcing/
├── acuity-homepage.html      (rename to index.html on deployment)
├── acuity-portfolio.html
├── README.md                  (optional)
└── .gitignore                (optional, if using version control)
```

### .gitignore (if using version control)
```
node_modules/
.DS_Store
.env
*.log
```

## Updating Content

### Homepage Changes
Edit `acuity-homepage.html` directly:
- Update hero text: Find `<section class="hero">`
- Modify principle descriptions: Find `<section class="principles">`
- Change CTA button: Find `<section class="cta">`
- Update footer info: Find `<footer>`

### Portfolio Changes
Edit `acuity-portfolio.html` directly:
- Add new case study: Copy an existing `<div class="case-study">` block
- Update existing case study: Find the case study by title
- Modify service section intro: Find `<section class="service-section">`

### Redeploying After Changes

**If using Vercel:**
```bash
git add .
git commit -m "Update case studies"
git push origin main
# Vercel auto-deploys on push
```

**If using GoDaddy/Manual hosting:**
1. Upload the updated files via FTP
2. Clear browser cache (Ctrl+Shift+Delete or Cmd+Shift+Delete)
3. Visit site to verify changes

## CSS Customization

All CSS is embedded in the HTML files. To modify:

1. **Colors** — Update CSS variables at the top of `<style>` block:
   ```css
   :root {
       --navy: #131F53;
       --teal: #1A9599;
       --green: #7EBD41;
       /* etc */
   }
   ```

2. **Typography** — Adjust font sizes and weights in relevant sections
3. **Spacing** — Modify padding/margin values
4. **Responsive breakpoints** — Edit the `@media (max-width: 768px)` section

## Performance Optimization

### Image Optimization (Future)
If you add images:
```bash
# Compress images before uploading
npm install -g imagemin-cli
imagemin src/*.{jpg,png} --out-dir=dist
```

### CSS/JS Minification (Optional)
For production, consider minifying:
```bash
npm install -g csso-cli
csso style.css -o style.min.css
```

Current setup is lightweight and doesn't require minification.

## Analytics & Tracking (Optional)

To add Google Analytics, add this before `</head>`:
```html
<script async src="https://www.googletagmanager.com/gtag/js?id=YOUR_GA_ID"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'YOUR_GA_ID');
</script>
```

## Troubleshooting

### Links Not Working
- Check file names match exactly (case-sensitive on Linux/Mac)
- Verify relative paths: `acuity-portfolio.html` not `/acuity-portfolio.html`
- On subdirectories, update links: `portfolio/acuity-portfolio.html`

### Styling Looks Wrong
- Clear browser cache (Ctrl+Shift+Delete)
- Check that CSS is intact in the HTML file
- Verify no CSS was accidentally modified during upload

### Mobile Responsiveness Issues
- Test in Chrome DevTools (F12 > Toggle Device Toolbar)
- Check that viewport meta tag is present: `<meta name="viewport" content="width=device-width, initial-scale=1.0">`

### Deployment Failures on Vercel
- Verify GitHub repository is public (or give Vercel access)
- Check that HTML files are in root directory
- Ensure file names don't have spaces

## Maintenance Checklist

- [ ] Test homepage on desktop and mobile
- [ ] Test portfolio on desktop and mobile
- [ ] Verify all internal links work
- [ ] Check footer links (email, LinkedIn)
- [ ] Test navigation header on all pages
- [ ] Verify brand colors display correctly
- [ ] Check load time (should be < 1s)
- [ ] Test on multiple browsers (Chrome, Firefox, Safari, Edge)

## Support & Further Customization

For Claude Code-specific help:
1. Use `claude code` in your terminal to open the code editor
2. Ask Claude to modify specific sections (colors, text, layout)
3. Claude can generate additional pages (services detail, about, etc.)

For deployment help:
- Vercel docs: https://vercel.com/docs
- GoDaddy help: https://www.godaddy.com/help
- General hosting: Contact your provider's support

---

**Last Updated:** May 2026
**Version:** 1.0
**Status:** Ready for Production Deployment
