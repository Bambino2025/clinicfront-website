# ClearDesk Homepage Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build a professional marketing homepage for ClearDesk AI receptionist product.

**Architecture:** Single HTML file with Tailwind CSS via CDN. All sections in one page, mobile-first responsive design. Minimal JavaScript for rotating hero text and mobile menu toggle.

**Tech Stack:** HTML, Tailwind CSS (CDN), Plus Jakarta Sans (Google Fonts), Lucide Icons (CDN)

---

## Task 1: Project Setup & Base HTML

**Files:**
- Create: `src/index.html`

**Step 1: Create base HTML structure with Tailwind and fonts**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>ClearDesk — AI Phone Answering for Private Clinics</title>
  <meta name="description" content="An AI receptionist that answers calls 24/7, books appointments, and writes directly into your existing scheduling software.">

  <!-- Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com"></script>

  <!-- Google Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700&display=swap" rel="stylesheet">

  <!-- Lucide Icons -->
  <script src="https://unpkg.com/lucide@latest/dist/umd/lucide.js"></script>

  <script>
    tailwind.config = {
      theme: {
        extend: {
          fontFamily: {
            sans: ['Plus Jakarta Sans', 'system-ui', 'sans-serif'],
          },
          colors: {
            primary: {
              DEFAULT: '#2563EB',
              dark: '#1D4ED8',
              light: '#DBEAFE',
            },
            text: {
              DEFAULT: '#1E293B',
              muted: '#64748B',
            },
            border: '#E2E8F0',
            subtle: '#F8FAFC',
          },
        },
      },
    }
  </script>

  <style>
    /* Hero rotating text animation */
    @keyframes fadeInOut {
      0%, 100% { opacity: 0; transform: translateY(10px); }
      10%, 90% { opacity: 1; transform: translateY(0); }
    }

    .rotate-text {
      animation: fadeInOut 3s ease-in-out infinite;
    }

    .rotate-text:nth-child(2) { animation-delay: 3s; }
    .rotate-text:nth-child(3) { animation-delay: 6s; }

    /* Only show one at a time */
    .rotating-container {
      position: relative;
      height: 2rem;
    }

    .rotating-container span {
      position: absolute;
      left: 50%;
      transform: translateX(-50%);
      opacity: 0;
    }
  </style>
</head>
<body class="font-sans text-text bg-white antialiased">

  <!-- Content will be added in subsequent tasks -->

  <script>
    // Initialize Lucide icons
    lucide.createIcons();
  </script>
</body>
</html>
```

**Step 2: Open in browser to verify setup**

Open `src/index.html` in a browser. Should see a blank white page with no console errors.

---

## Task 2: Navigation Bar

**Files:**
- Modify: `src/index.html`

**Step 1: Add navigation HTML after `<body>` tag**

```html
  <!-- Navigation -->
  <nav class="sticky top-0 z-50 bg-white border-b border-border">
    <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex items-center justify-between h-16">

        <!-- Logo -->
        <a href="/" class="text-xl font-bold text-primary">ClearDesk</a>

        <!-- Desktop Nav Links -->
        <div class="hidden md:flex items-center gap-8">
          <div class="relative group">
            <button class="flex items-center gap-1 text-text-muted hover:text-text transition-colors">
              Features
              <i data-lucide="chevron-down" class="w-4 h-4"></i>
            </button>
          </div>
          <div class="relative group">
            <button class="flex items-center gap-1 text-text-muted hover:text-text transition-colors">
              Use Cases
              <i data-lucide="chevron-down" class="w-4 h-4"></i>
            </button>
          </div>
          <div class="relative group">
            <button class="flex items-center gap-1 text-text-muted hover:text-text transition-colors">
              Resources
              <i data-lucide="chevron-down" class="w-4 h-4"></i>
            </button>
          </div>
          <a href="#pricing" class="text-text-muted hover:text-text transition-colors">Pricing</a>
        </div>

        <!-- Desktop CTAs -->
        <div class="hidden md:flex items-center gap-4">
          <a href="#contact" class="px-4 py-2 text-primary border border-primary rounded-lg hover:bg-primary-light transition-colors">
            Contact Sales
          </a>
          <a href="#login" class="text-text-muted hover:text-text transition-colors">
            Login
          </a>
        </div>

        <!-- Mobile Menu Button -->
        <button id="mobile-menu-btn" class="md:hidden p-2">
          <i data-lucide="menu" class="w-6 h-6"></i>
        </button>
      </div>
    </div>

    <!-- Mobile Menu (hidden by default) -->
    <div id="mobile-menu" class="hidden md:hidden border-t border-border bg-white">
      <div class="px-4 py-4 space-y-4">
        <a href="#features" class="block text-text-muted hover:text-text">Features</a>
        <a href="#use-cases" class="block text-text-muted hover:text-text">Use Cases</a>
        <a href="#resources" class="block text-text-muted hover:text-text">Resources</a>
        <a href="#pricing" class="block text-text-muted hover:text-text">Pricing</a>
        <hr class="border-border">
        <a href="#contact" class="block text-primary font-medium">Contact Sales</a>
        <a href="#login" class="block text-text-muted">Login</a>
      </div>
    </div>
  </nav>
