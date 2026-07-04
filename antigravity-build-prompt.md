# Antigravity Build Prompt — Arryan Portfolio (Claude Opus 4.6 · Thinking)

Paste the whole block below into Antigravity's agent chat with Opus 4.6 selected. Requires the Stitch MCP server already installed in Antigravity (Agent Manager → "···" → MCP Servers → Stitch). Swap in your real Stitch project name before sending.

---

```
ROLE
You are building a production-ready personal portfolio website for Arryan,
a video editor and graphic designer. Work autonomously: plan, scaffold,
build, verify in the integrated browser, and fix what doesn't match before
reporting back. Ask me only if something is genuinely ambiguous — otherwise
make the sensible call and note what you decided.

STEP 0 — PULL THE DESIGN (do this first, before scaffolding)
Use the Stitch MCP server to fetch the project named "[Your Stitch project
name]". Extract its color tokens, typography, spacing, and the generated
HTML/CSS for every screen (Home, Work index, Project detail, the four
service pages, About, Contact). Write everything you extract into
/DESIGN.md at the project root before writing any application code.
Precedence rule: where DESIGN.md and this prompt disagree, DESIGN.md wins
for exact visual values (colors, spacing, type sizes); this prompt wins
for structure, routing, and behavior. If the Stitch fetch fails or a
screen is missing, fall back to the baseline design system below and tell
me which screens you had to improvise.

BASELINE DESIGN SYSTEM (fallback only, if Stitch/DESIGN.md is incomplete)
Colors: obsidian #0B0B0C (dark bg / light-theme text), paper #F4F4F5
(light bg), surface-dark #17171A, surface-light #FFFFFF, magenta #FF007F
(primary accent, both themes), magenta-ink #D6006A (small text/links on
the light theme, for AA contrast), ink-muted-dark #A5A5AC, ink-muted-light
#6B6B72.
Type: Archivo Expanded (display/headings), Inter (body/UI), JetBrains Mono
(timecodes, tags, meta labels).
Concept — "The Reel": nav carries a thin magenta playhead line that tracks
scroll position; work is tagged with timecode-style metadata instead of
plain dates; project tiles preview video on hover.

TECH STACK (how to build)
- Next.js 16, App Router, TypeScript, Turbopack (default — don't add Webpack config).
- Tailwind CSS v4 — CSS-first config via @theme in globals.css, there is
  no tailwind.config.js. Right after "@import "tailwindcss";" add
  "@custom-variant dark (&:where(.dark, .dark *));" so class-based dark
  mode actually works — the old v3 darkMode:'class' option silently does
  nothing in v4.
- next-themes for the toggle: ThemeProvider in the root layout,
  attribute="class", defaultTheme="dark", suppressHydrationWarning on
  <html>. Dark is the default experience, not a system-preference guess.
- motion — this is the renamed Framer Motion; import from "motion/react",
  not "framer-motion". Use it for the playhead animation, hover states,
  and scroll reveals, only inside Client Components ("use client").
- next/image for every image; lazy-mount hover-preview videos — don't
  autoplay every tile on page load, only load/play on hover or in-view.
- lucide-react for icons. Optional: clsx + tailwind-merge for a small
  cn() className helper.
- Scaffold with npx create-next-app@latest — TypeScript, Tailwind, App
  Router, and ESLint are the current defaults, just confirm they're on.

WHERE TO BUILD — project structure
portfolio/
├─ app/
│  ├─ layout.tsx          → fonts, ThemeProvider, Nav, Footer
│  ├─ page.tsx             → Home
│  ├─ globals.css          → @theme tokens + light/dark variable overrides
│  ├─ work/
│  │  ├─ page.tsx          → Work index (filterable grid)
│  │  └─ [slug]/page.tsx   → Project detail — dynamic, generateStaticParams from content/projects.ts
│  ├─ services/
│  │  └─ [slug]/page.tsx   → one of the 4 services — dynamic, generateStaticParams from content/services.ts
│  ├─ about/page.tsx
│  └─ contact/page.tsx
├─ components/
│  ├─ layout/              → Nav, Footer, ThemeToggle, PlayheadLine
│  ├─ ui/                  → Button, Tag, FilterPill, etc.
│  └─ sections/             → Hero, WorkGrid, ProjectTile, ServiceCard, Gallery, ContactForm
├─ content/
│  ├─ projects.ts          → typed array: slug, title, category, year, role, tools, coverImage, previewVideo, gallery[], summary
│  └─ services.ts          → typed array: slug, name, positioning, includes[], process[], tools[]
├─ lib/utils.ts
└─ public/media/            → images + video previews — use clean placeholder blocks with labels until real assets land, same aspect ratios, so swapping in real files later is a one-line change

Route every project and every service through the two dynamic [slug]
routes above, reading from content/projects.ts and content/services.ts —
do not hand-write a separate page.tsx per project or per service.

WHAT TO BUILD — pages and behavior
1. Home (/) — filmstrip hero (muted looping clips/stills) with "Arryan"
   as the display headline and the playhead line running beneath it;
   Selected Work tiles seeded from content/projects.ts (Dipzz, Vault
   Vortex, a podcast video edit); four Service cards linking to
   /services/[slug]; a short first-person intro; CTA into /contact.
2. Work index (/work) — filter pills (All / Video Editing / Graphic
   Design / Motion Graphics / Logo Design) that re-filter the grid
   client-side without a reload; asymmetric tile grid; each tile shows a
   poster image that swaps to a muted looping video on hover/tap, plus a
   mono metadata line (category · year).
3. Project detail (/work/[slug]) — title plus a mono spec block (Role,
   Tools, Category, Year), hero media, a brief paragraph, a mixed-width
   gallery, and a "Next project" link at the bottom.
4. Service pages (/services/[slug]) — one template, four data entries
   (Video Editing, Graphic Design, Motion Graphics, Logo Design): hero
   statement, What's included list, a numbered Process, tool chips, 2-3
   related project tiles pulled from content/projects.ts by category, CTA
   into /contact.
5. About (/about) — bio (graphic design, video editing, and brand
   identity background; currently completing a BCA), skills as grouped
   mono tags (Design, Video, Dev: JavaScript, React, Node.js).
6. Contact (/contact) — name / email / project-type / message form
   (client-side validation is enough, no backend required unless I ask
   for one separately), plus direct email, Behance, and Instagram links.

Global: sticky nav (wordmark, Work, a Services dropdown, About, Contact,
theme toggle), footer (Behance, Instagram, email, back-to-top). Every page
needs to work fully in both themes — check each one in both, don't just
invert dark to get light and call it done.

QUALITY BAR
- Fully responsive, mobile through desktop — check each breakpoint, not
  just desktop.
- Visible magenta focus outline on every interactive element; respect
  prefers-reduced-motion (swap autoplay/parallax for static states, and
  gate motion's animations behind useReducedMotion).
- generateMetadata on every route for accurate per-page titles and
  descriptions (project name, service name); sensible Open Graph defaults
  in the root layout.
- Alt text on every image. Semantic landmarks (nav/main/footer), correct
  heading order.
- Use Next.js 16's native View Transitions (transitionTypes on <Link>)
  for page-to-page navigation feel; use motion for in-page reveals, hover
  states, and the playhead.
- No lorem ipsum in the final pass — use the real seeded project/service
  copy from content/, even while media is still a placeholder.

BUILD ORDER
1. Fetch the Stitch design (Step 0), write DESIGN.md.
2. Scaffold the project, install dependencies, wire up Tailwind v4 +
   next-themes + the dark variant.
3. Build the globals.css design tokens and confirm the theme toggle works
   with zero flash before building any pages.
4. Build Nav, Footer, PlayheadLine, ThemeToggle.
5. Build content/projects.ts and content/services.ts with the seeded data
   above.
6. Build the pages in this order: Home → Work index → Project detail →
   Service template → About → Contact.
7. Run the dev server, open it in the integrated browser, click through
   every route in both themes and at mobile width, and fix anything that
   doesn't match DESIGN.md or this brief before telling me it's done.

When you report back, show me the plan/artifact summary plus screenshots
of Home and one project page, in both themes.
```
