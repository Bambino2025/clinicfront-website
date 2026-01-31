
# Project Configuration

## Project Overview
This is the marketing website for an AI receptionist product for private medical clinics (starting with dental offices).

See docs/product-brief.md and docs/marketing.md for full business context.

**What we sell:** An AI-powered phone receptionist that answers calls 24/7, books appointments, and writes them directly into the clinic's existing scheduling software (Open Dental, Dentrix, etc.).

**Target audience:** Practice owners and office managers at small to mid-sized dental clinics, med spas, chiropractic offices, and aesthetic clinics.

**Core value prop:** "An AI receptionist that books appointments directly into your existing system—so your staff doesn't have to answer the phone."

## Frontend Aesthetics Guidelines

<frontend_aesthetics>
You tend to converge toward generic outputs. In frontend design, this creates what users call the "AI slop" aesthetic. Avoid this: make creative, distinctive frontends that surprise and delight.

Typography: Avoid generic fonts like Arial, Inter, Roboto, Open Sans, Lato, and system fonts. Use distinctive choices like: Satoshi, Cabinet Grotesk, General Sans, Plus Jakarta Sans, or DM Sans. Use clean weight contrasts. This is a professional SaaS product—keep it modern and trustworthy.

Color & Theme: Use CSS variables for consistency. Primary color should be a professional blue (#2563EB or similar). Light blue gradients for CTA sections. Clean white backgrounds. Dark text. This is healthcare-adjacent—feel trustworthy and competent, not playful.

Motion: Focus on subtle, professional animations. Rotating text in hero section. Smooth hover effects on cards. Scroll-triggered fade-ins. Nothing too flashy—this is for medical professionals.

Backgrounds: Clean white or very light gray. Use light blue gradients sparingly for CTA sections. Subtle shadows on cards for depth.

Avoid:
- Overused font families (Inter, Roboto, Arial, system fonts)
- Playful or startup-y color schemes (bright oranges, purples)
- Overly animated or flashy effects
- Generic SaaS template layouts
</frontend_aesthetics>

## Brand Context
- Professional and trustworthy (medical industry)
- Modern but not trendy
- Competent and reliable
- Reduces anxiety about AI adoption
- Target audience is busy clinic owners who want solutions, not tech demos

## Design References
See wireframes/ folder for:
- wireframe-homepage-kickcall-style.md (layout structure)
- Reference screenshots from KickCall.ai (visual style)

## Design Process
Before writing any frontend code, always:
1. Read docs/product-brief.md and docs/marketing.md
2. Review the wireframe in wireframes/
3. State your chosen font(s) and why
4. Define your color palette with CSS variables
5. Describe the aesthetic direction

## Tech Stack
- HTML, CSS, JavaScript with Tailwind CSS
- Google Fonts for typography
- Single-file components when possible

## Key Sections (from wireframe)
1. Nav — Logo, dropdown menus, Contact Sales, Login
2. Hero — Rotating feature text + headline + CTA
3. Video — Embedded video thumbnail with feature callouts
4. Stats/Channels — Light blue bg, channel cards (Phone, Voice Bot, Link, SMS)
5. Features List — Feature list with icons + calendar UI mockup
6. Support Levels — 3 cards showing L1/L2/L3 support tiers
7. Integrations — Grid of PMS integration cards (Open Dental, Dentrix, etc.)
8. Compliance — Trust badges (HIPAA, SOC 2, etc.)
9. Final CTA — Blue gradient bg, headline, CTA button, feature tags
10. Footer — Logo, link columns, copyright, legal links