```

**Step 2: Add mobile menu toggle script before closing `</body>`**

```html
  <script>
    // Initialize Lucide icons
    lucide.createIcons();

    // Mobile menu toggle
    const mobileMenuBtn = document.getElementById('mobile-menu-btn');
    const mobileMenu = document.getElementById('mobile-menu');

    mobileMenuBtn.addEventListener('click', () => {
      mobileMenu.classList.toggle('hidden');
    });
  </script>
```

**Step 3: Verify in browser**

- Desktop: Logo left, nav links center, CTAs right
- Mobile (< 768px): Logo left, hamburger right, menu toggles on click

---

## Task 3: Hero Section

**Files:**
- Modify: `src/index.html`

**Step 1: Add hero section after `</nav>`**

```html
  <!-- Hero Section -->
  <section class="py-20 md:py-32">
    <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 text-center">

      <!-- Rotating Text -->
      <div class="mb-6">
        <div class="inline-flex items-center gap-2 text-primary text-sm font-medium tracking-wide">
          <span class="w-2 h-2 bg-primary rounded-full animate-pulse"></span>
          <span id="rotating-text">Appointment Booking</span>
        </div>
      </div>

      <!-- Main Headline -->
      <h1 class="text-4xl md:text-5xl lg:text-6xl font-bold text-text leading-tight mb-6">
        AI Phone Answering<br>for Private Clinics
      </h1>

      <!-- Subtext -->
      <p class="text-lg md:text-xl text-text-muted max-w-2xl mx-auto mb-10">
        An AI receptionist that answers calls 24/7, books appointments, and writes directly into your existing scheduling software.
      </p>

      <!-- CTA Button -->
      <a href="#demo" class="inline-flex items-center gap-2 px-8 py-4 bg-primary text-white font-semibold rounded-lg hover:bg-primary-dark transition-colors shadow-lg shadow-primary/25">
        Book a Free Demo
        <i data-lucide="arrow-right" class="w-5 h-5"></i>
      </a>

    </div>
  </section>
```

**Step 2: Add rotating text JavaScript (update the script section)**

```html
  <script>
    // Initialize Lucide icons
    lucide.createIcons();

    // Mobile menu toggle
    const mobileMenuBtn = document.getElementById('mobile-menu-btn');
    const mobileMenu = document.getElementById('mobile-menu');

    mobileMenuBtn.addEventListener('click', () => {
      mobileMenu.classList.toggle('hidden');
    });

    // Rotating hero text
    const rotatingTexts = [
      'Appointment Booking',
      'Patient Questions',
      'After-Hours Calls',
      'Recall Reminders',
      'Rescheduling Requests'
    ];
    let currentIndex = 0;
    const rotatingElement = document.getElementById('rotating-text');

    setInterval(() => {
      rotatingElement.style.opacity = '0';
      rotatingElement.style.transform = 'translateY(-10px)';

      setTimeout(() => {
        currentIndex = (currentIndex + 1) % rotatingTexts.length;
        rotatingElement.textContent = rotatingTexts[currentIndex];
        rotatingElement.style.opacity = '1';
        rotatingElement.style.transform = 'translateY(0)';
      }, 300);
    }, 3000);
  </script>
```

**Step 3: Add transition styles to rotating text element**

Update the rotating text span in the hero:

```html
          <span id="rotating-text" class="transition-all duration-300">Appointment Booking</span>
```

**Step 4: Verify in browser**

- Centered content
- Text rotates every 3 seconds with fade effect
- Blue CTA button with hover state

---

## Task 4: Video Section

**Files:**
- Modify: `src/index.html`

**Step 1: Add video section after hero**

```html
  <!-- Video Section -->
  <section class="py-16 md:py-24 bg-subtle">
    <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="grid md:grid-cols-2 gap-12 items-center">

        <!-- Video Thumbnail -->
        <div class="relative group cursor-pointer">
          <div class="aspect-video bg-gradient-to-br from-primary to-primary-dark rounded-2xl flex items-center justify-center shadow-xl">
            <div class="text-center text-white">
              <div class="w-20 h-20 mx-auto mb-4 bg-white/20 rounded-full flex items-center justify-center group-hover:bg-white/30 transition-colors">
                <i data-lucide="play" class="w-10 h-10 fill-white text-white"></i>
              </div>
              <p class="text-lg font-medium">See ClearDesk in Action</p>
            </div>
          </div>
        </div>

        <!-- Feature Bullets -->
        <div class="space-y-6">
          <h2 class="text-2xl md:text-3xl font-bold text-text">
            How AI Voice Is Transforming Clinics
          </h2>

          <ul class="space-y-4">
            <li class="flex items-start gap-3">
              <div class="w-6 h-6 rounded-full bg-primary-light flex items-center justify-center flex-shrink-0 mt-0.5">
                <i data-lucide="check" class="w-4 h-4 text-primary"></i>
              </div>
              <span class="text-text-muted">Recall Reminders — Automated outreach to bring patients back</span>
            </li>
            <li class="flex items-start gap-3">
              <div class="w-6 h-6 rounded-full bg-primary-light flex items-center justify-center flex-shrink-0 mt-0.5">
                <i data-lucide="check" class="w-4 h-4 text-primary"></i>
              </div>
              <span class="text-text-muted">After-Hours Handling — Never miss a call, even at 2am</span>
            </li>
            <li class="flex items-start gap-3">
              <div class="w-6 h-6 rounded-full bg-primary-light flex items-center justify-center flex-shrink-0 mt-0.5">
                <i data-lucide="check" class="w-4 h-4 text-primary"></i>
              </div>
              <span class="text-text-muted">Appointment Booking — Books directly into your PMS</span>
            </li>
            <li class="flex items-start gap-3">
              <div class="w-6 h-6 rounded-full bg-primary-light flex items-center justify-center flex-shrink-0 mt-0.5">
                <i data-lucide="check" class="w-4 h-4 text-primary"></i>
              </div>
              <span class="text-text-muted">Fill Last-Minute Cancellations — AI calls waitlist patients</span>
            </li>
            <li class="flex items-start gap-3">
              <div class="w-6 h-6 rounded-full bg-primary-light flex items-center justify-center flex-shrink-0 mt-0.5">
                <i data-lucide="check" class="w-4 h-4 text-primary"></i>
              </div>
              <span class="text-text-muted">Reduce No-Shows — SMS confirmations and reminders</span>
            </li>
          </ul>
        </div>

      </div>
    </div>
  </section>
