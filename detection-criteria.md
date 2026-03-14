# Was This Site Vibecoded? A Forensic Guide

A checklist for identifying websites built by AI coding agents (Cursor, Claude Code, Lovable, Bolt, v0, Windsurf, Replit, etc.). These tools overwhelmingly default to the same visual stack — React, Tailwind CSS, shadcn/ui, Lucide icons, Framer Motion — producing a recognizable aesthetic. Use this guide to inspect any site and determine whether it was AI-generated, AI-assisted, or human-built based on 42 visual and code-level tells.

**If a site hits 10+, it was almost certainly AI-generated.**

---

## The "Every AI App Looks the Same" Starter Pack

These are the libraries responsible for the vibecoded aesthetic. Each one is fine individually — the problem is AI tools install all of them together, every time, producing identical-looking sites.

- **shadcn/ui** — the single biggest culprit. Every AI tool defaults to it. Identical gray cards, identical rounded corners, identical command palettes
- **Tailwind CSS** — not slop by itself, but AI generates the same `bg-white rounded-xl shadow-sm p-6` patterns endlessly
- **Lucide React** — same 1,400 icons on every vibecoded site. The thin-stroke aesthetic is now synonymous with AI output
- **Framer Motion** — same fade-up-on-scroll, same spring physics, same `whileHover={{ scale: 1.05 }}`
- **Recharts** — every dashboard has the same soft-gradient area chart with rounded tooltips
- **Sonner** — identical bottom-right toast on every app
- **cmdk** — same ⌘K command palette. Every vibecoded SaaS has one whether it needs it or not
- **Radix UI** — the invisible skeleton. Same dialog animations, same dropdown behavior, same sheet sliding in from the right
- **class-variance-authority** — why every button has the same `variant="outline"` / `variant="ghost"` / `variant="destructive"` taxonomy
- **next-themes** — same sun/moon toggle in the top-right corner
- **vaul** — same bottom drawer on mobile
- **embla-carousel-react** — same horizontal scroll testimonial carousel
- **React Day Picker** — same calendar popup for date selection
- **@tanstack/react-table** — same sortable data table with pagination dots
- **tw-animate-css** — same `animate-in fade-in slide-in-from-bottom` entrance on every section
- **Inter font** (not a lib but worth mentioning) — Anthropic's own blog admits Claude defaults to Inter + purple gradients without intervention

---

## 1. Typography

