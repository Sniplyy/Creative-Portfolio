# DESIGN.md — "The Reel" Portfolio Design System

> Extracted from Stitch MCP project: **Arryan: The Reel Portfolio**
> Project ID: `9785947145365767739`
> All 6 screens fetched successfully. No fallbacks needed.

---

## Screens Inventory

| Screen | Stitch Title | Status |
|--------|-------------|--------|
| Home | The Reel — Home | ✅ Fetched |
| Work Index | The Reel — Work | ✅ Fetched |
| Project Detail | The Reel — Dipzz Project Detail | ✅ Fetched |
| Service (Video Editing) | The Reel — Video Editing Service | ✅ Fetched |
| About | The Reel — About (Arryan // About) | ✅ Fetched |
| Contact | THE REEL // CONTACT | ✅ Fetched |

> **Note:** Stitch has only one Service screen (Video Editing). The other three services (Graphic Design, Motion Graphics, Logo Design) will use the same template pattern with data from `content/services.ts`.

---

## Color Tokens (Dark Mode — Primary Experience)

### Core Surface Colors
| Token | Value | Usage |
|-------|-------|-------|
| `background` | `#1f0e13` | Page background (dark mode) |
| `surface` | `#1f0e13` | Surface fill |
| `surface-dim` | `#1f0e13` | Dimmed surface |
| `surface-bright` | `#493338` | Elevated bright surface |
| `surface-container-lowest` | `#19090e` | Deepest container |
| `surface-container-low` | `#28161b` | Low elevation container |
| `surface-container` | `#2d1a1f` | Default container |
| `surface-container-high` | `#382529` | High elevation container |
| `surface-container-highest` | `#442f34` | Highest elevation container |
| `surface-variant` | `#442f34` | Variant surface |
| `surface-tint` | `#ffb1c4` | Tint overlay |

### Text / On-Surface
| Token | Value | Usage |
|-------|-------|-------|
| `on-surface` | `#fbdae1` | Primary text |
| `on-background` | `#fbdae1` | Text on background |
| `on-surface-variant` | `#e5bcc5` | Secondary / muted text |

### Primary (Magenta Family)
| Token | Value | Usage |
|-------|-------|-------|
| `primary` | `#ffb1c4` | Primary (light pink) |
| `primary-container` | `#ff4a8d` | Bold container |
| `primary-fixed` | `#ffd9e1` | Fixed primary |
| `primary-fixed-dim` | `#ffb1c4` | Dimmed fixed primary |
| `on-primary` | `#65002e` | Text on primary |
| `on-primary-container` | `#590028` | Text on primary container |
| `on-primary-fixed` | `#3f001a` | Text on fixed primary |
| `on-primary-fixed-variant` | `#8f0044` | Text on fixed primary variant |
| `inverse-primary` | `#ba005b` | Inverse primary |

### Brand Accent (Explicit)
| Token | Value | Usage |
|-------|-------|-------|
| `magenta` | `#FF007F` | Playhead, focus rings, CTAs, accent |
| `obsidian` | `#0B0B0C` | Deep dark background, CTA text on magenta |

### Secondary
| Token | Value | Usage |
|-------|-------|-------|
| `secondary` | `#c6c6cd` | Muted meta text |
| `secondary-container` | `#48494f` | Secondary container |
| `on-secondary` | `#2f3036` | Text on secondary |
| `on-secondary-container` | `#b8b8bf` | Text on secondary container |

### Tertiary (Green)
| Token | Value | Usage |
|-------|-------|-------|
| `tertiary` | `#63e063` | Status indicators ("Available") |
| `tertiary-container` | `#21a732` | Green container |

### Borders / Outlines
| Token | Value | Usage |
|-------|-------|-------|
| `outline` | `#ac878f` | Standard outline |
| `outline-variant` | `#5c3f46` | Hairline borders (1px dividers) |

### Error
| Token | Value | Usage |
|-------|-------|-------|
| `error` | `#ffb4ab` | Error state |
| `error-container` | `#93000a` | Error container |

### Inverse (Light Theme Seeds)
| Token | Value | Usage |
|-------|-------|-------|
| `inverse-surface` | `#fbdae1` | Light mode surface |
| `inverse-on-surface` | `#3f2b30` | Light mode text |

---

## Light Theme Override Tokens (from baseline spec)
| Token | Value |
|-------|-------|
| Paper (bg) | `#F4F4F5` |
| Obsidian (text) | `#0B0B0C` |
| Surface-light | `#FFFFFF` |
| Magenta-ink (AA text) | `#D6006A` |
| Ink-muted-dark | `#A5A5AC` |
| Ink-muted-light | `#6B6B72` |

---

## Typography

### Font Families
| Role | Family | Usage |
|------|--------|-------|
| Display / Headings | **Archivo Narrow** (700–900) | Hero titles, section headings, project names |
| Body / UI | **Inter** (400–700) | Paragraphs, descriptions, UI elements |
| Technical / Meta | **JetBrains Mono** (400–500) | Timecodes, tags, labels, metadata, nav links |

### Type Scale
| Token | Size | Line Height | Weight | Letter Spacing | Family |
|-------|------|-------------|--------|-----------------|--------|
| `display-xl` | 120px | 110px | 900 | -0.04em | Archivo Narrow |
| `display-xl-mobile` | 64px | 60px | 900 | -0.02em | Archivo Narrow |
| `headline-lg` | 48px | 52px | 700 | -0.02em | Archivo Narrow |
| `body-md` | 18px | 28px | 400 | — | Inter |
| `body-sm` | 15px | 24px | 400 | — | Inter |
| `meta-technical` | 13px | 16px | 500 | 0.05em | JetBrains Mono |

---

## Spacing

| Token | Value | Usage |
|-------|-------|-------|
| `base` | 8px | Base unit (8pt grid) |
| `section-gap` | 160px | Between major sections |
| `grid-gutter` | 24px | Grid column gutter |
| `max-width` | 1440px | Content max width |
| `margin-desktop` | 64px | Desktop side margins |
| `margin-mobile` | 20px | Mobile side margins |

---

## Border Radius
| Token | Value |
|-------|-------|
| DEFAULT | 0.25rem (4px) |
| lg | 0.5rem (8px) |
| xl | 0.75rem (12px) |
| full | 9999px |

> **Note:** The design system uses **sharp 0px corners** for most elements per the brutalist aesthetic. The border-radius tokens above are Tailwind defaults — project tiles, buttons, and inputs should use `rounded-none` explicitly.

---

## Component Patterns (from Stitch HTML)

### Playhead Progress Bar
- Fixed at `top: 0`, 2px height, `bg-magenta` (#FF007F)
- Width tracks scroll percentage via JS
- `z-index: 50+`

### Navigation (Sticky)
- Fixed top, `bg-background/90 backdrop-blur-md`
- 1px bottom border (`border-outline-variant`)
- Wordmark: "THE REEL" in `font-headline-lg`, `text-primary`, uppercase, tight tracking
- Nav links: `font-meta-technical`, uppercase, `text-on-surface-variant`
- Active link: `text-primary`, `border-b-2 border-primary`
- Theme toggle: Material Symbol `light_mode` / `dark_mode`
- Mobile: hamburger menu icon

### Project Tiles
- Asymmetric grid: 12-column grid, tiles span 4/8/12 cols
- Aspect ratios: `aspect-video` (16:9), `aspect-[4/5]`, `aspect-square`, `aspect-[21/9]`
- 1px hairline border (`border-outline-variant`)
- Hover: border color transitions to `magenta`, image scale 1.02, video overlay appears
- Video overlay: `bg-magenta/10` or `bg-surface-dim/60` with play_circle icon
- Timecode badge: top-right, `bg-background/80 backdrop-blur`, `font-meta-technical`, `text-primary`
- Title: `font-headline-lg`, uppercase
- Metadata: `font-meta-technical`, `text-on-surface-variant`, format: `CATEGORY · YEAR`
- Left border accent on hover: `border-l-2 border-primary`

### Service Cards (Home page)
- 4-column grid, each cell: `p-8`, full hairline border
- Number prefix: `font-meta-technical`, `text-on-surface-variant`
- Title: `font-headline-lg`, uppercase
- Arrow icon: slides in from left on hover, `text-magenta`
- Hover: `bg-surface-container`

### Filter Pills (Work page)
- `font-meta-technical`, uppercase
- Active: `text-on-surface` + magenta underline (2px `::after`)
- Inactive: `text-on-surface-variant`
- Categories: All, Video Editing, Graphic Design, Motion Graphics, Logo Design

### Project Detail Layout
- Back link: arrow_back + "BACK TO WORK", `font-meta-technical`
- Title: `display-xl-mobile` / `display-xl`, `text-primary`
- Spec block (right column): bordered card, `bg-surface-container-low`
  - Rows: ROLE, TOOLS, CATEGORY, YEAR
  - `font-meta-technical`, label `text-on-surface-variant`, value `text-on-background`
- Hero image: full-width `aspect-[21/9]`
- Gallery: 12-col grid, mixed 4/8/12 col spans
- Next Project: display-xl title, circular arrow button, grayscale preview → color on hover

### Service Page Layout
- Label: "SERVICE // 01", `font-meta-technical`, `text-secondary`
- Title: `display-xl-mobile` / `display-xl`, `text-primary`
- Subtitle: `font-headline-lg`, `text-secondary`
- Hero image: `aspect-[~16:9]`, grayscale → color on hover
- Timecode badge in corner
- Two-column layout:
  - Left (4 cols): What's Included checklist + Tool chips
  - Right (8 cols): Numbered Process steps (01–04)
- Related Work: 2-col grid of project tiles
- CTA section: `bg-surface-container-low`, hairline border, "READY TO EDIT?" heading

### About Layout
- Split grid: 5 cols (typographic hero) + 7 cols (bio + skills)
- Hero: ARRYAN in `display-xl`, rotated -90° on desktop, `text-surface-tint`
- Technical corner labels: "ID: 01_ABOUT", "V.1.0 // NLE"
- Bio: `font-body-md`, two paragraphs
- Skills: 3-column grid (DESIGN, VIDEO, DEV)
  - Tags: `font-meta-technical`, hairline border, `bg-surface-container-low`
  - Hover: `border-magenta text-magenta`

### Contact Layout
- Two-column: 7-8 cols (form) + 4-5 cols (contact info)
- Title: "LET'S MAKE SOMETHING", `display-xl-mobile` / `display-xl`, `text-primary`
- Form inputs: bottom-border only, `border-outline-variant`, `focus:border-inverse-primary`
- Labels: `font-meta-technical`, uppercase
- Fields: Name, Email, Project Scope (select), Brief/Details (textarea)
- Submit: "TRANSMIT", `bg-inverse-primary text-white`
- Contact info: DIRECT LINE (Email), PORTFOLIO (Behance), SOCIAL (Instagram)
  - Labels: `font-meta-technical text-on-surface-variant`
  - Values: `font-headline-lg text-on-surface`
- Status badge: green dot + "AVAILABLE FOR COMMISSIONS", `text-tertiary`

### Footer
- `bg-surface-container` (Home) or `bg-surface-container-lowest` (other pages)
- Top border: `border-outline-variant`
- "THE REEL" wordmark, copyright line
- Links: Behance, Instagram, Email, Back to Top
- `font-meta-technical`, `text-on-surface-variant`, hover `text-primary`

### Global Styles
- Focus: `outline: 2px solid #FF007F`, `outline-offset: 4px`
- Selection: `bg-magenta text-obsidian`
- Custom scrollbar: 4-8px, track = background color, thumb = magenta or surface-variant
- Scroll reveal: `opacity: 0, translateY(30px)` → `opacity: 1, translateY(0)`, 0.8s cubic-bezier
- Filmstrip pan animation: `translateX(0)` → `translateX(-50%)`, 60s linear infinite
- Playhead animation (hero): width 0 → 100%, 2s cubic-bezier, 0.5s delay

---

## Stitch-Provided Image URLs

Images from Stitch for seeding project tiles and hero sections:

### Home — Filmstrip Background
1. Urban night cityscape (grainy 35mm)
2. Camera lens macro
3. Editorial fashion silhouette
4. Glitching digital display

### Project Cover Images
- **Dipzz**: Bold red/black brand identity - `https://lh3.googleusercontent.com/aida-public/AB6AXuBLx8QuQwYpBgLeFHym7ZATZ0DFAe0Rai_fTmWToh3fngiUksDM-eCz3Vp4a2eRjS_Vk8eqDLvMcOamnUaepjEEpOOTmq3jdyOQgmi4jcgOITkMA-NhknqStsXyzIddIgDW0TG6pm3vEieely1n5lzND-chS2z_dVZgMUq_gCiZzLkCU4ig4jz3F72xKoO1DcHTiShrfOV49wRBfMlBgevvZ8oiXahBxaXcdHQvhTguMoUvXVd5fE_9muAVYfoWi-s_p8eoD88X1kU`
- **Vault Vortex**: Metallic logo on obsidian card - `https://lh3.googleusercontent.com/aida-public/AB6AXuCy4F1RvZ-Kx18jOOn1bg2A9iKNr8OlO_iJQ_LSJnaBApq6rAZ_ShgZOtnNhTNmWWcWQ-aqDEsgyelKjk5gxYqpngeo9a5JizgRcPqtrJ6D7nbQVKKAdr-NFkoYz5XvQAwhYa6If8YAGbXutYg2Vtgd6buxpqLSr0JvPlb5xJCs1U6HYExdIDI-QnBPM0gV-2ub0Jkb2k8dtbmWJWPfeXuHLUuziQr2FyRLSJ-5QWS4kAC6VbOahO00Ilgc3M9WrmDcwFHAsUEVcEo`
- **Podcast Series**: Cinematic podcast studio - `https://lh3.googleusercontent.com/aida-public/AB6AXuCO7wDTi8Zc9TBRBagzEYU3TKh1pvn6158rqZl6iCM2l54w0CUL-fKnKKXyQ8fIYHuiyyXAvT49OVzjZMWCeX8dgQb50wmv20qeWNQFnsXMCTlh5MppHzPcNFPb17__Sq7gn4SfOBv9Kui2tAU9c8PE-NFUYf3DrDb9p3YostMTsyMAdLgmwaWEx6OXsXlhlpRgRfjAIBI7Wrthts4okMVkRxTY5Dyy57tAFP3a9wCYGQVVp99R0sNZNfULjhkwmPfd_0WqxhprXGA`
- **Motion Reel 2025**: Explosive 3D geometry - `https://lh3.googleusercontent.com/aida-public/AB6AXuDSoWFXVZ86KgQEgVtFCFHLaM8dHs8F9OeMX0SUY_a5IffX-eQ87FeyVbpKbouV-q6IPedhJO2TtRj9Tlp1DFFLKwTCrKCy6JiGz3_iA3zWe0cBV58e5CMJVs3khXboWkvYquPZUDwKyRpwkxrXRa_sMKfTv10JYjD1Px6tyLjxZzp2NA6u-lc-5Dxge00bj0lq10kg1cfAGx6qVGUqKOMrEa10WP_Xybk9lk8tFmSk0LrF3T33-PqnifnomPaa9mGNnb-8ZsfGy20`
- **Architectural Silhouettes**: Brutalist poster series - `https://lh3.googleusercontent.com/aida-public/AB6AXuA8RbS0Ceo3ratemiLUkO_xMCwLKnv3Grr0wr_MLQrWanwSVAg6eLrD151FUAWJmqNiSrVjbzTHl7CzjsCsF0rqHvGvqQSspW30JLtq_mRuxDfvdXkoYWOzkyStpVotm864JzRNTvcycW4ErzsiV-em0woo_wH8K8J_2RAcX4wKrak8fSjUfvC7urnW8JqN8lmL4sSmGc06W_UB94--I8FPOwRAaoqGkCBHVGXKyuMhjFoSQ_3m1VUUZMKyfrAKUlKaifUCEp8uyNM`