```

**Step 2: Verify in browser**

- Two columns on desktop, stacked on mobile
- Video placeholder with play button
- Bullet list with check icons

---

## Task 5: Channels Section

**Files:**
- Modify: `src/index.html`

**Step 1: Add channels section after video section**

```html
  <!-- Channels Section -->
  <section class="py-16 md:py-24 bg-primary-light">
    <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">

      <!-- Header -->
      <div class="text-center mb-12">
        <h2 class="text-3xl md:text-4xl font-bold text-text mb-4">
          Capturing Every Conversation
        </h2>
        <p class="text-lg text-text-muted">
          <span class="font-semibold text-primary">80% resolved by AI.</span> 20% ready for human action.
        </p>
      </div>

      <!-- Channel Cards -->
      <div class="grid sm:grid-cols-2 lg:grid-cols-4 gap-6">

        <!-- Phone Calls -->
        <div class="bg-white rounded-xl p-6 shadow-sm hover:shadow-md transition-shadow">
          <div class="w-12 h-12 bg-primary-light rounded-lg flex items-center justify-center mb-4">
            <i data-lucide="phone" class="w-6 h-6 text-primary"></i>
          </div>
          <h3 class="text-lg font-semibold text-text mb-2">Phone Calls</h3>
          <p class="text-sm text-text-muted">Human-like voice, call actions, seamless transfers to staff when needed.</p>
        </div>

        <!-- Website Voice Bot -->
        <div class="bg-white rounded-xl p-6 shadow-sm hover:shadow-md transition-shadow">
          <div class="w-12 h-12 bg-primary-light rounded-lg flex items-center justify-center mb-4">
            <i data-lucide="bot" class="w-6 h-6 text-primary"></i>
          </div>
          <h3 class="text-lg font-semibold text-text mb-2">Website Voice Bot</h3>
          <p class="text-sm text-text-muted">Real-time voice chat on your website for lead capture and booking.</p>
        </div>

        <!-- Share Link -->
        <div class="bg-white rounded-xl p-6 shadow-sm hover:shadow-md transition-shadow">
          <div class="w-12 h-12 bg-primary-light rounded-lg flex items-center justify-center mb-4">
            <i data-lucide="link" class="w-6 h-6 text-primary"></i>
          </div>
          <h3 class="text-lg font-semibold text-text mb-2">Share Link</h3>
          <p class="text-sm text-text-muted">Shareable link opens a live AI assistant for patients anywhere.</p>
        </div>

        <!-- SMS -->
        <div class="bg-white rounded-xl p-6 shadow-sm hover:shadow-md transition-shadow relative">
          <span class="absolute top-4 right-4 text-xs font-medium text-text-muted bg-subtle px-2 py-1 rounded">Coming Soon</span>
          <div class="w-12 h-12 bg-primary-light rounded-lg flex items-center justify-center mb-4">
            <i data-lucide="message-square" class="w-6 h-6 text-primary"></i>
          </div>
          <h3 class="text-lg font-semibold text-text mb-2">SMS</h3>
          <p class="text-sm text-text-muted">Automated reminders and two-way scheduling via text message.</p>
        </div>

      </div>

      <!-- CTA -->
      <div class="text-center mt-10">
        <a href="#demo" class="inline-flex items-center gap-2 px-6 py-3 bg-primary text-white font-semibold rounded-lg hover:bg-primary-dark transition-colors">
          Get Started Now
          <i data-lucide="arrow-right" class="w-5 h-5"></i>
        </a>
      </div>

    </div>
  </section>
