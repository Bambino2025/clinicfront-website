# ClearDesk Homepage Design

## Overview

Marketing homepage for ClearDesk, an AI receptionist product for private medical clinics. Professional, trustworthy SaaS aesthetic in blue/white.

## Typography & Color

### Font

**Plus Jakarta Sans** (Google Fonts)
- Headlines: 700 weight
- Body: 400/500 weight

### Color Palette

```css
:root {
  --color-primary: #2563EB;
  --color-primary-dark: #1D4ED8;
  --color-primary-light: #DBEAFE;

  --color-text: #1E293B;
  --color-text-muted: #64748B;

  --color-bg: #FFFFFF;
  --color-bg-subtle: #F8FAFC;

  --color-border: #E2E8F0;
}
```

### CTA Gradient

```css
background: linear-gradient(135deg, #2563EB 0%, #3B82F6 100%);
```

---

## Layout Structure

- Max content width: 1200px, centered
- Section padding: 80px vertical (desktop), 48px (mobile)
- Cards: White, subtle shadow (`box-shadow: 0 1px 3px rgba(0,0,0,0.08)`), 8px border-radius
- Breakpoints: 1024px (tablet), 640px (mobile)

---

## Section 1: Navigation Bar

- Sticky on scroll, white background, subtle bottom border
- Logo left, nav links center, CTAs right
- Dropdowns: Features, Use Cases, Resources
- "Contact Sales" outlined button, "Login" text link

---

## Section 2: Hero

```
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│            · Appointment Booking ·                          │  ← rotating text
│            · Patient Questions ·                            │    (cycles every 3s)
│            · After-Hours Calls ·                            │
│                                                             │
│          AI Phone Answering                                 │  ← 48px, bold
│          for Private Clinics                                │
│                                                             │
│     An AI receptionist that answers calls 24/7,             │  ← 18px, muted
│     books appointments, and writes directly into            │
│     your existing scheduling software.                      │
│                                                             │
│                [ Book a Free Demo ]                         │  ← blue button
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

- Rotating text: fade animation, 3-second interval
- Centered layout

---

## Section 3: Video Section

Two-column layout (stacks on mobile):

- **Left:** Video thumbnail with play button overlay, blue gradient background
  - Text: "See ClearDesk in Action"
  - Links to YouTube/Vimeo embed modal (or placeholder if no video)
- **Right:** Bullet list with blue check icons
  - Recall Reminders
  - After-Hours Handling
  - Appointment Booking
  - Fill Last-Minute Cancellations
  - Reduce No-Shows

---

## Section 4: Channels Section

Light blue background (`--color-primary-light`)

**Header:**
- "Capturing Every Conversation"
- "80% resolved by AI. 20% ready for human action."

**4 Channel Cards** (white, 3-column grid → 1-column mobile):

| Phone Calls | Website Voice Bot | Share Link | SMS (Coming Soon) |
|-------------|-------------------|------------|-------------------|
| Human-like voice, call actions, transfers | Real-time voice chat, lead capture, booking | Shareable link opens live AI assistant | Automated reminders & scheduling |

- SMS card has subtle "Coming Soon" badge

---

## Section 5: Features Section

Two-column layout:

**Left: Feature List** (with blue icons from Lucide/Heroicons)
- Appointment Booking — Let your AI handle scheduling, confirms, and calendar updates
- Call Transfer to Human — Seamless handoff when needed
- Direct PMS Integration — Writes directly to Open Dental, Dentrix, etc.
- Knowledge Base — Answers common clinic questions
- Multilingual Support — Serve patients in their language

**Right: Calendar Mockup**
- CSS-only calendar illustration showing September 2025
- Small card below: "Dr. Smith · 19 Appointments"

---

## Section 6: Support Levels

Three cards with subtle blue top border:

| L1: Frontline Queries | L2: Action Requests | L3: Complex Issues |
|-----------------------|---------------------|---------------------|
| AI handles common questions instantly — hours, location, services, insurance basics | Booking, rescheduling, cancellations routed directly to PMS | Escalates to staff; if unavailable, AI captures details for follow-up |

- Hover effect: slight lift with shadow increase
- Small CSS/SVG illustrations in each card

---

## Section 7: Integrations Grid

**Header:**
- "Integrations · 20+ tools"
- "Seamless data flow with your existing clinic software"

**Grid (4-column → 2-column mobile):**

| Open Dental | Dentrix | Eaglesoft | Curve Dental |
|-------------|---------|-----------|--------------|
| Practice Fusion | Google Calendar | | |

- Cards: white with subtle border
- Logo placeholder: colored square with initials (e.g., "OD" for Open Dental)
- Subtext: "AI Receptionist for [PMS] users"
- Hover: subtle blue border
- "See All Integrations" link below

---

## Section 8: Compliance Section

**Header:**
- "Compliance & Certification"
- "We have compliance certifications and protocols in place to ensure every patient interaction is private and secure."

**CTA:** "Book a Free Demo" button

**Trust Badges** (4 inline, muted colors):
- ISO 27001
- SOC 2 Type 2
- HIPAA
- GDPR

Badges are CSS boxes with shield/checkmark icons.

---

## Section 9: Final CTA

Blue gradient background (`linear-gradient(135deg, #2563EB 0%, #1D4ED8 100%)`)

**Content:**
- Headline: "Ready to Add AI Voice to Your Clinic?"
- Subtext: "Automate calls, handle more patients, and grow — with zero disruption to your current setup."
- CTA: White button with blue text — "Book a Free Demo"

**Feature Tags** (2x4 grid, white text, checkmark icons):
- 24/7 Call Handling
- Smart Appointment Booking
- Multilingual Support
- AI-Powered Receptionist
- Live Call Transfer
- Direct PMS Integration
- HIPAA Compliant
- No Workflow Changes

---

## Section 10: Footer

Light gray background (`--color-bg-subtle`)

**4-Column Link Grid:**

| Product | Use Cases | Resources | Company |
|---------|-----------|-----------|---------|
| Features | Dental Clinics | Blog | About |
| Integrations | Med Spas | Help Center | Contact |
| Pricing | Chiropractic | Case Studies | |
| Security | Aesthetic | | |

**Bottom Row:**
- © 2025 ClearDesk. All rights reserved.
- Privacy Policy · Terms of Service · HIPAA Compliance

---

## Technical Notes

### Tech Stack
- HTML + Tailwind CSS
- Google Fonts (Plus Jakarta Sans)
- Single-file component (index.html)
- No frameworks required

### Animations
- Hero rotating text: CSS keyframes with opacity fade
- Card hover: transform + shadow transition
- Scroll-triggered fade-ins (optional, CSS or minimal JS)

### Icons
- Lucide Icons or Heroicons (outline style)
- Consistent 24px size

### Responsive Strategy
- Mobile-first CSS
- Breakpoints: 640px, 1024px
- Stack columns on mobile, reduce padding
- Hamburger menu for nav on mobile