- [ ] **Inter font** — the #1 giveaway. AI defaults to Inter unless told otherwise
- [ ] **Geist or Geist Mono** — second most common. Vercel's font, v0 loves it
- [ ] `text-sm` body text (14px) with `text-muted-foreground` gray (#71717a or similar)
- [ ] Headings use `tracking-tight` with `font-bold` — never font-black, never font-medium
- [ ] No custom font pairing. One font family for everything
- [ ] Section headers follow the exact pattern: small uppercase colored label → large bold heading → gray subtext paragraph

## 2. Color & Theme

- [ ] **Purple-to-blue gradient** as primary accent — Claude/Sonnet's default aesthetic
- [ ] HSL color variables in `:root` following shadcn's exact naming: `--background`, `--foreground`, `--primary`, `--muted`, `--accent`, `--destructive`
- [ ] **Zinc/Slate gray palette** — not neutral gray, specifically Tailwind's zinc scale
- [ ] Dark mode is pure `zinc-950` (#09090b) background, not true black
- [ ] Light mode is `white` or `zinc-50` — never cream, never warm whites
- [ ] Accent colors limited to: purple, blue, violet, or emerald. Almost never orange, red, or yellow as primary
- [ ] Sun/moon theme toggle in the **top-right corner of the navbar** (next-themes)

## 3. Layout & Spacing

- [ ] **`max-w-7xl mx-auto px-4`** container on everything
- [ ] Sections use `py-16 md:py-24` vertical rhythm — robotically consistent
- [ ] **CSS Grid with `grid-cols-1 md:grid-cols-2 lg:grid-cols-3`** for feature cards — always this exact breakpoint pattern
- [ ] Hero section: centered text → heading → subtext → two buttons side by side (`flex gap-4`)
- [ ] Footer with 4 columns of links, no creativity in layout
- [ ] Padding is always multiples of 4 (p-4, p-6, p-8) — never odd values like p-5 or p-7

## 4. Cards & Containers

- [ ] **`rounded-xl` or `rounded-2xl`** on every card — never `rounded-md`, never sharp corners
- [ ] `bg-white dark:bg-zinc-900` with `border border-zinc-200 dark:border-zinc-800`
- [ ] `shadow-sm` — never `shadow-md`, never `shadow-lg`, never no shadow
- [ ] Hover state is **`hover:shadow-md transition-shadow`** or `hover:border-zinc-300`
- [ ] Cards have `p-6` padding — almost never `p-4` or `p-8`
- [ ] Identical card heights in grids using `flex flex-col` with a `flex-1` body section

## 5. Buttons

- [ ] **shadcn variant taxonomy**: `default`, `outline`, `ghost`, `destructive`, `secondary` — inspectable in class names or via CVA
- [ ] Primary button: solid fill with `rounded-md` (not `rounded-full`, not `rounded-lg`)
- [ ] Ghost buttons everywhere for secondary actions
- [ ] Button text is always `text-sm font-medium`
- [ ] CTA pairs: one solid + one outline button side by side
- [ ] Hover is a slight shade change — never a color shift, never an underline

## 6. Icons

- [ ] **Lucide icons** — thin 1.5px stroke weight, 24x24 default. Recognizable style
- [ ] Icons are `h-4 w-4` or `h-5 w-5` — never `h-6 w-6`, never custom sizes
- [ ] `text-muted-foreground` gray on icons — never colored icons unless in a badge
- [ ] Same icons repeat across vibecoded sites: `ChevronRight`, `ArrowRight`, `Check`, `X`, `Moon`, `Sun`, `Menu`, `Search`, `Settings`, `User`, `Mail`
- [ ] Feature cards: icon sitting alone above heading text, always `h-5 w-5` or wrapped in a colored circle

## 7. Animation

- [ ] **Fade-up on scroll** — `animate-in fade-in slide-in-from-bottom-4` on every section entry
- [ ] `transition-all duration-200` or `duration-300` on every interactive element
- [ ] Framer Motion `whileHover={{ scale: 1.02 }}` or `1.05` on cards
- [ ] `spring` physics on page transitions — same bounce, same stiffness every time
- [ ] Staggered children animations: cards animate in one after another with 100ms delays
- [ ] No animation on mobile — AI usually forgets to adapt motion for touch devices

## 8. Navigation

- [ ] **Sticky navbar** with `backdrop-blur-sm bg-white/80 dark:bg-zinc-950/80 border-b`
- [ ] Logo on left, links center, CTA button + theme toggle on right
- [ ] Mobile: hamburger menu (three lines, `Menu` icon from lucide) that opens a **sheet from the right** (vaul/radix)
- [ ] Nav links use `text-sm font-medium text-muted-foreground hover:text-foreground`
- [ ] No dropdown menus on mobile — just a flat list in the sheet

## 9. Forms & Inputs

- [ ] **shadcn Input** — `h-10 rounded-md border border-input bg-background px-3 py-2 text-sm`
- [ ] Focus ring: `ring-2 ring-ring ring-offset-2` — the exact shadcn focus style
- [ ] Labels are `text-sm font-medium` above the input, never inside
- [ ] Error messages in `text-sm text-destructive` below the field
- [ ] Select dropdowns use Radix Select — recognizable by the portal rendering and animation
- [ ] Calendar date picker pops up in a perfectly styled popover (react-day-picker + radix popover)

## 10. Toasts & Feedback

- [ ] **Bottom-right toast** (sonner) — slides up with a subtle shadow
- [ ] Toast has a close X, optional action button, auto-dismisses in ~4 seconds
- [ ] Success = subtle green. Error = red. Info = default. Never custom toast designs
- [ ] Loading states use a spinning `Loader2` icon from lucide (the animated one)

## 11. Command Palette

- [ ] **⌘K search** (cmdk) — even on sites with 3 pages and nothing to search
- [ ] Radix Dialog overlay with the cmdk input + grouped results
- [ ] Same keyboard shortcut hint badge in the search input: `⌘K` in a rounded gray pill

## 12. Data Display

- [ ] **Tables**: shadcn Table with `@tanstack/react-table` — alternating row shading, sortable column headers, bottom pagination
- [ ] **Charts**: Recharts with soft-gradient `<Area>` fills, rounded `<Line>` strokes, same tooltip style
- [ ] Dashboard cards: number top-left, label below, tiny sparkline or percentage badge with up/down arrow
- [ ] Badge component: `rounded-full px-2.5 py-0.5 text-xs font-medium` — always this exact sizing

## 13. Page Patterns

- [ ] **Hero**: centered heading (text-4xl md:text-6xl) → gray subtext → two CTAs → optional screenshot/mockup below
- [ ] **Features grid**: 3-column grid of icon + heading + paragraph cards
- [ ] **Testimonials**: horizontal carousel (embla) or 3-column grid of quote cards with avatar circles
- [ ] **Pricing**: 3 cards, middle one "highlighted" with a border or `scale-105` and "Most Popular" badge
- [ ] **CTA section**: centered text on a slightly different background with one button
- [ ] **Footer**: 4-column link grid → bottom bar with copyright + social icons
- [ ] The **entire page** follows this exact section order: hero → logos → features → how-it-works → testimonials → pricing → CTA → footer

## 14. Code-Level Tells (inspect element)

- [ ] `data-slot` attributes on primitives (shadcn v4 / React 19)
- [ ] `data-state="open"` / `data-state="closed"` on interactive elements (Radix)
- [ ] CSS variables named `--radius`, `--background`, `--foreground`, `--card`, `--popover`, `--primary`, `--muted`, `--accent`, `--destructive` in `:root`
- [ ] Tailwind classes in the HTML — `flex items-center justify-between` visible in DOM
- [ ] `__next` div wrapper (Next.js) or `#root` (Vite)
- [ ] `<svg>` icons with `xmlns="http://www.w3.org/2000/svg"` and consistent `strokeWidth="2"` `strokeLinecap="round"` `strokeLinejoin="round"` (lucide signature)
- [ ] `role="dialog"` portals appended to `<body>` (Radix)
- [ ] `cmdk-root`, `cmdk-input`, `cmdk-list` data attributes in DOM if command palette exists

---

## Scoring

| Hits | Verdict |
|------|---------|
| 0–4 | Probably human-built |
| 5–9 | Likely used AI assistance but a developer cleaned it up |
| 10–17 | Almost certainly vibecoded with some customization |
| 18–25 | Pure vibecode. Developer never touched the defaults |
| 26+ | The AI built this, deployed it, and the human never opened the code |

---

## The Single Fastest Tell

Open DevTools → Elements tab → search for `data-slot` or `data-state`. If you find both, it's shadcn + Radix. That alone confirms AI-assisted with ~90% confidence in 2025-2026, because almost no one was manually choosing this stack before vibecoding made it the default.

Second fastest: View Source → Ctrl+F for `--destructive`. If the CSS variable exists, it's shadcn's theming. Case closed.