```

**Step 2: Verify in browser**

- Light blue background
- 4-column grid on desktop, 2 on tablet, 1 on mobile
- SMS card has "Coming Soon" badge

---

## Task 6: Features Section

**Files:**
- Modify: `src/index.html`

**Step 1: Add features section after channels**

```html
  <!-- Features Section -->
  <section class="py-16 md:py-24">
    <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">

      <!-- Header -->
      <div class="text-center mb-12">
        <h2 class="text-3xl md:text-4xl font-bold text-text mb-4">
          Value-Added Features of Our Voice AI Agent
        </h2>
        <p class="text-lg text-text-muted max-w-2xl mx-auto">
          Our AI handles real clinic tasks—like booking appointments and syncing with your PMS—automatically and intelligently.
        </p>
      </div>

      <div class="grid lg:grid-cols-2 gap-12 items-center">

        <!-- Feature List -->
        <div class="space-y-6">

          <div class="flex items-start gap-4 p-4 rounded-lg hover:bg-subtle transition-colors">
            <div class="w-10 h-10 bg-primary-light rounded-lg flex items-center justify-center flex-shrink-0">
              <i data-lucide="calendar" class="w-5 h-5 text-primary"></i>
            </div>
            <div>
              <h3 class="font-semibold text-text mb-1">Appointment Booking</h3>
              <p class="text-sm text-text-muted">Let your AI handle scheduling, confirmations, and calendar updates in real time.</p>
            </div>
          </div>

          <div class="flex items-start gap-4 p-4 rounded-lg hover:bg-subtle transition-colors">
            <div class="w-10 h-10 bg-primary-light rounded-lg flex items-center justify-center flex-shrink-0">
              <i data-lucide="phone-forwarded" class="w-5 h-5 text-primary"></i>
            </div>
            <div>
              <h3 class="font-semibold text-text mb-1">Call Transfer to Human</h3>
              <p class="text-sm text-text-muted">Seamless handoff to your staff when patients need personal attention.</p>
            </div>
          </div>

          <div class="flex items-start gap-4 p-4 rounded-lg hover:bg-subtle transition-colors">
            <div class="w-10 h-10 bg-primary-light rounded-lg flex items-center justify-center flex-shrink-0">
              <i data-lucide="zap" class="w-5 h-5 text-primary"></i>
            </div>
            <div>
              <h3 class="font-semibold text-text mb-1">Direct PMS Integration</h3>
              <p class="text-sm text-text-muted">Writes directly to Open Dental, Dentrix, Eaglesoft, and more.</p>
            </div>
          </div>

          <div class="flex items-start gap-4 p-4 rounded-lg hover:bg-subtle transition-colors">
            <div class="w-10 h-10 bg-primary-light rounded-lg flex items-center justify-center flex-shrink-0">
              <i data-lucide="book-open" class="w-5 h-5 text-primary"></i>
            </div>
            <div>
              <h3 class="font-semibold text-text mb-1">Knowledge Base</h3>
              <p class="text-sm text-text-muted">Answers common questions about hours, location, services, and insurance.</p>
            </div>
          </div>

          <div class="flex items-start gap-4 p-4 rounded-lg hover:bg-subtle transition-colors">
            <div class="w-10 h-10 bg-primary-light rounded-lg flex items-center justify-center flex-shrink-0">
              <i data-lucide="globe" class="w-5 h-5 text-primary"></i>
            </div>
            <div>
              <h3 class="font-semibold text-text mb-1">Multilingual Support</h3>
              <p class="text-sm text-text-muted">Serve patients in their preferred language automatically.</p>
            </div>
          </div>

        </div>

        <!-- Calendar Mockup -->
        <div class="bg-subtle rounded-2xl p-8">

          <!-- Calendar -->
          <div class="bg-white rounded-xl p-6 shadow-sm mb-6">
            <div class="flex items-center justify-between mb-4">
              <h4 class="font-semibold text-text">September 2025</h4>
              <div class="flex gap-2">
                <button class="p-1 hover:bg-subtle rounded">
                  <i data-lucide="chevron-left" class="w-4 h-4 text-text-muted"></i>
                </button>
                <button class="p-1 hover:bg-subtle rounded">
                  <i data-lucide="chevron-right" class="w-4 h-4 text-text-muted"></i>
                </button>
              </div>
            </div>

            <div class="grid grid-cols-7 gap-1 text-center text-sm">
              <span class="text-text-muted font-medium py-2">S</span>
              <span class="text-text-muted font-medium py-2">M</span>
              <span class="text-text-muted font-medium py-2">T</span>
              <span class="text-text-muted font-medium py-2">W</span>
              <span class="text-text-muted font-medium py-2">T</span>
              <span class="text-text-muted font-medium py-2">F</span>
              <span class="text-text-muted font-medium py-2">S</span>

              <span class="py-2"></span>
              <span class="py-2 text-text-muted">1</span>
              <span class="py-2 text-text-muted">2</span>
              <span class="py-2 text-text-muted">3</span>
              <span class="py-2 text-text-muted">4</span>
              <span class="py-2 text-text-muted">5</span>
              <span class="py-2 text-text-muted">6</span>

              <span class="py-2 text-text-muted">7</span>
              <span class="py-2 text-text-muted">8</span>
              <span class="py-2 text-text-muted">9</span>
              <span class="py-2 text-text-muted">10</span>
              <span class="py-2 text-text-muted">11</span>
              <span class="py-2 text-text-muted">12</span>
              <span class="py-2 text-text-muted">13</span>

              <span class="py-2 text-text-muted">14</span>
              <span class="py-2 text-text-muted">15</span>
              <span class="py-2 text-text-muted">16</span>
              <span class="py-2 text-text-muted">17</span>
              <span class="py-2 text-text-muted">18</span>
              <span class="py-2 w-8 h-8 bg-primary text-white rounded-full flex items-center justify-center mx-auto">19</span>
              <span class="py-2 text-text-muted">20</span>

              <span class="py-2 text-text-muted">21</span>
              <span class="py-2 text-text-muted">22</span>
              <span class="py-2 text-text-muted">23</span>
              <span class="py-2 text-text-muted">24</span>
              <span class="py-2 text-text-muted">25</span>
              <span class="py-2 text-text-muted">26</span>
              <span class="py-2 text-text-muted">27</span>

              <span class="py-2 text-text-muted">28</span>
              <span class="py-2 text-text-muted">29</span>
              <span class="py-2 text-text-muted">30</span>
            </div>
          </div>

          <!-- Appointment Card -->
          <div class="bg-white rounded-xl p-4 shadow-sm flex items-center gap-4">
            <div class="w-12 h-12 bg-primary-light rounded-full flex items-center justify-center">
              <i data-lucide="user" class="w-6 h-6 text-primary"></i>
            </div>
            <div>
              <p class="font-semibold text-text">Dr. Smith</p>
              <p class="text-sm text-text-muted">19 Appointments booked by AI</p>
            </div>
          </div>

        </div>

      </div>
    </div>
  </section>
```

**Step 2: Verify in browser**

- Two columns on desktop
- Feature list with icons on left
- Calendar mockup on right
- Day 19 highlighted in blue

---

## Task 7: Support Levels Section

**Files:**
- Modify: `src/index.html`

**Step 1: Add support section after features**

```html
  <!-- Support Levels Section -->
  <section class="py-16 md:py-24 bg-subtle">
    <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">

      <!-- Header -->
      <div class="text-center mb-12">
        <h2 class="text-3xl md:text-4xl font-bold text-text mb-4">
          Streamline Patient Support with ClearDesk
        </h2>
        <p class="text-lg text-text-muted max-w-2xl mx-auto">
          Transform patient support with an advanced AI-powered receptionist that combines speed, flexibility, and ease of use.
        </p>
      </div>

      <!-- Support Cards -->
      <div class="grid md:grid-cols-3 gap-8">

        <!-- L1 Support -->
        <div class="bg-white rounded-xl overflow-hidden shadow-sm hover:shadow-lg hover:-translate-y-1 transition-all">
          <div class="h-1 bg-primary"></div>
          <div class="p-6">
            <div class="w-14 h-14 bg-primary-light rounded-xl flex items-center justify-center mb-4">
              <i data-lucide="headphones" class="w-7 h-7 text-primary"></i>
            </div>
            <h3 class="text-xl font-bold text-text mb-2">L1 Support</h3>
            <p class="text-sm font-medium text-primary mb-3">Frontline Queries</p>
            <p class="text-text-muted">
              Entirely powered by AI, ensuring quick responses and precise solutions for common questions about hours, location, services, and insurance.
            </p>
          </div>
        </div>

        <!-- L2 Support -->
        <div class="bg-white rounded-xl overflow-hidden shadow-sm hover:shadow-lg hover:-translate-y-1 transition-all">
          <div class="h-1 bg-primary"></div>
          <div class="p-6">
            <div class="w-14 h-14 bg-primary-light rounded-xl flex items-center justify-center mb-4">
              <i data-lucide="calendar-check" class="w-7 h-7 text-primary"></i>
            </div>
            <h3 class="text-xl font-bold text-text mb-2">L2 Support</h3>
            <p class="text-sm font-medium text-primary mb-3">Action Requests</p>
            <p class="text-text-muted">
              From booking to rescheduling, AI takes care of task-based requests and routes them directly to your practice management system.
            </p>
          </div>
        </div>

        <!-- L3 Support -->
        <div class="bg-white rounded-xl overflow-hidden shadow-sm hover:shadow-lg hover:-translate-y-1 transition-all">
          <div class="h-1 bg-primary"></div>
          <div class="p-6">
            <div class="w-14 h-14 bg-primary-light rounded-xl flex items-center justify-center mb-4">
              <i data-lucide="users" class="w-7 h-7 text-primary"></i>
            </div>
            <h3 class="text-xl font-bold text-text mb-2">L3 Support</h3>
            <p class="text-sm font-medium text-primary mb-3">Complex Issues</p>
            <p class="text-text-muted">
              Complex issues are escalated to your staff. If unavailable, AI captures all details and schedules a follow-up.
            </p>
          </div>
        </div>

      </div>
    </div>
  </section>
```

**Step 2: Verify in browser**

- Three cards in a row on desktop
- Blue top border on each card
- Hover effect: lift and shadow increase

---

## Task 8: Integrations Section

**Files:**
- Modify: `src/index.html`

**Step 1: Add integrations section after support**

```html
  <!-- Integrations Section -->
  <section class="py-16 md:py-24">
    <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">

      <!-- Header -->
      <div class="text-center mb-12">
        <h2 class="text-3xl md:text-4xl font-bold text-text mb-4">
          Integrations <span class="text-text-muted font-normal">· 20+ tools</span>
        </h2>
        <p class="text-lg text-text-muted">
          Seamless data flow with your existing clinic software.
        </p>
      </div>

      <!-- Integration Cards -->
      <div class="grid sm:grid-cols-2 lg:grid-cols-3 gap-6 mb-10">

        <!-- Open Dental -->
        <div class="bg-white border border-border rounded-xl p-6 hover:border-primary transition-colors group">
          <div class="flex items-center gap-4 mb-4">
            <div class="w-12 h-12 bg-blue-100 rounded-lg flex items-center justify-center text-blue-600 font-bold text-lg">
              OD
            </div>
            <h3 class="font-semibold text-text">Open Dental</h3>
          </div>
          <p class="text-sm text-text-muted">AI Receptionist for Open Dental users</p>
        </div>

        <!-- Dentrix -->
        <div class="bg-white border border-border rounded-xl p-6 hover:border-primary transition-colors group">
          <div class="flex items-center gap-4 mb-4">
            <div class="w-12 h-12 bg-green-100 rounded-lg flex items-center justify-center text-green-600 font-bold text-lg">
              DX
            </div>
            <h3 class="font-semibold text-text">Dentrix</h3>
          </div>
          <p class="text-sm text-text-muted">AI Receptionist for Dentrix users</p>
        </div>

        <!-- Eaglesoft -->
        <div class="bg-white border border-border rounded-xl p-6 hover:border-primary transition-colors group">
          <div class="flex items-center gap-4 mb-4">
            <div class="w-12 h-12 bg-orange-100 rounded-lg flex items-center justify-center text-orange-600 font-bold text-lg">
              ES
            </div>
            <h3 class="font-semibold text-text">Eaglesoft</h3>
          </div>
          <p class="text-sm text-text-muted">AI Receptionist for Eaglesoft users</p>
        </div>

        <!-- Curve Dental -->
        <div class="bg-white border border-border rounded-xl p-6 hover:border-primary transition-colors group">
          <div class="flex items-center gap-4 mb-4">
            <div class="w-12 h-12 bg-purple-100 rounded-lg flex items-center justify-center text-purple-600 font-bold text-lg">
              CD
            </div>
            <h3 class="font-semibold text-text">Curve Dental</h3>
          </div>
          <p class="text-sm text-text-muted">AI Receptionist for Curve users</p>
        </div>

        <!-- Practice Fusion -->
        <div class="bg-white border border-border rounded-xl p-6 hover:border-primary transition-colors group">
          <div class="flex items-center gap-4 mb-4">
            <div class="w-12 h-12 bg-teal-100 rounded-lg flex items-center justify-center text-teal-600 font-bold text-lg">
              PF
            </div>
            <h3 class="font-semibold text-text">Practice Fusion</h3>
          </div>
          <p class="text-sm text-text-muted">AI Receptionist for Practice Fusion users</p>
        </div>

        <!-- Google Calendar -->
        <div class="bg-white border border-border rounded-xl p-6 hover:border-primary transition-colors group">
          <div class="flex items-center gap-4 mb-4">
            <div class="w-12 h-12 bg-red-100 rounded-lg flex items-center justify-center text-red-600 font-bold text-lg">
              GC
            </div>
            <h3 class="font-semibold text-text">Google Calendar</h3>
          </div>
          <p class="text-sm text-text-muted">AI Receptionist for Google Calendar users</p>
        </div>

      </div>

      <!-- See All Link -->
      <div class="text-center">
        <a href="#integrations" class="inline-flex items-center gap-2 text-primary font-medium hover:underline">
          See All Integrations
          <i data-lucide="arrow-right" class="w-4 h-4"></i>
        </a>
      </div>

    </div>
  </section>
```

**Step 2: Verify in browser**

- 3-column grid on desktop
- Each card has colored initials as logo placeholder
- Hover shows blue border

---

## Task 9: Compliance Section

**Files:**
- Modify: `src/index.html`

**Step 1: Add compliance section after integrations**

```html
  <!-- Compliance Section -->
  <section class="py-16 md:py-24 bg-subtle">
    <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">

      <div class="flex flex-col lg:flex-row items-center justify-between gap-10">

        <!-- Left Content -->
        <div class="lg:max-w-lg">
          <h2 class="text-3xl md:text-4xl font-bold text-text mb-4">
            Compliance & Certification
          </h2>
          <p class="text-lg text-text-muted mb-6">
            We have compliance certifications and protocols in place to ensure every patient interaction is private and secure.
          </p>
          <a href="#demo" class="inline-flex items-center gap-2 px-6 py-3 bg-primary text-white font-semibold rounded-lg hover:bg-primary-dark transition-colors">
            Book a Free Demo
            <i data-lucide="arrow-right" class="w-5 h-5"></i>
          </a>
        </div>

        <!-- Trust Badges -->
        <div class="flex flex-wrap items-center justify-center gap-4">

          <div class="bg-white border border-border rounded-lg px-6 py-4 flex items-center gap-3">
            <i data-lucide="shield-check" class="w-6 h-6 text-text-muted"></i>
            <div>
              <p class="font-semibold text-text text-sm">ISO 27001</p>
              <p class="text-xs text-text-muted">Certified</p>
            </div>
          </div>

          <div class="bg-white border border-border rounded-lg px-6 py-4 flex items-center gap-3">
            <i data-lucide="shield-check" class="w-6 h-6 text-text-muted"></i>
            <div>
              <p class="font-semibold text-text text-sm">SOC 2 Type 2</p>
              <p class="text-xs text-text-muted">Compliant</p>
            </div>
          </div>

          <div class="bg-white border border-border rounded-lg px-6 py-4 flex items-center gap-3">
            <i data-lucide="shield-check" class="w-6 h-6 text-text-muted"></i>
            <div>
              <p class="font-semibold text-text text-sm">HIPAA</p>
              <p class="text-xs text-text-muted">Compliant</p>
            </div>
          </div>

          <div class="bg-white border border-border rounded-lg px-6 py-4 flex items-center gap-3">
            <i data-lucide="shield-check" class="w-6 h-6 text-text-muted"></i>
            <div>
              <p class="font-semibold text-text text-sm">GDPR</p>
              <p class="text-xs text-text-muted">Compliant</p>
            </div>
          </div>

        </div>

      </div>
    </div>
  </section>
```

**Step 2: Verify in browser**

- Two-column layout: text left, badges right
- Badges have shield icons
- Responsive stacking on mobile

---

## Task 10: Final CTA Section

**Files:**
- Modify: `src/index.html`

**Step 1: Add final CTA section after compliance**

```html
  <!-- Final CTA Section -->
  <section class="py-16 md:py-24 bg-gradient-to-br from-primary to-primary-dark">
    <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 text-center">

      <!-- Content -->
      <h2 class="text-3xl md:text-4xl font-bold text-white mb-4">
        Ready to Add AI Voice to Your Clinic?
      </h2>
      <p class="text-lg text-white/80 mb-8">
        Automate calls, handle more patients, and grow — with zero disruption to your current setup.
      </p>

      <!-- CTA Button -->
      <a href="#demo" class="inline-flex items-center gap-2 px-8 py-4 bg-white text-primary font-semibold rounded-lg hover:bg-gray-100 transition-colors shadow-lg">
        Book a Free Demo
        <i data-lucide="arrow-right" class="w-5 h-5"></i>
      </a>

      <!-- Divider -->
      <div class="my-12 border-t border-white/20"></div>

      <!-- Feature Tags -->
      <div class="grid grid-cols-2 md:grid-cols-4 gap-4 text-white/90 text-sm">
        <div class="flex items-center justify-center gap-2">
          <i data-lucide="check" class="w-4 h-4"></i>
          <span>24/7 Call Handling</span>
        </div>
        <div class="flex items-center justify-center gap-2">
          <i data-lucide="check" class="w-4 h-4"></i>
          <span>Smart Booking</span>
        </div>
        <div class="flex items-center justify-center gap-2">
          <i data-lucide="check" class="w-4 h-4"></i>
          <span>Multilingual</span>
        </div>
        <div class="flex items-center justify-center gap-2">
          <i data-lucide="check" class="w-4 h-4"></i>
          <span>AI Receptionist</span>
        </div>
        <div class="flex items-center justify-center gap-2">
          <i data-lucide="check" class="w-4 h-4"></i>
          <span>Live Transfer</span>
        </div>
        <div class="flex items-center justify-center gap-2">
          <i data-lucide="check" class="w-4 h-4"></i>
          <span>PMS Integration</span>
        </div>
        <div class="flex items-center justify-center gap-2">
          <i data-lucide="check" class="w-4 h-4"></i>
          <span>HIPAA Compliant</span>
        </div>
        <div class="flex items-center justify-center gap-2">
          <i data-lucide="check" class="w-4 h-4"></i>
          <span>No Workflow Changes</span>
        </div>
      </div>

    </div>
  </section>
```

**Step 2: Verify in browser**

- Blue gradient background
- White text and button
- Feature tags in 4-column grid

---

## Task 11: Footer

**Files:**
- Modify: `src/index.html`

**Step 1: Add footer before closing `</body>` tag (before scripts)**

```html
  <!-- Footer -->
  <footer class="bg-subtle border-t border-border">
    <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 py-12">

      <!-- Footer Grid -->
      <div class="grid grid-cols-2 md:grid-cols-4 gap-8 mb-12">

        <!-- Product -->
        <div>
          <h4 class="font-semibold text-text mb-4">Product</h4>
          <ul class="space-y-3">
            <li><a href="#features" class="text-text-muted hover:text-text transition-colors">Features</a></li>
            <li><a href="#integrations" class="text-text-muted hover:text-text transition-colors">Integrations</a></li>
            <li><a href="#pricing" class="text-text-muted hover:text-text transition-colors">Pricing</a></li>
            <li><a href="#security" class="text-text-muted hover:text-text transition-colors">Security</a></li>
          </ul>
        </div>

        <!-- Use Cases -->
        <div>
          <h4 class="font-semibold text-text mb-4">Use Cases</h4>
          <ul class="space-y-3">
            <li><a href="#dental" class="text-text-muted hover:text-text transition-colors">Dental Clinics</a></li>
            <li><a href="#medspa" class="text-text-muted hover:text-text transition-colors">Med Spas</a></li>
            <li><a href="#chiro" class="text-text-muted hover:text-text transition-colors">Chiropractic</a></li>
            <li><a href="#aesthetic" class="text-text-muted hover:text-text transition-colors">Aesthetic</a></li>
          </ul>
        </div>

        <!-- Resources -->
        <div>
          <h4 class="font-semibold text-text mb-4">Resources</h4>
          <ul class="space-y-3">
            <li><a href="#blog" class="text-text-muted hover:text-text transition-colors">Blog</a></li>
            <li><a href="#help" class="text-text-muted hover:text-text transition-colors">Help Center</a></li>
            <li><a href="#cases" class="text-text-muted hover:text-text transition-colors">Case Studies</a></li>
          </ul>
        </div>

        <!-- Company -->
        <div>
          <h4 class="font-semibold text-text mb-4">Company</h4>
          <ul class="space-y-3">
            <li><a href="#about" class="text-text-muted hover:text-text transition-colors">About</a></li>
            <li><a href="#contact" class="text-text-muted hover:text-text transition-colors">Contact</a></li>
          </ul>
        </div>

      </div>

      <!-- Bottom Row -->
      <div class="pt-8 border-t border-border flex flex-col md:flex-row items-center justify-between gap-4">

        <div class="flex items-center gap-2">
          <span class="text-xl font-bold text-primary">ClearDesk</span>
        </div>

        <p class="text-sm text-text-muted">
          &copy; 2025 ClearDesk. All rights reserved.
        </p>

        <div class="flex items-center gap-6 text-sm">
          <a href="#privacy" class="text-text-muted hover:text-text transition-colors">Privacy Policy</a>
          <a href="#terms" class="text-text-muted hover:text-text transition-colors">Terms of Service</a>
          <a href="#hipaa" class="text-text-muted hover:text-text transition-colors">HIPAA Compliance</a>
        </div>

      </div>
    </div>
  </footer>
```

**Step 2: Verify in browser**

- 4-column link grid
- Logo, copyright, legal links at bottom
- Light gray background

---

## Task 12: Final Review & Polish

**Files:**
- Modify: `src/index.html`

**Step 1: Re-initialize Lucide icons**

Make sure the script at the bottom properly initializes all icons:

```html
  <script>
    // Initialize Lucide icons
    lucide.createIcons();

    // Mobile menu toggle
    const mobileMenuBtn = document.getElementById('mobile-menu-btn');
    const mobileMenu = document.getElementById('mobile-menu');

    if (mobileMenuBtn && mobileMenu) {
      mobileMenuBtn.addEventListener('click', () => {
        mobileMenu.classList.toggle('hidden');
      });
    }

    // Rotating hero text
    const rotatingTexts = [
      'Appointment Booking',
      'Patient Questions',
      'After-Hours Calls',
      'Recall Reminders',
      'Rescheduling Requests'
    ];
    let currentIndex = 0;
    const rotatingElement = document.getElementById('rotating-text');

    if (rotatingElement) {
      setInterval(() => {
        rotatingElement.style.opacity = '0';
        rotatingElement.style.transform = 'translateY(-10px)';

        setTimeout(() => {
          currentIndex = (currentIndex + 1) % rotatingTexts.length;
          rotatingElement.textContent = rotatingTexts[currentIndex];
          rotatingElement.style.opacity = '1';
          rotatingElement.style.transform = 'translateY(0)';
        }, 300);
      }, 3000);
    }
  </script>
```

**Step 2: Test responsive behavior**

- Desktop (1200px+): Full layout
- Tablet (768-1024px): 2-column grids
- Mobile (<768px): Single column, hamburger menu

**Step 3: Verify all sections render correctly**

Scroll through entire page and check:
- [ ] Nav sticky and functional
- [ ] Hero text rotates
- [ ] Video section layout correct
- [ ] Channel cards display properly
- [ ] Features section two-column
- [ ] Support cards have hover effects
- [ ] Integration cards show colored initials
- [ ] Compliance badges display
- [ ] Final CTA has gradient
- [ ] Footer links organized

---

## Summary

| Task | Section | Status |
|------|---------|--------|
| 1 | Project Setup | |
| 2 | Navigation Bar | |
| 3 | Hero Section | |
| 4 | Video Section | |
| 5 | Channels Section | |
| 6 | Features Section | |
| 7 | Support Levels | |
| 8 | Integrations | |
| 9 | Compliance | |
| 10 | Final CTA | |
| 11 | Footer | |
| 12 | Final Review | |
